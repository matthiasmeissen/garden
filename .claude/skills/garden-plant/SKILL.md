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
  principles-and-philosophy.md      ← philosophy and first principles only
  computation/
    _index.md                        ← table of contents + ideas
    rust/_index.md
    embedded-systems/_index.md
    dsp/_index.md
    shaders/_index.md
    touchdesigner/_index.md
    game-engines/_index.md
    web/_index.md
  making/
    _index.md                        ← table of contents + ideas
    woodworking/_index.md
    electronics/_index.md
    music-making-and-synthesis/_index.md
```

**File rules:**
- Max 3 levels deep — never go deeper
- One concept per file, 500–2000 words ideal
- `_index.md` files are hubs — always update them when adding concept files
- Tags connect across domains — use them in every file

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

| Content type | Action |
|---|---|
| New concept worth its own file | Create new file in subdomain folder, update subdomain `_index.md` |
| Small concept or clarification | Append to existing concept file, or add inline to subdomain `_index.md` |
| Resource (book, tool, link) | Add to Key Resources in subdomain `_index.md` |
| Idea or open question | Add to Ideas in subdomain `_index.md` |
| Cross-domain concept | Create file in primary domain; add See Also link in secondary domain `_index.md` |
| First-principles insight | Append to `principles-and-philosophy.md` |

### Step 4 — Write the files

**Creating a new concept file:**
```
# Concept Name

[tags: #tag1 #tag2]

[body: 500–2000 words, plain language, written for your future self after a long break]

## See Also
- [[../_index|Domain Index]]
- [[../../other-domain/subdomain/concept|Related Concept]] — why they relate
```

**Updating a subdomain `_index.md`:**
- Add new concept files to the table of contents as `[[filename|Display Name]]`
- Add resources to Key Resources: `- Title — Author — one-liner — expertise: beginner/intermediate/advanced`
- Add ideas to Ideas as bullet points
- Add a See Also section if cross-references exist

**Updating `principles-and-philosophy.md`:**
- Append new principles as concise bullet points under the relevant section
- Don't duplicate existing principles — read first

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