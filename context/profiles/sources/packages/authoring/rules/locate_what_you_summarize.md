# Declare a Locator for Every Summarized Passage

When a summary or analysis binds a claim to where the source says it,
declare the location with `<ctxmod_locator>…</ctxmod_locator>` at the
passage that carries the material. Citations then bind through the
locator index instead of free-floating prose suffixes.

## Rationale

Declared locators are indexed and matchable; undeclared suffixes pass
through as prose. A locator is a human-facing address (`p. 12`, `§3`,
`density.md`), plain text with no nested markup, written as the reader
should see it — normalization is case-fold plus whitespace collapse.

- [Sources layout](../reference/sources_layout.md)

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
