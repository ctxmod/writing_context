---
description: >-
  Step-level reference-sync mechanics: read the schema, inventory the
  current state, detect implementation drift, prioritize, apply
  updates, create missing files, validate.
binds_to_depth: procedure
---

# Project Reference Sync Procedure

Execute the project reference sync procedure and return its result.
The procedure detects drift between the project's own context reference
files and current implementation state, then corrects outdated content.

Project reference sync is procedure-rooted below its phase: there is no
parent workflow skill, and procedure work is dispatched directly into
this skill.

## Procedure Selection

Read the reference file matching the assigned task. The single
procedure covers the full sync lifecycle (discovery through
validation); variant dispatch happens at the phase depth, not here.

| Assigned task | Read |
|---------------|------|
| Detect drift in the project's context reference files and correct it | `reference/sync.md` |

### Reference Sync

Ensure the project's context reference files accurately reflect current
project state by detecting drift and correcting outdated content.
Produces updated reference files plus a sync report documenting the
drift found and the corrections applied.

The full procedure (prerequisites, schema read, inventory, drift
detection, prioritization, update application, missing-file creation,
validation, decision points, success criteria) is in `reference/sync.md`
of this skill.

## Execution Discipline

- Execute only the assigned procedure; do not expand into adjacent steps.
- Report results to the caller-provided path; return a summary, not the
  full body.
- Reference findings with `file:line` ranges rather than inlining content.
- Note explicitly when a procedure's prerequisites are unmet rather than
  improvising a substitute.
- Implementation is authoritative over documentation: when they
  conflict, update documentation to match.

## Phase Context

This procedure serves the `project_reference_sync_phase` skill of this
package; sync work dispatches directly into that phase.

## Cross-Cutting Reference

- The KISS, DRY, and single-source-of-truth principles (the `engineering` module's `principles` profile).
- Context efficiency and reference over duplication: `context_efficiency.md` and `reference_over_duplication.md` in the `density` package of this module's `core` profile.
