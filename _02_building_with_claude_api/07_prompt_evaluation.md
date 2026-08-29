# Prompt Evaluation
---

*Definitions only for now — the deeper mechanics (grading methods,
building an actual eval pipeline) come later in the course as their
own topics.*

## Prompt Engineering

Techniques that help you write effective, better prompts — so Claude
understands exactly what you're asking for, and how you want it to
respond.

## Prompt Evaluation

But how do you actually measure whether a prompt is effective and
well-written? That's what **prompt evals** are for: an automated test
to measure how well a prompt works.

What it does:
- Tests against expected answers
- Compares different versions of the same prompt
- Reviews outputs for errors

> **Together:** prompt engineering + prompt evaluation = *building
effective prompts, and testing how they perform.*

## What to do once a prompt is written

| Option | Approach | Risk |
|---|---|---|
| 1 | Test once, ship to production | An unexpected user input breaks production |
| 2 | Test with ~4-5 use cases + edge cases, then wait | Still relies on real users to surface what wasn't covered |
| 3 | Build an eval pipeline, score it, iterate | More upfront work — but reliable, and scales |

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif", "fontSize": "15px"}, "flowchart": {"htmlLabels": true, "padding": 20, "nodeSpacing": 35, "rankSpacing": 60}}}%%
flowchart LR
    P([" ✍️ Prompt written "]) --> O1([" ① Ship untested "])
    P --> O2([" ② Manual spot-check "])
    P --> O3([" ③ Eval pipeline "])
    O1 --> R1([" 🔥 Breaks in prod<br/>on unexpected input "])
    O2 --> R2([" 🤞 Users find<br/>what you missed "])
    O3 --> R3([" ✅ Caught during<br/>development "])

    classDef start fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef risky fill:#EF4444,stroke:#DC2626,color:#ffffff
    classDef mid fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef good fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef out fill:#22C55E,stroke:#16A34A,color:#ffffff
    class P start
    class O1 risky
    class O2 mid
    class O3 good
    class R1 risky
    class R2 mid
    class R3 out
```

## Option 3: the evaluation-first approach

- Identify weaknesses before they become production issues
- Compare different prompt versions objectively
- Iterate with confidence, based on measurable improvements
- Build more reliable AI applications

> **The goal:** catch problems during development — not after users
encounter them.
