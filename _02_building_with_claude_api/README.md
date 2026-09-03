# Building with Claude API

Notes are split one file per topic — open the relevant file directly to
refresh a concept rather than scanning everything. Same pattern as
[../_01_claude_code_101](../_01_claude_code_101/).

## Topics

| # | File | Covers | Status |
|---|---|---|---|
| 00 | [00_model_overview.md](00_model_overview.md) | Opus/Sonnet/Haiku tiers — reasoning depth, cost, latency trade-offs; model-tiered strategy example | 🟢 done |
| 01 | [01_accessing_the_api.md](01_accessing_the_api.md) | The 5-stage request lifecycle; why the backend hop exists; request/response anatomy; inside the model — tokenize, embed, positional encoding, self-attention, generation/softmax/temperature | 🟢 done |
| 02 | [02_multi_turn_conversations.md](02_multi_turn_conversations.md) | Why the API is stateless; client-side message history (user + assistant turns); growing context/cost tradeoff. Notebook: [notebooks/02_multi_turn_convo.ipynb](notebooks/02_multi_turn_convo.ipynb). Practice exercise: [notebooks/02_chat_exercise.ipynb](notebooks/02_chat_exercise.ipynb) — a working `input()`-driven chat loop; fixed a real bug extracting text from `response.content` (don't assume `content[0]` is always a text block) | 🟢 done |
| 03 | [03_system_prompts.md](03_system_prompts.md) | The `system` parameter vs. `messages`; applies every turn; guardrails (soft, not hard-enforced) + defense layers; grounding vs. validating output (foreshadows RAG). Practice: [notebooks/03_system_prompts.ipynb](notebooks/03_system_prompts.ipynb) — Hindi-translation chat with a system prompt enforcing consistent output format across turns | 🟢 done |
| 04 | [04_temperature.md](04_temperature.md) | Where temperature sits in the pipeline (sampling, after generation); logit/temperature/softmax mechanism; Anthropic's 0-1 range; practical low/medium/high use-case mapping | 🟢 done |
| 05 | [05_streaming.md](05_streaming.md) | Why streaming improves UX; the message_start/content_block/message_delta/message_stop event sequence (verified against a real captured event); text_stream vs raw event iteration; live-text-then-clean-Markdown pattern. Notebook: [notebooks/05_streaming.ipynb](notebooks/05_streaming.ipynb) | 🟢 done |
| 06 | [06_structured_outputs.md](06_structured_outputs.md) | System prompt vs. real `output_config.format` (grammar-constrained, guaranteed JSON); JSON-only limitation for non-JSON/code; prefilling deprecation (wider cutoff than temperature's, Haiku 4.5 included). Notebook: [notebooks/06_structured_outputs.ipynb](notebooks/06_structured_outputs.ipynb) | 🟢 done |
| 07 | [07_prompt_evaluation.md](07_prompt_evaluation.md) | Prompt engineering vs. prompt evaluation; the three post-writing options (ship untested / manual spot-check / eval pipeline); definitions only — depth comes later in the course | 🟢 done |
| 08 | [08_prompt_evals_workflow.md](08_prompt_evals_workflow.md) | The 5-step eval loop (draft → dataset → feed → grade → iterate) with the worked math/oatmeal/Moon example; dataset generation methods; code/model/human grader types; golden answers; prompt scoring removes guesswork. Exercise: [notebooks/08_prompt_evals_exercise.ipynb](notebooks/08_prompt_evals_exercise.ipynb) — a real 6-iteration Hindi-translation eval loop (3.4 → 9.6) | 🟢 done |
| 09 | [09_prompt_engineering.md](09_prompt_engineering.md) | Why prompting is iterative (LLMs are probabilistic); the 5-step cycle (goal → initial prompt → evaluate → apply technique → re-evaluate); the "change one thing at a time" discipline; ties back to the real Hindi-translation iteration history. Exercise: [notebooks/09_prompting.ipynb](notebooks/09_prompting.ipynb) — course-provided `PromptEvaluator` scaffold, upgraded off deprecated temperature/prefill onto real `output_config.format` Structured Outputs; live-run verified (9 real test cases generated) | 🟢 done |
| 10 | [10_prompt_engineering_techniques.md](10_prompt_engineering_techniques.md) | All prompt engineering techniques on one page (easier to scan/compare): Simple + Direct (5 moves, solar-panel/geothermal examples), Be Specific (guidelines vs. process steps), Use Delimiters (keep data separate from instructions with custom XML tags), Providing Examples (one-shot/few-shot, tied back to the real Hindi-translation system prompt) | 🟢 done |

*(New rows get added here as each topic is started — files are only created
when a topic is actually begun, not scaffolded ahead of time.)*
