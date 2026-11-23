# Editing Layers

A context ecosystem keeps shared content in `context/` and device-local
content in `context.local/`. Choosing the layer before editing prevents
both failure modes: lost changes (shared content regenerated over a
local edit) and unnecessary divergence (local specifics leaking into
shared files). The single-source-of-truth principle is behind the
split.

## The three scenarios

**Edit the shared source** when a change benefits every consumer of the
content. The edit propagates with the next sync or refresh. Correcting
an error, adding a generally useful principle, tightening a rule all
consumers read — edit `context/`.

- **Correct**: fix an error in a shared reference file by editing the
  source in `context/`, then let the fix propagate to every consumer.
- **Incorrect**: fix the error in rendered output (or in a consumer's
  copy of the module). The fix disappears the next time the output is
  rendered or the module is refreshed.

**Create a local override** when one device or workspace needs a
customization of existing shared content. The local file mirrors the
shared logical path and replaces it in the effective view for that
workspace only. Correct shape: the same relative path under
`context.local/`.

- **Correct**: create
  `context.local/profiles/<profile>/packages/<package>/rules/<rule>.md`
  to customize the shared rule at the same path under `context/` for
  this workspace's needs.
- **Incorrect**: edit the shared source to add workspace-specific
  content. The change reaches every consumer.

**Create add-only content** when new content has no shared
counterpart. New content defaults to `context/`; write it to
`context.local/` only when it is explicitly device-private. Updating
an existing file targets its actual owner.

- **Correct**: document a project-internal concept with no shared
  equivalent as new content in the project's own context root (its
  `context/`, or `context.internal/` when it concerns only development
  of the repository itself).
- **Incorrect**: add the file to a shared module that other projects
  consume when only one project needs it. Every other consumer receives
  unnecessary content.

## Decision guide

| Question | If yes |
| --- | --- |
| Does this change benefit every consumer of the shared content? | Edit the shared source |
| Does this customize existing shared content for one workspace? | Create a local override |
| Is this new content with no shared counterpart? | Create add-only content |
| Is the target rendered or generated output? | Stop; edit the source or the override instead |

There are no exceptions: every edit falls into one of the three
scenarios.

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
