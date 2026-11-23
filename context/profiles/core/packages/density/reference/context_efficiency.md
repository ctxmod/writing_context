# Context Efficiency

Every token consumed by an agent has cost—computational, financial, and cognitive. Context efficiency maximizes the value delivered per token.

## Core Principle

Maximize signal-to-noise ratio. Include only information that directly contributes to the agent's objective. Exclude everything else. The target is the smallest set of high-signal tokens that makes the desired behavior likely.

Context is an **attention budget**, not only a capacity limit. Models degrade as input grows well before the window is full — **context rot**: recall and reasoning over a long input become less reliable as its length rises, topically related but irrelevant passages (distractors) pull accuracy down further, and the effect varies by model. So off-task material is not merely wasted budget: it competes for attention with the material that matters. Efficient context use enables more comprehensive objectives, deeper reasoning, more parallel sub-agents, and longer orchestration sequences; wasted tokens reduce all of these.

## Input Context Strategies

Reduce the tokens sent to agents by loading only what matters.

| Strategy | Application |
|----------|-------------|
| Reference files | Point to files instead of inlining content |
| Line ranges | Reference specific lines, not entire files |
| Summaries | Use low-verbosity inlines for overview |
| Selective loading | Load required context; skip optional when uncertain |
| Persistent intent via compulsory read | Receive specifications via file reference |

When an agent needs information from a 500-line file but only 20 lines are relevant, reference those 20 lines. The remaining 480 lines consume budget without contributing value.

### Just-in-Time Retrieval

Prefer handing the agent **lightweight identifiers** — paths, queries, links, record ids — that it resolves with its own tools when a step needs the content, over pre-loading the content itself. The identifier costs a line; the body loads only on the branch that reaches it, and the agent reads the live version rather than a snapshot. Names, folder structure, and timestamps are themselves signal an agent uses to decide what to open.

The trade is latency: runtime exploration is slower than reading pre-computed context, and an agent without guidance can waste turns on dead ends. The working pattern is **hybrid** — load a small, stable core up front (the project instruction file, the always-loaded rules), and let the agent retrieve everything else just in time. This is the pointer principle applied to retrieval: see <ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/pointers.md" />.

### Cache-Stable Prefixes

Model providers cache the processed prefix of a request, and cached input tokens are billed and served far cheaper than uncached ones (the cited production report prices cached input at a tenth of uncached on one vendor's list; discounts vary by vendor). A cache hit requires the prefix to be byte-identical, so a change at any point invalidates everything after it. Always-loaded material therefore earns a second property beyond sparsity: **stability**.

- Keep the always-loaded prefix stable across turns and sessions — no timestamps, counters, or per-run values near its top.
- Grow context by appending; avoid rewriting earlier turns or reordering loaded files.
- Serialize structured content deterministically (stable key order), so equal content produces equal bytes.

Caching lowers the price of a resident token; it does not lower its attention cost. A stable but bloated prefix is still bloated.

## Output Context Strategies

Reduce tokens in agent responses by externalizing findings.

| Strategy | Application |
|----------|-------------|
| Report externalization | Write findings to files, return references |
| Concise summaries | Sub-agent responses point to reports |
| Structured output | Predictable formats reduce parsing overhead |
| No redundancy | State each finding once |
| Intent externalization | Orchestrator writes preflight analysis to file, sub-agents read selectively |

A sub-agent that writes a detailed report to disk and returns a three-line summary preserves context budget for the orchestrating agent's reasoning.

### Tool-Result Economy

Tool output lands in the agent's context exactly like any other input, so the tools an agent calls — and the scripts, test harnesses, and check gates it runs — are context authors too.

| Strategy | Application |
|----------|-------------|
| Bounded results | Paginate, filter, select ranges, and truncate large outputs with sensible defaults; when truncating, say so and point at the narrower query that gets the rest |
| Verbosity switch | Offer a concise and a detailed form of the same result; default to concise and keep the identifiers a follow-up call needs |
| Meaningful fields | Return names and human-readable labels rather than opaque ids, MIME types, or raw tracebacks |
| Actionable errors | An error states what was wrong and what valid input looks like, so the next call can succeed |
| Quiet harnesses | Print a few summary lines and a grep-able failure marker; write the detail to a log file the agent can open on demand |

The last row is the just-in-time principle applied to output: a check gate that prints thousands of passing lines pollutes context with material no branch needs.

### Intent Externalization

Orchestrating agents perform preflight analysis to understand requirements. Rather than holding this analysis in context across all subsequent launches, the orchestrator writes it to a persistent file and passes the path to sub-agents. This:

1. **Preserves orchestration context**: Orchestrator budget remains for coordination logic
2. **Ensures consistency**: All sub-agents receive identical specifications
3. **Enables reproducibility**: Intent persists across sessions
4. **Supports debugging**: Exact specifications available for review

Sub-agents read the file via compulsory read, extracting only relevant sections for their specific objective.

## Turn Minimization

Each turn resends the full conversation history. Three turns at 10,000 tokens each sends 30,000 tokens of history; prompt caching discounts the repeated prefix but leaves it resident, so every turn still adds to what the model must attend over. Reduce turns by planning orchestration before execution and batching related operations, and — if your resolved `allow-parallel-agents` posture is `true` — by maximizing independent sub-agent launches per turn. Five parallel sub-agents use one turn while sequential execution uses five turns with accumulated history, but that saving is only available to agents granted the permission; for everyone else the sequential turn cost is the correct price of conflict-free work and inherited context.

## Measurement

Assess context efficiency through three ratios:

1. **Input ratio**: Relevant tokens divided by total input tokens
2. **Output ratio**: Actionable content divided by total output tokens
3. **Turn efficiency**: Actions completed divided by turns consumed

High ratios across all measures indicate efficient context use.

## Common Mistakes

| Mistake | Consequence |
|---------|-------------|
| Inlining large files | Bloats context, reduces reasoning space |
| Verbose summaries | Consumes budget without adding value |
| Redundant context | Same information sent multiple times |
| Unnecessary turns | Full history resent for minor actions |
| Optional context overload | Low-relevance content displaces high-relevance |

## Related

Context efficiency motivates reference-over-duplication (fewer tokens), SSOT (one read, not repeated lookups), and density matching (loading frequency determines appropriate verbosity). The density principle covers the loading-frequency/density relationship comprehensively, including cognitive foundations and measurement. These principles reinforce each other.

<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/reference_over_duplication.md" />
`ssot` (module `engineering`, profile `principles`, package `design`)
<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/density_by_frequency.md" />
<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/agent_facing_writing.md" />

Context that must outlive one window — compaction, structured notes, memory, and sub-agent summaries — is covered in <ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/long_horizon_context.md" />.

The agent-facing writing levers are the reader-side complement of this token accounting: context pointers, the two loads (context load on the agent's window, cognitive load on the human as index), and the information hierarchy that decides what earns residence in always-loaded material at all.

## Sources

- https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents — attention budget, context rot, just-in-time retrieval, the hybrid strategy (Anthropic Engineering, 2025-09-29; accessed 2026-11-22)
- https://www.trychroma.com/research/context-rot — context-rot measurements across 18 models: degradation with input length, distractor effects (Chroma technical report, 2025-07-14; accessed 2026-11-22)
- https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus — KV-cache hit rate as a production metric, stable prefixes, append-only context, deterministic serialization (2025-07-18; accessed 2026-11-22)
- https://www.anthropic.com/engineering/writing-tools-for-agents — tool-result token efficiency, concise/detailed response formats, meaningful identifiers, actionable errors (Anthropic Engineering, 2025-09-11; accessed 2026-11-22)
- https://www.anthropic.com/engineering/building-c-compiler — harness output as context pollution: few summary lines, grep-able ERROR markers, details in log files (Anthropic Engineering, 2026-02-05; accessed 2026-11-22)
