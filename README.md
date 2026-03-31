# quill

Academic deliverables in Typst. Learn a field, build an outline, render to reports, slides, or articles.

Works with [Claude Code](https://claude.ai/claude-code). Skill format inspired by [superpowers](https://github.com/obra/superpowers). Built on the foundations of [sci-brain](https://github.com/QuantumBFS/sci-brain).

## Quick Start

**Claude Code:**

```
/plugin install Br0kenSmi1e/quill
```

Then type `/overview <topic>` and start learning.

## What `/overview` Is Like

You give it a topic. It gathers research material — either from a [sci-brain](https://github.com/QuantumBFS/sci-brain) survey registry if you've run `/survey` before, or by searching the web and arxiv on its own.

Then it teaches you the field through a four-act narrative:

1. **The Problem** — why this field exists, what breaks without it
2. **The Failed Attempts** — what people tried, where and why each approach breaks
3. **The Solution Landscape** — what actually works, motivated by why the failures fail
4. **The Open Frontier** — what's still unsolved, what the barriers are

Every explanation is failure-driven — you understand solutions by first seeing why alternatives break. Every claim is grounded in a concrete example.

At the end, it generates a **markdown outline** from the conversation. You curate it — pick what to include, reorder sections, cut what doesn't matter for your deliverable. The outline references the conversation log by line range, so nothing is lost.

The outline is then ready for a renderer skill to turn into slides, a report, or an article in Typst.

## The Pipeline

```
/overview <topic>     <- learn the field, produce a curated outline
/script <outline.md>  <- turn outline into a brief speaking/review script
[renderer] (planned)  <- turn outline into slides, notes, articles, or posters
```

The outline file is the interface between the two stages. Any outline generator can feed any renderer.

## Renderers

- **Script** (`/script`) — brief bullet-point cues for speaking or review

### Planned

Four additional deliverable types:

- **Slides** — presentations, talks, conferences
- **Notes** — field entry material, less formal than articles (your "theoretic minimal")
- **Articles** — polished writeups for publication or public sharing
- **Posters** — conference posters

## Pedagogical Principles

1. **Motivate through irreplaceability** — show why the problem *must* be solved
2. **Explain through history** — origin scenarios, not textbook definitions
3. **Teach through failure** — success explained by why alternatives fail
4. **Ground in concrete scenarios** — every claim gets a specific example

## Works Great With sci-brain

If you have [sci-brain](https://github.com/QuantumBFS/sci-brain) installed, run `/survey` first to build a literature registry. `/overview` automatically picks it up for a richer experience. But sci-brain is not required — `/overview` works standalone.

```
/survey <topic>       <- (sci-brain) build a literature map
/overview <topic>     <- learn the field, produce outline
/script <outline.md>  <- brief speaking/review script
[renderer] (planned)  <- slides, notes, articles, posters
```

## MCP Servers (Optional, Recommended)

These improve research quality when no survey registry is available:

| MCP server | What it adds |
|------------|--------------|
| [arxiv-mcp-server](https://github.com/blazickjp/arxiv-mcp-server) | Search arxiv by topic, download full papers |
| [paper-search-mcp](https://github.com/langrocks/paper-search-mcp) | PubMed, bioRxiv, CrossRef |
| [Semantic Scholar MCP](https://github.com/YUZongmin/semantic-scholar-mcp) | Citation chains, related work |

Without them, everything falls back to web search — still works, just less thorough.

## Where Things Are Saved

- **Conversation logs** — `docs/discussion/YYYY-MM-DD-HHMMSS-overview-log.md`
- **References** — `docs/discussion/YYYY-MM-DD-HHMMSS-overview-references.bib`
- **Outlines** — `docs/discussion/YYYY-MM-DD-HHMMSS-overview-outline.md`
- **User profile** — `docs/discussion/user-profile.md`
- **Rendered output** — `deliverables/`

## Roadmap

- [x] `/overview` — learn a field, produce a curated outline
- [x] `/script` — outline to brief speaking/review script
- [ ] Slides renderer — outline to Typst slides
- [ ] Notes renderer — outline to Typst notes
- [ ] Articles renderer — outline to Typst articles
- [ ] Posters renderer — outline to Typst posters
- [ ] Additional outline generators

## License

MIT
