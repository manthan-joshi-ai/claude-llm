> **Spoiler note:** same rule as the AI Fluency companion doc — this is an instructor
> reference/answer-key, not a shortcut. Read a module's concept section here to prime
> intuition, but the actual `NN_*.md` notes files in this folder are written from
> *your own* understanding after we've talked it through, not copied from here.
> This file exists to keep the course map straight and track progress, not to be
> transcribed into notes.

# Building with the Claude API — Course Map & Progress

Course: Anthropic Academy, "Building with the Claude API." 9 modules, 67 lessons,
8 quizzes, ~9 hours total.

---

## Progress tracker

| Module | Lessons | Status | Notes files |
|---|---|---|---|
| 1. Accessing Claude with the API | 9 | 🟢 done | [00](00_model_overview.md)–[06](06_structured_outputs.md) |
| 2. Prompt Evaluation | 7 | 🟢 done | [07](07_prompt_evaluation.md), [08](08_prompt_evals_workflow.md) |
| 3. Prompt Engineering Techniques | 6 | 🟢 done (4/4 techniques + quiz pending) | [09](09_prompt_engineering.md) (cycle), [10](10_prompt_engineering_techniques.md) (all techniques, one page) |
| 4. Tool Use with Claude | 13 | ⚪ not started | — |
| 5. RAG and Agentic Search | 7 | ⚪ not started | — |
| 6. Features of Claude | 9 | ⚪ not started | — |
| 7. Model Context Protocol | 11 | ⚪ not started | — |
| 8. Anthropic Apps | 4 | ⚪ not started | — |
| 9. Agents and Workflows | 8 | ⚪ not started | — |
| Final Assessment | 2 | ⚪ not started | — |

*(Update this table as we go — it's the fastest way to see where we actually are.)*

---

## Module 1 — Accessing Claude with the API

Lessons: Accessing the API → Getting an API key → Making a request → Multi-turn
conversations → System prompts → Temperature → Response streaming → Structured data.

Covered end to end in notes [00](00_model_overview.md) through [06](06_structured_outputs.md),
including two real notebook exercises (chat loop, Hindi-translation system prompt) and the
deprecated-prefill/temperature cleanup work in [09_prompting.ipynb](notebooks/09_prompting.ipynb).

## Module 2 — Prompt Evaluation

Lessons: Prompt evaluation → typical eval workflow → generating test datasets → running
the eval → model-based grading → code-based grading.

Covered in [07](07_prompt_evaluation.md) (definitions) and [08](08_prompt_evals_workflow.md)
(the 5-step loop, dataset generation methods, the three grader types), backed by the real
6-iteration Hindi-translation eval exercise (3.4 → 9.6).

## Module 3 — Prompt Engineering Techniques

Lessons: Prompt engineering → **being clear and direct** → **being specific** → structure
with XML tags → providing examples.

Progress: the cycle itself is in [09](09_prompt_engineering.md); techniques live together
in [10_prompt_engineering_techniques.md](10_prompt_engineering_techniques.md) — one page
per technique, easier to scan/compare than separate files. All four techniques logged:
Simple + Direct, Be Specific, Use Delimiters, Providing Examples. Only the module quiz is
left before moving to Module 4 (Tool Use with Claude).

## Module 4 — Tool Use with Claude

Not started. Lessons: introducing tool use → project overview → tool functions → tool
schemas → handling message blocks → sending tool results → multi-turn conversations with
tools → implementing multiple turns → using multiple tools → fine-grained tool calling →
the text edit tool → the web search tool.

## Module 5 — RAG and Agentic Search

Not started. Lessons: introducing RAG → text chunking strategies → text embeddings → the
full RAG flow → implementing the RAG flow → BM25 lexical search → a multi-index RAG
pipeline.

## Module 6 — Features of Claude

Not started. Lessons: extended thinking → image support → PDF support → citations →
prompt caching → rules of prompt caching → prompt caching in action → code execution and
the Files API.

## Module 7 — Model Context Protocol

Not started. Lessons: introducing MCP → MCP clients → project setup → defining tools with
MCP → the server inspector → implementing a client → defining resources → accessing
resources → defining prompts → prompts in the client.

## Module 8 — Anthropic Apps

Not started. Lessons: Anthropic apps → Claude Code setup → Claude Code in action →
enhancements with MCP servers.

## Module 9 — Agents and Workflows

Not started. Lessons: agents and workflows → parallelization workflows → chaining
workflows → routing workflows → agents and tools → environment inspection → workflows
vs. agents.

---

## Working pattern for this course (reminder to self)

Same as always: you explain your understanding first, I verify/correct against real docs
where needed, we brainstorm, and *then* I write the `NN_*.md` note in your own words —
no fetched examples, no stats pulled from the course site, no source citations in the
notes files themselves. This `context.md` is the only place course-sourced structure
lives; the numbered notes stay yours.
