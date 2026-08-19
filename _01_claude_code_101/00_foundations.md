# Foundations: Gen AI, AI Agents & Context
---

Vocabulary and mental models that everything else in this module builds on —
Gen AI / LLM / AI Agent / Agentic AI System, and what "context" means.

## Introduction: Gen AI vs AI Agent vs Agentic AI

Before getting into Claude Code, here's the basic vocabulary. Claude Code itself
is an **AI Agent** that helps write code as per prompts — everything below sets
up that context.

### 1. Gen AI (Generative AI)

The field of AI that **generates new content** (text, images, audio, code)
instead of just analyzing/classifying existing data.

- **LLM (Large Language Model)** is a sub-field of Gen AI, focused on language.
- Core trick: predict the next token based on the sequence seen so far.
  - `"How are ___?"` → `"How are you?"`
- Classic shape: text in → text out (modern LLMs are increasingly multimodal).

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart LR
    A(["📥 Input tokens<br/>'How are'"]) --> B[["🧠 LLM"]]
    B --> C(["📤 Predicted token<br/>'you'"])
    C -.fed back in.-> A

    classDef input fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef brain fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef output fill:#14B8A6,stroke:#0D9488,color:#ffffff
    class A input
    class B brain
    class C output
```

### 2. AI Agent

An LLM alone just answers once. An **AI Agent** wraps an LLM with the ability
to **take actions** and **use their results** to decide what to do next.

> AI Agent = LLM (brain) + Tools (hands) + a loop to reason → act → observe

This loop is called **ReAct** (Reason + Act):

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart LR
    R(["🤔 Reason<br/>LLM thinks about next step"]) --> AC(["🛠️ Act<br/>call a tool, e.g. hit an API"])
    AC --> O(["👀 Observe<br/>see the real-world result"])
    O --> R
    R -->|goal reached| Done(["✅ Done"])

    classDef reason fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef act fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef observe fill:#14B8A6,stroke:#0D9488,color:#ffffff
    classDef done fill:#22C55E,stroke:#16A34A,color:#ffffff
    class R reason
    class AC act
    class O observe
    class Done done
```

Note: this looks similar to how a transformer generates tokens one at a time
and feeds them back in — but that loop happens *inside* one LLM call
(token-by-token, no real-world action). ReAct is the *outer* loop — each
"Reason" step is a full LLM call, and "Act" touches the real world (APIs,
code execution, files, etc.).

### 3. Agentic AI System

An application built using one or more AI Agents to autonomously achieve an
end goal. With just one agent, no orchestration is needed. With **multiple
agents**, something needs to coordinate who does what and in what order —
this is called **orchestration**.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart TB
    U(["🎯 Goal"]) --> O(["🧭 Orchestrator Agent"])
    O --> A1(["🔎 Agent 1<br/>research"])
    O --> A2(["💻 Agent 2<br/>write code"])
    O --> A3(["✅ Agent 3<br/>test"])
    A1 --> O
    A2 --> O
    A3 --> O
    O --> Result(["🏁 Final Result"])

    classDef goal fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef orch fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef agent fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef result fill:#22C55E,stroke:#16A34A,color:#ffffff
    class U goal
    class O orch
    class A1 agent
    class A2 agent
    class A3 agent
    class Result result
```

### Quick summary

| Term | What it is |
|---|---|
| Gen AI | Field of AI that generates new content |
| LLM | Gen AI model specialized in language (next-token prediction) |
| AI Agent | LLM + Tools + ReAct loop (reason → act → observe) |
| Agentic AI System | App built from one or more agents, orchestrated to reach a goal |

*(Note to self: agent-to-agent communication and MCP are separate topics —
covering later.)*

### How the four terms nest

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart TB
    subgraph GenAI["🎨 Gen AI — generates new content"]
        subgraph LLMbox["💬 LLM — language-focused Gen AI"]
            subgraph AgentBox["🤖 AI Agent — LLM + Tools + ReAct"]
                SysBox["🏗️ Agentic AI System<br/>multiple agents + orchestration"]
            end
        end
    end

    style GenAI fill:#3B82F6,stroke:#2563EB,color:#ffffff
    style LLMbox fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    style AgentBox fill:#F59E0B,stroke:#D97706,color:#ffffff
    style SysBox fill:#22C55E,stroke:#16A34A,color:#ffffff
```

## Context & Context Window

### Real-world analogy first

Say I'm building an API that consumes movie reviews from an open-source
platform, in Java + Spring Boot, saving results to a DB. To do this task I
need information like: API endpoint, auth mechanism, request/response
format, status codes, which response fields actually matter, plus general
know-how (Java, Spring Boot, how to persist to a DB).

That information splits into two kinds:

- **Already "in my head" (prior knowledge)** — Java, Spring Boot, DB basics,
  general REST conventions. I didn't have to go fetch this for today's task,
  I already know it.
- **Task-specific (have to go fetch it)** — this particular API's endpoint,
  auth scheme, response schema, rate limits. I don't know these until I
  *actually go read the docs / make a test call*.

Importantly: knowing Java doesn't help until it's *applied*, and the API's
auth mechanism isn't useful to me until I've *actually read it* — merely
being capable of looking it up doesn't count, only what's actually in front
of me while I work does.

### Deriving the actual term

**Context** = the specific information currently available to act on a
task. Some of it is prior/baked-in knowledge, some has to be actively
fetched (docs, files, API responses) — but either way, it only counts as
context once it's actually loaded and in front of you (or, for an agent, in
its context window).

For an AI Agent, context = prompts, conversation history, tool/observation
outputs, file contents it has read, etc. It's the agent's **working
memory for the current task** — not persistent long-term memory. Once the
session ends (or older content gets dropped/summarized), that memory is
gone unless something outside the model preserves it (a file, a DB, a
saved summary).

**Context window** = the hard limit (measured in tokens) on how much
context the model can hold at once. Everything competing for that budget —
system prompt, conversation history, tool definitions, tool outputs — counts
against the same limit.

In an agent's ReAct loop, context **grows with every loop iteration** —
each "Observe" step appends its result to context before the next "Reason"
step. That's exactly why long-running agents eventually approach the
context window limit and need strategies like summarization, pruning old
tool outputs, or offloading to external memory.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart LR
    I(["🔁 Loop iteration<br/>Observe appends to context"]) --> Limit{"⚠️ Near context<br/>window limit?"}
    Limit -->|No| I
    Limit -->|Yes| Manage(["🗜️ Summarize / prune /<br/>offload to external memory"])

    classDef iter fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef check fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef manage fill:#22C55E,stroke:#16A34A,color:#ffffff
    class I iter
    class Limit check
    class Manage manage
```

Zooming back out to where that context actually comes from, in the movie-review
example:

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart LR
    P(["🧑 Prior knowledge<br/>Java, Spring Boot, DB basics"]) --> CTX(["📦 Context"])
    F(["📄 Fetched info<br/>API docs, response, endpoint"]) --> CTX
    CTX --> W(["🧠 Context window<br/>token limit"])

    classDef prior fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef fetched fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef ctx fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef window fill:#EC4899,stroke:#DB2777,color:#ffffff
    class P prior
    class F fetched
    class CTX ctx
    class W window
```

## What is Claude Code?

**Goal:** have a companion that helps write code.

Claude Code is an **AI Agent** — and can behave like an **Agentic AI System**
when it delegates work to sub-agents. It's built from the same pieces covered
above:

- **Brain**: an LLM — Sonnet / Opus / Haiku
- **Hands**: Tools — terminal commands, file read/write/edit, search, web
  fetch, and even spawning sub-agents for bigger tasks
- **Operating pattern**: the ReAct loop (reason → act → observe → repeat)

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart TB
    G(["🎯 Goal: coding companion"]) --> CC[["⚡ Claude Code"]]
    CC --> LLM(["🧠 LLM brain<br/>Sonnet / Opus / Haiku"])
    CC --> T(["🛠️ Tools<br/>terminal, files, search, web..."])
    LLM --> Loop(["🔁 ReAct loop"])
    T --> Loop
    Loop --> Sub(["🧩 Sub-agents<br/>(when task needs orchestration)"])

    classDef goal fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef cc fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef brain fill:#EC4899,stroke:#DB2777,color:#ffffff
    classDef tool fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef loop fill:#14B8A6,stroke:#0D9488,color:#ffffff
    classDef sub fill:#22C55E,stroke:#16A34A,color:#ffffff
    class G goal
    class CC cc
    class LLM brain
    class T tool
    class Loop loop
    class Sub sub
```

### Tools, zoomed in

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart TB
    T(["🛠️ Tools"]) --> Term(["💻 Terminal / Bash<br/>run commands"])
    T --> File(["📁 Files<br/>read / write / edit"])
    T --> Search(["🔍 Search<br/>find code, symbols"])
    T --> Web(["🌐 Web fetch<br/>docs, URLs"])
    T --> Sub(["🧩 Sub-agents<br/>delegate a sub-task"])

    classDef root fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef leaf fill:#F59E0B,stroke:#D97706,color:#ffffff
    class T root
    class Term leaf
    class File leaf
    class Search leaf
    class Web leaf
    class Sub leaf
```

