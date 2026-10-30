# Example Source

A small synthetic source stored under the `sources/example/` directory of
the `ctxmod_source_example` example package
(`profiles/sources/examples/ctxmod_source_example/`). It demonstrates
the sources structure — chunks with declared locators, a summary citing
chunks through implicit path specifiers, and the citation forms the
citations profile teaches.

The package around it is the worked demonstration of a well-formed
package: a `package.yaml` entrypoint, content domains (`rules/`,
`reference/`) whose bodies carry the module's live citations, and this
directory-form source they resolve against (the package's own sources
are the first scope in the outward-first-match chain).

This source covers no external material: every chunk is synthetic
teaching prose written for this module, so `source.yaml` declares no
`coverage:`. Its citation key is the derived qualified name
`writing_context_sources_ctxmod_source_example_example` — module name,
profile segment, package segment, and source name underscore-joined.
The live citations in shared content outside this package are none:
every shared occurrence is taught inside a code span, so this package
is the only place a live citation of this source stands.

## Locators

- `chunks/01_writing_principles.md` declares the locator
  `writing principles`.
- `chunks/02_context_principles.md` declares the locator
  `context principles`.
- `chunks/03_citations_and_locators.md` declares the locator
  `citations and locators`.
- Every file also carries its implicit path locator
  (`chunks/01_writing_principles.md`, `summary/overview.md`, `SOURCE.md`),
  so `[@writing_context_sources_ctxmod_source_example_example#chunks/01_writing_principles.md]`
  addresses the first chunk without any declared locator.
