# Discovery-Only Sync

Use when detecting drift in project reference files without making corrections. Produces a drift report with a severity per file. Read-only operation.

Dispatch prompt:

```text
Detect drift in project reference files without correcting.

Compulsory reads:
- the project_reference_sync_procedure skill
- the discovery report structure (the reporting guidance for discovery reports)

Parameters:
- Report: create it just in time, immediately before writing, as
  `ctxmod work new report "{nn} reference drift discovery" --parent <work item, if any>`;
  return the record path
- SCOPE=the context module's reference domain (context/reference/ and package reference/ directories)

Delimitations:
- Discovery only; do not modify files
- Report drift severity for each file
```
