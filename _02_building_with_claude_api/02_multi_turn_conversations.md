# Multi-Turn Conversations
---

Companion notebook: [notebooks/02_multi_turn_convo.ipynb](notebooks/02_multi_turn_convo.ipynb)

## The problem

The Messages API is **stateless** — no built-in memory of prior turns.
Every request stands completely alone. Most real applications are
conversational (chat, assistants), so a raw stateless call isn't enough
on its own.

> [!NOTE]
> ### It's not "random," it's "unaware"
> A follow-up sent with no prior messages doesn't get a *wrong* or
> *random* answer — the model responds correctly to exactly what it
> received. It simply has no way to know an earlier exchange existed.
> Working as designed, just on incomplete input.

## The fix: client-side history

The client accumulates the conversation as a list of `{role, content}`
objects — both the **user's** messages *and* the **assistant's own past
replies** — and sends the *entire* list with every new request. The
model only "remembers" what's literally included in that list.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif", "fontSize": "15px"}, "flowchart": {"htmlLabels": true, "padding": 22, "nodeSpacing": 35, "rankSpacing": 60}}}%%
flowchart TB
    U1(["🧑 user: 'How do you say<br/>hello in Hindi?'"]) --> M1(["📋 messages: user1"])
    M1 --> C1(["🧠 chat messages"])
    C1 --> A1(["🤖 assistant: 'Namaste'"])
    A1 --> M2(["📋 messages: user1, assistant1"])
    M2 --> U2(["🧑 user: 'What about city?'"])
    U2 --> M3(["📋 messages: user1, assistant1, user2"])
    M3 --> C2(["🧠 chat messages"])
    C2 --> A2(["🤖 assistant: 'शहर (Shahar)'<br/>— correctly resolved 'city'<br/>using turn 1's context"])

    classDef user fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef hist fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef call fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef assist fill:#22C55E,stroke:#16A34A,color:#ffffff
    class U1 user
    class U2 user
    class M1 hist
    class M2 hist
    class M3 hist
    class C1 call
    class C2 call
    class A1 assist
    class A2 assist
```

## The three-function pattern

The notebook implements this with three small helpers, keeping the
running `messages` list as the single source of truth:

| Function | Job |
|---|---|
| `add_user_message(messages, text)` | Append a `{"role": "user", ...}` entry |
| `add_assistant_message(messages, text)` | Append a `{"role": "assistant", ...}` entry — the model's own past reply |
| `chat(messages)` | Call `client.messages.create(...)` with the *whole* running list, return the reply text |

Usage is then just: add user turn → `chat()` → add assistant's reply →
add next user turn → `chat()` again → repeat.

## The tradeoff this creates

> [!IMPORTANT]
> ### Context grows every turn — same shape as the agent loop
> Every turn re-sends the **entire accumulated conversation**, not just
> the new message. This is the exact same "context grows with every
> loop iteration" idea from
> [Claude Code 101 → the agent loop](../_01_claude_code_101/01_how_claude_code_works.md),
> just at chat-app granularity instead of per-tool-call:
> - **Context window** — a long-running conversation eventually
>   approaches the model's total capacity, same as covered in
>   [Context Management](../_01_claude_code_101/03_context_management.md).
> - **Cost** — token usage grows every turn too, since the *entire*
>   history gets re-sent and re-billed each time, not just the newest
>   message.
>
> Eventually this needs the same kind of management already covered
> for agents: summarizing older turns into a condensed form rather than
> keeping the full verbatim history forever.

## Quick recap

| | Stateless single call | Multi-turn (client-managed history) |
|---|---|---|
| Memory of prior turns | None | Full — via the `messages` list |
| Who's responsible for context | Nobody | The client |
| Must include | — | Both user *and* assistant messages |
| Growing cost | N/A | Every turn re-sends + re-bills the whole history |
