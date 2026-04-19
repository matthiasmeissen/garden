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
    computation.md                        <- domain hub
    rust/rust.md
    embedded-systems/embedded-systems.md
    dsp/dsp.md
    shaders/shaders.md
    touchdesigner/touchdesigner.md
    game-engines/game-engines.md
    web/web.md
  making/
    making.md                             <- domain hub
    woodworking/woodworking.md
    electronics/electronics.md
    music-making-and-synthesis/music-making-and-synthesis.md
  philosophy/
    philosophy.md                         <- domain hub
    [concept files, one per idea]
```

**Hub file naming:** Every folder has one hub file named after the folder itself (e.g. `rust/rust.md`). This makes Obsidian graph nodes readable. Never use `_index.md`.

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
- The domain hub (e.g. `computation/computation.md`)
- The subdomain hub (e.g. `computation/dsp/dsp.md`)
- Any existing concept files that might overlap with what you're planting

This prevents duplicating content that's already there.

### Step 3 — Decide what goes where

Default bias: **create a new file**. Only touch an index for navigation updates, one-line resource entries, and one-line ideas.

| Content type | Action |
|---|---|
| Any named concept, approach, or idea with more than a sentence to say | Create a new concept file |
| Resource (book, tool, link) | One line in Key Resources of the relevant subdomain hub (e.g. `dsp/dsp.md`) |
| Idea or open question | One line in Ideas of the relevant subdomain hub |
| Cross-domain concept | Create file in primary domain; add See Also link in secondary domain hub |
| Philosophy / principle / approach | Create a file in `philosophy/` — e.g. `philosophy/finding-good-information.md` |
| Core vault description or "about" content | `philosophy/philosophy.md` one-paragraph description only |

**Never route full concepts, explanations, or multi-bullet sections into any hub file.**

### Step 4 — Write the files

**Creating a new concept file:**
```
# Concept Name

[tags: #tag1 #tag2]

[body: plain language, written for your future self after a long break]

## See Also
- [[../subdomain-name|Subdomain Hub]]
- [[../../other-domain/subdomain/concept|Related Concept]] — why they relate
```

**Updating any hub file (hub entries only):**
```
## Contents
- [[concept-filename|Concept Name]] — one-line description

## Key Resources
- Title — Author — one-liner — expertise: beginner/intermediate/advanced

## Ideas
- one-line idea or open question
```

**`philosophy/philosophy.md` specifically:**
- One short paragraph: what this domain is and why it exists
- Contents list linking to concept files
- No principles written out here — those live in concept files like `philosophy/ephemeralization.md`

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