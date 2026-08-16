> **Spoiler note:** the "Worked example" / "Capstone" blocks below are the instructor's answer key, not a
> shortcut. If you want hints-only coaching in chat (which is how we're running this), read the concept
> sections freely but hold off on the worked-example blocks for a given exercise until *after* you've
> attempted it yourself and gotten feedback — otherwise you'll just be reading the answer.

# AI Fluency: Framework & Foundations — Study Notes & Instructor Guide

Course: Anthropic Academy, by Prof. Joseph Feller (UCC) & Prof. Rick Dakan (Ringling College).
~3 hours, 10 modules, ends in a quiz + certificate. Also mirrored on Coursera.

> **How to use this doc:** Read a module's section here *before* you open it in Skilljar — it primes the
> intuition so the reading lands faster. Do the exercise on a **real task from your own work**, not a toy
> example — the course is designed that way on purpose (see "Get the best out of it" at the bottom). Then
> paste what you produced back into this chat and I'll critique it like a real instructor would — that's
> where the actual skill-building happens, not in reading alone.

---

## 0. The one-sentence version

AI fluency ≠ prompting tricks. It's a repeatable discipline for deciding **what to hand to AI, how to
brief it, how to judge what comes back, and how to stay accountable for it** — the 4 D's: **Delegation →
Description → Discernment → Diligence**, run in a loop, not a straight line.

---

## 1. Course map

| # | Module | Time | Type |
|---|--------|------|------|
| 1 | Introduction to AI Fluency | 4 min | reading |
| 2 | The AI Fluency Framework | 15 min | reading (2) + **Exercise 1 (5 min, likely)** |
| 3 | Deep Dive 1 — What is Generative AI | 13 min | reading (2) |
| 4 | **Delegation** | 26 min | reading (2) + hands-on (unconfirmed) |
| 5 | **Description** | 10 min | reading |
| 6 | Deep Dive 2 — Effective Prompting Techniques | 10 min | reading |
| 7 | **Discernment** | 5 min | reading |
| 8 | The Description–Discernment Loop | 10 min | reading + **hands-on** |
| 9 | **Diligence** | 20 min | reading |
| 10 | Conclusion | ~1 hr | reading + self-assessment + **quiz** |

The four bolded modules (4, 5, 7, 9) are the actual framework; everything else is scaffolding around them.

---

## 2. The core mental model: the 4D Framework × 3 Modes

**The 4 D's** (competencies, used in a loop, not once):

- **Delegation** — deciding *what* to hand off to AI and *how much control* to keep.
- **Description** — briefing the AI so it can actually succeed (the "spec").
- **Discernment** — judging the output critically before you trust or use it.
- **Diligence** — owning the consequences: what you created, what you disclosed, what happens downstream.

**The 3 Modes** (how much the AI is doing per task):

- **Automation** — AI does it end-to-end, no human in the loop per-instance (low stakes, fully verifiable).
- **Augmentation** — human and AI go back and forth; human stays in the driver's seat.
- **Agency** — AI operates with autonomy over multiple steps, human sets goals/guardrails and checks in at intervals.

**Intuition:** these aren't fixed labels for a *tool* — they're a decision you make per *task*, and often per
*subtask*. The same person writing the same report might automate the citation formatting, augment the
argument-building, and never delegate the final sign-off at all. Delegation is the act of picking the right
mode for each piece of work based on **stakes** (how bad is it if wrong?), **reversibility** (can you undo
it?), and **verifiability** (can you actually check the output, or are you just trusting it?).

Keep this matrix in your head — you'll use it in every exercise below.

---

## 3. Module-by-module walkthrough

### Module 1 — Introduction to AI Fluency
**Point:** reframes the course as being about *collaboration with AI*, not *tool mechanics*. No exercise —
just sets the frame: you're building a working relationship/process, not memorizing prompts.

### Module 2 — The AI Fluency Framework ⭐ (Exercise 1 attaches here, not Module 4 — see note)
**Point:** "Why fluency matters" + first look at the 4D × 3-mode framework (section 2 above).
**Intuition to take away:** fluency is what lets you move *fluidly* between modes as a task evolves —
starting augmented, escalating to agentic once you trust the pattern, dropping back to augmented the moment
stakes rise.

**📍 Placement note:** based on the user's own reported sequence (finished the "4D Framework" reading →
went straight into Exercise 1), Exercise 1 lives right here, immediately after this module — not attached
to Module 4 as originally guessed. Not 100% confirmed (no literal Skilljar screenshot of the nav), but
strong circumstantial evidence. See Module 4 below for the exercise's actual (verified) text.

### Module 3 — Deep Dive 1: What is Generative AI
**Point:** mental model of the underlying system — context windows, emergent capabilities, knowledge
cutoffs, hallucination, reasoning limits.
**Why it matters for later modules:** this is the *technical grounding* for Discernment (Module 7/8) — you
can't judge an output critically if you don't know *why* models fail (pattern-completion without a source
of truth, no persistent memory outside context, confident-sounding errors near the edges of training data).
**Pro tip:** map each limitation to a Discernment check now — e.g. "knowledge cutoff" → always ask "could
this fact have changed since training?" for anything time-sensitive.

---

### Module 4 — Delegation

**⚠️ Correction:** this section used to claim Module 4 "has the first hands-on exercise" and described an
invented "executable delegation plan" exercise (goal → decomposition → mode-per-subtask → checkpoints →
fallback), built from a vague marketing-copy description before ever seeing the actual exercise text. Two
things were wrong: the invented exercise structure, and the module it was attached to — Exercise 1 (below)
almost certainly belongs to **Module 2** (see the placement note there), not here. Keeping the verified
exercise text below for reference since it's already written up; Module 4 itself may or may not have its
own separate hands-on activity — unconfirmed either way. Confirmed, verbatim, from the user pasting the
actual Skilljar page:

> **Exercise 1: Apply the 4D's** — *Estimated time: 5 minutes*
>
> Pick one of these collaboration scenarios and consider how you might apply the 4D Framework:
>
> - **Communication project** — drafting a series of marketing-campaign emails with an AI assistant.
> - **Research project** — using AI to analyze a large dataset for a research paper.
> - **Creative project** — collaborating with AI on character concepts for a story.
>
> For your chosen scenario, answer one short question per D:
> - **Delegation** — what would you handle yourself vs. collaborate on with AI?
> - **Description** — how would you communicate your vision/context/success-criteria to the AI?
> - **Discernment** — what criteria would you use to evaluate the AI's output?
> - **Diligence** — what transparency/responsibility considerations matter here?

That's it — a ~5 minute reflection exercise, one short answer per D, on **one** scenario (the three given,
though nothing stops you from picking your own real project instead — see note below). It is *not* asking
for a full project decomposition, mode-by-mode justification, checkpoints, or a fallback plan.

**What to actually do with the deeper material below:** the goal/decomposition/mode/checkpoint/fallback
structure, the worked competitive-analysis example, and the pitfall/intuition notes are still genuinely
good *bonus* practice — a much more rigorous version of the same 4D thinking, useful for actually building
delegation instinct rather than just passing the module. Just don't mistake it for what Exercise 1
literally requires. If you already did the deep version on a real project (e.g. scoping an actual tool
you're building), you've over-delivered relative to the exercise — answering the real Exercise 1's 4
one-liners off the back of that work will now take you two minutes.

<details>
<summary>Bonus deep-practice version (optional, not the real exercise — click to expand)</summary>

A fuller "executable delegation plan" you can build for real practice, beyond what Exercise 1 asks:

1. **Goal / definition of done** — one sentence, plus what "done and good" looks like.
2. **Decomposition** — break the project into subtasks. This is the single highest-leverage step; most bad
   delegation happens because people delegate a *vague whole* instead of *scoped parts*.
3. **Mode per subtask** — for each subtask, pick Automation / Augmentation / Agency, and *justify it* against
   stakes / reversibility / verifiability.
4. **Checkpoints** — where do you review before the next subtask starts?
5. **Fallback** — what do you do if the AI output at a checkpoint is wrong?

**Worked example** (use this as a template, don't copy it — swap in your own project):

> **Project:** Write a competitive-analysis report on 4 competitors for an internal strategy doc.
> - Research each competitor's public positioning → **Augmentation** (verifiable against sources, but needs
>   your judgment on what's relevant) → checkpoint: skim each summary for obviously wrong/outdated claims.
> - Draft comparison table (features/pricing) → **Automation** once you've supplied the raw data (low
>   stakes, easy to eyeball-verify a table).
> - Write the "so what does this mean for us" section → **Agency**, but tightly scoped: AI drafts a first
>   pass reasoning through implications, you don't accept it uncritically — this is high-stakes,
>   low-verifiability territory (opinion, not fact), so the checkpoint here is mandatory, not optional.
> - Final sign-off / anything going to leadership → **stays human**, always. Not delegated at all.

**Common pitfall:** delegating the *whole report* as one Agency task with no checkpoints — the "vague
whole" failure mode. It feels efficient but you lose the ability to catch drift early.

**Optimal-solution intuition:** good delegation plans look almost boringly modular — small subtasks, an
explicit mode + reason for each, and checkpoints placed *before* irreversible or hard-to-verify steps.

</details>

---

### Module 5 — Description
**Point:** the Description framework — three lenses for briefing the AI:

- **Product Description** — what the output should *be*: format, length, audience, tone.
- **Process Description** — *how* to get there: steps, sources, method, reasoning approach you want used.
- **Performance Description** — the *bar* it needs to clear: quality standard, constraints, explicit
  things to avoid.

**Intuition:** this maps almost exactly to a PRD/spec (what / how / how-good), and it's the antidote to
under-specified prompts. Most disappointing AI output traces back to only having specified Product ("write
me a summary") and skipping Process and Performance entirely.

**Quick self-check for any prompt you write from now on:** does it answer *what* (Product), *how*
(Process), and *how good / what to avoid* (Performance)? If you can only answer one, that's your prompt's
weak point.

### Module 6 — Deep Dive 2: Effective Prompting Techniques
Six concrete techniques, each of which is really just a tool for filling in one of the three Description
lenses above:

| Technique | Feeds which lens |
|---|---|
| Providing context | Process (grounds *how* it should reason) |
| Showing examples (few-shot) | Product + Performance (shows the bar concretely) |
| Defining constraints | Performance |
| Decomposing tasks | Process |
| Requesting reasoning ("think step by step") | Process — also makes Discernment *possible*, since you can now inspect the reasoning, not just the answer |
| Assigning role / tone | Product |

**Pro tip:** "requesting reasoning" is the highest-leverage technique for the Discernment module that comes
next — a visible reasoning trace is what you actually evaluate; a bare answer gives you nothing to discern.

---

### Module 7 — Discernment
**Point:** evaluating output quality and catching reasoning problems.
**Intuition:** discernment is not "does this sound right" — it's a checklist mindset:
- Can I verify the factual claims against a source I trust?
- Does the reasoning chain actually support the conclusion, or does it just *sound* fluent?
- Is this confident-but-wrong on something near a training-cutoff edge (tie back to Module 3)?
- Would I catch an error here, given my own expertise on this topic? (If not — that's a signal to raise the
  mode down from Agency to Augmentation for this subtask, looping back to Delegation.)

### Module 8 — The Description–Discernment Loop (hands-on)
**⚠️ Same caveat as Module 4:** the exercise description below is inferred from marketing copy, not
confirmed against the live course text. Treat it as bonus-practice framing until verified — paste the real
exercise text when you get there and I'll correct this the same way Module 4 got fixed.

**Exercise (unverified):** apply iterative refinement to a multi-step project.
**What the loop actually is:**

```
Describe → get output → Discern gaps → refine the Description (not just "try again") → repeat
```

**The key skill here, and the thing people get wrong:** when output is bad, the instinct is to regenerate.
The *optimal* move is to diagnose *which lens failed* — was Product unclear? Process under-specified? Was
the bar in Performance never stated? — and fix *that specific lens* in your next Description. This turns
each iteration into a targeted fix instead of a random re-roll, and it's exactly analogous to
debugging-by-hypothesis rather than debugging-by-guessing.

**Practice it on:** take the project from your Module 4 delegation plan, run one subtask through 2–3 loop
iterations, and note in your plan *what lens you fixed* each time. That artifact — a short log of
"iteration → what was wrong → which lens I fixed → result" — is the strongest evidence you actually
internalized this module.

---

### Module 9 — Diligence
**Point:** responsible AI use through three lenses:

- **Creation** — how was this actually made? (attribution, what's genuinely yours vs. AI-drafted)
- **Transparency** — have you disclosed AI involvement to the people who need to know?
- **Deployment** — who is affected once this output goes out into the world, and what could go wrong for
  them?

**Intuition:** Diligence is Delegation's mirror image — Delegation asks "what am I comfortable handing off,"
Diligence asks "what am I still accountable for, regardless of who/what did the work." Delegating a task
never delegates the accountability.

**Practical habit:** for anything leaving your desk, ask all three lenses explicitly before sending — most
people only ever think about Transparency ("should I mention I used AI"), and skip Creation (did I actually
verify my own contribution vs. just relaying) and Deployment (whose interests are on the line if this is
wrong).

---

### Module 10 — Conclusion
Wraps with: competency self-assessment, building a **personalized prompt library** (worth doing for real —
save your best Description templates from Modules 4–8), a structured development plan, and the final
15-minute quiz for the certificate.

**Before the quiz:** the quiz tests the framework vocabulary precisely (4D names, 3 modes, the three
Description lenses, the three Diligence lenses) — re-skim section 2–3 of this doc rather than the raw
readings; it's denser and faster.

---

## 4. Capstone: run one real task through all four D's

Pick something you actually need to do this week. Example — "prepare onboarding notes for a new teammate":

1. **Delegate:** decompose (gather-facts / structure-doc / write-tone) → mode each (Augment / Automate /
   Agency-with-checkpoint) → checkpoints before the doc goes to the teammate.
2. **Describe:** Product = "a 1-page onboarding doc, markdown, casual-but-precise tone." Process = "pull
   from our existing docs, don't invent processes we don't have." Performance = "flag anything you're
   unsure is still accurate."
3. **Discern:** check every claimed process against what you know is actually current; check the reasoning
   behind any prioritization AI made ("why did it put repo access before Slack invites?").
4. **Diligence:** Creation — you reviewed and own this, not just relayed it. Transparency — mention to the
   teammate this was AI-drafted/human-reviewed if that matters in your org's norms. Deployment — a wrong
   onboarding doc wastes a new hire's first week, so the review checkpoint isn't optional here.

Do this once, deliberately, and the whole framework stops being vocabulary and becomes a habit.

---

## 5. Getting the best out of the course

- **Use your own real project for every exercise**, not the course's suggestions if it gives generic ones —
  the entire course is designed around "scope a real project," so a toy example under-trains you.
- **Don't read Modules 4–9 passively.** After each, immediately do the 2-minute version of its exercise on
  something on your actual plate today.
- **Build the prompt library as you go**, not just in Module 10 — save your best Description write-ups
  (Product/Process/Performance) from Module 5 onward; by the end you'll have a working template set instead
  of a blank page.
- **Come back here module by module.** Paste me your delegation plan, your Description prompt, or your
  Description–Discernment log, and I'll review it against the "optimal-solution intuition" notes above —
  that feedback loop is where this actually turns into skill, not the readings alone.
- **Retake the self-assessment in Module 10 seriously** — it's the only part of the course that points at
  *your* specific weak D, which is more useful than the generic content.

---

## 6. One-page cheat sheet

- **4 D's:** Delegate → Describe → Discern → be Diligent (loop, not line).
- **3 Modes:** Automation (no human per-instance) / Augmentation (human drives) / Agency (AI drives,
  human checks in).
- **Pick mode by:** stakes, reversibility, verifiability.
- **3 Description lenses:** Product (what) / Process (how) / Performance (how good / avoid what).
- **6 prompting techniques:** context, examples, constraints, decomposition, request reasoning, role/tone.
- **Discernment checklist:** verify claims → check reasoning chain → watch training-cutoff edges → "would I
  catch an error here?"
- **3 Diligence lenses:** Creation (how made) / Transparency (disclosed?) / Deployment (who's affected).
- **The loop that fixes bad output:** diagnose *which Description lens* failed, fix that lens, don't just
  regenerate.
