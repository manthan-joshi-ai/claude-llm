# 💥 Simple + Direct
---

Two techniques, one headline — they travel together. Being **simple**
without being **direct** just gets you a clean but vague prompt. Being
**direct** without being **simple** buries the instruction in jargon.
You need both. 🤝

## 🧭 The Five Moves

*(Tags in `code` at the end of each line are mine — my own memory
hooks, not official terminology.)*

- 🧼 Keep the language for your prompt simple `(Simple)`
- 🎯 Explicitly state what the task is for the LLM `(Explicit)`
- ✂️ Keep the first line crisp and clear `(First Line Principle)`
- 🗣️ Be direct — give the LLM instructions, not questions `(Direct)`
- 🏃 Use action verbs to highlight the task `(Action verbs)`

## 🔬 Examples

### 🌞 Example 1

```
Instead of:
"I need to know about those things people put on their roofs that use sun - those solar panel
things, I think they're called"

Use: "Write three paragraphs about
how solar panels work"
```

### 🌋 Example 2

```
Instead of: "I was reading about renewable energy and geothermal energy sounds neat. What countries
use it?"

Use: "Identify three countries that use geothermal energy. Include
generation stats for each."
```

Notice the pattern in both: the "instead of" version **rambles toward**
the ask — you don't know what's actually being requested until the very
end, if at all. The fixed version **leads with an action verb** (`Write`,
`Identify`) and states the exact deliverable up front. That's *Simple*,
*Explicit*, *First Line*, *Direct*, and *Action verbs* — all five moves,
in one sentence. 🎯

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif", "fontSize": "15px"}, "flowchart": {"htmlLabels": true, "padding": 20, "nodeSpacing": 35, "rankSpacing": 55}}}%%
flowchart LR
    V([" 😵‍💫 Vague, rambling prompt "]) --> S([" 🧼 Simple language "])
    S --> E([" 🎯 Explicit task "])
    E --> F([" ✂️ Crisp first line "])
    F --> D([" 🗣️ Direct instruction "])
    D --> A([" 🏃 Leads with an action verb "])
    A --> R([" ✅ Clear, gradeable prompt "])

    classDef bad fill:#EF4444,stroke:#DC2626,color:#ffffff
    classDef step fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef good fill:#22C55E,stroke:#16A34A,color:#ffffff
    class V bad
    class S step
    class E step
    class F step
    class D step
    class A step
    class R good
```

## 📈 Proof it moves the needle

Straight from the course itself: applying these five moves to a meal-
planning prompt took its evaluation score from **2.32 → 3.92** (same
1–10 scale from [Prompt Evals Workflow](08_prompt_evals_workflow.md)).

Same story as your own Hindi-translation exercise — this isn't a vibe,
it's a **measured** improvement. 📊

> [!NOTE]
> ### 📚 Source
> [Being clear and direct — Claude Academy](https://academy.claude.com/courses/building-with-the-claude-api/being-clear-and-direct)
