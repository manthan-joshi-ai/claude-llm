# Model Overview
---

Anthropic offers three main model families — **Opus**, **Sonnet**, and
**Haiku**. All three share the same core LLM foundation. What differs
between them is **how they approach a task, how much time/computation they
spend on it, and how well/accurately they solve it** — reasoning depth,
speed, and cost scale together across the three tiers.

*(A fourth tier, Fable, also exists — positioned above Opus. Its specific
characterization, e.g. use case around security, is unverified against
course material and not written up here until confirmed.)*

## ⚡ 60-Second Revision Snapshot

| | 🧠 Opus | ⚖️ Sonnet | ⚡ Haiku |
|---|:---:|:---:|:---:|
| **Reasoning** | ●●●●● | ●●●○○ | ●●○○○ *(no extended thinking)* |
| **Speed** | ●●○○○ | ●●●○○ | ●●●●● |
| **Cost** | ●●●●● | ●●●○○ | ●○○○○ |
| **Pick it for** | Complex, long-running work | Everyday practical work | Speed/cost-sensitive, simple work |

## The three tiers

> [!IMPORTANT]
> ### 🧠 Opus — deepest reasoning
>
> - Most intelligent model, highest cost, generally higher latency — the
>   extra time is spent reasoning toward a better-quality answer.
> - Can still return a quick response for genuinely simple tasks — latency
>   scales with task complexity, not a fixed cost.
> - **Use when:** complex, independent, long-running work — e.g.
>   independent software development, tasks that need real reasoning
>   depth.

> [!TIP]
> ### ⚖️ Sonnet — the balanced default
>
> - Most widely used among developers — handles almost all practical,
>   common tasks well.
> - Moderate cost, moderate reasoning, faster than Opus.
> - The right default for most use cases — good balance of outcome vs.
>   cost/latency.
> - **Use when:** code implementation from a spec/design doc, process
>   automation, image analysis — the everyday workload.

> [!NOTE]
> ### ⚡ Haiku — fastest, cheapest
>
> - Fastest latency, lowest cost.
> - **Does not support extended thinking** (no dedicated step-by-step
>   deliberation mode before answering) — per the course, this is why
>   it's described as having "no reasoning." Worth being precise about
>   what that actually means: it's still a capable LLM that follows
>   instructions and produces coherent, structured output — it just
>   lacks that one dedicated reasoning mechanism the other two tiers
>   have. Not "low quality" in general, just a lower ceiling for deep,
>   multi-step problems.
> - **Use when:** speed/cost matter most, or for simple tasks —
>   text/info retrieval, translation, and user-facing production apps
>   like chat support or a Q&A agent.

## Quick comparison

| | Opus | Sonnet | Haiku |
|---|---|---|---|
| Reasoning depth | Highest | Moderate | No extended thinking |
| Cost | Highest | Moderate | Lowest |
| Latency | Higher (task-dependent) | Faster than Opus | Fastest |
| Best for | Complex/long-running work | Everyday practical tasks | Speed/cost-sensitive, simple/high-volume tasks |

## Practical takeaway: tier the model to the task, not the app

A single application doesn't have to pick one model for everything. A
model-tiered strategy for a dev workflow, as an example:

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif", "fontSize": "15px"}, "flowchart": {"htmlLabels": true, "padding": 22, "nodeSpacing": 35, "rankSpacing": 60}}}%%
flowchart LR
    Plan(["🧠 Opus<br/>plan + design the<br/>scalable architecture"]) --> Data(["⚡ Haiku<br/>retrieve/extract data<br/>from docs, fast + cheap"])
    Data --> Reason(["🧠 Opus<br/>reason over the<br/>retrieved data"])
    Reason --> Build(["⚖️ Sonnet<br/>implement against<br/>the design doc"])

    classDef opus fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef haiku fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef sonnet fill:#3B82F6,stroke:#2563EB,color:#ffffff
    class Plan opus
    class Reason opus
    class Data haiku
    class Build sonnet
```

This is a real cost-optimization pattern in production LLM applications:
spend the expensive, high-reasoning model only where reasoning depth is
actually needed, and use the cheap/fast model for high-volume, low-
complexity legwork like data retrieval.
