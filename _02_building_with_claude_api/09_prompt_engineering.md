# ✍️ Prompt Engineering
---

**Definition:** the technique of writing effective prompts — the input
you give an LLM to get the output you *actually* want, not the output
you hoped for and crossed your fingers about. 🤞

## 🎲 Why it's iterative, not one-pass

An LLM is **probabilistic** — its behavior can't be predicted with
certainty. Translation: you don't get to write "the correct prompt" on
attempt #1 and just... trust it. You have to actually **test** it to
know if it works. No shortcuts, no vibes-based prompting. 🚫🔮

This is exactly why [Prompt Evaluation](07_prompt_evaluation.md) exists
as its own discipline — the two are a matched pair, joined at the hip:

1. ✍️ Write a basic prompt.
2. 🧪 Evaluate the results.
3. 🔁 Iteratively refine using prompt engineering techniques.

## 🌀 The Cycle

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
| 🎯 ① Set a goal | Define what the prompt should accomplish, and what "good" looks like |
| ✍️ ② Write an initial prompt | A basic first attempt — a baseline, not a final answer |
| 🧪 ③ Evaluate | Test it against your criteria (see [Prompt Evals Workflow](08_prompt_evals_workflow.md)) |
| 🔧 ④ Apply prompt engineering techniques | Use specific methods to improve performance |
| 🔁 ⑤ Re-evaluate | Verify the change actually improved the results — don't assume |

> [!IMPORTANT]
> ### 🧬 Change one thing at a time
> Step ④'s real discipline: make **one change per iteration**, not five
> at once like you're clearing a to-do list. If you change multiple
> things together and the score moves, you have no idea *which* change
> did it — one genuine improvement could be quietly canceling out
> another change that actually hurt. Isolate the variable. 🔬 Then build
> on what's *confirmed* to work, not what you *hope* worked.

## 🏆 Proof this actually works: the Hindi translation exercise

This cycle isn't theory-crafted, it's exactly what happened across
[08_prompt_evals_exercise.ipynb](notebooks/08_prompt_evals_exercise.ipynb)
— receipts included: 🧾

| Iteration | Score | What changed |
|---|---|---|
| 2 | 3.4 😬 | Verbose bullet-heavy prompt |
| 3 | 3.2 😅 | Simplified, but lost too much |
| 4 | 7.2 🙂 | "Human conversation" framing found |
| 5 | 9.5 😎 | Added rules (loanwords, trailing `?` nuance) |
| 6 | 9.6 🏅 | Fixed a register contradiction between two rules |

Six real iterations, each one **tested before trusting it** — the cycle
above, done for real, not just described in a diagram. That's the whole
point: prompt engineering isn't a one-shot art, it's a grind you can
actually measure. 📈
