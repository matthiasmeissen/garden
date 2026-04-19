---
name: garden-plant
description: Take a harvested markdown document (produced by garden-harvest) and directly write it into the garden knowledge vault. Reads existing vault files, creates new concept files, updates hub files, and adds cross-references — all using file tools. Use this skill whenever the user says "plant this in my garden", "add this to the vault", "plant this", or pastes a harvest document and wants it committed to the vault. Also trigger after garden-harvest completes when the user is ready to save learnings. This skill is designed to run inside the garden repo via Claude Code — it acts directly on files, not just produces instructions. Trigger liberally — if the user has a harvest document and wants it in the vault, this is the right tool.
---

# Garden Plant

Read a harvest document and write it directly into the garden vault using file tools.

## Context

This skill runs inside the `garden/` repo via Claude Code. It reads, creates, and edits files directly. It does not produce instructions for a human to follow.

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
    making.md
    woodworking/woodworking.md
    electronics/electronics.md
    music-making-and-synthesis/music-making-and-synthesis.md
  philosophy/
    philosophy.md
    [concept files]
```

**Hub naming:** Every folder has one hub file named after the folder. Never `_index.md`.

## Frontmatter

Every file Claude creates must include YAML frontmatter.

**Hub:**
```markdown
---
type: hub
category: computation
tags: [dsp, audio]
---
```

**Concept:**
```markdown
---
type: concept
category: computation
tags: [dsp, filters, rust]
reference: https://github.com/matthiasmeissen/dsp-playground
---
```

`reference` is optional — include when the concept directly relates to a project or external resource.

**Categories:** `computation` / `making` / `philosophy`

## The Index Budget — CRITICAL

Hub files are navigation only:
- One short paragraph description
- Contents list (one line per file)
- Key Resources (one line per resource)
- Ideas (one line per idea — user-managed only)

**Default bias: create a new concept file.** Only touch a hub for navigation and one-line entries.

## How to Plant

### Step 1 — Read the harvest

Parse: domain(s), category, tags, insights, resources, cross-references.

### Step 2 — Read the current vault state

Read the relevant hub files and any existing concept files that might overlap. Prevents duplication.

### Step 3 — Decide what goes where

| Content type | Action |
|---|---|
| Any insight or concept | New concept file in the subdomain folder |
| Resource | One line in Key Resources of subdomain hub |
| Cross-domain concept | File in primary domain; See Also link in secondary domain hub |
| Philosophy / principle / approach | New file in `philosophy/` |

**Never add ideas unprompted.**
**Never put explanatory content in hub files.**

### Step 4 — Write the files

**Concept file:**
```markdown
---
type: concept
category: [computation/making/philosophy]
tags: [tag1, tag2]
reference: [optional url]
---
# Concept Name

Body — plain language, for your future self after a long break.

## Related Concepts
- [[related-file]]
- [[other-file]] — one line on why they relate
```

**Hub update (navigation only):**
```markdown
## Contents
- [[concept-filename|Concept Name]] — one-line description

## Key Resources
- Title — Author — one-liner — expertise: beginner/intermediate/advanced
```

**`philosophy/` hub:**
- One short paragraph only
- Contents list linking to concept files
- No principles written inline

### Step 5 — Confirm and suggest commit

Summarise what was created and updated, then:

> "Planted. Suggested commit: `plant: [topic] learnings`"

Do not run git automatically.

## Naming

- Filenames: lowercase, hyphenated (`moog-ladder-filter.md`)
- Always start with `# Title` h1
- Flat within subdomains — no nested subdirectories

## What Not to Plant

- Common knowledge or beginner tutorial content
- Content already in the vault — update instead
- Raw code dumps — extract the pattern, link to the repo
- Ideas unless explicitly requested

## Error Handling

If the harvest references a subdomain that doesn't exist:
- Ask before creating a new folder
- If confirmed, create folder with hub file and update parent domain hub