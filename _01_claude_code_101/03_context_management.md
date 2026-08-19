# Context Management
---

Context is a **budget**, not a bottomless bag. Everything that participates
in a task — prompt, tool calls, tool results, file contents, past turns —
gets added to it and takes up space in the
[context window](00_foundations.md#context--context-window). This file
covers the tools to **inspect**, **spend**, and **reclaim** that budget.

## 1. The fuel gauge

Think of the context window like a fuel tank that only fills up, never
empties on its own, until you take an explicit action.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart LR
    subgraph Tank["⛽ Context Window"]
        direction LR
        S1["🟢 low"] --- S2["🟢 low"] --- S3["🟡 mid"] --- S4["🟠 high"] --- S5["🔴 near limit"]
    end
    Tank --> Auto{"🤖 Auto-compact<br/>fires near the limit"}
    Auto --> Sum(["📝 Summarized,<br/>lossy"])

    classDef low fill:#22C55E,stroke:#16A34A,color:#ffffff
    classDef mid fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef high fill:#EF4444,stroke:#DC2626,color:#ffffff
    classDef decide fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef sum fill:#3B82F6,stroke:#2563EB,color:#ffffff
    class S1 low
    class S2 low
    class S3 mid
    class S4 high
    class S5 high
    class Auto decide
    class Sum sum
    style Tank fill:#1E1B4B,stroke:#7C3AED,color:#ffffff
```

Nothing frees up space by itself — the tank only drains through one of the
three commands below, or by auto-compact stepping in when you're about to
run dry.

## 2. The three commands

| Command | What it does | When to reach for it |
|---|---|---|
| **`/context`** | Inspect only — shows what's consuming the window and how full it is (system prompt, tool defs, conversation, etc.) | Anytime you want a read before deciding whether to act |
| **`/compact`** | Summarize the conversation so far, trading detail for space, **on your own timing** | Long session that's still going, but you don't need the full blow-by-blow history anymore |
| **`/clear`** | Wipe the context entirely, start with a blank slate | Starting an unrelated task, or want zero bias from prior turns |

**Important nuance:** `/compact` doesn't *keep* the past work history intact
— it **summarizes** it. That's a lossy operation: it preserves the gist, not
every detail. Auto-compact (the system doing this for you as you approach
the limit) is the *exact same mechanism*, just triggered automatically
instead of on your command — and it fires *before* the limit is truly hit,
since compacting itself needs some working room to run in.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart TB
    Ctx(["📦 Full context"]) -->|"/context"| Read(["👀 Inspect only<br/>nothing changes"])
    Ctx -->|"/compact (manual)"| Sum1(["📝 Summarized<br/>on your timing"])
    Ctx -->|"auto-compact (automatic)"| Sum2(["📝 Summarized<br/>system's timing, near limit"])
    Ctx -->|"/clear"| Empty(["🆕 Empty<br/>fresh start"])

    classDef ctx fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef read fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef sum fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef empty fill:#22C55E,stroke:#16A34A,color:#ffffff
    class Ctx ctx
    class Read read
    class Sum1 sum
    class Sum2 sum
    class Empty empty
```

## 3. Spending the budget wisely

Two levers that reduce how fast the tank fills in the first place —
different from the three commands above, which act *after* the fact.

### Pay for what you use, not what you might use

**MCP servers** load their full tool definitions into context **upfront**,
whether you end up using them or not — every connected server is a fixed
tax on the window from turn one.

**Skills** are lazy: only a short description loads upfront; the full
content only loads into context **when actually invoked**.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart LR
    subgraph MCP["🔌 MCP Server"]
        M1["Full tool schemas<br/>loaded upfront"]
    end
    subgraph SK["🎯 Skill"]
        K1["Short description<br/>loaded upfront"]
        K2["Full content —<br/>loaded only if invoked"]
    end

    classDef mcp fill:#EF4444,stroke:#DC2626,color:#ffffff
    classDef skdesc fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef skfull fill:#22C55E,stroke:#16A34A,color:#ffffff
    class M1 mcp
    class K1 skdesc
    class K2 skfull
    style MCP fill:#450A0A,stroke:#DC2626,color:#ffffff
    style SK fill:#052E16,stroke:#16A34A,color:#ffffff
```

**Practical move:** turn off MCP servers you're not actively using for the
task at hand — each one left on is a fixed cost you're paying regardless of
value delivered.

### Isolate exploration with sub-agents

A sub-agent gets its **own separate context window**. Whatever it reads,
searches, or tries stays inside its own tank — only the **final result**
gets merged back into the main conversation's context.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart LR
    Main(["🧠 Main context"]) -->|delegate| Sub

    subgraph Sub["🧩 Sub-agent — own context window"]
        direction TB
        E1["🔍 Explore, search,<br/>read files..."]
        E2["📚 all of this stays<br/>inside the sub-agent"]
        E1 --> E2
    end

    Sub -->|"only the final result"| Main2(["🧠 Main context<br/>+ small result"])

    classDef main fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef sub fill:#3B82F6,stroke:#2563EB,color:#ffffff
    class Main main
    class Main2 main
    class E1 sub
    class E2 sub
    style Sub fill:#1E3A8A,stroke:#2563EB,color:#ffffff
```

Same underlying idea as the MCP-vs-Skills point: **do the expensive,
detailed work somewhere it doesn't cost the main budget, and only pay for
the summary.**

## Summary

| Tool | Type | Effect |
|---|---|---|
| `/context` | inspect | Read-only, no change |
| `/compact` | reclaim | Manual summarization, lossy, your timing |
| auto-compact | reclaim | Same as `/compact`, system-triggered near the limit |
| `/clear` | reclaim | Full reset, no history carried forward |
| Disabling unused MCP servers | spend less upfront | Removes a fixed per-turn tax |
| Skills over MCP where possible | spend less upfront | Lazy-loaded, pay only on invocation |
| Sub-agents | spend less upfront | Isolate exploration in a separate window, merge back only the result |
