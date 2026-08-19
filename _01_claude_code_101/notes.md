# Claude Code 101
---

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


## Reference Links:

- Skill Course: https://anthropic.skilljar.com/claude-code-101/469788

