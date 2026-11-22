# Agent-Facing Writing

Documents an agent consumes — context profiles and packages, rules and reference files, skill bodies, work items — share one reader: an agent that takes the same process every run. The packaging differs; the writing does not. The levers below make that process predictable whichever artifact carries it.

## Context Pointers

A **context pointer** is a reference held in the agent's context that names out-of-context material and encodes the condition for reaching it: a skill summary, a link component in a reference file, a rule line naming its reference. The pointer's wording, not its target, decides when the agent reaches the material and how reliably. A must-have target behind a weakly worded pointer is a variance bug: sharpen the wording first, and inline the material only when sharpening fails.

A pointer does two jobs: it states what the material is, and it lists the **branches** that should trigger reaching it (a branch is a distinct case the material handles, so different runs take different paths through it). Every word of an always-loaded pointer costs on every turn, so it earns harder pruning than the body:

- Front-load the leading word — the pointer is where it does its triggering work.
- One trigger per branch; synonyms that rename a single branch are one branch written twice.
- Cut identity the body already carries.

## The Two Loads

Every document and pointer spends one of two budgets:

- **Context load** is the cost of always-loaded material on the agent's window — a profile line, a skill summary, anything resident every turn, spending budget and attention whether or not it fires.
- **Cognitive load** is the cost on the human of knowing what exists and when to reach for it. The human is the index. Spend it where human judgement matters; remove it where it does not.

Material behind a pointer escapes context load at the price of the pointer's own line; material with no pointer rides entirely on cognitive load. In this corpus: profile and rules content is context load, the reference tree behind links is disclosed material, and knowing that the work store holds the work items is cognitive load.

## Information Hierarchy

A document combines two content types: **steps** (the ordered actions the agent performs) and **reference** (definitions, rules, facts consulted on demand). The hierarchy ranks each piece by how immediately the agent needs it:

1. **In-file step** — what the agent does, in order.
2. **In-file reference** — consulted on demand; a flat peer-set of rules on one rung is a fine arrangement.
3. **Disclosed reference** — pushed into a separate file behind a context pointer, loaded only when the pointer fires.

**Progressive disclosure** is the move down the ladder so the top stays legible. The branch test decides placement: inline what every branch needs, and disclose behind a pointer what only some branches reach. Reference burying the steps turns attending to them into a coin-flip — a variance cost, not only a legibility one.

**Co-location** is the within-file companion: a concept's definition, rules, and caveats sit under one heading, so reading one part brings its neighbors with it. Scattering fragments one meaning across many headings; duplication, by contrast, repeats one meaning in two places.

**Sprawl** is the failure mode: a document too long even when every line is live and unique. Attention thins across the excess. The cure is the ladder — disclose reference behind pointers, and split by branch or sequence so each path carries only what it needs.

## Completion Criteria

Every step ends on a **completion criterion**: the condition that tells the agent the work is done. Two properties make it a lever:

- **Clarity** — can the agent tell done from not-done? A vague bound ("understanding reached") invites **premature completion**: the step ends early while attention slides to being done. Sharpen the bound first; hide later steps only across a real context boundary (a hand-off or sub-agent dispatch — an inline call leaves the later steps in context and clears nothing).
- **Demand** — how much the bound requires. "Every modified file accounted for" forces thorough work where "produce a change list" does not. Demand drives **legwork**: the digging latent in the wording rather than written as its own step.

The strongest criteria are both checkable and exhaustive. In this repository the lever's surface is acceptance criteria in work items and step ends in skill and phase files; their schemas stay owned by the work-item and skill structure doctrine, and this file carries the writing lever only.

## Splitting by Sequence

Split a run of steps when the post-completion steps tempt the agent to rush the one in front of it: keeping them out of view drives more legwork on the current task. Merging sequences exposes later steps to what follows and invites premature completion — the cut earns its keep in both directions.

## Leading Words

A **leading word** is a compact concept already living in the model's pretraining that the agent thinks with while running the document (a lesson, the fog of war, tracer bullets). Repeated as a token, never as a sentence, it anchors a whole region of behavior in the fewest tokens by recruiting priors the model already holds. A coined word recruits no priors: it pays in definition tokens what a pretrained word gives free, so reach for an existing word first.

A leading word anchors twice. In the body it stabilizes execution: the same behavior every time the word appears. In a pointer it sharpens invocation: shared language across prompts, documents, and code links the agent to the material more reliably.

Hunt for restatements a leading word retires — a triad spelled out at three sites ("fast, deterministic, low-overhead" becomes *tight*), or a pointer spending a sentence to gesture at one idea. The win is doubled: fewer tokens, and a sharper hook for the agent to hang its thinking on.

## Negation

Steering by prohibition drags the banned behavior into context and makes it more available: the negation is a weak modifier a strongly-activated concept overruns, so the ban half-reads as an instruction to do the thing. Prompt the positive — state the target behavior ("write one-line comments") so the banned one is never spoken. A prohibition earns its place only as a hard guardrail phrased no other way, and then pairs with the positive target so attention lands on what to do.

## Pruning

- Keep each meaning in a **single source of truth**: one authoritative place, so changing the behavior is a one-place edit. Duplication costs maintenance, tokens, and inflated prominence on the hierarchy.
- The **environment** is a source of truth too: config files, `.config/` TOML, `--help` output. A document that restates the environment is a **cache** — a copy of a lookup, earning its load only when the lookup is expensive. Cache what looking cannot find: the unwritten convention, the reason behind a choice, the gotcha no config confesses. Leave one-command lookups to the environment, where they cannot go stale.
- Check every line for **relevance**: does it bear on what the document does now? Lines lose relevance by never bearing on the task or by going stale as the described behavior changes. Without a pruning discipline the default fate is **sediment**: stale layers that settle because adding feels safe, until finding the live text means coring down through them.
- Hunt **no-ops** sentence by sentence: an instruction the model already obeys by default pays load to say nothing. The test — does it change behavior versus the default? — is model-relative, settled by running the document. A failing sentence deletes whole; a leading word too weak to beat the default needs a stronger word, not a different technique.

## Related

- The token and turn accounting these levers spend — <ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/context_efficiency.md" />
- Density as the per-artifact tuning of the same budgets — <ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/density_by_frequency.md" />
- Pointing at sources instead of copying them, the file-level form of a context pointer — <ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/reference_over_duplication.md" />

Skill-specific mechanics — skill properties, invocation choice, router skills — stay owned by the authoring doctrine: skill structure in `skills_authoring.md` of the `authoring` profile, and the context tool's own property reference for the metadata mechanics. This file carries the general levers; those files carry the packaging.
