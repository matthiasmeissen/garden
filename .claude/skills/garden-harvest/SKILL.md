---
name: garden-harvest
description: Extract key learnings, concepts, resources, and ideas from a Claude conversation or working session and format them as structured markdown ready to be planted into the garden knowledge vault. Use this skill whenever the user says "harvest this conversation", "extract learnings", "summarize this session for my garden", "what did we learn", "save this to my garden", or pastes a conversation transcript and wants it captured. Also trigger when the user finishes a working session on any topic (DSP, Rust, embedded systems, woodworking, electronics, shaders, synthesis) and wants to preserve what was figured out. Trigger liberally — if the user wants to capture knowledge from a session, this skill is the right tool.
---

# Garden Harvest

Extract the signal from a conversation or working session and structure it for the garden vault.

## What This Skill Does

Reads a conversation or session transcript and produces a structured markdown document containing:
- Key concepts learned or clarified
- Decisions made and the reasoning behind them
- Resources mentioned (books, tools, links, papers)
- Ideas and open questions that emerged
- Cross-references to other garden domains

The output is ready to hand to `garden-plant` for vault insertion.

## Garden Structure (for reference)

```
garden/
  principles-and-philosophy.md
  computation/
    _index.md
    rust/         embedded-systems/   dsp/
    shaders/      touchdesigner/      game-engines/   web/
  making/
    _index.md
    woodworking/  electronics/   music-making-and-synthesis/
```

**Domain tags to use:** `#rust` `#embedded` `#dsp` `#shaders` `#touchdesigner` `#game-engines` `#web` `#woodworking` `#electronics` `#synthesis` `#eurorack` `#faust` `#vcv-rack` `#supercollider` `#pcb` `#cnc` `#3d-printing` `#sewing`

## How to Harvest

### Step 1 — Read the input

The user will either:
- Paste a conversation transcript directly
- Say "harvest this conversation" (meaning the current session)
- Reference a topic/session they just finished

If the input is ambiguous, ask: "Should I harvest the current conversation, or do you have a transcript to paste?"

### Step 2 — Identify the domain(s)

Map the content to one or more garden domains. A session on Moog ladder filters touches both `computation/dsp` and `making/music-making-and-synthesis`. Flag cross-domain content explicitly.

### Step 3 — Extract with intention

Pull out only what has lasting value. Ignore conversational filler, dead ends, and things that were corrected later. Focus on:

- **Concepts**: Things that were explained, clarified, or understood for the first time
- **Decisions**: Choices made and why (e.g. "chose TPT approach over bilinear because...")
- **Code patterns**: Reusable patterns, idioms, or architecture decisions
- **Resources**: Books, papers, crates, tools, YouTube channels, links — with expertise level if mentioned
- **Ideas**: Things to explore later, open questions, "what if" thoughts
- **Warnings**: Gotchas, failure modes, things that don't work

### Step 4 — Produce the harvest document

Output a markdown document in this exact format:

---

```markdown
# Harvest: [Topic] — [YYYY-MM-DD]

## Domain
[primary domain path, e.g. computation/dsp]
[secondary domain path if cross-domain, e.g. making/music-making-and-synthesis]

## Tags
[space-separated tags, e.g. #dsp #rust #filters #synthesis]

## Key Concepts

- **[Concept name]**: [1-3 sentence explanation in plain language]
- **[Concept name]**: ...

## Decisions & Reasoning

- **[Decision]**: [Why this was chosen over alternatives]

## Code Patterns

[Only include if session contained code worth preserving]

```[language]
// brief comment explaining what this does
[minimal illustrative code snippet]
```

## Resources

- [Title] — [Author/Source] — [brief note on what it covers] — expertise: [beginner/intermediate/advanced]

## Ideas & Open Questions

- [idea or question]

## Cross-References

- Relates to: [other garden domain or concept]
```

---

## What to Leave Out

- Long code dumps (reference the repo instead)
- Things that were tried and abandoned without insight
- Conversational back-and-forth that didn't produce knowledge
- Anything already well-documented in the garden

## Tone

Write concepts in plain language as if explaining to your future self after a long break. Assume you've forgotten the details but not the context.

## After Harvesting

Tell the user: "Here's your harvest. You can now use `garden-plant` to get instructions for adding this to the vault."