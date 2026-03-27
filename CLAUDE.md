# CLAUDE.md

## Project Overview

Quill is a skill-based plugin for AI coding assistants that produces academic deliverables in Typst. It follows a two-stage pipeline: outline generation (understanding a topic and structuring it) followed by rendering (producing slides, notes, articles, or posters).

## Architecture

**Outline as interface:** Multiple skills can generate a markdown outline file. Renderers consume the outline and produce Typst deliverables. The outline format is the contract between the two halves.

```
[Outline Generators]           [Renderers]
  /overview ──┐                 ┌── slides (.typ)
  /??? ───────┼── outline.md ──┼── notes (.typ)
  /??? ───────┘                 ├── articles (.typ)
                                └── posters (.typ)
```

## Skills

- **overview** — Interactive field overview using a failure-driven four-act narrative. Teaches a topic, then produces a curated markdown outline from the conversation. Optionally uses sci-brain survey registry if available, otherwise does its own research.

## Key Conventions

- Outline format: Markdown (structure + content markers + conversation references)
- Output format: Typst
- Conversation logs: `docs/discussion/`
- Design docs: `docs/plans/`
