# Keep Shared Content Standalone

Organization-shared context must be understandable by a consumer with no
access to private tooling or agent-internal structure: no private tool
names, no orchestration machinery, no internal directory references in
shared content — not even to explain their absence.

## Rationale

Shared modules load into projects whose consumers cannot resolve
internal references. A rule that leans on private machinery is inert or
misleading everywhere except its birthplace, and internal paths in
committed content rot invisibly.

Links in shared content point only at shared files or public external
sources. Working material — plans, research notes, drafts — stays out of
shared context entirely; the shared tree carries what every consumer
needs and nothing else.

- [Organization scope](../reference/organization_scope.md)

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
