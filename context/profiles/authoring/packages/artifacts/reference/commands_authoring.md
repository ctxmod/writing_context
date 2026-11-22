# Writing Commands

Write sparse commands that define orchestration workflows through phased agent invocations. This guide specializes the shared writing objective for commands.

ctxmod has no command domain. A command is expressed as a skill that runs at main depth (or as a depth-bound package prompt), or written for the agent host's own slash-command mechanism where the host has one; the guidance below holds for every form. The governing principles are orchestration planning and parallelization (the `agentic` module).

## Generalization Requirement

Commands in a shared module reach every consumer of that module. Orchestration workflows must apply universally regardless of project type, language, or domain.

**Scope-based exceptions**: only commands whose package or profile declares a narrower scope may assume that context:

- a command in a Go validation package may assume Go
- a command in a specification-writing package may assume specifications
- a command in a general validation package must work for any artifact type

Workflow phases and agent invocations should describe general orchestration patterns. Avoid assumptions about specific languages, frameworks, or artifact types unless the command's scope indicates that context.

## Density Requirements

Commands are **low density**:

- **Target**: 100-200 words (excluding workflow definitions)
- **Content**: Usage + phased workflow + context references
- **Structure**: Workflow phases dominate
- **Examples**: None (show orchestration, not examples)

Commands are developer-invoked. They define orchestration structure, not explanation.

## Structure Template

```markdown
---
description: One-sentence description of what this command orchestrates.
binds_to_depth: main
---

# Command Name

One-sentence description of what this command orchestrates.

## Usage

`/command_name [args]`

| Argument | Required | Description |
|----------|----------|-------------|
| `arg1` | Yes | First argument purpose |
| `arg2` | No | Optional argument purpose |

## Workflow

### Phase 1: Discovery

Launch parallel discovery agents.

- `discovery_source`
- `discovery_docs` (parallel)

### Phase 2: Analysis

Analyze discovery reports.

- `analysis_synthesis`

### Phase 3: Execution

Execute based on analysis.

- `implementation_task`

### Remediation (if needed)

Handle failures and retry.

- `remediation_coordinator`

## Context

Links to the orchestration patterns the workflow follows.

## Notes

Additional guidance for developers (only if essential).
```

## Content Guidelines

### Usage Section

Define invocation syntax and arguments:

```markdown
## Usage

`/write_context_file [domain] [name]`

| Argument | Required | Description |
|----------|----------|-------------|
| `domain` | Yes | Target domain (reference, rules, skills, agents, tools) |
| `name` | Yes | File identifier |
```

### Workflow Section

Define orchestration through phases:

```markdown
### Phase 1: Discovery (parallel)

- `discovery_source`
- `discovery_docs`

### Phase 2: Validation (sequential, after Phase 1)

- `validation_report`
```

Each phase specifies:

- Purpose (in the heading or a brief description)
- Agents to invoke
- Execution mode (parallel/sequential)
- Dependencies (what must complete first)

### Agent References

Name agents by their declared name:

```markdown
- `discovery_source`
- `validation_report` (for each report, parallel)
```

Parenthetical notes indicate:

- Execution mode: `(parallel)`, `(sequential)`
- Iteration: `(for each X)`
- Conditions: `(if validation fails)`

### Remediation Phase

Include remediation for recoverable failures:

```markdown
### Remediation (if needed)

If validation fails:
1. `correction_coordinator`
2. Return to Phase 2
```

### Context Section

Link to orchestration patterns with link components: the parallel orchestration pattern and the remediation phase skill the workflow falls back on (`remediation_phase` in the `agentic` module's `workflows` profile).

## Command Types

### Repetitive Commands

Require minimal input. Clear constraints:

```markdown
## Workflow

1. Discover current state
2. Apply transformation
3. Verify result

No additional input required.
```

### Template Commands

Require developer-provided context:

```markdown
## Usage

`/implement_feature [description]`

Developer provides an objective description. The workflow adapts to input.
```

## Pre-Writing Checklist

Before writing a command:

- [ ] Identify the orchestration goal
- [ ] Identify the required phases
- [ ] Identify agents for each phase
- [ ] Determine parallelization opportunities
- [ ] Check for existing commands or skills with a similar purpose

## Post-Writing Checklist

After writing:

- [ ] Usage section complete with arguments
- [ ] All phases defined
- [ ] Agents named correctly
- [ ] Parallel/sequential execution specified
- [ ] Remediation phase included
- [ ] Total prose within 100-200 words
- [ ] Command placed in its package (as a skill or prompt) or in the host's command location

## Output

Deliver:

1. The command written to its location
2. Brief confirmation: "Wrote command: {path}"
