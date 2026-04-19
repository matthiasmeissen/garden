---
name: garden-harvest
description: Extract key learnings, concepts, resources, and ideas from a Claude conversation or working session and format them as structured markdown ready to be planted into the garden knowledge vault. Use this skill whenever the user says "harvest this conversation", "extract learnings", "summarize this session for my garden", "what did we learn", "save this to my garden", or pastes a conversation transcript and wants it captured. Also trigger when the user finishes a working session on any topic (DSP, Rust, embedded systems, woodworking, electronics, shaders, synthesis) and wants to preserve what was figured out. Trigger liberally — if the user wants to capture knowledge from a session, this skill is the right tool.
---

# Garden Harvest

Distil a conversation down to what's genuinely worth keeping. Not a summary — a selection.

## The Core Test

Before including anything, ask: **"Would I already know this, or could I find it in five minutes?"**

If yes — drop it. Only include things that changed understanding, resolved a non-obvious question, or captured reasoning that would otherwise be lost.

A good harvest is short. Typically 3–7 distilled insights, a few resources if any were found, a handful of ideas. If it's longer, it's still summarising rather than distilling.

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
    making.md                        <- domain hub
    woodworking/woodworking.md
    electronics/electronics.md
    music-making-and-synthesis/music-making-and-synthesis.md
  philosophy/
    philosophy.md                    <- domain hub
    finding-good-information.md      <- example concept file
    [other concept files...]
```

**Hub file naming:** Every folder has one hub file named after the folder itself (e.g. `rust/rust.md`).

**Domain tags:** `#rust` `#embedded` `#dsp` `#shaders` `#touchdesigner` `#game-engines` `#web` `#woodworking` `#electronics` `#synthesis` `#eurorack` `#faust` `#vcv-rack` `#supercollider` `#pcb` `#cnc` `#3d-printing` `#sewing` `#philosophy` `#learning` `#epistemology` `#systems-thinking`

## How to Harvest

### Step 1 — Read the input

The user will either:
- Say "harvest this conversation" (meaning the current session)
- Paste a transcript from another session

If ambiguous, ask: "Should I harvest the current conversation, or do you have a transcript to paste?"

### Step 2 — Identify the domain(s)

Map the content to one or more garden domains. Flag cross-domain content explicitly.

### Step 3 — Distil ruthlessly

Read the whole session. Then ask: what here would be genuinely useful to know six months from now, to someone who already understands the basics of this topic?

**Keep:**
- Insights that required reasoning to arrive at — not things obvious or easily Googled
- Decisions with non-obvious reasoning ("chose X over Y because Z")
- Patterns or approaches that took effort to figure out
- Resources that are hard to find or specifically recommended

**Drop:**
- Anything conversational or exploratory that didn't land anywhere
- Concepts that are common knowledge in the domain
- Things that were tried and corrected mid-session
- Anything a beginner's tutorial would cover
- Structural decisions about the garden itself
- Ideas, next steps, or things to investigate — never infer these unprompted; only add if the user explicitly asks

### Step 4 — Produce the harvest document

```markdown
# Harvest: [Topic] — [YYYY-MM-DD]

## Domain
[primary domain path, e.g. computation/dsp]
[secondary domain if cross-domain]

## Tags
[space-separated, e.g. #dsp #rust #filters]

## Distilled Insights

- **[Insight name]**: [1–2 sentences. Plain language. Written for your future self after a long break.]

## Resources

- [Title] — [Author] — [why it's worth reading] — expertise: [beginner/intermediate/advanced]

## Cross-References

- Relates to: [other domain/file] — [one line on why]
```

Omit any section that has nothing worth adding. No Ideas section — ideas are added manually by the user directly in the vault.

## Tone

Write as if leaving a note for yourself after a long break. Assume you remember the context but have forgotten the specifics. Be direct — no preamble, no "in this session we explored...".

## After Harvesting

Tell the user: "Here's your harvest. Use `garden-plant` inside the garden repo to write this into the vault."