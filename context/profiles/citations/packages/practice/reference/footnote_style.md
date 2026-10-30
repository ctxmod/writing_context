# Footnote Style

Citations render as named footnote markers, one entry per unique cited
target, the list sorted by qualified name.

## Reading the rendered form

`[@writing_context_sources_ctxmod_source_example_example, context principles]`
renders as `[^writing_context_sources_ctxmod_source_example_example, context principles]`-style
inline text with the entry keyed by that same name carrying the
source's bibliography entry. The locator
stays inline; the entry is shared by every citation of that target.

Source entries render bibliography-style from `source.yaml` fields,
with `(inferred: …)` appended when inference markers apply. Context
entities (packages, profiles, skills) render provenance-style entries —
kind, qualified name, module path, relative path, locality.

## Writing for that rendering

- **One claim per citation site, one entry per target.** Cite the same
  source at many sites freely; the list does not grow.
- **Locators are prose, tuned for reading.** `p. 12`, `§3`,
  `context principles` — write what the reader should see at the site.
- **Suffixes that match no declared locator** are carried through as
  prose affixes; do not rely on them binding.
- **Footnote ordering is qualified-name order**, chosen for `--diff`
  stability: nothing renumbers, so inserting a new citation early is
  diff-stable.
- **Unqualified keys may resolve outward** to a target other than the
  one you meant; qualified names resolve by identity and never tie, so
  cite `writing_context_sources_ctxmod_source_example_example` in full when
  disambiguation matters.

## Narrative versus parenthetical

Narrative (`@key`) emphasizes the source in the sentence — use when
discussing specific contributions. Parenthetical (`[@key]`) emphasizes
the finding — use for supporting claims. Mix both to avoid mechanical
placement. The example source's citation guidance reaches the same
conclusion — placement varies so attribution never goes mechanical; the
narrative form, taught rather than fired here, would read
`@writing_context_sources_ctxmod_source_example_example`.

See also [citation syntax](citation_syntax.md) and
`[@writing_context_sources_ctxmod_source_example_example, citations and locators]`.
