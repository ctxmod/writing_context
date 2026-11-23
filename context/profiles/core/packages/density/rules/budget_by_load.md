# Budget by Load

Place every item of context in one load tier, decided by when the agent
needs it: always, by location, on demand, or never. Density follows the
tier, so what is always resident stays sparse and what is read on
demand may be dense.

The test per item: tier 1 only if a session that never touches its
subject would go wrong without it; tier 2 only under a glob true
exactly when it matters (a glob true in nearly every session is tier 1
in disguise); tier 3 when it is consulted at a moment the agent can
recognize, named by a one-line tier-1 or tier-2 pointer that says what,
when and where.

- [Information hierarchy](../reference/information_hierarchy.md): the tiers, their ctxmod mechanisms, and the first-write caveat
- [The two loads](../reference/two_loads.md)
- [Density by category](../reference/density_by_category.md)

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
