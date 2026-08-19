# CLAUDE.md
---

File-based **persistent memory** for Claude Code. Set once, reused across
every subsequent session — instead of re-explaining the same things, or
Claude re-discovering them, every single time.

## The problem it solves

Without CLAUDE.md, every new session re-runs the **Explore** stage of
[Explore → Plan → Code → Commit](02_explore_plan_code_commit.md) from
scratch — the same brainstorming, the same discovery, for things that
haven't changed since last time (conventions, setup steps, known gotchas).

CLAUDE.md lets you **skip re-Exploring** the stable stuff, so a new session
can jump straight past repeated discovery into the actual task.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart LR
    subgraph Without["🔁 Without CLAUDE.md"]
        direction TB
        S1(["Session 1<br/>🔍 Explore from zero"]) ~~~ S2(["Session 2<br/>🔍 Explore from zero"]) ~~~ S3(["Session 3<br/>🔍 Explore from zero"])
    end
    subgraph With["⚡ With CLAUDE.md"]
        direction TB
        T1(["Session 1<br/>🔍 Explore + 📄 write it down"]) --> T2(["Session 2<br/>📄 load memory, skip ahead"]) --> T3(["Session 3<br/>📄 load memory, skip ahead"])
    end

    classDef repeat fill:#EF4444,stroke:#DC2626,color:#ffffff
    classDef once fill:#22C55E,stroke:#16A34A,color:#ffffff
    classDef fast fill:#3B82F6,stroke:#2563EB,color:#ffffff
    class S1 repeat
    class S2 repeat
    class S3 repeat
    class T1 once
    class T2 fast
    class T3 fast
    style Without fill:#450A0A,stroke:#DC2626,color:#ffffff
    style With fill:#052E16,stroke:#16A34A,color:#ffffff
```

The real win isn't just speed — it's **consistency**, and one more thing
that matters even more: **it removes guesswork.** Without it, anything not
explicitly stated has to be *inferred* — your conventions, why a strange
workaround exists, what "done" actually means here — and an inference can
simply be wrong. CLAUDE.md turns those from guesses into stated fact, so
the agent acts on what you actually meant instead of its best guess at it.

### The "new employee, every single day" analogy

Without CLAUDE.md, every session is like hiring a brilliant new employee who
shows up knowing nothing about the company, gets a full onboarding briefing
from you, does great work all day — and then wakes up tomorrow with total
amnesia. Same briefing, same day, forever. 🔁

CLAUDE.md is the **onboarding doc** that new employee reads *before* their
first coffee — so day 2 starts as day 2, not day 1 again.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart TB
    Day(["🌅 New session starts"]) --> Q{"📄 Onboarding doc<br/>on file?"}
    Q -->|"No — Groundhog Day 🔁"| Brief(["🗣️ You re-explain everything<br/>from scratch, again"])
    Brief --> Work1(["💪 Good day's work"])
    Work1 -.amnesia overnight.-> Day
    Q -->|"Yes — Day 2, for real"| Read(["📖 Reads CLAUDE.md<br/>over coffee ☕"])
    Read --> Work2(["🚀 Straight to the actual task"])

    classDef q fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef bad fill:#EF4444,stroke:#DC2626,color:#ffffff
    classDef good fill:#22C55E,stroke:#16A34A,color:#ffffff
    class Day q
    class Q q
    class Brief bad
    class Work1 bad
    class Read good
    class Work2 good
```

### Or, if you'd rather think in video-game terms: it's the save file

No CLAUDE.md = a roguelike. Die (close the session), respawn at Level 1,
every single run — full inventory wiped, boss fight forgotten, that one
trap you learned about the hard way? Walking into it again.

CLAUDE.md = a **save point**. Load the file, spawn back in with your gear,
your map, and the scars you already earned — and go straight for the boss
you're actually here to fight.

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart LR
    subgraph Rogue["👾 Roguelike — no save file"]
        direction TB
        R1(["🎮 Run 1<br/>learn the trap the hard way"]) --> R2(["💀 Die / session ends"])
        R2 --> R3(["🎮 Run 2<br/>walk into the SAME trap"])
        R3 --> R4(["💀 Die / session ends"])
        R4 --> R5(["🎮 Run 3<br/>...you know how this goes"])
    end
    subgraph Save["💾 Save file — CLAUDE.md"]
        direction TB
        G1(["🎮 Run 1<br/>learn the trap"]) --> W(["💾 Write it to<br/>the save file"])
        W --> G2(["🎮 Run 2<br/>load save, trap is known,<br/>walk straight to the boss"])
        G2 --> Boss(["🏆 Boss fight<br/>the thing you actually came for"])
    end

    classDef bad fill:#EF4444,stroke:#DC2626,color:#ffffff
    classDef good fill:#22C55E,stroke:#16A34A,color:#ffffff
    classDef save fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef boss fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    class R1 bad
    class R2 bad
    class R3 bad
    class R4 bad
    class R5 bad
    class G1 good
    class G2 good
    class W save
    class Boss boss
    style Rogue fill:#450A0A,stroke:#DC2626,color:#ffffff
    style Save fill:#052E16,stroke:#16A34A,color:#ffffff
```

Every session without CLAUDE.md is a fresh character select screen. Every
session *with* it is a continue button.

## What goes in it

- Project conventions, setup/build/test commands, codebase structure
- Personal preferences (how you like things done)
- Known gotchas: root cause + solution for problems that tend to recur, so
  you don't re-debug the same thing twice

## The levels

| Level | Location | Scope |
|---|---|---|
| **Project** | root of the repo | Shared with the team (usually checked into version control) |
| **User** | user's home profile | Personal, applies across *all* projects |
| **Subdirectory** *(bonus)* | anywhere deeper in the repo | Loaded on-demand only when working in that part of the codebase — useful when a subsystem has its own conventions |

```mermaid
%%{init: {"theme": "base", "themeVariables": {"primaryColor": "#8B5CF6", "primaryTextColor": "#ffffff", "primaryBorderColor": "#7C3AED", "lineColor": "#94A3B8", "fontFamily": "Segoe UI, sans-serif"}}}%%
flowchart TB
    U(["👤 User-level CLAUDE.md<br/>personal, all projects"]) --> Sess(["🚀 Session start"])
    P(["📁 Project-level CLAUDE.md<br/>root, shared with team"]) --> Sess
    Sess --> Task(["Working in a subsystem?"])
    Task -->|yes| Sub(["📂 Subdirectory CLAUDE.md<br/>loaded on-demand"])
    Task -->|no| Go(["✅ Proceed with loaded memory"])
    Sub --> Go

    classDef user fill:#3B82F6,stroke:#2563EB,color:#ffffff
    classDef project fill:#8B5CF6,stroke:#7C3AED,color:#ffffff
    classDef sess fill:#F59E0B,stroke:#D97706,color:#ffffff
    classDef sub fill:#14B8A6,stroke:#0D9488,color:#ffffff
    classDef go fill:#22C55E,stroke:#16A34A,color:#ffffff
    class U user
    class P project
    class Sess sess
    class Task sess
    class Sub sub
    class Go go
```

## Quick-add shortcut

Typing `#` at the start of a message in Claude Code appends whatever
follows straight into the memory file — handy for capturing a root-cause
note the moment you hit it, without manually opening and editing the file.

## Same pattern, different tool

This is the same idea as Claude's own general memory system (project/user
level files, loaded automatically so context doesn't need to be rebuilt
from scratch each session) — just applied specifically inside Claude Code.
