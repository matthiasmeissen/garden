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

Ideas are never generated or inferred by Claude unprompted. Claude only adds ideas when explicitly told to — e.g. "add this idea to DSP" or "note this as an idea in woodworking". The Ideas section in hub files is the user's space to curate.

The one exception: garden-care may flag an idea entry that has already been acted on (i.e. a concept file now exists for it), so the user can decide to clean it up.

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