# Garden — Claude Guide

This is a personal knowledge vault built from conversations, experiments, and practice. It is fed primarily via Claude Code sessions.

## Structure

```
garden/
  computation/       — code, embedded systems, DSP, shaders, web, tools
  making/            — woodworking, electronics, music and synthesis
  philosophy/        — principles, learning approaches, epistemology
```

Each domain and subdomain has one **hub file** named after its folder (e.g. `computation/dsp/dsp.md`). Never use `_index.md`.

Max 3 levels deep. No exceptions.

## Frontmatter

Every file starts with YAML frontmatter:

**Hub file:**
```markdown
---
type: hub
category: computation
tags: [dsp, audio]
---
```

**Concept file:**
```markdown
---
type: concept
category: computation
tags: [dsp, filters, rust]
reference: https://github.com/matthiasmeissen/dsp-playground
---
```

**Categories:** `computation` / `making` / `philosophy`

Tags are lowercase arrays. Reference is optional — a URL or location string when the concept relates directly to a project or resource.

## Hub Files

Navigation only. Hard limits — a hub contains only:

1. One short paragraph describing what this domain is about
2. Contents list: `[[filename|Display Name]] — one-line description`
3. Key Resources: one line per resource
4. Ideas: one line per idea (user-managed only)

If content is more than one line, it needs its own concept file.

## Concept Files

One concept per file. Named lowercase and hyphenated (`moog-ladder-filter.md`). Start with a `# Title` h1. End with a `## Related Concepts` section with wiki-links — these create the graph connections in Obsidian.

```markdown
---
type: concept
category: computation
tags: [dsp, filters]
reference: https://github.com/matthiasmeissen/dsp-playground
---
# Moog Ladder Filter

Body here — plain language, written for your future self after a long break.

## Related Concepts
- [[tpt-approach]]
- [[filter-design]]
```

## Graph Connections

Obsidian's graph is built from wiki-links only — frontmatter does not create edges. Every concept file should link to related files via `## Related Concepts`. Hub files create edges via their contents list. This is how the knowledge graph grows naturally.

## Ideas

An idea is a concrete, actionable thing to do, build, learn, or acquire. Examples:
- Learn about LoRa networks
- Sew a new jacket
- Order new chisels from Dictum

Claude never generates or infers ideas unprompted. Only adds ideas when explicitly told to.

## Simple Edits

For quick tasks, just do them directly — no skill needed:
- "Add this book to woodworking resources" → one line in `making/woodworking/woodworking.md` Key Resources
- "Add an idea to DSP" → one line in `computation/dsp/dsp.md` Ideas
- "Create a concept file about X" → create with correct frontmatter, add to hub contents

## Skills

- `garden-harvest` — extract key learnings from a conversation
- `garden-plant` — write a harvest document into the vault
- `garden-care` — review the vault, find issues, propose and apply fixes

## Commit Convention

```
plant: [topic] learnings
care: [what was tidied]
refactor: [structural change]
add: [what was added]
```