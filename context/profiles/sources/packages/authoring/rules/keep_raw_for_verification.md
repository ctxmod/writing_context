# Keep Raw Material Only When Verification Demands It

Store original material under `raw/` only when its content is likely to
be requested for verification and is not retrievable from a public
location. Otherwise summarize, analyze, and cite — and store nothing.

## Rationale

The test is verifiability demand, not size. A PDF a citing claim is
checked against belongs in the source; a dataset whose value beyond its
summaries is nil does not.

Raw binaries are the typical `context.local` candidate: heaviest, and
most often device-private. Shared sources never depend on local ones,
so a shared source citing its own `raw/` carries that raw deliberately.

`raw/**` is data only — never scanned for citations, locators, or
components. Extract anything you need scanned into `chunks/` or
`summary/`.

- [Raw material and locality](../reference/raw_and_locality.md)

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
