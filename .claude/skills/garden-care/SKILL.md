---
name: garden-care
description: Review and maintain the garden knowledge vault by finding duplicates, consolidating related content, flagging bloated indexes, and identifying orphaned files. Always proposes changes first and waits for approval before acting. Can be scoped to a specific domain or subdomain. Use this skill whenever the user says "tend the garden", "clean up the garden", "care for the garden", "prune the garden", "check for duplicates", "consolidate the vault", or "review the garden". Also trigger when the user says things like "the garden is getting messy" or "I think there's a lot of overlap". This skill runs inside the garden repo via Claude Code — it reads files directly and only writes after explicit user approval. Trigger liberally — if the user wants to maintain or review vault health, this is the right tool.
---

# Garden Care

Review the garden vault, identify issues, propose changes, and act only after approval.

## Context

This skill runs inside the `garden/` repo via Claude Code. It has filesystem access. It never modifies files without explicit user approval. It always shows a proposed change plan first and waits for a go-ahead.

## Garden Structure

```
garden/
  computation/
    computation.md                        <- domain hub
    rust/rust.md        embedded-systems/embedded-systems.md   dsp/dsp.md
    shaders/shaders.md  touchdesigner/touchdesigner.md         game-engines/game-engines.md
    web/web.md
  making/
    making.md
    woodworking/woodworking.md   electronics/electronics.md   music-making-and-synthesis/music-making-and-synthesis.md
  philosophy/
    philosophy.md
    [concept files]
  projects/
    [thin wrappers — data managed by script, only Related Concepts section is editable]
```

**Hub file naming:** Every folder has one hub file named after the folder (e.g. `rust/rust.md`). Never `_index.md`.

**Categories:** `computation` / `making` / `device` / `philosophy`

## Scope

If no scope is given, ask: "Should I review the whole garden, or a specific section?"

- "Care for the whole garden" → scan everything
- "Care for philosophy/" → scan only that folder
- "Care for computation/dsp" → scan only that subdomain

Never scan or modify `projects/` frontmatter or descriptions — those are script-managed.

## How to Care

### Step 1 — Read the scope

Read all files within the requested scope. Build a map of what exists, what hubs link to, and what tags are in use.

### Step 2 — Run the checks

**Missing or malformed frontmatter**
- Every file should have YAML frontmatter with `type`, `category`, and `tags`
- Hub files: `type: hub`, Concept files: `type: concept`

**Bloated hub files**
- Any hub containing explanatory paragraphs, multi-bullet concept sections, or "How I approach X" content
- Hubs should only contain: one short paragraph, contents list, key resources (one line each), ideas (one line each)

**Duplicate or overlapping content**
- Two or more files covering the same concept
- Content in a hub that duplicates a concept file

**Orphaned files**
- Concept files not linked from any hub file
- Files with no tags and no Related Concepts links

**Oversized concept files**
- Files significantly over 2000 words that could be split into two focused files

**Ideas to review**
- An idea is a concrete future action ("build X", "learn Y", "order Z") — added by user only
- Flag idea entries where a concept file already exists for that topic (acted on)
- Never rewrite, remove, or add ideas — only flag for the user to decide

**Inconsistent tags**
- Similar concepts tagged differently (e.g. `synthesis` vs `synth`)
- Flag for standardisation — don't change without approval

**Missing cross-references**
- Concept files in different domains that clearly relate but have no Related Concepts links between them

**Project files with no Related Concepts**
- Flag projects that have no concept links yet — these are opportunities to connect the vault

### Step 3 — Produce the care report

```markdown
# Garden Care Report — [scope] — [YYYY-MM-DD]

## Summary
[X files reviewed. Y issues found across Z categories.]

---

## Missing Frontmatter

### computation/dsp/filter-types.md
No frontmatter found.
→ Proposed: add frontmatter with type: concept, category: computation, tags: [dsp]

---

## Bloated Hub Files

### philosophy/philosophy.md
"First Principles" section (8 bullet points) should be a concept file.
→ Proposed: extract to `philosophy/ephemeralization.md`, replace with hub entry

---

## Duplicates & Overlap

### computation/dsp/dsp.md + computation/dsp/filters.md
Hub contains a full explanation of filter types that duplicates filters.md.
→ Proposed: remove explanation from hub, keep the link

---

## Orphaned Files

### computation/shaders/noise-functions.md
Not linked from `computation/shaders/shaders.md`.
→ Proposed: add to shaders hub contents list

---

## Ideas to Review

### computation/dsp/dsp.md — Ideas section
- "Build a node-based UI in Rust" — concept file already exists at `computation/rust/node-graph-ui.md`
→ Proposed: remove the idea entry since it has been acted on

---

## Inconsistent Tags

- `synthesis` (4 files) and `synth` (2 files) — same concept
→ Proposed: standardise to `synthesis`

---

## Missing Cross-References

### computation/dsp/ <-> making/music-making-and-synthesis/
Several DSP files relate to synthesis files but have no Related Concepts links.
→ Proposed: add links in [specific files]

---

## Project Files With No Related Concepts

### projects/dsp-playground.md
No concept links yet.
→ Flag: consider linking [[moog-ladder-filter]], [[tpt-approach]] when those files exist

---

## Approved Actions

[ ] All of the above
[ ] Only: [user specifies]
[ ] Skip: [user specifies]
```

### Step 4 — Wait for approval

After presenting the report, ask:

> "Which of these would you like me to apply? You can say 'all of it', name specific sections, or tell me what to skip."

Do not make any changes until the user responds.

### Step 5 — Apply approved changes

After completing:
- Summarise what was done
- Suggest commit: `git commit -m "care: [brief description]"`

Do not run git automatically.

## What Garden Care Never Does

- Deletes files without explicit approval
- Merges files without showing merged content first
- Changes content meaning — only structure and organisation
- Edits project file frontmatter or descriptions
- Adds or removes ideas — only flags them