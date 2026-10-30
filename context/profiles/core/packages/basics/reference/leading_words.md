# Leading Words and Steering

## Leading words

A leading word is a compact concept the model already carries from
pretraining, reused as a token rather than explained as a sentence
("tracer bullets", "the fog of war", "tight"). It anchors a region of
behavior in the fewest tokens by recruiting priors the model already
holds.

- Reuse an existing word before coining one; a coined word pays in
  definition tokens what a pretrained word gives free.
- A leading word anchors twice: in the body it stabilizes execution; in
  a pointer it sharpens invocation through shared language across
  prompts and documents.
- Hunt restatements a leading word retires — a triad spelled out at
  three sites ("fast, deterministic, low-overhead" becomes *tight*), or
  a pointer spending a sentence to gesture at one idea.

## Negation and steering

Steering by prohibition drags the banned behavior into context and makes
it more available; the ban half-reads as an instruction to do the thing.
Prompt the positive: state the target behavior so the banned one is
never spoken.

A prohibition is legitimate only as a hard guardrail phrased no other
way, and then pairs with the positive target so attention lands on what
to do. The prose-level form of the same failure — "it's not X, it's Y"
constructions that create false depth — is an anti-pattern to eliminate
systematically.

See also `[@writing_context_sources_ctxmod_source_example_example, writing principles]`.
