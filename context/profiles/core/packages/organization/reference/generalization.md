# Generalization

Context content shared across consumers must be **fully
artifact-agnostic** — it works equally well regardless of what the
consumer is working on.

## What "fully general" means

A consumer could be building a CLI, writing documentation, editing a
specification, configuring infrastructure, or reviewing research. The
only way shared content may assume a specific context is if its path
declares it:

| Path | May assume |
| --- | --- |
| `rules/go/lint.md` | Go toolchain and build tooling |
| `reference/validation/spec/*.md` | Specification validation |
| `rules/quality/*.md` | Nothing specific — any artifact |

## Making content artifact-agnostic

- **Examples span domains.** Avoid source-code-only examples; mix
  source, configuration, documentation, and data. Abstract placeholders
  (`{category}/{topic}.{ext}`) are acceptable where no diverse example
  earns its space.
- **Terminology is universal.** "Component" not "module", "artifact" not
  "source file", unless the path scopes the domain.
- **Language does not assume artifact type.** "When creating
  artifacts…" not "When writing code…"; "processing" not "building or
  compiling" unless path-scoped.

## Validation checklist

1. Examples from three or more artifact types, or abstract.
2. No single-domain jargon at general paths.
3. Guidance holds for documentation, specs, and research.
4. No implicit assumption that the consumer writes code.

Path-based specialization is the escape hatch: place specialized content
in an appropriately named subdirectory whose path declares the assumed
context, and keep everything else fully general.

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
