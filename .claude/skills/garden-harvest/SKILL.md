---
name: garden-harvest
description: Extract key learnings, concepts, resources, and ideas from a Claude conversation or working session and format them as structured markdown ready to be planted into the garden knowledge vault. Use this skill whenever the user says "harvest this conversation", "extract learnings", "summarize this session for my garden", "what did we learn", "save this to my garden", or pastes a conversation transcript and wants it captured. Also trigger when the user finishes a working session on any topic (DSP, Rust, embedded systems, woodworking, electronics, shaders, synthesis) and wants to preserve what was figured out. Trigger liberally — if the user wants to capture knowledge from a session, this skill is the right tool.
---

# Garden Harvest

Distil a conversation down to what's genuinely worth keeping. Not a summary — a selection.

## The Core Test

Before including anything, ask: **"Would I already know this, or could I find it in five minutes?"**

Only include things that changed understanding, resolved a non-obvious question, or captured reasoning that would otherwise be lost.

A good harvest is short. Typically 3–7 distilled insights, a few resources if any were found. If it's longer, it's still summarising rather than distilling.

## Garden Structure (for reference)

```
garden/
  computation/
    computation.md                   <- domain hub
    rust/rust.md                     <- subdomain hub
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
    [concept files...]
```

**Categories:** `computation` / `making` / `philosophy`

**Tags:** `#rust` `#embedded` `#dsp` `#shaders` `#touchdesigner` `#game-engines` `#web` `#woodworking` `#electronics` `#synthesis` `#eurorack` `#faust` `#vcv-rack` `#supercollider` `#pcb` `#cnc` `#3d-printing` `#sewing` `#philosophy` `#learning` `#epistemology` `#systems-thinking`

## How to Harvest

### Step 1 — Read the input

The user will either say "harvest this conversation" or paste a transcript. If ambiguous, ask.

### Step 2 — Identify the domain(s)

Map to one or more garden domains. Flag cross-domain content explicitly.

### Step 3 — Distil ruthlessly

**Keep:**
- Insights that required reasoning to arrive at
- Decisions with non-obvious reasoning ("chose X over Y because Z")
- Patterns or approaches that took effort to figure out
- Resources that are hard to find or specifically recommended

**Drop:**
- Conversational filler that didn't land anywhere
- Common knowledge in the domain
- Things tried and corrected mid-session
- Anything a beginner's tutorial would cover
- Structural decisions about the garden itself
- Ideas — never infer these unprompted. An idea is a concrete future action ("build X", "learn Y") — distinct from an insight.

### Step 4 — Produce the harvest document

```markdown
# Harvest: [Topic] — [YYYY-MM-DD]

## Domain
[primary domain path, e.g. computation/dsp]
[secondary domain if cross-domain]

## Category
[computation / making / philosophy]

## Tags
[space-separated, e.g. #dsp #rust #filters]

## Distilled Insights

- **[Insight name]**: [1–2 sentences. Plain language. For your future self after a long break.]

## Resources

- [Title] — [Author] — [why it's worth reading] — expertise: [beginner/intermediate/advanced]

## Cross-References

- Relates to: [other domain/file] — [one line on why]
```

Omit any section with nothing worth adding. No Ideas section.

## Tone

Direct. No preamble. Write as if leaving a note for yourself after a long break.

## After Harvesting

Tell the user: "Here's your harvest. Use `garden-plant` inside the garden repo to write this into the vault."