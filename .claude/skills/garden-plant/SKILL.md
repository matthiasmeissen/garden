---
name: garden-plant
description: Take a harvested markdown document (produced by garden-harvest) and generate precise instructions for inserting it into the garden knowledge vault. Tells an LLM or the user exactly which files to create or update, what content to add, and what cross-references to make. Use this skill whenever the user says "plant this in my garden", "add this to the vault", "where does this go in my garden", or pastes a harvest document and wants to know how to integrate it. Also trigger after garden-harvest completes, when the user is ready to commit learnings to the vault. Trigger liberally — if the user has a harvest document and wants to get it into their garden, this is the right tool.
---

# Garden Plant

Turn a harvest document into precise vault insertion instructions.

## What This Skill Does

Reads a harvest document and produces a step-by-step instruction set for populating the garden vault. The output is designed to be handed directly to Claude Code (or another LLM with file access) to execute, or followed manually.

## Garden Structure (for reference)

```
garden/
  principles-and-philosophy.md      ← philosophy, first principles only
  computation/
    _index.md                        ← table of contents + ideas for computation
    rust/_index.md
    embedded-systems/_index.md
    dsp/_index.md
    shaders/_index.md
    touchdesigner/_index.md
    game-engines/_index.md
    web/_index.md
  making/
    _index.md                        ← table of contents + ideas for making
    woodworking/_index.md
    electronics/_index.md
    music-making-and-synthesis/_index.md
```

**File rules:**
- Max 3 levels deep
- One concept per file (500–2000 words ideal)
- `_index.md` files are hubs — update them when adding new concept files
- Tags connect across domains — use them liberally

## How to Plant

### Step 1 — Read the harvest document

Identify: domain(s), tags, concepts, resources, ideas, cross-references.

### Step 2 — Decide what goes where

For each piece of content in the harvest:

| Content type | Where it goes |
|---|---|
| New concept worth its own file | New file in the relevant subdomain folder |
| Small concept or clarification | Append to existing concept file, or add to `_index.md` |
| Resource (book, tool, link) | Key Resources section of the relevant `_index.md` |
| Idea or open question | Ideas section of the relevant `_index.md` |
| Cross-domain concept | Primary domain gets the file; secondary domain `_index.md` gets a cross-reference link |
| First-principles insight | `principles-and-philosophy.md` |

### Step 3 — Produce insertion instructions

Output a clear instruction block formatted for an LLM or human to execute. Use this format:

---

```markdown
# Plant Instructions: [Topic] — [YYYY-MM-DD]

## Summary
[1-2 sentences: what this harvest contains and where it's going]

## Files to Create

### [domain/subdomain/concept-name.md]
Create this file with the following content:

[full markdown content of the new file]

---

## Files to Update

### [domain/subdomain/_index.md]
In the **Key Resources** section, add:
- [resource entry]

In the **Ideas** section, add:
- [idea entry]

In the **table of contents**, add:
- [[concept-name|Concept Name]]

---

## Cross-References to Add

In [domain-a/subdomain/_index.md], add under a "See Also" section:
- [[../../domain-b/subdomain/concept-name|Concept Name]] — [one line on why they relate]

---

## Tags Used
[list all tags applied in this plant operation]
```

---

## Naming Conventions

- File names: lowercase, hyphenated, descriptive (`moog-ladder-filter.md`, not `filter.md`)
- Concept files start with a `# Title` h1
- Keep the structure flat within subdomains — no deeper nesting

## What Not to Plant

- Don't create files for one-off experiments with no lasting insight
- Don't duplicate content already in the vault — update existing files instead
- Don't add raw code dumps — link to the repo and extract only the pattern

## After Planting

Tell the user: "Here are your plant instructions. Hand these to Claude Code with access to your garden repo, or apply them manually. After planting, commit with a message like `plant: [topic] learnings`."