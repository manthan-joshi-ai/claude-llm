# Building with Claude API

Notes are split one file per topic — open the relevant file directly to
refresh a concept rather than scanning everything. Same pattern as
[../_01_claude_code_101](../_01_claude_code_101/).

## Topics

| # | File | Covers | Status |
|---|---|---|---|
| 00 | [00_model_overview.md](00_model_overview.md) | Opus/Sonnet/Haiku tiers — reasoning depth, cost, latency trade-offs; model-tiered strategy example | 🟢 done |
| 01 | [01_accessing_the_api.md](01_accessing_the_api.md) | The 5-stage request lifecycle; why the backend hop exists; request/response anatomy; inside the model — tokenize, embed, positional encoding, self-attention, generation/softmax/temperature | 🟢 done |
| 02 | [02_multi_turn_conversations.md](02_multi_turn_conversations.md) | Why the API is stateless; client-side message history (user + assistant turns); growing context/cost tradeoff. Notebook: [notebooks/02_multi_turn_convo.ipynb](notebooks/02_multi_turn_convo.ipynb) | 🟢 done |

*(New rows get added here as each topic is started — files are only created
when a topic is actually begun, not scaffolded ahead of time.)*
