# Citation Syntax

Citations use the pandoc Markdown citation syntax. The recognized forms:

| Form | Spelling | Meaning |
| --- | --- | --- |
| Parenthetical | `[@key]` | Bracketed citation |
| Narrative | `@key` | Author named in prose |
| Suppress author | `[-@key]` | Bracketed, author omitted |
| Prefix | `[@see @key]` | Text before the key inside brackets |
| Suffix / locator | `[@key, p. 33-35]` | Locator or affix after the key |
| Multiple | `[@k1; @k2]` | Semicolon-separated keys |
| Braced key | `@{key with spaces}` | Arbitrary key text |
| Locator braces | `[@key {…}]` | Braced suffix data, carried verbatim |

Escapes, code spans, fences, and raw HTML suppress citations — they are
recorded as suppressed occurrences, not active ones.

## Referencable names

Citations can name sources and context entities alike. Authored
directories carry local segments only, and each entity's qualified
referencable name is derived by underscore-joining the segment chain
from the module's referencable name down, normalized to snake_case:

| Entity | Qualified name |
| --- | --- |
| Module | logical-path basename, normalized, or the `name:` override (`writing_context`) |
| Profile | module name + profile segment (`writing_context_core`) |
| Package | profile name + package segment (`writing_context_core_basics`) |
| Source | parent name + source name (`writing_context_sources_ctxmod_source_example_example`) |

Reference files, chunks, summaries, and the like are not referencable —
they are *specifiers* addressed within a citable target.

## Resolution

An unqualified key resolves **outward, first match**: the citing
entity's own sources, then its ownership ancestors' (package, then
profile, then module), then the rest of the active composition in
activation order. No match is an error; an ambiguous match across
owners is not — first match wins, and rendered footnotes always carry
the qualified form. Where one unqualified key matches both a source and
a referencable in the same scope, sources win.

A **qualified name** — the full derived referencable name — resolves by
identity and never participates in the outward search, so it never ties
(composition-wide uniqueness is validated). The braced form `@{key}`
exists for key text that is not pandoc-key-legal; a derived name is
always key-legal, so braces are needed only for overridden
`name:`/`id:` values containing spaces.

## Specifiers: where in the target

1. **Declared locator** in the suffix position — `[@key, p. 12]` binds
   through the locator index to the file declaring `p. 12` (matching
   normalizes by case fold plus whitespace collapse).
2. **Path specifier** — `[@key#chunks/03-proof.md]` names the file under
   the source directory; this form is validated against the source tree.

See also [footnote style](footnote_style.md).
