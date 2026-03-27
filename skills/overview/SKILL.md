---
name: overview
description: Use when learning a field and building an outline — teaches through a failure-driven four-act narrative, then produces a curated markdown outline for downstream renderers
---

## Overview

An interactive field overview that teaches newcomers through a failure-driven, four-act narrative. The overview *teaches* and produces a **curated outline** — it does not render final deliverables (that's a renderer's job).

### Four Pedagogical Principles

These principles drive every explanation throughout the session:

1. **Motivate through irreplaceability** — show why the problem *must* be solved and can't be avoided.
2. **Explain through history, not textbooks** — go back to the origin scenario, not abstract definitions.
3. **Teach through failure** — success is explained by why alternatives fail. Never say "this method succeeds because it can do X." Say "this method succeeds because others cannot do X."
4. **Ground in concrete scenarios** — every claim gets a specific example or thought experiment. No claim without illustration.

---

### Prologue

**Entry:** `/overview <topic>` — topic is a required argument.

**Step 1 — Gather research material.** Check for a survey registry at `~/.claude/survey/<topic>/` and `.claude/survey/<topic>/`.

- **If found:** Read `summary.md` and `references.bib` from the registry.
- **If not found:** Do your own research. Use WebSearch, arxiv MCP, Semantic Scholar MCP, or whatever tools are available. Gather enough material (key papers, historical context, known approaches) to support the four-act narrative. Store references in `docs/discussion/YYYY-MM-DD-HHMMSS-overview-references.bib`.

**Step 2 — User background.** Check for `docs/discussion/user-profile.md`. If found, read it and summarize what you know:

> "I have your profile from before — [brief summary]. Anything changed, or shall we dive in?"

If not found, ask the user's background: field, experience level, and what they already know about this topic. Save the profile to `docs/discussion/user-profile.md`.

**Step 3 — Identify the central problem.** Analyze the gathered material to identify the field's central problem — the one thing that makes this field necessary.

If the material reveals multiple independent problems (i.e., the topic spans several sub-fields), present them via `AskUserQuestion` and let the user pick which one to focus on.

---

### Additional Research

Before starting the narrative, search beyond any existing material for:
- **Origin story** — who first faced this problem, when, what was the context
- **Historical failed approaches** — what was tried and why it didn't work
- **Common misconceptions** newcomers have about this field

Store additional references in `docs/discussion/YYYY-MM-DD-HHMMSS-overview-references.bib`. Quality is relaxed — blogs, tutorials, lecture notes, Wikipedia articles are all fine. Only requirement: a working URL.

**Never modify the survey registry** (if one was found).

---

### Conversation Log

Maintain a running log at `docs/discussion/YYYY-MM-DD-HHMMSS-overview-log.md` (timestamp from session start). Create the `docs/discussion/` directory if it doesn't exist.

**Append-only logging.** Save progress by appending to the log at checkpoints. Each append captures the **full conversation content** since the last save — all options presented (with descriptions), reasoning shared, user responses, search results, and key explanations. Not a summary — a readable record of what was actually said.

**When to append (checkpoints):**
- Every 3-5 exchanges, at a natural pause — when a topic wraps up or the conversation shifts
- At act transitions (entering Act 1, Act 2, Act 3, Act 4)
- At session wrap-up (Epilogue)

Don't log after every message. Wait for a natural checkpoint — the end of a thread, a comprehension check, a topic shift.

**Order: log first, then reply.** At a checkpoint, append to the log file before writing your response to the user. This ensures progress is saved even if the session is interrupted mid-reply.

**File header** — write once when creating the log:

```markdown
# Overview Session — YYYY-MM-DD HH:MM
## Topic: <topic>
```

---

### Act 1 — The Problem

Show why this field exists and why the problem *cannot* be left unsolved.

- **What breaks without this field?** Give a concrete scenario showing what goes wrong.
- **Why can't you ignore the problem?** Show that avoidance leads to something worse.
- **Why can't existing tools from other fields solve it?** Demonstrate with a specific example where an obvious approach from outside the field falls apart.

**Goal:** The user feels this problem *cannot* be left unsolved — it demands its own field.

**Pause for questions.** After presenting Act 1, check comprehension:

> "Does it make sense why [the problem] can't just be handled by [obvious alternative]? Any questions before we look at what people tried?"

---

### Act 2 — The Failed Attempts

Be **broad** — cover as many failed approaches as possible, not just a select few. The user should see the full landscape of what was tried before the field matured.

**Phase 1 — Catalog.** Compile a comprehensive numbered list of *all* failed approaches found in the research material. Each entry gets a one-liner: name + core intuition. The goal is breadth.

**Phase 2 — Deep-dive.** Pick the most instructive failures — the ones that teach the most about why the problem is hard — and give each the full treatment:

- **What it tried** — the intuition behind it
- **Where it breaks** — a concrete example of the failure mode
- **What it teaches** — what this failure reveals about the shape of the problem

Briefly explain why these were chosen for the deep-dive.

**Phase 3 — User choice.** After the deep-dives, invite the user to explore further:

> "Any of the other approaches you'd like me to unpack?"

If the user picks entries from the catalog, give them the same full treatment.

The user builds intuition for *why the problem is hard* by seeing the full landscape of what doesn't work. Each failure narrows the space of possible solutions, making the real solution feel inevitable.

**Pause for questions.** After all deep-dives (and any user-requested expansions) are done, check comprehension:

> "Does it make sense why [approach] breaks down when [scenario]? Before we see what actually works — based on these failures, what properties would a solution need to have?"

---

### Act 3 — The Solution Landscape

Now the real solutions, motivated by the failures in Act 2. The user should feel that these solutions are *inevitable* given what they've learned about the problem.

**If multiple solutions exist:** Compare by what the *others can't do*, not what each one can do. For each solution, explain which failure from Act 2 it specifically overcomes — and which failures it doesn't.

**If one solution dominates:** Explain why alternatives fail, which reveals why the winner works. The dominant solution is understood through the inadequacy of its competitors.

Always connect back to Act 2: "Remember how [naive approach] broke because of [X]? [Solution] handles this by [Y]."

**Pause for questions.** After presenting the solution landscape, check comprehension:

> "Does it make sense how [solution] avoids the problems we saw with [failed approach]? Any questions before we look at what's still open?"

---

### Act 4 — The Open Frontier

What's still unsolved. For each open problem, explain three things using concrete scenarios:

1. **Why it matters** — what breaks or stays impossible if unsolved, what becomes possible if solved.
2. **What the barrier is** — a concrete example of where current approaches fail. The barrier can take many forms: engineering/resource limitations, missing mathematical proofs, knowledge gaps between communities, lack of experimental data, or the need for a fundamentally new idea. Explain the specific barrier concretely rather than categorizing it.
3. **What people believe could work** — promising directions and what's still missing.

**Pause for questions.** After presenting the open frontier, check comprehension:

> "Any of these open problems particularly interesting to you? Questions about the barriers?"

---

### Epilogue — Outline Generation

**Step 1 — Recap.** Give a brief recap of the four-act arc: the problem that demanded this field, the approaches that failed and what they taught, the solutions that emerged, and the frontier that remains.

**Step 2 — Generate draft outline.** Produce a markdown outline from the conversation. Each point references the conversation log by line range. Use this format:

```markdown
# Overview Outline: <topic>

## Metadata
- Topic: <topic>
- Date: YYYY-MM-DD
- Conversation log: docs/discussion/YYYY-MM-DD-HHMMSS-overview-log.md
- References: docs/discussion/YYYY-MM-DD-HHMMSS-overview-references.bib

## Act 1: The Problem
- <point summary> [log:<start>-<end>]
- <point summary> [log:<start>-<end>]

## Act 2: The Failed Attempts
- <Approach>: <core intuition>
  - What it tried [log:<start>-<end>]
  - Where it breaks [log:<start>-<end>]

## Act 3: The Solution Landscape
- <Solution>: overcomes <failure> [log:<start>-<end>]

## Act 4: The Open Frontier
- <Open problem>: <why it matters> [log:<start>-<end>]
```

The `[log:<start>-<end>]` references point to line ranges in the conversation log. The renderer reads both files.

**Step 3 — Student curates.** Present the draft outline to the user. The user decides:
- What to keep, cut, or reorder
- Which points are most important for their deliverable

Incorporate the user's feedback and produce the final outline.

**Step 4 — Save.** Write the final outline to `docs/discussion/YYYY-MM-DD-HHMMSS-overview-outline.md`.

**Step 5 — Handoff.** The outline is ready for a renderer skill. Tell the user:

> "Your outline is saved. When you're ready, use a renderer skill to turn it into slides, a report, or an article."

---

### Interaction Style

- **Section-by-section pauses** — pause for questions after each act. Don't rush through; let the user absorb.
- **Comprehension checkpoints** on hard conceptual leaps: "Does it make sense why X fails here?"
- **Re-explain on confusion** — if the user is confused, re-explain using a different analogy or concrete example. Never repeat the same explanation.
- **Cite key format** — use `[AuthorYear]` when referencing papers (e.g., `[Shor1994]`).

---

### What /overview Does NOT Do

- Make presentation decisions (that's the renderer's job)
- Generate a finished document (that's the renderer's job)
- Require sci-brain (uses survey registry if available, researches independently if not)
- Add presentation annotations to the outline (the renderer decides figures vs. text)
