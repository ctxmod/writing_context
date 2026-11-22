# Context Efficiency

Every token consumed by an agent has cost—computational, financial, and cognitive. Context efficiency maximizes the value delivered per token.

## Core Principle

Maximize signal-to-noise ratio. Include only information that directly contributes to the agent's objective. Exclude everything else.

Agents operate within fixed context limits. Efficient context use enables more comprehensive objectives, deeper reasoning, more parallel sub-agents, and longer orchestration sequences. Wasted tokens reduce all of these.

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

### Intent Externalization

Orchestrating agents perform preflight analysis to understand requirements. Rather than holding this analysis in context across all subsequent launches, the orchestrator writes it to a persistent file and passes the path to sub-agents. This:

1. **Preserves orchestration context**: Orchestrator budget remains for coordination logic
2. **Ensures consistency**: All sub-agents receive identical specifications
3. **Enables reproducibility**: Intent persists across sessions
4. **Supports debugging**: Exact specifications available for review

Sub-agents read the file via compulsory read, extracting only relevant sections for their specific objective.

## Turn Minimization

Each turn resends the full conversation history. Three turns at 10,000 tokens each costs 30,000 tokens in history alone. Reduce turns by planning orchestration before execution and batching related operations, and — if your resolved `allow-parallel-agents` posture is `true` — by maximizing independent sub-agent launches per turn. Five parallel sub-agents use one turn while sequential execution uses five turns with accumulated history, but that saving is only available to agents granted the permission; for everyone else the sequential turn cost is the correct price of conflict-free work and inherited context.

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

The agent-facing writing levers are the reader-side complement of this token accounting: context pointers, the two loads (context load on the agent's window, cognitive load on the human as index), and the information hierarchy that decides what earns residence in always-loaded material at all.
