# Writing Rule Files

Write concise rule files that state behavioral constraints and reference detailed rationale. This guide specializes the shared writing objective for the `rules/` domain of a context package.

The governing principle is context efficiency (`context_efficiency.md` in the `density` package of this module's `core` profile); the load economics are the `budget_by_load` rule of the same package.

## Generalization Requirement

Rule files in a shared module reach every consumer of that module. Constraints must apply universally regardless of project type, language, or domain.

**Scope-based exceptions**: only files whose package or profile declares a narrower scope, or whose `paths:` scope them to matching files, may assume that context:

- a rule in a Go profile's package, or one with `paths:` matching `*.go` files at each depth, may assume Go
- a rule scoped to Markdown files may assume Markdown
- a rule in a general validation package must work for any artifact type

Write constraints in general terms. Avoid language-specific or domain-specific assumptions unless the file's scope indicates that context.

## Density Requirements

Rule files are **low density**:

- **Target**: 50-150 words (excluding examples)
- **Content**: Constraint statement + rationale reference
- **Structure**: Minimal sections
- **Examples**: Brief, illustrative

Rules auto-load for agents. Every token has high marginal cost.

## Structure Template

A rule's frontmatter carries one interpreted property, `paths:`; omit the block entirely for a rule that always applies. Each pattern is a full workspace-relative path where `*` and `?` match within one segment, so a pattern matches only paths with its own segment count; there is no `**`.

```markdown
---
paths:
  - "*.md"
  - "*/*.md"
---

# Rule Title

One-sentence statement of the rule using imperative language.

## Rationale

Brief explanation (2-3 sentences) of why this rule exists, then a link
to the principle that carries the depth:
<ctxmod_path path="…/reference/ssot.md" />

## Examples

**Correct**:
> Example of compliant behavior

**Incorrect**:
> Example of violation

## Exceptions

When this rule does not apply (if any).
```

## Content Guidelines

### Constraint Statements

Use imperative language:

- "Always reference files instead of inlining content"
- "Give each sub-agent only the context its task needs"
- "Run independent sub-agents in parallel"

Avoid hedging. Rules state requirements:

- **Good**: "Agents must validate input before processing"
- **Bad**: "Agents should consider validating input"

Steer toward the target behavior; reserve a bare prohibition for a hard guardrail, paired with the behavior to do instead (the `steer_positively` rule of this module's `core` profile).

### Rationale Section

Keep rationale brief. Link to reference files for detailed explanation:

```markdown
## Rationale

Duplicated content increases maintenance burden and risks inconsistency.
<ctxmod_path path="…/reference/ssot.md" />
```

The reference file provides depth. The rule extracts the constraint.

### Examples Section

Provide concrete, brief examples:

```markdown
## Examples

**Correct**:
> Sub-agent receives a link to the discovery objective as context.

**Incorrect**:
> Sub-agent receives the full text of the discovery objective inlined in its prompt.
```

### Exceptions Section

Document exceptions explicitly. If none exist, omit the section:

```markdown
## Exceptions

This rule does not apply when:
- The referenced file is fewer than 10 lines
- The agent operates without file access
```

## Pre-Writing Checklist

Before writing a rule:

- [ ] Identify the specific constraint
- [ ] Identify the principle providing rationale
- [ ] Check for existing rules covering similar constraints
- [ ] Determine the appropriate profile and package, and whether `paths:` should scope it

## Post-Writing Checklist

After writing:

- [ ] Constraint stated in one sentence
- [ ] Rationale links to a reference file
- [ ] Examples are brief and clear
- [ ] Total words within 50-150 (excluding examples)
- [ ] `paths:` patterns, if any, written per depth (no `**`)
- [ ] File placed in `profiles/{profile}/packages/{package}/rules/{name}.md`

## Output

Deliver:

1. The rule file written to `profiles/{profile}/packages/{package}/rules/{name}.md`
2. Brief confirmation: "Wrote rule: {path}"
