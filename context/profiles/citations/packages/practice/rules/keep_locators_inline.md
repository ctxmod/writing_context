# Keep Locators Inline, Targets Unique

Locators stay at the citation site; each uniquely cited target gets one
footnote entry.

## Rationale

A work cited forty times costs one bibliography line, not forty. The
locator (`p. 12`, `density.md`) is read where the citation stands, so
it stays inline and never enters the footnote list.

In rendered output a citation becomes a named footnote marker —
`[^writing_context_sources_ctxmod_source_example_example]` alone, or
`[^writing_context_sources_ctxmod_source_example_example, p. 12]`
with a locator or suffix. Write citations expecting that
rendering: suffix text is reader prose, and a suffix matching no
declared locator is not an error; only the `#path` specifier form is
validated against the source tree.

- [Footnote style](../reference/footnote_style.md)
- [Citation syntax](../reference/citation_syntax.md)

See also `[@writing_context_sources_ctxmod_source_example_example, citations and locators]`.
