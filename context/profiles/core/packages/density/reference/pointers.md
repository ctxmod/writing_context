# Pointers

A **context pointer** is a reference held in the agent's context that
names out-of-context material and encodes the condition for reaching it:
a skill summary, a link line in a reference file, a rule line naming its
reference. Tool descriptions and sub-agent descriptions are pointers
too: a harness that selects a tool or delegates to an agent decides
from the description alone, so the same wording discipline applies.

The pointer's wording, not its target, decides when the agent reaches
the material and how reliably. A must-have target behind a weakly worded
pointer is a variance bug: sharpen the wording first, and inline the
material only when sharpening fails.

A pointer does two jobs:

1. It states what the material is.
2. It lists the **branches** that should trigger reaching it — a branch
   is a distinct case the material handles, so different runs take
   different paths through it.

Every word of an always-loaded pointer costs on every turn, so it earns
harder pruning than the body it points at:

- Front-load the leading word; the pointer is where it does its
  triggering work.
- One trigger per branch; synonyms that rename a single branch are one
  branch written twice.
- Cut identity the body already carries.

The uncondensed sources: [agent-facing writing](agent_facing_writing.md) and [reference over duplication](reference_over_duplication.md).

See also [two loads](two_loads.md),
[information hierarchy](information_hierarchy.md), and
`[@writing_context_sources_ctxmod_source_example_example, writing principles]`.
