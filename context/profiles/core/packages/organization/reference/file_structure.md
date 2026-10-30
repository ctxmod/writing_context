# File Structure

Structural patterns for context files across categories.

## Frontmatter and naming

Reference files may omit frontmatter entirely; entrypoints and rules
parse it. Use snake_case names for files and directories everywhere —
the reference domain warns for non-snake_case names and non-Markdown
files. Ordered sequences use a two-or-more-digit ordinal prefix
(`01-intro.md`); this is the required spelling inside source `chunks/`
and works for any ordered run.

## Content hierarchy

1. Title (H1) matching the file's subject.
2. Overview of one to three sentences when the title needs expansion.
3. Sections (H2) as the main divisions.
4. Subsections (H3) when needed.
5. H4 rarely; frequent use signals restructuring.

Target 200–500 words per H2 section; consider splitting above 800;
merge below 100.

## Tables, lists, prose

- **Tables** compare items across shared dimensions or support quick
  lookup.
- **Lists** carry sequential or parallel items needing brief individual
  explanation.
- **Prose** explains relationships and rationale.

## Cross-references

Use relative Markdown links inside a package
(`[editing layers](../reference/editing_layers.md)`); the tool parses them into
managed references. Use standard Markdown for external links. Point at
line ranges (`file.md:15-42`) when only part of a file is relevant.

## Category density map

| Content | Density | Loaded |
| --- | --- | --- |
| `reference/` | High — read once, single source of truth | On demand |
| `rules/` | Low — auto-loaded constraints | Automatically |
| Skill bodies | Low — aggregate references | By name |
| Command bodies | Low — orchestration steps | By invocation |
| Agent prompts | Medium — independent execution | Per agent |

Within a category keep density consistent; readers develop expectations.

See also [generalization](generalization.md) and
`[@writing_context_sources_ctxmod_source_example_example, context principles]`.
