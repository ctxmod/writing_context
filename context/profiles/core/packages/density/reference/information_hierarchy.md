# Information Hierarchy

A document combines two content types: **steps** (the ordered actions
the agent performs) and **reference** (definitions, rules, and facts
consulted on demand). Rank each piece by how immediately the agent needs
it:

1. **In-file step** — what the agent does, in order.
2. **In-file reference** — consulted on demand; a flat peer-set of rules
   on one rung is a fine arrangement.
3. **Disclosed reference** — pushed into a separate file behind a
   context pointer, loaded only when the pointer fires.

**Progressive disclosure** is the move down the ladder so the top stays
legible. The **branch test** decides placement: inline what every branch
needs; disclose behind a pointer what only some branches reach. Burying
the steps under reference turns attending to them into a coin-flip — a
variance cost, not only a legibility one.

**Co-location** is the within-file companion: a concept's definition,
rules, and caveats sit under one heading, so reading one part brings its
neighbors with it. Scattering fragments one meaning across many
headings; duplication, by contrast, repeats one meaning in two places.

**Sprawl** is the failure mode: a document too long even when every line
is live and unique. The cure is the ladder — disclose reference behind
pointers, and split by branch or sequence so each path carries only what
it needs.

Splitting by sequence earns its keep when post-completion steps tempt
the agent to rush the one in front of it: keeping them out of view
drives more legwork on the current task.

The uncondensed sources: [agent-facing writing](agent_facing_writing.md) and [density by frequency](density_by_frequency.md).

See also [two loads](two_loads.md),
[pointers](pointers.md), and
`[@writing_context_sources_ctxmod_source_example_example, writing principles]`.
