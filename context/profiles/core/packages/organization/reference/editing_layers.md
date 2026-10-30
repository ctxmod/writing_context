# Editing Layers

A context ecosystem keeps shared content in `context/` and device-local
content in `context.local/`. Choosing the layer before editing prevents
both failure modes: lost changes (shared content regenerated over a
local edit) and unnecessary divergence (local specifics leaking into
shared files).

## The three scenarios

**Edit the shared source** when a change benefits every consumer of the
content. The edit propagates with the next sync or refresh. Correcting
an error, adding a generally useful principle, tightening a rule all
consumers read — edit `context/`.

**Create a local override** when one device or workspace needs a
customization of existing shared content. The local file mirrors the
shared logical path and replaces it in the effective view for that
workspace only. Correct shape: the same relative path under
`context.local/`.

**Create add-only content** when new content has no shared
counterpart. New content defaults to `context/`; write it to
`context.local/` only when it is explicitly device-private.

## Direction of dependence

Shared content must never depend on local content — not through links,
inherited metadata, package relationships, or inlines. Local content may
depend on shared content. A shared file cannot become portable merely
because a local override supplies its missing target; validation runs
both projections: source validity (shared alone) and effective-view
validity (combined).

## No implicit promotion

No local override implicitly deletes, promotes, or rewrites its shared
source. Publishing local context into shared context is a deliberate
promotion with a reviewed plan (what depends on what, what the
shared-only view needs); it never happens as a side effect of being
rendered or found useful.

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
