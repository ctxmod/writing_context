# Place Content in Its Layer

Every context edit lands in exactly one layer, chosen before writing:

| Question | If yes | Layer |
| --- | --- | --- |
| Does every consumer of the shared content benefit? | Edit the shared source | `context/` |
| Does one device need to customize shared content? | Create a local override | `context.local/` |
| Is this new content with no shared counterpart? | Create new content, shared by default | `context/`, or `context.local/` if device-private |
| Is the target rendered or generated output? | Stop: edit the source layer and render again | none |

Every context edit falls into one of the three layer scenarios; there
are no exceptions.

Nothing under `context.local` becomes shared by being selected,
rendered, or found useful; publishing it is a deliberate promotion.

- [Editing layers](../reference/editing_layers.md): the failure modes, examples per scenario, and promotion

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
