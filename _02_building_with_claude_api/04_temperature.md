# Temperature
---

**Temperature** — how much randomness we want in the output.

## Recap: where this sits in the pipeline

Same transformer pipeline from
[Accessing the API](01_accessing_the_api.md), for context:

**Tokenization → Embedding → Positional Encoding → Self-Attention
(Contextualization) → Generation → Softmax → Sampling**

Temperature acts at the very last step — **sampling** — after the input
has already been fully processed. It doesn't touch tokenization,
embedding, or attention at all; it only shapes *how the final token gets
picked* from the probabilities the model already computed.

## The actual mechanism

The generation step produces a raw score (**logit**) for every possible
next token — not yet a probability. **Temperature divides those logits
before softmax converts them into a probability distribution:**

```
adjusted_logit = logit / temperature
```

This division is *why* low vs. high temperature behaves the way it
does:

- **Low temperature** (e.g. 0.1) — dividing by a small number
  **stretches apart** the differences between logits, so after softmax
  the already-most-likely token becomes even more dominant. Sharper,
  more deterministic distribution.
- **High temperature** (e.g. 1.5–2, on providers that allow it) —
  dividing by a large number **shrinks** the differences between
  logits, so after softmax the probabilities flatten out and even
  low-probability tokens get a real shot. More varied/creative
  distribution.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif", "fontSize": "15px"}, "flowchart": {"htmlLabels": true, "padding": 20, "nodeSpacing": 35, "rankSpacing": 55}}}%%
flowchart TB
    L(["🎯 Raw logits<br/>from generation"]) --> D{"➗ Divide by<br/>temperature"}
    D -->|"low temp<br/>e.g. 0.1"| Sharp(["📈 Sharper distribution<br/>top token dominates"])
    D -->|"high temp<br/>e.g. 1.5-2"| Flat(["📉 Flatter distribution<br/>low-prob tokens viable"])
    Sharp --> SM1(["Softmax"])
    Flat --> SM2(["Softmax"])
    SM1 --> S1(["🎲 Sample<br/>→ deterministic-ish"])
    SM2 --> S2(["🎲 Sample<br/>→ varied/creative"])

    classDef logit fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef divide fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef sharp fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef flat fill:#EC4899,stroke:#DB2777,color:#ffffff
    classDef sample fill:#22C55E,stroke:#16A34A,color:#ffffff
    class L logit
    class D divide
    class Sharp sharp
    class Flat flat
    class SM1 sharp
    class SM2 flat
    class S1 sample
    class S2 sample
```

## Confirmed behavior

| | Low Temperature | High Temperature |
|---|---|---|
| Distribution shape | Sharper, peaked | Flatter |
| Most likely token | Even more dominant | Less dominant |
| Low-probability tokens | Rarely chosen | Real chance of being chosen |
| Output character | More deterministic | More creative/varied |

> [!IMPORTANT]
> ### Anthropic's temperature range is 0 to 1 — not 0 to 2
> Some other providers (e.g. OpenAI) allow a 0–2 range. Anthropic's API
> caps at 1. Worth keeping straight since the groupings below assume
> the 0–1 scale.

## Practical mapping: temperature by use case

| Range | Band | Use cases |
|---|---|---|
| **0.0 – 0.3** | 🧊 Low | Factual responses, coding assistance, data extraction, content moderation |
| **0.4 – 0.7** | 🌤️ Medium | Summarization, educational content, problem-solving, creative writing with constraints |
| **0.8 – 1.0** | 🔥 High | Brainstorming, creative writing, marketing content, joke generation |

**The underlying logic:** low temperature suits tasks with **one
"correct" or clearly-best answer** — a fact, a working piece of code, an
extracted data value — where variation is a bug, not a feature. High
temperature suits tasks where **multiple good answers exist** and
variety/novelty is actually the goal. Medium sits in between: enough
structure to stay coherent and on-task, enough freedom to not sound
robotic (e.g. summarizing without just parroting word-for-word, or
creative writing that still respects given constraints).

## A real-world wrinkle: temperature is being deprecated on newer models

Discovered this hands-on while building the practice notebook, and it's
worth knowing before picking a model to test temperature against.

> [!WARNING]
> ### Not every current model still accepts `temperature`
> Per Anthropic's own docs and SDK release notes: on **Claude Opus
> 4.7+, Sonnet 5, Fable, and Mythos**, `temperature` is deprecated —
> only the default value is accepted, and a non-default value (even
> something like `0.2`) gets the **entire request rejected with a 400
> error**. These models replaced it with a different, unrelated
> parameter: **`effort`** (`low`/`medium`/`high`/`xhigh`/`max`), which
> controls *how much reasoning/exploration the model does before
> answering* — not randomness. Temperature and effort are mutually
> exclusive on a single request.
>
> **Claude Haiku 4.5 still supports classic numeric temperature
> (0.0–1.0)** — it predates this generation's shift to `effort`. Use
> Haiku 4.5 for temperature exercises going forward, e.g.
> `claude-haiku-4-5-20251001`.

**Separately, the SDK itself changed too:** `anthropic` v1.0+ removed
`temperature` from `messages.create()`'s typed parameter list entirely
(a client-side change, on top of the model-side deprecation above). The
workaround, if staying on the latest SDK: route it through `extra_body`,
which merges arbitrary keys into the raw request body, bypassing the
client's type-checked signature:

```python
response = client.messages.create(
    model="claude-haiku-4-5-20251001",
    max_tokens=1024,
    messages=messages,
    extra_body={"temperature": temperature}   # instead of temperature=... directly
)
```

**Effort vs. temperature, for clarity — two genuinely different axes:**

| | Temperature | Effort |
|---|---|---|
| Controls | Randomness in **token sampling** (which token gets picked from the computed probabilities) | How much **reasoning/exploration** the model does before answering |
| Same amount of "thinking"? | Yes — only the final pick changes | No — more effort means more computation spent |
| Available on | Haiku 4.5 and earlier-generation models | Opus 4.7+, Sonnet 5, Fable, Mythos |
| Values | Continuous, 0.0–1.0 | Discrete: low / medium / high / xhigh / max |
