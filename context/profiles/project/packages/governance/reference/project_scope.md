# Project Scope

Project-specific context lives beside the project's published content
but answers a different question: published documentation explains the
product to its users; project context tells an agent working in the
repository what the repository itself cannot.

## What belongs in project context

- Conventions the code does not confess: naming decisions, deliberate
  exceptions, the history behind a counterintuitive choice.
- Workflow overrides and add-only content with no shared counterpart.
- Toolchain quirks that no config file carries (ordering constraints,
  host-specific behavior, undocumented build prerequisites).

## What does not

- Anything one command answers: flags, paths, current versions, `--help`
  text.
- Content that belongs in the project's published documentation —
  project context is agent-facing, not user-facing.
- Content the shared context already carries correctly; customize by
  local override rather than divergence.

## Layer discipline in a project

A project consuming shared modules customizes through local overrides
that mirror shared logical paths; it adds project-only content as new
files under its own context root. Editing a shared source to add
project-specific content leaks the project into every other consumer.

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
