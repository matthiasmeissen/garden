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
    [concept files]
```

**Hub file naming:** Every folder has one hub file named after the folder itself (e.g. `rust/rust.md`). Hub files are navigation only — not content files.

## Scope

The user may ask to care for the whole vault or a specific section:

- "Care for the whole garden" → scan everything
- "Care for philosophy/" → scan only that folder
- "Care for computation/dsp" → scan only that subdomain

If no scope is given, ask: "Should I review the whole garden, or a specific section?"

## How to Care

### Step 1 — Read the scope

Read all files within the requested scope. Build a mental map of:
- What files exist and what they contain
- What each `_index.md` links to
- What tags are in use

### Step 2 — Run the checks

Check for each of the following issues:

**Bloated hub files**
- Any hub file (e.g. `dsp/dsp.md`, `philosophy/philosophy.md`) containing explanatory paragraphs, multi-bullet concept sections, or "How I approach X" content
- Hub files should only contain: one-paragraph description, contents list, key resources (one line each), ideas (one line each)

**Duplicate or overlapping content**
- Two or more files covering the same concept
- Content in an index that duplicates a concept file
- Harvests from different sessions that landed in the same place and now repeat each other

**Orphaned files**
- Concept files not linked from any hub file
- Files with no tags and no See Also links

**Oversized concept files**
- Files significantly over 2000 words that could be split into two focused files

**Stale ideas**
- Ideas are added manually by the user and should not be touched by plant or harvest
- Care may flag ideas that have grown into full concept files already (i.e. the idea was acted on and a file now exists) so the idea entry can be cleaned up
- Never remove or rewrite ideas — only flag them for the user to decide

**Inconsistent tags**
- Similar concepts tagged differently across files (e.g. `#synthesis` vs `#synth`)
- Tags used only once that might be redundant

**Missing cross-references**
- Concept files in different domains that clearly relate but have no See Also links between them

### Step 3 — Produce the care report

Output a structured report grouped by issue type. For each issue, show exactly what the proposed change is. Keep it scannable — the user should be able to read it quickly and decide what to approve.

Format:

---

```markdown
# Garden Care Report — [scope] — [YYYY-MM-DD]

## Summary
[X files reviewed. Y issues found across Z categories.]

---

## Bloated Hub Files

### philosophy/philosophy.md
The "First Principles" section (8 bullet points) and "How I Approach Topics" section should move to concept files.
→ Proposed: extract to `philosophy/ephemeralization.md` and `philosophy/learning-strategies.md`, replace with hub entries

---

## Duplicates & Overlap

### computation/dsp/dsp.md + computation/dsp/filters.md
The hub contains a full explanation of filter types that duplicates filters.md.
→ Proposed: remove the explanation from the hub, keep the link

---

## Orphaned Files

### computation/shaders/noise-functions.md
Not linked from `computation/shaders/shaders.md`.
→ Proposed: add to shaders hub contents list

---

## Oversized Files

### philosophy/finding-good-information.md
~3200 words. Covers both the problem (algorithmic bias) and the solution (upstream sources).
→ Proposed: split into `finding-good-information.md` (the approach) and `algorithmic-incentives.md` (the problem)

---

## Ideas to Review

### computation/dsp/dsp.md — Ideas section
- "Build a node-based UI in Rust" — a concept file already exists at `computation/rust/node-graph-ui.md`
→ Proposed: remove the idea entry since it has been acted on

---

## Inconsistent Tags

- `#synthesis` (used in 4 files) and `#synth` (used in 2 files) — same concept
→ Proposed: standardise to `#synthesis` across all files

---

## Missing Cross-References

### computation/dsp/ ↔ making/music-making-and-synthesis/
Several DSP concept files relate directly to synthesis files but have no See Also links.
→ Proposed: add cross-references in [list of specific files]

---

## Approved Actions

[ ] All of the above
[ ] Only: [user specifies]
[ ] Skip: [user specifies]
```

---

### Step 4 — Wait for approval

After presenting the report, ask:

> "Which of these would you like me to apply? You can say 'all of it', name specific sections, or tell me what to skip."

Do not make any changes until the user responds.

### Step 5 — Apply approved changes

Once approved, make only the changes the user confirmed. After completing:
- Summarise what was done (files created, updated, removed)
- Suggest a commit: `git commit -m "care: [brief description of what was tidied"`

Do not run git automatically — leave committing to the user.

## What Garden Care Never Does

- Deletes files without explicit approval
- Merges files without showing the merged content first
- Changes content meaning — only structure and organisation
- Acts on unapproved items even if they seem obvious

## Edge Cases

- If a file seems important but is orphaned, flag it rather than quietly linking it — the user may have intentionally left it unlinked
- If two files overlap significantly, show both before proposing a merge so the user can see what would be lost
- If an idea in an index is ambiguous (keep as idea vs. make a file vs. drop), ask rather than decide