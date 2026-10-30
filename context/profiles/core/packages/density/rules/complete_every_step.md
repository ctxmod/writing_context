# Complete Every Step

Every step in an agent-facing document ends on a completion criterion:
the condition that tells the agent the work is done.

## Rationale

A vague bound ("understanding reached") invites premature completion —
the step ends early while attention slides to being done. A criterion
needs two properties:

- **Clarity**: the agent can tell done from not-done.
- **Demand**: the wording forces the legwork latent in the task ("every
  modified file accounted for", not "produce a change list").

The strongest criteria are both checkable and exhaustive. Hide later
steps only across a real context boundary — a hand-off or sub-agent
dispatch; an inline call leaves the later steps in context and clears
nothing.

- [Information hierarchy](../reference/information_hierarchy.md)

See also `[@writing_context_sources_ctxmod_source_example_example, writing principles]`.
