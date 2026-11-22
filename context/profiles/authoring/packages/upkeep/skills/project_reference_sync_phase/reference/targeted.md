# Targeted Sync

Use when updating specific project reference files rather than performing a full synchronization. Operates on named file paths and verifies each against current implementation state.

Dispatch prompt:

```text
Update specific project reference files: {file paths}.

Compulsory reads:
- the project_reference_sync_procedure skill
- the implementation report structure (the reporting guidance for implementation reports)

Parameters:
- Report: create it just in time, immediately before writing, as
  `ctxmod work new report "{nn} reference sync targeted" --parent <work item, if any>`;
  return the record path
- TARGET_FILES={specific file paths}

Delimitations:
- Only update specified files
- Verify against implementation state
```
