# General Project Reference Sync

Use for full synchronization of all project reference files with current implementation state. Updates the context module's reference files, detects drift, and corrects outdated content.

Dispatch prompt:

```text
Synchronize project reference files with current implementation state.

Compulsory reads:
- the project_reference_sync_procedure skill
- the implementation report structure (the reporting guidance for implementation reports)

Parameters:
- Report: create it just in time, immediately before writing, as
  `ctxmod work new report "{nn} project reference sync" --owner <work item, if any>`;
  return the record path
- SCOPE=the context module's reference domain (context/reference/ and package reference/ directories)

Delimitations:
- Only update the project's own reference files
- Do not modify generated or tool-managed files (rendered output,
  context.local overlays, modules fetched from elsewhere)

Notes:
- Read the schema first to understand expected structure
- Prioritize high-impact drift
- Skip speculative content
```
