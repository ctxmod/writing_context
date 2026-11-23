# Information Hierarchy

Context is ranked on two scales. **Load tiers** decide when an item
enters a session at all, and the **in-document ladder** decides where
it sits inside the file that carries it. Place an item on the first
scale before the second.

## Load Tiers

Every item of context belongs to exactly one tier, decided by **when
the agent needs it**, not by how important it is.

| Tier | Loads | Belongs here | ctxmod mechanism |
| --- | --- | --- | --- |
| 1. Always | every session | Obligations that bind in most turns and that the agent cannot discover by itself: binding rulings and red lines, the tests for any prose the agent writes, and the index of everything else | an unscoped rule or a bound package prompt, kept to obligation plus test |
| 2. By location | once the session reads or writes a matching file | Rules for one file type or one tree of a repository | a rule's `paths:`; where the ctxmod in use supports it, package-level path binding (`binds_to_paths`) and path-conditioned default profiles |
| 3. On demand | when the agent decides to read it | Procedures, audits, runbooks, invoked skills, worked examples, catalogues, rationale, history, long tables | reference files; gated packages and skills (`gated_by_depth`) |
| 4. Never | not in context | Provenance logs, archives, superseded material that no pointer names | an archive outside any package, or deletion when the material has no remaining reader |

The tests, one per tier:

- **Tier 1:** would a session that never touches the item's subject
  still go wrong without it? If not, it is not tier 1.
- **Tier 2:** is there a glob that is true exactly when the item
  matters? If so, scope the item by it. A glob that is true in nearly
  every session (Markdown files at every depth, in a documentation
  repository) is tier 1 in disguise; leave such an item unscoped and
  budget it as tier 1.
- **Tier 3:** is the item consulted at a moment the agent can
  recognize ("before writing a migration", "when asked to audit the
  tree")? If so, a pointer naming that moment is enough.
- **Tier 4:** does no pointer name the item, and would no reader miss
  it? Archive it or delete it.

**The index.** Every tier-3 item is named by a tier-1 or tier-2
pointer that says what it is, when to read it, and where it lives, in
one line. An on-demand item that nothing names is tier 4 by accident,
because the agent cannot reach what no pointer names. How to word the pointer
is in [pointers](pointers.md).

**The first write.** A rule scoped to a file type arrives at the step
after the session's first matching read or write. Where an obligation
must already hold for the very first write of a new file of that type,
the tier-1 index line carries its one-sentence essence.

A rule's body budget within tiers 1 and 2 is set by how tightly its
`paths:` scope predicts relevance; the budget table is
`rule_authoring.md` in the `authoring` profile.

## The In-Document Ladder

A document combines two content types: **steps** (the ordered actions
the agent performs) and **reference** (definitions, rules, and facts
consulted on demand). Rank each piece by how immediately the agent needs
it:

1. **In-file step** — what the agent does, in order.
2. **In-file reference** — consulted on demand; a flat peer-set of rules
   on one rung is a fine arrangement.
3. **Disclosed reference** — pushed into a separate file behind a
   context pointer, loaded only when the pointer fires. This is load
   tier 3, seen from inside the document.

**Progressive disclosure** is the move down the ladder so the top stays
legible. The **branch test** decides placement: inline what every branch
needs; disclose behind a pointer what only some branches reach. Burying
the steps under reference turns attending to them into a coin-flip — a
variance cost, not only a legibility one.

**Co-location** is the within-file companion: a concept's definition,
rules, and caveats sit under one heading, so reading one part brings its
neighbors with it. Scattering fragments one meaning across many
headings; duplication, by contrast, repeats one meaning in two places.

**Sprawl** is the failure mode: a document too long even when every line
is live and unique. The cure is the ladder — disclose reference behind
pointers, and split by branch or sequence so each path carries only what
it needs.

Splitting by sequence earns its keep when post-completion steps tempt
the agent to rush the one in front of it: keeping them out of view
drives more legwork on the current task.

The uncondensed sources: [agent-facing writing](agent_facing_writing.md) and [density by frequency](density_by_frequency.md).

See also [two loads](two_loads.md),
[pointers](pointers.md), and
`[@writing_context_sources_ctxmod_source_example_example, writing principles]`.
