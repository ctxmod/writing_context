# Reference Over Duplication

When content exists in a file, reference that file instead of copying its content. This principle applies to agent prompts, reports, summaries, and documentation.

## Core Principle

A reference consumes fewer tokens than the content it points to and maintains a live connection to the source. Pasted content creates a drifting snapshot; references ensure readers always see the current version.

## Reference Patterns

### File References

Point to entire files when the whole file is relevant:

```markdown
Read: reference/principles/ssot.md
```

### Line Range References

Point to specific sections when only part is relevant:

```markdown
Read: reference/principles/ssot.md:15-42
```

Line ranges focus the reader's attention and reduce cognitive load. They also signal that the surrounding content may be less relevant to the current context.

### Cross-Reference Mechanisms

Projects often provide structured reference syntax. Use whatever mechanism your project supports:

```markdown
<!-- Standard markdown links -->
See [SSOT principles](docs/principles/ssot.md)

<!-- Include directives (varies by tooling) -->
!include docs/principles/ssot.md

<!-- Template tags (syntax varies by tooling) -->
include("principles/ssot")
```

Structured references enable automatic validation and resolution during builds or documentation generation.

## Decision Criteria

| Situation | Approach |
|-----------|----------|
| Content exceeds 50 lines | Reference |
| Content needed for immediate understanding | Inline with low verbosity |
| Content referenced multiple times | Reference (read once) |
| Content may change | Reference (stays current) |
| Content is self-contained context | Inline |
| Specifications needed by multiple sub-agents | Reference via persistent file path |

Default to referencing. Inline only when comprehension requires immediate access to the content.

## Delegated Work

When delegating tasks to other processes, provide references rather than content.

**Inefficient**:
```markdown
Here is the full analysis report:
[500 lines of report content]

Analyze this report and...
```

**Efficient**:
```markdown
Read: reports/{date}/source-analysis.md

Analyze this report and...
```

The downstream process reads the file once. The orchestrator's context remains lean. Both operate on the same source.

**Persistent intent pattern**:
```markdown
Orchestrator creates: {base}/{date}/{time}-specifications.md

Sub-agent receives:
Compulsory reads:
@{SPECIFICATIONS_PATH}

[Sub-agent reads specifications once, orchestrator context remains lean]
```

This ensures all sub-agents operate on identical specifications without the orchestrator restating requirements.

## Report Writing

Processes that generate findings should write reports to files and return references.

**Inefficient response**:
```
I found the following patterns:
[200 lines of findings]
```

**Efficient response**:
```
Wrote findings to reports/{date}/14-45-patterns.md

Summary: Identified 12 patterns across 4 packages. Key finding:
inconsistent error handling in pkg/api.
```

The orchestrator receives a concise summary and a reference for details, keeping orchestration context minimal while preserving full access to findings.

## Documentation Cross-References

Reference related content rather than repeat it:

```markdown
# API Error Handling
[Full explanation of error response format]

# Writing Controllers
See docs/api/error-handling.md for response format requirements.
When writing controllers, focus on...
```

This ensures consistency and reduces maintenance burden. The anti-pattern: two sections restating the same error format with minor variations, drifting apart over time.

## Benefits

Token efficiency (references are smaller than content), consistency (single source prevents drift), automatic propagation of updates, and clear separation between source and consumer. The reference principle covers measured benefits in detail.

`reference_over_copy` (module `engineering`, profile `principles`, package `design`)

## Implementation Checklist

Before pasting content: (1) check if it exists in a file, (2) if yes, reference the file with line range if partial, (3) if no, consider whether it should become a file, (4) only inline when immediate comprehension requires it.
