# Generalization

Context content shared across consumers (reference, rules, skills,
agents, prompts) must be **fully artifact-agnostic** — it works equally
well regardless of what the consumer is working on.

## What "fully general" means

Shared content assumes nothing about the consumer's work. A consumer
could be working on:

- CLI tools or desktop applications
- Source code files, modules, or packages
- Documentation sections or technical writing
- Specification files or formal descriptions
- Configuration files or infrastructure definitions
- APIs, data pipelines, or integrations
- External research or literature reviews
- Research reports or analysis documents
- Test suites or quality artifacts
- Absolutely anything else

The **only** way shared content may assume a specific context is if
its scope declares it — the profile or package it lives in, or, for a
rule, the `paths:` that scope it:

| Scope | May assume |
| --- | --- |
| a Go profile's lint rule (`rules/go_lint.md` in a `go` profile) | Go toolchain and build tooling |
| a specification-validation package | Specification validation |
| a general validation package, `rules/quality_*.md` in a core profile | Nothing specific — any artifact |

## Shared versus project-specific content

| Content type | Location | Shared with consumers | Artifact assumptions |
| --- | --- | --- | --- |
| Universal principles | a shared module's `context/` | Yes | None — fully general |
| Guidance specific to developing one repository | that repository's `context.internal/` | No | May assume that repository's context |
| Project-agnostic rules | a shared module's `context/` | Yes | None — fully general |
| One project's development rules | that project's own context root | No | May assume that project's context |

### Origin of project-specific files

A repository's own context files are written de novo by its
maintainers for its own development. They do not exist elsewhere first
and are not derived, extracted, or migrated from a shared module: the
maintainers write them from scratch to customize shared content for
their repository's needs.

Examples of files that belong in a context tool's own development
context rather than in its shared module:

- the tool's own file-structure conventions, adding to the shared structure guide
- documentation of the tool's own reference syntax (its link components), which has no general equivalent
- the tool's source package organization
- template examples specific to the tool, one per content category
- the tool's own orchestration patterns for its development work

Some of these override shared counterparts through the local layer (a
repository-specific addition to a shared structure guide); others are
entirely new content with no shared counterpart (documentation of the
tool's own syntax).

### Projects write their own

Each project creates its own original context files for its
project-specific needs; it does not copy content out of shared modules
into its own tree. A project's context holds original customizations
written for that project: project-specific tooling references, domain
knowledge, custom orchestration patterns, and workflow overrides.

## Making content artifact-agnostic

### Examples span domains

Shared content uses examples from multiple, diverse domains:

| Avoid | Use instead |
| --- | --- |
| Examples drawn only from the context tree itself | `src/models/*.py`, `config/*.yaml`, `docs/*.md`, `spec/*.json` |
| Source code only | A mix of source, config, docs, specs, data |
| A single language | Multiple languages, or language-agnostic |

Example of diverse examples in a principle file:

```markdown
## Application

This principle applies across artifact types:

- **Source code**: Module boundaries in `pkg/auth/` should...
- **Configuration**: YAML files in `deploy/` should...
- **Documentation**: Sections in `docs/architecture/` should...
- **Specifications**: Schemas in `api/schemas/` should...
```

Abstract placeholders (`{category}/{topic}.{ext}`) are acceptable
where no diverse example earns its space.

### Terminology is universal

Replace domain-specific terminology with universal equivalents unless
the scope declares the domain:

| Specific | Universal |
| --- | --- |
| A context tool's frontmatter | Metadata |
| A context tool's link syntax | Cross-reference mechanisms |
| Agent identifiers | Process or worker identifiers |
| Skill files | Capability definitions |
| Source files | Artifacts |
| Code | Content (unless specifically about code) |
| Module (meaning a code unit) | Component |

### Language does not assume artifact type

| Artifact-specific | Artifact-agnostic |
| --- | --- |
| "When writing code..." | "When creating artifacts..." |
| "The function should..." | "The component should..." |
| "Parse the source file..." | "Process the artifact..." |
| "In the codebase..." | "In the project..." |

"Processing" or "generating", not "building" or "compiling", unless
the scope is a build domain.

### Placeholders for structure

Use placeholder syntax when describing paths or structures:

```markdown
# Correct (generic)
Files follow `{category}/{subcategory}/{topic}.{ext}` hierarchy.
Target artifacts located at `{root}/{domain}/{name}.*`.

# Incorrect (tool-specific or code-specific)
Files follow `reference/principles/context.md` hierarchy.
Source code located at `src/pkg/{name}.go`.
```

## Validation checklist

Before placing content in a shared module:

1. **Diverse examples**: examples from three or more artifact types, or abstract.
2. **Universal terminology**: no tool-specific or code-specific jargon at general scope.
3. **Generic paths**: placeholders or diverse real examples.
4. **Non-software validity**: guidance holds for documentation, specs, and research.
5. **No implicit assumptions**: no assumption that the consumer writes code.

## Scope-based specialization

Scope-based specialization is the escape hatch. When content
legitimately applies only to specific artifact types, place it where
its scope declares the assumed context — a profile or package named
for that context — and keep everything else fully general:

```
profiles/validation/packages/
├── general/reference/format.md          # general (all artifact types)
├── general/reference/completeness.md    # general (all artifact types)
├── go/rules/go_lint.md                  # Go-specific (scope declares context)
├── spec/rules/schema_compliance.md      # spec-specific (scope declares context)
└── docs/rules/link_validation.md        # docs-specific (scope declares context)
```

Content outside a specialized scope must remain fully general.

## Common violations

| Violation | Correction |
| --- | --- |
| "When implementing this pattern in your code..." | "When applying this pattern to your artifacts..." |
| Examples only show `.go`, `.py`, `.ts` files | Add examples with `.yaml`, `.md`, `.json`, `.sql` |
| "The module should export..." | "The component should expose...", or scope-based specialization |
| Assumes "building" or "compiling" | Use "processing" or "generating" unless scoped |

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
