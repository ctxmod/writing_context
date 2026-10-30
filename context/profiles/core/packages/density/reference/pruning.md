# Pruning

## Single source of truth

Keep each meaning in one authoritative place, so changing the behavior
is a one-place edit. Duplication costs maintenance, tokens, and inflated
prominence on the information hierarchy.

## The toolchain is a source of truth too

Config files, command `--help` output, and tool metadata are sources of
truth. A document that restates the toolchain is a **cache** — a copy
of a lookup, earning its load only when the lookup is expensive. Cache
what looking cannot find: the unwritten convention, the reason behind a
choice, the gotcha no config confesses. Leave one-command lookups to the
toolchain, where they cannot go stale.

## Relevance and sediment

Check every line: does it bear on what the document does now? Lines lose
relevance by never bearing on the task or by going stale as the
described behavior changes. Without a pruning discipline the default
fate is **sediment** — stale layers that settle because adding feels
safe, until finding the live text means coring down through them.

## No-ops

Hunt no-ops sentence by sentence: an instruction the model already obeys
by default pays load to say nothing. The test — does it change behavior
versus the default? — is model-relative and settled by running the
document. A failing sentence deletes whole; a leading word too weak to
beat the default needs a stronger word, not a different technique.

See also [pointers](pointers.md) and
`[@writing_context_sources_ctxmod_source_example_example, writing principles]`.
