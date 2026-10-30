# Generalize Shared Content

Shared context assumes nothing about the consumer's work. Only a path or
profile scope may specialize: content at a general path applies equally
to code, configuration, documentation, specifications, research, and
anything else the consumer touches.

## Rationale

A shared module loads into projects working on any artifact type.
Content written for one artifact type silently misleads every other one;
the wrong example teaches the wrong habit.

- Examples in shared content span at least three artifact types or stay
  abstract (placeholders, patterns).
- Terminology is universal ("artifact", "component") unless the path
  scopes the domain.
- Legitimate specialization moves into a path-scoped location
  (`rules/go/*.md` may assume Go; `rules/*.md` may not).

- [Generalization](../reference/generalization.md)
- [File structure](../reference/file_structure.md)

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
