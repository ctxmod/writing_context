# Personal Scope

`context.local/` is the personal layer: shared among agents that can
access the same physical workspace, not private to one agent, and not
synchronized anywhere by default.

## What belongs here

- Personal workflow preferences and device-specific knowledge.
- Working material: drafts, plans, research notes not yet ready to
  publish.
- The device-private part of otherwise shared sources (typically
  `raw/` binaries).
- Local overrides mirroring shared logical paths to customize shared
  content for this workspace.

## Ownership and precedence

Updating an existing file targets its actual owner: a local override
edits the local file, a shared file edits the shared source. A local
override never implicitly deletes, promotes, or rewrites its shared
source.

## Promotion

Promoting local content into shared context is a reviewed plan, not a
copy:

1. The shared-only projection must be valid — every dependency the
   content carries must resolve without any local contribution.
2. Local references are rewritten or deliberately republished.
3. The plan names every file and reference rewrite before anything
   moves.

If step 1 fails, the content is not yet promotable: fix the dependency
direction in the local file first.

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
