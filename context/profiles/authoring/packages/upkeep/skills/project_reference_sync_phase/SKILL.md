---
description: >-
  Synchronize a repository's own context reference domain with the
  current implementation state: detect drift, then correct outdated
  content, choosing the discovery-only, full, or targeted variant by
  scope.
binds_to_depth: phase
---

# Project Reference Sync Phase

Synchronize the project's own context reference files (the `reference/`
domain of the repository's context module, `context/reference/` and its
package `reference/` directories) with current implementation state.
This phase detects drift between project reference documentation and
actual project state, then corrects outdated content.

Project reference sync is phase-rooted: there is no parent workflow
skill. The phase stands on its own, and sync work is dispatched
directly into this phase rather than reached through a workflow.

## When to Use

Use the project reference sync phase when:

- Project implementation has evolved since reference files were last updated
- Reference files may contain outdated information
- Agent decisions depend on accurate project context
- Periodic maintenance of project documentation is needed

This phase ensures project references remain a reliable source of truth.

## Variant Selection

Read the variant file matching the assigned task. Do not read all
three: each is independently applicable, and reading extras wastes
context.

| Sync scenario | Read |
|---------------|------|
| **Discovery only**: detect drift without modifying files; produce a severity-rated drift report | `reference/discovery_only.md` |
| **Full sync**: synchronize every project reference file against current implementation state | `reference/general.md` |
| **Targeted sync**: update specific named files; verify each against current implementation state | `reference/targeted.md` |

## Model Selection

Reference synchronization involves comparison and targeted updates; a
mid-tier model handles it efficiently. Use the strongest available model
when drift detection requires deep understanding of implementation
patterns, or when the reference content requires sophisticated writing.

## Coordination Pattern

Project reference sync follows the sequential pattern, each step
consuming the previous step's output:

1. Read the schema to understand expected structure
2. Inventory current reference files
3. Detect drift from implementation
4. Prioritize updates
5. Apply corrections
6. Validate results

Validation may embed a validation loop that iterates until the
references pass the schema's validation rules (for a ctxmod module, a
clean `ctxmod vet --root .`).

## Context Requirements

**Parameters provided by the dispatching agent**:

| Parameter | Required | Purpose |
|-----------|----------|---------|
| Report | Yes | The sub-agent creates its report just in time, immediately before writing, as a work record (`ctxmod work new report <title> --owner <owning work item, if any>`), writes there, and returns the record path |
| SCOPE | Yes | Reference directory to sync |
| TARGET_FILES | For targeted | Specific files to update |
| Work item context | If applicable | The owning work records (epic, story, issue) |

## Transition Criteria

Project reference sync completes when:

- Schema-expected files are present
- Content reflects current implementation
- Schema validation passes
- Cross-references resolve

If some drift cannot be corrected automatically, document and escalate.

## Decision Points

**Implementation vs. documentation conflict**: Implementation is
authoritative. Update documentation to match.

**Uncertain state**: Investigate before documenting. Incorrect content
causes more harm than absent content.

**Schema mismatch**: If the project needs structure not in the schema,
consider whether the schema should evolve rather than forcing
non-standard content.

## Anti-Patterns

| Avoid | Why | Instead |
|-------|-----|---------|
| Sync without schema read | May miss expected structure | Always read the schema first |
| Updating without verification | May introduce errors | Validate updates |
| Ignoring implementation | References diverge | Always compare to actual state |
| Over-documentation | Exceeds schema density | Follow schema guidelines |
| Speculative content | Incorrect references harm decisions | Only document verified state |

## Procedure

This phase dispatches to a single procedure for the step-level
correction mechanics, the `project_reference_sync_procedure` skill of
this package.

## Cross-Cutting Reference

- The KISS, DRY, and single-source-of-truth principles (the `engineering` module's `principles` profile).
- Context efficiency and reference over duplication: `context_efficiency.md` and `reference_over_duplication.md` in the `density` package of this module's `core` profile.

## Sub-Layer Launch

When this phase requires step-level execution, dispatch a procedure-depth
agent with the `project_reference_sync_procedure` skill. The dispatch
prompt carries:

```text
Step: <step-name>
<procedure-specific instructions>
Create your report just in time, immediately before writing:
`ctxmod work new report <short title> --owner <owning work item, if any>`;
write there and return the record path.
```

The procedure agent works against the sync procedure in that skill's
`reference/sync.md`.
