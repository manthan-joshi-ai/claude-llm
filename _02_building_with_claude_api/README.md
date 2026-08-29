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

*(New rows get added here as each topic is started — files are only created
when a topic is actually begun, not scaffolded ahead of time.)*
