# Sources Layout

A source is raw material with metadata, stored under a `sources/`
directory of a package, profile, or module. A source's referencable
identity is its owner's referencable name underscore-joined with the
source name (`writing_context_sources_ctxmod_source_example_example`), so two
owners never merge the same source.

## Two canonical layouts

- **Flat:** `sources/<name>.yaml` — metadata only; citable for its
  bibliography entry without stored content (a web page retrievable at
  its URL).
- **Directory:** `sources/<name>/` with `source.yaml` as the entrypoint
  plus any of the content directories below.

Two entrypoints for the same source name at the same owner are a
diagnostic. The directory name is the source's name; nothing inside
`source.yaml` renames it.

Prefer short, non-repeating source names. A word repeated across the
composed referencable name draws a warning; renaming the directory is
the remedy.

## Directory content taxonomy

| Path | Content | Scanned? |
| --- | --- | --- |
| `chunks/<nn>*.md` | Raw-content chunks in reading order, two-or-more-digit ordinal prefix (`01-intro.md`); may carry XML containers such as `<page n="12">` | Yes |
| `raw/**` | Original material: PDFs, images, data, large Markdown | Never — data only |
| `summary/**/*.md` | Reference chunks or other summaries; may cite their own source and others | Yes |
| `analysis/**/*.md` | Syntheses; may integrate and cite material from other sources | Yes |
| `overview/*.md` | Navigational overviews | Yes |
| `SOURCE.md` | Authored source overview at the source root — the source's own entry document | Yes |

Producing chunks and summaries from `raw/` is authored work; the tool
enforces the structure, indexes it, and renders citations — it does not
split or transform anything.

## Metadata

`source.yaml` is YAML approximating the CSL-JSON schema, parsed
permissively: unknown fields survive.

| Field | Status |
| --- | --- |
| `type` | Required — a CSL item type (`article-journal`, `book`, `webpage`, `report`, `dataset`, …) |
| `title` | Required |
| `id` | Optional — citation-key override; defaults to the derived qualified name |
| `coverage` | Optional — source-root-relative paths or globs naming exactly which files/material the source covers |
| `author`, `editor` | Optional — `{family, given}` lists or literal names |
| `issued` | Optional — date or year |
| `container-title`, `publisher` | Optional — venue, site, publisher |
| `doi`, `url` | Optional — `DOI`/`URL` spellings accepted |
| `accessed` | Optional — access date for online items |
| `version`, `language`, `page`, `note`, `abstract` | Optional |

**Inference latitude:** record a value you did not verify against the
source only by listing the field name in a top-level `inferred:` list.
Footnote entries carry an `(inferred: …)` marker for listed fields, so a
rendered bibliography never presents an unverifiable detail as verified.
`inferred:` naming an absent field is a vet warning.

Unknown directories inside a source survive permissively but gain no
semantics.

A source must be focused: it declares exactly which files it covers
through `coverage:`, and every summary and analysis within it names the
specific files it summarizes in its citation suffix, so the chain from
summary back to raw material is auditable. A broad catch-all source
spanning an entire corpus is an anti-pattern.

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
