---
name: script
description: Use to generate a brief speaking/review script from a curated outline — produces terse bullet-point cues in Typst
---

## Script Renderer

Generates a brief script from a curated outline. The user co-created the outline, so they already understand the material — the script is a concise speaking/review guide of bullet-point cues, not a lecture transcript.

---

### Invocation

**Entry:** `/script <path-to-outline.md>` — outline path is a required argument.

---

### Process

**Step 1 — Read the outline.** Read the outline file at the given path. If the file doesn't exist or is unreadable, tell the user and stop.

**Step 2 — Parse metadata.** Extract from the metadata block:
- `Topic` — used for the document title and output filename
- `Conversation log` — path to the conversation log file

If the metadata block is missing or doesn't contain a conversation log path, proceed without log enrichment.

**Step 3 — Read the conversation log.** If a conversation log path was found and the file exists, read it. This provides context for enriching the script with key examples and analogies from the original discussion.

**Step 4 — Generate the script.** For each section in the outline:

1. Read the section's bullet points and their `[log:<start>-<end>]` references
2. If the conversation log is available, read the referenced line ranges to extract key examples, analogies, or concrete scenarios
3. If a `[log:<start>-<end>]` reference points to nonexistent lines, skip it silently and use the outline point as-is
4. Distill each point into a terse bullet-point cue

**Cue style guidelines:**
- Short phrases, not full sentences — "trigger words" that remind you what to say
- Include concrete names, numbers, or examples where they help (e.g., "Shor's algorithm — exponential speedup over classical factoring")
- Capture the *key insight* of each point, not a summary of the explanation
- If a point involves a tradeoff or comparison, state it tersely (e.g., "accuracy vs latency — can't have both without X")

**Step 5 — Write the Typst file.** Wrap the generated cues in a Typst document and write to `deliverables/<topic>-script.typ`. Create the `deliverables/` directory if it doesn't exist.

Use this format:

```typ
= Script: <topic>

== <Section Title from Outline>

- Key point as short phrase
- Another cue — concrete example name
- Core tradeoff: X vs Y

== <Next Section Title>

- Why naive approach fails
- Critical insight: <phrase>
- Open question: <phrase>
```

No `#set` overrides — Typst defaults are fine. Each outline section becomes a `==` heading. Each point becomes a terse bullet cue. No figures, no columns, no fancy layout.

**Step 6 — Handoff.** Tell the user where the script was saved:

> "Script saved to `deliverables/<topic>-script.typ`. You can compile it with `typst compile <path>`."

---

### What /script Does NOT Do

- Assume any particular outline structure (works with any outline generator)
- Generate long prose or full sentences
- Make pedagogical decisions (that's the outline generator's job)
- Add figures, diagrams, or visual elements
- Support languages other than English
- Auto-detect outlines (the user must provide the path)
