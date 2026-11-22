# Reference Sync Procedure

Ensure the project's context reference files (the `reference/` domain of the repository's context module) accurately reflect current project state by detecting drift and correcting outdated content.

## Prerequisites

- Access to the project codebase
- Access to the context module's reference files

## Governing Principles

- Single source of truth, DRY, and KISS (the `engineering` module's `principles` profile)
- Reference over duplication: `reference_over_duplication.md` and the `point_cite_never_paste` rule in the `density` package of this module's `core` profile

## Steps

### 1. Read Schema

The project's context schema is the single source of truth for directory structure, expected files, and validation rules. For a ctxmod module that is the module layout (`module.yaml`, `profiles/<profile>/packages/<package>/` with its content domains) together with the project's own conventions for what its reference domain must hold; the `project` profile of this module states what belongs in project context and what does not.

Read this schema to understand:

- Which subdirectories should exist
- Which files are expected within each subdirectory
- Density and format requirements per category
- Validation rules to apply

Do not assume structure. The schema may change; this procedure remains valid by reading it.

### 2. Inventory Current State

Scan the reference files against the schema:

- List existing files and subdirectories
- Compare against the schema-defined structure
- Note file modification dates
- Identify files present but not in the schema (may indicate schema evolution needed)

### 3. Detect Implementation Drift

For each existing reference file:

1. Identify what implementation state the file describes
2. Examine current implementation state
3. Compare for drift signals:
   - Structural changes (new/removed components)
   - Behavioral changes (modified patterns)
   - Terminology changes (new/deprecated terms)

Use file system timestamps, git history, and codebase scanning.

### 4. Prioritize Updates

Rank by impact of outdated content:

| Priority | Criteria |
|----------|----------|
| High | Changes affecting agent decision-making |
| Medium | Changes with indirect agent impact |
| Low | Minor additions without behavior change |

### 5. Apply Updates

For each file requiring update:

1. Read current file content
2. Gather current implementation state
3. Write updated content

Apply writing standards:

- the writing anti-patterns and clarity principles: `anti_patterns.md` and `clarity.md` in the `basics` package of this module's `core` profile
- reader expertise and reader intent: the `audience` package of the `writing` module's `documentation` profile
- section construction and section hierarchy: the `structure` package of the `writing` module's `documentation` profile
- documentation review and content evolution: the `maintenance` package of the `writing` module's `documentation` profile

### 6. Create Missing Files

For schema-expected files that do not exist:

**Create when**:

- Project complexity warrants the file
- Agents would benefit from the context
- Content can be accurately generated

**Skip when**:

- Project is too simple for the category
- Content would be speculative

Follow the schema-defined format and density guidelines.

### 7. Validate

Apply the validation rules from the schema (for a ctxmod module, `ctxmod vet --root .` must pass clean). Verify:

- Schema-defined constraints satisfied
- Content reflects current implementation
- Cross-references resolve

## Decision Points

**Implementation vs documentation conflict**: Implementation is authoritative. Update documentation to match.

**Uncertain state**: Investigate before documenting. Incorrect content causes more harm than absent content.

**Schema mismatch**: If the project needs structure not in the schema, consider whether the schema should evolve.

## Success Criteria

- Reference files reflect current implementation
- Schema-defined validation rules pass
- Writing standards applied
- No contradictions between files

## Common Issues

**Stale examples**: Verify example targets exist before writing.

**Scope creep**: Refer to the schema for subdirectory purposes; split files accordingly.

**Over/under-documentation**: Follow the schema-defined density guidelines.
