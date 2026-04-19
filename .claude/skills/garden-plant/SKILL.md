---
name: garden-plant
description: Take a harvested markdown document (produced by garden-harvest) and directly write it into the garden knowledge vault. Reads existing vault files, creates new concept files, updates hub files, and adds cross-references — all using file tools. Use this skill whenever the user says "plant this in my garden", "add this to the vault", "plant this", or pastes a harvest document and wants it committed to the vault. Also trigger after garden-harvest completes when the user is ready to save learnings. This skill is designed to run inside the garden repo via Claude Code — it acts directly on files, not just produces instructions. Trigger liberally — if the user has a harvest document and wants it in the vault, this is the right tool.
---

# Garden Plant

Read a harvest document and write it directly into the garden vault using file tools.

## Context

This skill runs inside the `garden/` repo via Claude Code. It has filesystem access. It reads, creates, and edits files directly. It does not produce instructions for a human to follow.

## Garden Structure

```
garden/
  computation/
    computation.md                        <- domain hub
    rust/rust.md                          <- subdomain hub
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
  projects/
    [one .md per project — thin wrappers, data managed by script]
```

**Hub file naming:** Every folder has one hub file named after the folder (e.g. `rust/rust.md`). Never use `_index.md`.

## Frontmatter

Every file Claude creates must include YAML frontmatter.

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

**Categories:** `computation` / `making` / `device` / `philosophy`

## The Index Budget — CRITICAL

Hub files are navigation only. Hard limits:
- One short paragraph description
- Contents list (one line per file)
- Key Resources (one line per resource)
- Ideas (one line per idea — user-managed only)

No explanatory paragraphs. No multi-bullet concept sections. If content is more than one line, it needs its own concept file.

**Default bias: create a new file.** Only touch a hub for navigation updates and one-line resource entries.

## How to Plant

### Step 1 — Read the harvest document

Parse out: domain(s), category, tags, insights, resources, related projects, cross-references.

### Step 2 — Read the current vault state

Before writing, read:
- The relevant subdomain hub (e.g. `computation/dsp/dsp.md`)
- Any existing concept files that might overlap

This prevents duplicating content already there.

### Step 3 — Decide what goes where

| Content type | Action |
|---|---|
| Any named insight or concept | Create a new concept file in the subdomain folder |
| Resource (book, tool, link) | One line in Key Resources of the subdomain hub |
| Cross-domain concept | Create file in primary domain; add See Also link in secondary domain hub |
| Philosophy / principle / approach | Create a file in `philosophy/` |
| Related project | Add wiki-link to `## Related Concepts` in the relevant `projects/` file |

**Never add ideas unprompted. Only add an idea if the user explicitly asks.**
**Never route full concepts or explanations into any hub file.**

### Step 4 — Write the files

**Concept file template:**
```markdown
---
type: concept
category: [computation/making/device/philosophy]
tags: [tag1, tag2]
---
# Concept Name

[Body — plain language, written for your future self after a long break.]

## Related Concepts
- [[related-file]]
- [[other-file]] — one line on why they relate
```

**Hub update (navigation entries only):**
```markdown
## Contents
- [[concept-filename|Concept Name]] — one-line description

## Key Resources
- Title — Author — one-liner — expertise: beginner/intermediate/advanced
```

**Project file — Related Concepts only:**
```markdown
## Related Concepts
- [[concept-filename]] — one line on how it relates
```
Never edit frontmatter or description in project files — those are managed by script.

**`philosophy/` hub specifically:**
- One short paragraph: what this domain is and why it exists
- Contents list linking to concept files
- No principles written inline — those live in concept files

### Step 5 — Confirm and suggest commit

After writing, summarise what was created and updated, then tell the user:

> "Planted. Suggested commit: `plant: [topic] learnings`"

Do not run git automatically.

## Naming Conventions

- Filenames: lowercase, hyphenated (`moog-ladder-filter.md`)
- No spaces, no uppercase
- Concept files always start with a `# Title` h1
- Flat within subdomains — no subdirectories inside subdomain folders

## What Not to Plant

- One-off experiments with no lasting insight
- Content already in the vault — update instead of duplicating
- Raw code dumps — extract the pattern only, link to the repo
- Frontmatter or descriptions in project files

## Error Handling

If the harvest references a subdomain that doesn't exist yet:
- Check with the user before creating a new subdomain folder
- If confirmed, create the folder with a fresh hub file and update the parent domain hub