# Long-Horizon Context

Work that outlives one context window needs context written for a
reader who arrives without the conversation: the same agent after
compaction, a fresh session, or a parent receiving a sub-agent's
result. Four techniques carry state across that boundary; they differ
in what they keep and who writes it.

## The four techniques

| Technique | What it does | Writing duty |
|-----------|--------------|--------------|
| **Tool-result clearing** | Drops old tool calls and results the agent no longer needs; the lightest form of compaction | Keep the identifier (path, URL, query) so the cleared body can be re-fetched — compression must be restorable |
| **Compaction** | Summarizes a window near its limit and continues in a fresh one from the summary | Tune for recall first (every decision, open problem, and unresolved bug survives), then for precision (drop redundant tool output) |
| **Structured notes** | The agent writes persistent notes outside the window — a progress log, a task list, a decision file — and re-reads them later | Write the state a fresh reader cannot reconstruct; re-read the plan before acting on it |
| **Sub-agent summaries** | A sub-agent explores in a clean window and returns a condensed result — commonly on the order of 1,000-2,000 tokens — to its parent | Return the distilled result plus pointers to the full record on disk, never the full exploration |

Compaction and memory are different mechanisms: compaction rewrites
turns inside one window; notes and memory persist across sessions and
are read or searched only when needed. Both are irreversible choices
about what to keep, so the durable record — files, the work store, the
transcript — stays the source of truth, and the window is a working
view of it.

## What to write down

The selection rule is the pruning rule applied to time: **cache what
looking cannot find** (<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/pruning.md" />).

- **Write** strategy, plans, and tested rules the environment does not
  show; verified facts together with how they were verified; traps
  found on the way; the exact resume point.
- **Skip** state the agent can read directly with one lookup (the
  current file contents, the branch, a config value) — a note that
  restates it goes stale and then misleads.
- **Mark** unverified notes as such: a wrong note is trusted by every
  later session that reads it.

Indiscriminate logging is the failure mode on the other side: an agent
that records everything spends its steps reorganizing notes instead of
working. Tell the agent what the notes are *for*, not a fixed rule for
what to record — a rigid rule ("record only failures") can throw away
the gain notes exist to provide.

## Shape of persistent notes

- **One writer per file.** Concurrent writers to one page drop facts;
  give each agent its own file and merge deliberately.
- **Structured where the content is state.** A task list with a status
  field per item survives repeated sessions better as structured data
  (JSON, a table) than as prose, because agents are less inclined to
  rewrite structure they were told only to update.
- **Small always-loaded index, deep store.** Injected-at-start memory
  pays context load every session and spreads its errors everywhere;
  keep that top layer to an index of pointers into the deeper notes
  (<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/two_loads.md" />).
- **Recite the goal.** Rewriting a short task list near the end of a
  long run keeps the objective in recent context, countering drift in
  long tool-call sequences.
- **Keep failures visible.** A failed action and its error, left in
  context or in the log, stop the agent from repeating it; scrubbing
  them removes the evidence the next attempt needs.

## Related

- Token and turn accounting, just-in-time retrieval, tool-result
  economy — <ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/context_efficiency.md" />
- Session structure for long-running agent work (initializer and
  worker sessions, progress artifacts, clean state per session) is
  agent-orchestration doctrine, outside this module: the
  `long_running_sessions` reference of the agentic module's `core`
  profile.

## Sources

- https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents — compaction (recall then precision), tool-result clearing, structured note-taking, sub-agent summaries of roughly 1,000-2,000 tokens (Anthropic Engineering, 2025-09-29; accessed 2026-11-22)
- https://www.anthropic.com/engineering/components-of-agent-memory — memory layers, what to write (what tools cannot show, verified facts with provenance, traps), failure modes (trusted wrong notes, indiscriminate logging, rigid recording rules, concurrent writers, injected-note cost) (Anthropic Engineering, 2026-11-06; accessed 2026-11-22)
- https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents — progress file and JSON feature list as cross-session state; JSON chosen because agents are less likely to overwrite it (Anthropic Engineering, 2025-11-26; accessed 2026-11-22)
- https://www.anthropic.com/engineering/managed-agents — the context window is not the source of truth; a durable session log outside it (Anthropic Engineering, 2026-04-08; accessed 2026-11-22)
- https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus — restorable compression, recitation via a todo file, keeping errors in context (2025-07-18; accessed 2026-11-22)
