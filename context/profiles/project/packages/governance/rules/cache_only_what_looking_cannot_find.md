# Cache Only What Looking Cannot Find

Project context caches knowledge, not lookups. A document that restates
the toolchain — tool flags, file locations, command output — is a copy
of a lookup that goes stale; leave one-command lookups to the
toolchain.

## Rationale

Config files and `--help` output are sources of truth. Context earns its
load only by carrying what the toolchain cannot answer: the unwritten
convention, the reason behind a choice, the gotcha no config confesses.

Project context therefore holds project-specific knowledge and workflow
overrides — not a mirror of the repository's own documentation or of
tool behavior. Before writing a project-context file, ask: could the
agent find this in one command? If yes, the file is a defect.

- [Project scope](../reference/project_scope.md)

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
