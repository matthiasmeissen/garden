# Garden — Claude Guide

This is a personal knowledge vault built from conversations, experiments, and practice. It is fed primarily via Claude Code sessions.

## Structure

```
garden/
  computation/       — code, embedded systems, DSP, shaders, web, tools
  making/            — woodworking, electronics, music and synthesis
  philosophy/        — principles, learning approaches, epistemology
  projects/          — thin wrappers around projects.json, one file per project
```

Each domain and subdomain has one **hub file** named after its folder (e.g. `computation/dsp/dsp.md`). Never use `_index.md`.

Max 3 levels deep. No exceptions.

## Frontmatter

Every file starts with YAML frontmatter. Use these types:

**Hub file:**
```markdown
---
type: hub
category: computation
tags: [dsp, audio, rust]
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

**Project file:**
```markdown
---
type: project
category: computation
tags: [rust, embedded, rp2350]
reference: https://github.com/matthiasmeissen/clocked-modulator
---
```

**Categories:** `computation` / `making` / `device` / `philosophy`
- `computation` — pure software and code projects
- `making` — pure physical and craft projects
- `device` — own hardware with firmware, where computation and making meet
- `philosophy` — principles, approaches, epistemology

Tags are arrays matching the projects.json vocabulary. Reference is a URL or location string (e.g. "Dropbox", "Physical").

## Hub Files

Hub files are navigation only. They must stay lean — no explanatory paragraphs, no multi-bullet concept sections. A hub contains:

1. One short paragraph describing what this domain is about
2. A contents list linking to concept files: `[[filename|Display Name]] — one-line description`
3. Key Resources — one line per resource: `Title — Author — one-liner — expertise: beginner/intermediate/advanced`
4. Ideas — one line per idea (user-managed, see below)

If content is more than one line, it needs its own concept file.

## Concept Files

One concept per file. Named lowercase and hyphenated (`moog-ladder-filter.md`). Start with a `# Title` h1. End with a `## Related Concepts` section with wiki-links.

```markdown
---
type: concept
category: computation
tags: [dsp, filters]
---
# Moog Ladder Filter

Body here — plain language, written for your future self after a long break.

## Related Concepts
- [[tpt-approach]]
- [[filter-design]]
```

## Project Files

Thin wrappers around `projects.json`. One file per project, named after the JSON key (e.g. `clocked-modulator.md`). Data is updated by script from the JSON — do not edit the frontmatter manually. The `## Related Concepts` section is the only part Claude should ever write to.

```markdown
---
type: project
category: device
tags: [rust, embassy, embedded, rp2350, midi, easyeda, pcb]
reference: https://github.com/matthiasmeissen/clocked-modulator
---
# Clocked Modulator

Clocked modulation MIDI controller on a Raspberry Pi Pico 2, built in embedded Rust.

## Related Concepts
<!-- Wiki-link concept notes here as they grow, e.g. [[moog-ladder-filter]] -->
```

## Ideas

An idea is a concrete, actionable thing to do, build, learn, or acquire in the future. Examples:
- Learn about LoRa networks
- Sew a new jacket
- Build an injection moulding machine
- Order new chisels from Dictum
- Explore waveguide synthesis

Ideas are never generated or inferred by Claude unprompted. Claude only adds ideas when explicitly told to — e.g. "add this idea to DSP" or "note this as an idea in woodworking".

Ideas are distinct from insights (concept files), resources (Key Resources), and cross-references.

The one exception: garden-care may flag an idea entry where a concept file already exists for that topic, so the user can decide to clean it up.

## Simple Edits

For quick tasks, just do them directly — no skill needed:
- "Add this book to woodworking resources" → add one line to `making/woodworking/woodworking.md` Key Resources
- "Add an idea to DSP" → add one line to `computation/dsp/dsp.md` Ideas
- "Create a concept file about X in philosophy" → create the file with correct frontmatter, add it to `philosophy/philosophy.md` contents
- "Link this concept to the Clocked Modulator project" → add a wiki-link to `projects/clocked-modulator.md` Related Concepts

## Skills

For complex or repeatable tasks, use the installed skills:
- `garden-harvest` — extract key learnings from a conversation into a structured harvest document
- `garden-plant` — take a harvest document and write it into the vault
- `garden-care` — review the vault, find issues, propose and apply fixes

## Commit Convention

```
plant: [topic] learnings
care: [what was tidied]
refactor: [structural change]
add: [what was added]
```