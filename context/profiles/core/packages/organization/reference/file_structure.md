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

## Generality of shared files

Shared files must remain fully general unless their scope (profile,
package, or a rule's `paths:`) explicitly narrows the context; the full
treatment is [generalization](generalization.md). When shared files
include examples, those examples span multiple artifact types or
remain abstract:

**Incorrect** (assumes source code context):
> "Validate that imports are sorted alphabetically."

**Correct** (general):
> "Validate that elements follow the ordering convention for their artifact type."

**Also correct** (scoped, in a code profile's `rules/import_order.md`):
> "Validate that imports are sorted alphabetically."

Project-specific assumptions belong in the project's own context root,
which can both override (through `context.local/`) and add to the
shared modules it consumes.

## Category templates

Each category has a structural pattern: reference files are dense and
comprehensive (title, overview, core concepts, details, examples,
related); rules state one constraint with a brief rationale, examples,
and exceptions; skills are minimal prose that aggregates references and
agents; commands are orchestration steps with agent references; agent
prompts set up context for independent execution (objective, context,
constraints, output). The full templates are the artifact authoring
guides of the `authoring` profile (`reference_authoring.md`,
`rules_authoring.md`, `skills_authoring.md`, `commands_authoring.md`,
`agents_authoring.md`).

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

## Signposting

- **Section previews.** Open a complex section with a preview of its
  content: "This section covers three aspects: X, Y, and Z."
- **Section conclusions.** Close a major section with synthesis:
  "Together, these patterns ensure context efficiency while maintaining
  flexibility."
- **Transitions between sections.** Connect sections logically: "Having
  established the principles, we now examine their application."

## Checklist

Before finalizing any context file:

- [ ] Metadata only where the domain interprets it (entrypoint and skill
      properties, a rule's `paths:`); none on reference files
- [ ] Title matches or expands the file's subject
- [ ] Sections organized logically
- [ ] No section exceeds 800 words
- [ ] Tables, lists, and prose used appropriately
- [ ] Cross-references are managed links that resolve
- [ ] Signposting aids navigation
- [ ] Shared files are fully general (no context assumptions unless scoped)

See also [generalization](generalization.md) and
`[@writing_context_sources_ctxmod_source_example_example, context principles]`.
