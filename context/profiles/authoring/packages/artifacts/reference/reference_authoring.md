# Writing Reference Files

Write comprehensive reference files that serve as the single source of truth for their topic. This guide specializes the shared writing objective for the `reference/` domain of a context package.

The governing principles are the single source of truth (the `engineering` module's `principles` profile) and density by usage frequency (`density_by_frequency.md` in the `density` package of this module's `core` profile).

## Generalization Requirement

Reference files in a shared module reach every consumer of that module. Content must apply universally regardless of project type, language, or domain.

**Scope-based exceptions**: only files whose package or profile declares a narrower scope may assume that context:

- a reference in a Go profile's package may assume Go
- a reference in a specification profile may assume specification files
- a reference in a general package (core writing, shared patterns) must work for any artifact type

When writing reference content, use general terms:

| Avoid | Use Instead |
|-------|-------------|
| "the function" | "the artifact", "the target" |
| "the module" (meaning a code unit) | "the component", "the unit" |
| "source code" | "content", "artifacts" |
| "compile errors" | "validation failures" |

Examples should illustrate principles without assuming specific technologies unless the file's scope indicates that technology.

## Density Requirements

Reference files are **high density**:

- **Target**: 300-800 words
- **Content**: Comprehensive coverage of the topic
- **Structure**: Multiple sections with depth
- **Examples**: Included when they aid understanding

Reference files are read deliberately for understanding. Completeness matters more than brevity.

## Structure Template

ctxmod does not interpret frontmatter on reference files (a leading `---` block renders as body), so the file opens with its title and an overview sentence that does the summary's work. Cross-references go in the body as link components.

```markdown
# Topic Title

Brief overview establishing scope (1-3 sentences); the first sentence
says what the file provides.

## Core Concepts

Foundational information required for understanding.

## Details

In-depth coverage of specifics. Multiple subsections as needed.

## Examples

Concrete illustrations (when applicable).

## Anti-Patterns

What to avoid (when applicable).

## Related

Cross-references to related reference files, as ctxmod link
components (`<ctxmod_path path="…" />`).
```

## Content Guidelines

### Completeness

Cover the topic comprehensively. A reader should not need external sources to understand the topic after reading this file.

### Self-Containment

Minimize dependencies on other files for basic understanding. Reference other files for related topics, not for essential context.

### Authoritative Tone

Reference files define truth. Use definitive language:

- "The system uses..." (not "The system may use...")
- "Files must include..." (not "Files should include...")
- "This pattern prevents..." (not "This pattern might prevent...")

### Examples

Include examples when:

- The concept is abstract
- Implementation varies by context
- Common mistakes need illustration

Format examples as code blocks or quoted text.

## Variant Hierarchies

When a topic has a base and variants (a general writing objective and its per-artifact specializations, a principle and its domain applications), keep the base in one file and give each variant its own file beside it in the same package:

```
packages/artifacts/reference/
├── writing_objective.md       # base
├── reference_authoring.md     # this variant
├── rules_authoring.md
└── ...
```

A variant names its base once, near the top, with a link component, and adds only what differs; it never copies the base. Where the base must travel with the variant, inline it with `<ctxmod_inline path="…" />` instead of pasting it.

## Pre-Writing Checklist

Before writing a reference file:

- [ ] Identify the topic scope
- [ ] Check for existing files covering the topic
- [ ] Identify related files to reference
- [ ] Determine the appropriate profile and package
- [ ] Plan the section structure

## Post-Writing Checklist

After writing:

- [ ] Opening sentence states what the file provides; no frontmatter block
- [ ] All sections populated
- [ ] Cross-references are link components that resolve (`ctxmod vet` passes)
- [ ] No anti-patterns in writing
- [ ] Appropriate density achieved
- [ ] File placed in the correct package, with a snake_case name

## Output

Deliver:

1. The reference file written to `profiles/{profile}/packages/{package}/reference/{name}.md`
2. Brief confirmation: "Wrote reference file: {path}"
