# Budget by Load

Match a document's density to how often it loads. The more often
material is resident, the tighter its budget: automatically loaded
files stay sparse; on-demand files may be dense.

## Rationale

Every always-loaded line pays on every turn. Rules: one constraint
plus a rationale pointer, sparse body. Reference: dense,
self-contained, the single source of truth. Skills and commands:
minimal prose, aggregated references. Agent prompts: balanced — enough
for independent execution, no more.

Word targets per category: reference 300-800; rules, skills, and
commands 50-150 (excluding code examples); agent prompts 100-250. A
rule is a pointer whose body budget is set by how tightly its `paths:`
scope predicts relevance: unbounded 1-10 body lines, slightly bounded
(a whole file type) 10-25, bounded (specific patterns) 25-50, very
bounded (one package's files, always relevant there) 50-200. The tiers
in full are `rule_authoring.md` in the `authoring` profile.

- [The two loads](../reference/two_loads.md)
- [Information hierarchy](../reference/information_hierarchy.md)
- [Density by category](../reference/density_by_category.md)

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
