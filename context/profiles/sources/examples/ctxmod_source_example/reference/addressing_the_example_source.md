# Addressing the Example Source

The example source supports every specifier form this module teaches.
Each form below is live and resolves against
`sources/example/` within this package.

## Declared locators in the suffix position

`[@writing_context_sources_ctxmod_source_example_example, writing principles]`
binds through the locator index to
`chunks/01_writing_principles.md`, the file declaring `writing
principles`. A suffix that matches no declared locator is prose carried
through, not an error.

## Path specifiers

`[@writing_context_sources_ctxmod_source_example_example#chunks/02_context_principles.md]`
names the file directly under the source directory; this form is
validated against the source tree. `summary/overview.md` cites all
three chunks this way — the auditable route from summary back to
covered material.

## Narrative and suppressed-author forms

The example source demonstrates the synthetic levers
@writing_context_sources_ctxmod_source_example_example, and a mention
that omits the author in a bracketed cluster
[-@writing_context_sources_ctxmod_source_example_example] reads the
same way rendered.

## Multiple targets in one bracket group

[@writing_context_sources_ctxmod_source_example_example, writing
principles; @writing_context_sources_ctxmod_source_example_example,
context principles] cites two locators of one target in a single
group; the footnote list still carries one entry for the target.

- [Carry the live citations in the example](../rules/carry_the_live_citations.md)
- [The example source](../sources/example/SOURCE.md)
