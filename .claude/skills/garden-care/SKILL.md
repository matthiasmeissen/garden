---
name: garden-care
description: Review and maintain the garden knowledge vault by finding duplicates, consolidating related content, flagging bloated indexes, and identifying orphaned files. Always proposes changes first and waits for approval before acting. Can be scoped to a specific domain or subdomain. Use this skill whenever the user says "tend the garden", "clean up the garden", "care for the garden", "prune the garden", "check for duplicates", "consolidate the vault", or "review the garden". Also trigger when the user says things like "the garden is getting messy" or "I think there's a lot of overlap". This skill runs inside the garden repo via Claude Code — it reads files directly and only writes after explicit user approval. Trigger liberally — if the user wants to maintain or review vault health, this is the right tool.
---

# Garden Care

Review the garden vault, identify issues, propose changes, and act only after approval.

## Context

Runs inside the `garden/` repo via Claude Code. Never modifies files without explicit user approval. Always shows a proposed change plan first.

## Garden Structure

```
garden/
  computation/
    computation.md    rust/rust.md    embedded-systems/embedded-systems.md
    dsp/dsp.md        shaders/shaders.md    touchdesigner/touchdesigner.md
    game-engines/game-engines.md    web/web.md
  making/
    making.md
    woodworking/woodworking.md    electronics/electronics.md
    music-making-and-synthesis/music-making-and-synthesis.md
  philosophy/
    philosophy.md    [concept files]
```

**Categories:** `computation` / `making` / `philosophy`

## Scope

If no scope given, ask: "Should I review the whole garden, or a specific section?"

## How to Care

### Step 1 — Read the scope

Read all files in scope. Map what exists, what hubs link to, what tags are in use.

### Step 2 — Run the checks

**Missing or malformed frontmatter**
- Every file needs `type`, `category`, `tags`
- Hubs: `type: hub` — Concepts: `type: concept`

**Bloated hub files**
- Hubs with explanatory paragraphs, multi-bullet sections, or "How I approach X" content
- Hubs should only contain: one paragraph, contents list, key resources (one line), ideas (one line)

**Duplicate or overlapping content**
- Two files covering the same concept
- Hub content that duplicates a concept file

**Orphaned files**
- Concept files not linked from any hub
- Files with no tags and no Related Concepts links

**Oversized concept files**
- Files significantly over 2000 words that could split into two focused files

**Ideas to review**
- Ideas are added by user only — never touch without flagging
- Flag entries where a concept file already exists for that topic
- Never add, remove, or rewrite ideas

**Inconsistent tags**
- Similar concepts tagged differently (e.g. `synthesis` vs `synth`)
- Flag for standardisation, don't change without approval

**Missing cross-references**
- Concept files that clearly relate but have no `## Related Concepts` links
- These are missing graph edges in Obsidian

### Step 3 — Produce the care report

```markdown
# Garden Care Report — [scope] — [YYYY-MM-DD]

## Summary
[X files reviewed. Y issues found across Z categories.]

---

## Missing Frontmatter
### computation/dsp/filter-types.md
No frontmatter found.
→ Proposed: add type: concept, category: computation, tags: [dsp]

---

## Bloated Hub Files
### philosophy/philosophy.md
"First Principles" section should be a concept file.
→ Proposed: extract to `philosophy/ephemeralization.md`, replace with hub entry

---

## Duplicates & Overlap
### computation/dsp/dsp.md + computation/dsp/filters.md
Hub contains full explanation that duplicates filters.md.
→ Proposed: remove from hub, keep link

---

## Orphaned Files
### computation/shaders/noise-functions.md
Not linked from shaders hub.
→ Proposed: add to shaders hub contents list

---

## Ideas to Review
### computation/dsp/dsp.md
- "Build a node-based UI in Rust" — concept file already exists at rust/node-graph-ui.md
→ Flag: consider removing since it has been acted on

---

## Inconsistent Tags
- `synthesis` (4 files) and `synth` (2 files)
→ Proposed: standardise to `synthesis`

---

## Missing Cross-References
### computation/dsp/ <-> making/music-making-and-synthesis/
Related files with no wiki-links between them — missing graph edges.
→ Proposed: add Related Concepts links in [specific files]

---

## Approved Actions
[ ] All of the above
[ ] Only: [user specifies]
[ ] Skip: [user specifies]
```

### Step 4 — Wait for approval

> "Which of these would you like me to apply?"

Do not make any changes until the user responds.

### Step 5 — Apply and commit

After completing: summarise what was done, suggest commit:

> `git commit -m "care: [brief description]"`

Do not run git automatically.

## What Garden Care Never Does

- Deletes files without approval
- Merges files without showing merged content first
- Changes content meaning — structure and organisation only
- Adds, removes, or rewrites ideas