# Organization Scope

Organization-wide context is the published layer: every consumer
receives it, so every line justifies itself to a reader who has never
seen the authoring toolchain.

## Publication is deliberate

Adding, changing, or removing organization-shared content is a decision
with a blast radius of every consuming project. Publish when a change
benefits all consumers; keep working material uncommitted and
device-local until it does.

## What the shared layer carries

- Principles and rules that apply across consumer projects, written
  artifact-agnostically unless a path scopes them.
- Self-contained reference corpora: dense, defined on their own terms,
  citable from any consumer.
- Sources whose raw material serves verification demand across the
  organization.

## What it never carries

- Project-specific knowledge (that is the project layer's).
- Device-local specifics (that is the personal layer's).
- Private machinery: internal tool names, orchestration identifiers, or
  agent-context paths a consumer cannot resolve.

## Boundary tests

Before publishing a shared edit:

1. Could every consumer apply this unchanged?
2. Does every link resolve within the shared tree or to a public
   source?
3. Is anything in the diff only true on one device, one checkout, or
   for one author?

A yes to question 3 sends the line back to `context.local/`.

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
