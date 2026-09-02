# Prompt Engineering
---

**Definition:** the technique of writing effective prompts — the input
you give an LLM to get the output you actually want.

## Why it's iterative, not one-pass

An LLM is **probabilistic** — its behavior can't be predicted with
certainty. That means you can't just write "the correct prompt" in a
single attempt and trust it; you have to actually test it to know if it
works.

This is exactly why [Prompt Evaluation](07_prompt_evaluation.md) exists
as its own discipline — the two are a matched pair:

1. Write a basic prompt.
2. Evaluate the results.
3. Iteratively refine using prompt engineering techniques.

## The cycle

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif", "fontSize": "15px"}, "flowchart": {"htmlLabels": true, "padding": 20, "nodeSpacing": 35, "rankSpacing": 55}}}%%
flowchart LR
    G([" 🎯 ① Set a goal "]) --> P([" ✍️ ② Write initial prompt "])
    P --> E([" 🧪 ③ Evaluate "])
    E --> T([" 🔧 ④ Apply technique "])
    T --> R([" 🔁 ⑤ Re-evaluate "])
    R -->|" verify it actually helped "| T

    classDef goal fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef draft fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef eval fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef apply fill:#EC4899,stroke:#DB2777,color:#ffffff
    classDef re fill:#22C55E,stroke:#16A34A,color:#ffffff
    class G goal
    class P draft
    class E eval
    class T apply
    class R re
```

| Step | What it means |
|---|---|
| ① Set a goal | Define what the prompt should accomplish, and what "good" looks like |
| ② Write an initial prompt | A basic first attempt — a baseline, not a final answer |
| ③ Evaluate | Test it against your criteria (see [Prompt Evals Workflow](08_prompt_evals_workflow.md)) |
| ④ Apply prompt engineering techniques | Use specific methods to improve performance |
| ⑤ Re-evaluate | Verify the change actually improved the results — don't assume |

> [!IMPORTANT]
> ### Change one thing at a time
> Step ④'s real discipline: make **one change per iteration**, not
> several at once. If you change multiple things together and the score
> moves, you don't actually know *which* change caused it — one
> improvement could be masking another change that quietly hurt. Isolate
> the variable, then build on what's confirmed to work.

## Proof this actually works: the Hindi translation exercise

This cycle isn't theoretical — it's exactly what happened across
[08_prompt_evals_exercise.ipynb](notebooks/08_prompt_evals_exercise.ipynb):

| Iteration | Score | What changed |
|---|---|---|
| 2 | 3.4 | Verbose bullet-heavy prompt |
| 3 | 3.2 | Simplified, but lost too much |
| 4 | 7.2 | "Human conversation" framing found |
| 5 | 9.5 | Added rules (loanwords, trailing `?` nuance) |
| 6 | 9.6 | Fixed a register contradiction between two rules |

Six real iterations, each one tested before trusting it — the cycle
above, done for real, not just described.
