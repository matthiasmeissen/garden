# Chunk-Based Learning

[tags: #philosophy #learning #epistemology #systems-thinking]

A method for structuring a long-form learning effort by breaking a domain into natural knowledge units that build on each other, then working through them one at a time inside a longer time container. Evolved across three iterations of trying to learn hard subjects well.

## The Three Generations

1. **Consistency practice** — roughly 30 minutes a day for 100 days. Builds the habit and surfaces the fact that you care about the topic, but without structure it drifts. You end up doing whatever is in front of you rather than what moves you forward.
2. **LLM-guided curriculum with daily micro-tasks** — adds structure, but flattens everything into a uniform cadence. Easy days and hard days collapse into the same shape. Hard things get too little time; easy things get too much.
3. **Chunk-based learning** — the topic is subdivided into natural knowledge units of varying size. The 100 days remains the outer container, but inside it you work in chunks, not a continuous grind. Each chunk has its own scope, endpoint, and sense of completion.

The key shift from (2) to (3) is that the chunks are sized by the material, not by the calendar.

## Chunk Discovery via Triangulation

Generating a good set of chunks is the whole game. The best source mix:

- **University curricula** — show the academic structure of a field and what foundational material looks like.
- **Online resources and courses** — show the practical coverage, the things people actually do with the material.
- **Skill trees** — pre-built hierarchical breakdowns that communities and practitioners have already validated. Often the fastest way to see the whole shape of a domain.

Feed all three into an LLM as context and ask for a chunk breakdown. Then filter the result against your actual goal and your prior knowledge — the filtering step is where the method earns its value.

## Domain Knowledge as Filter

Without some baseline in a domain, LLM-generated chunks are hard to evaluate. Once you have a bit, you can spot:

- Segmentation that is **too coarse** — chunks the size of whole subfields
- Segmentation that is **too fine** — chunks that are really just subtasks
- Segmentation that is **misaligned** with your outcome — academically tidy, practically irrelevant

The human judgment step is non-negotiable. The LLM is a chunk proposer; you are the chunk approver.

## Agents and Skills as Chunk Reviewers

In code-heavy domains, automatic chunk reviewers and skill generators (like Claude Code skills) turn into quality gates — each chunk can have its own small agent that checks exit criteria before moving on. This is a natural extension of the chunk model: the feedback loops get automated where they can, without requiring you to manually evaluate every step. The human stays in the loop for chunk design and final review; the agent handles the repeated checks.

## Note on Vault Structure

The chunk model maps naturally onto the garden vault structure — each chunk is roughly one concept file or subdomain hub. Planning a learning effort and planning the notes that come out of it can use the same skeleton.

## See Also

- [[philosophy|Philosophy]]
- [[learning-strategies|Learning Strategies]] — the strategic layer: foundational texts, making early, triangulating sources
