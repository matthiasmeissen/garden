# Garden — Claude Guide

This is a personal knowledge vault built from conversations, experiments, and practice. It is fed primarily via Claude Code sessions.

## Structure

Three top-level domains:

```
garden/
  computation/       — code, embedded systems, DSP, shaders, web, tools
  making/            — woodworking, electronics, music and synthesis
  philosophy/        — principles, learning approaches, epistemology
```

Each domain and subdomain has one **hub file** named after its folder (e.g. `computation/dsp/dsp.md`). Never use `_index.md`.

Max 3 levels deep. No exceptions.

## Hub Files

Hub files are navigation only. They must stay lean — no explanatory paragraphs, no multi-bullet concept sections. A hub contains:

1. One short paragraph describing what this domain is about
2. A contents list linking to concept files: `[[filename|Display Name]] — one-line description`
3. Key Resources — one line per resource: `Title — Author — one-liner — expertise: beginner/intermediate/advanced`
4. Ideas — one line per idea

If content is more than one line, it needs its own concept file.

## Concept Files

One concept per file. Named lowercase and hyphenated (`moog-ladder-filter.md`). Start with a `# Title` h1. Include tags on the second line. End with a `## See Also` section linking to related files.

## Tags

Tags connect across domains — use them in every file. Tools get tags, not folders: `#eurorack`, `#faust`, `#vcv-rack`, `#supercollider`, `#pcb`, `#3d-printing` etc.

## Ideas

An idea is a concrete, actionable thing to do, build, learn, or acquire in the future. It is always personal intent — something the user wants to pursue. Examples:

- Learn about LoRa networks
- Sew a new jacket
- Build an injection moulding machine
- Order new chisels from Dictum
- Explore waveguide synthesis
- Build a VCV Rack module in Rust

Ideas are distinct from:
- **Insights** — things understood or figured out (go in concept files)
- **Resources** — books, tools, links worth referencing (go in Key Resources)
- **Cross-references** — connections between existing files

Claude never generates or infers ideas unprompted. Only add an idea when the user explicitly says to — e.g. "add this idea to woodworking" or "note this as an idea in DSP".

## Simple Edits

For quick tasks, just do them directly — no skill needed:
- "Add this book to woodworking resources" → add one line to `making/woodworking/woodworking.md` Key Resources
- "Add an idea to DSP" → add one line to `computation/dsp/dsp.md` Ideas
- "Create a concept file about X in philosophy" → create the file, add it to `philosophy/philosophy.md` contents

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
```