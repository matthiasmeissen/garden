---
name: garden-plant
description: Take a harvested markdown document (produced by garden-harvest) and directly write it into the garden knowledge vault. Reads existing vault files, creates new concept files, updates _index.md hubs, and adds cross-references — all using file tools. Use this skill whenever the user says "plant this in my garden", "add this to the vault", "plant this", or pastes a harvest document and wants it committed to the vault. Also trigger after garden-harvest completes when the user is ready to save learnings. This skill is designed to run inside the garden repo via Claude Code — it acts directly on files, not just produces instructions. Trigger liberally — if the user has a harvest document and wants it in the vault, this is the right tool.
---

# Garden Plant

Read a harvest document and write it directly into the garden vault using file tools.

## Context

This skill runs inside the `garden/` repo via Claude Code. It has filesystem access. It does not produce instructions for a human to follow — it reads, creates, and edits files directly.

## Garden Structure

```
garden/
  computation/
    _index.md                        <- table of contents + ideas
    rust/_index.md
    embedded-systems/_index.md
    dsp/_index.md
    shaders/_index.md
    touchdesigner/_index.md
    game-engines/_index.md
    web/_index.md
  making/
    _index.md                        <- table of contents + ideas
    woodworking/_index.md
    electronics/_index.md
    music-making-and-synthesis/_index.md
  philosophy/
    _index.md                        <- core principles and manifesto
    [concept files, one per idea]
```

**File rules:**
- Max 3 levels deep — never go deeper
- One concept per file, 500–2000 words ideal
- `_index.md` files are navigation hubs only — they must stay lean (see Index Budget below)
- Tags connect across domains — use them in every file
- When in doubt, create a new file rather than expanding an index

## The Index Budget — CRITICAL

`_index.md` files serve one purpose: **navigation**. They are not content files.

An `_index.md` must contain only:
1. A one-paragraph description of what this domain/subdomain is about
2. A table of contents linking to concept files (`[[filename|Display Name]]`)
3. A Key Resources list — one line per resource, no prose
4. An Ideas section — one line per idea, no prose

**Hard limits:**
- No explanatory paragraphs in indexes
- No sections with multiple bullet points expanding on a concept
- No "How I approach X" sections — those belong in concept files
- If content is more than one line, it needs its own file

This applies equally to `philosophy/_index.md`. The philosophy index is a signpost to concept files, not a place to write philosophy.

## How to Plant

### Step 1 — Read the harvest document

Parse out: domain(s), tags, concepts, decisions, resources, ideas, cross-references.

### Step 2 — Read the current vault state

Before writing anything, read the relevant existing files:
- The domain `_index.md` (e.g. `computation/_index.md`)
- The subdomain `_index.md` (e.g. `computation/dsp/_index.md`)
- Any existing concept files that might overlap with what you're planting

This prevents duplicating content that's already there.

### Step 3 — Decide what goes where

Default bias: **create a new file**. Only touch an index for navigation updates, one-line resource entries, and one-line ideas.

| Content type | Action |
|---|---|
| Any named concept, approach, or idea with more than a sentence to say | Create a new concept file |
| Resource (book, tool, link) | One line in Key Resources of the relevant `_index.md` |
| Idea or open question | One line in Ideas of the relevant `_index.md` |
| Cross-domain concept | Create file in primary domain; add See Also link in secondary domain `_index.md` |
| Philosophy / principle / approach | Create a file in `philosophy/` — e.g. `philosophy/finding-good-information.md`, `philosophy/learning-strategies.md` |
| Core vault description or "about" content | `philosophy/_index.md` one-paragraph description only |

**Never route full concepts, explanations, or multi-bullet sections into any `_index.md`.**

### Step 4 — Write the files

**Creating a new concept file:**
```
# Concept Name

[tags: #tag1 #tag2]

[body: plain language, written for your future self after a long break]

## See Also
- [[../_index|Domain Index]]
- [[../../other-domain/subdomain/concept|Related Concept]] — why they relate
```

**Updating any `_index.md` (index entries only):**
```
## Contents
- [[concept-filename|Concept Name]] — one-line description

## Key Resources
- Title — Author — one-liner — expertise: beginner/intermediate/advanced

## Ideas
- one-line idea or open question
```

**`philosophy/_index.md` specifically:**
- One short paragraph: what this domain is and why it exists
- Contents list linking to concept files
- No principles written out here — those live in concept files like `ephemeralization.md`, `finding-good-information.md`

### Step 5 — Confirm and suggest commit

After writing all files, summarise what was planted (files created, files updated) and tell the user:

> "Planted. Suggested commit: `plant: [topic] learnings`"

Do not run git automatically — leave committing to the user.

## Naming Conventions

- File names: lowercase, hyphenated, descriptive (`moog-ladder-filter.md` not `filter.md`)
- No spaces, no uppercase in filenames
- Concept files always start with a `# Title` h1
- Keep structure flat within subdomains — no subdirectories inside subdomain folders

## What Not to Plant

- One-off experiments with no lasting insight
- Content already in the vault — update instead of duplicating
- Raw code dumps — extract the pattern only, link to the repo for full code
- Conversational filler from the harvest

## Error Handling

If the harvest document references a subdomain that doesn't exist yet (e.g. `computation/faust/`):
- Check with the user before creating a new subdomain folder
- If confirmed, create the folder with a fresh `_index.md` and update the parent domain `_index.md`