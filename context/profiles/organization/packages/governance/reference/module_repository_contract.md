# Module Repository Contract

A module collection publishes each module from its own repository, and
every repository in the collection follows one contract so consumers
and maintainers can rely on the same layout everywhere. The ctxmod
collection under `github.com/ctxmod` is the worked instance below.

## One module per repository

- The repository, its directory name and the module share one name:
  origin `git@github.com:ctxmod/<name>.git`.
- `context/module.yaml` is the module manifest. Its `path` is the
  repository path followed by the directory holding the manifest,
  written without a scheme: `github.com/ctxmod/<name>/context`. There
  is no `name` field; the `path` is the identity.
- `requires` is declared only when the module requires peers; an empty
  array is redundant. The context-writing, academic-writing and
  Swedish-writing modules require `github.com/ctxmod/writing/context`,
  so the general writing doctrine reaches a consumer transitively.
- `default_profiles` lists the profiles a consumer gets when it names
  none — typically `core`.

## Internal root

- `context.internal/module.yaml` declares
  `github.com/ctxmod/<name>/context.internal` with `private: true`.
- Its `requires` lists the sibling modules relevant to authoring this
  module's own context, as full module paths.
- The internal root is committed: it carries maintainer- and
  agent-facing material, held to the same standalone rule as the shared
  tree.

## Tracked surface

- Tracked content is `.gitignore`, `context/`, `context.internal/` and,
  optionally, a `README.md` summarising the profiles.
- The `.gitignore` is a whitelist: `/*` first, then the un-ignores for
  exactly the tracked entries, then waste patterns (`.DS_Store`,
  `Thumbs.db`, `desktop.ini`, `*.swp`) that apply at any depth.
- Everything else — `context.local/`, caches, work state — is
  device-local and never committed.

## Profiles and packages

- A profile is `context/profiles/<profile>/profile.yaml` with packages
  under `packages/<package>/`, each governed by its `package.yaml` and
  carrying `rules/` and `reference/` files.
- A profile is referenced canonically as `<module-path>/profiles/<name>`
  — for example `github.com/ctxmod/writing/context/profiles/core` — and
  an `extends` entry spells the reference the same way.
- External sources are carried as pointers and summaries, never as bulk
  copies.

## Commits

Conventional commits (`feat:`, `fix:`, `docs:`, `chore:`), lowercase,
with a subject that describes the change in the module's own
vocabulary.
