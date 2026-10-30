# The Derivation Pipeline

External material becomes context through a ladder of artifacts, each
rung more processed than the last:

```text
raw material -> chunks -> summaries -> analyses -> rules / reference / profiles
```

## The rungs

| Rung | Artifact | Nature |
| --- | --- | --- |
| 1 | `chunks/` | Raw content in reading order, minimally segmented |
| 2 | `summary/` | Faithful mapping of one source's own material |
| 3 | `analysis/` | Integration, comparison, and conclusion across passages or sources |
| 4 | Rules | One-constraint pointers for auto-loaded context |
| 4 | Reference | Dense, self-contained coverage for on-demand loading |
| 4 | Profiles and packages | Governance and selection over the derived content |

## Rules of movement

- **Downward only with attribution.** Material moves from a lower rung
  into a rule or reference only when the source is citable from the
  consuming entity: cite with a locator, and the claim stays checkable.
- **Summaries map; analyses argue.** A summary claims "the source says
  this, here"; an analysis claims "these passages together mean that".
  Mislabeling the rung misrepresents the evidence.
- **Inference is marked at every rung.** Unverified metadata is listed
  in the source's `inferred:` list; derived prose beyond the source is
  analysis, never silently presented as summary.
- **Each rung stays readable alone.** Chunks serve readers who want the
  original segment; summaries serve readers who want the map; rules and
  references serve agents who want the behavior.
- **The pipeline is authored work.** No tool splits, transforms, or
  summarizes; the tooling indexes the structure, enforces the taxonomy,
  and renders citations. Production is deliberate writing.

The rung-1-through-3 artifacts live inside the source's own directory
taxonomy (`chunks/`, `summary/`, `analysis/`); rung 4 lands in the
consuming package's `rules/` and `reference/` domains.

See also `[@writing_context_sources_ctxmod_source_example_example, context principles]`.
