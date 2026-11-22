# Writing Agent Definitions

Write medium-density agent definitions that provide focused execution context for sub-agents. This guide specializes the shared writing objective for agents declared by a context package.

The governing principle is context efficiency (`context_efficiency.md` in the `density` package of this module's `core` profile).

## Generalization Requirement

Agents declared in a shared module reach every consumer of that module. Agent definitions must apply universally regardless of project type, language, or domain.

**Scope-based exceptions**: only agents whose package or profile declares a narrower scope may assume that context:

- an agent in a Go validation package may assume Go
- an agent in a specification-writing package may assume specifications
- an agent in a general validation package must work for any artifact type

Agent objectives, constraints, and output formats should use general terms. Avoid assumptions about specific languages, frameworks, or artifact types unless the agent's scope indicates that context.

## Density Requirements

Agent definitions are **medium density**:

- **Target**: 100-250 words (excluding inlined content)
- **Content**: Objective inline + context references + constraints + output
- **Structure**: Balanced sections
- **Examples**: Only when essential for execution

Agents receive their content as sub-agent prompts. The definition must be sufficient for independent execution, not bloated.

## Declaration

A package declares its agents in its entrypoint's `agents:` map; each key is the agent's name, with a `description` and the `agent_depth` it runs at (main, workflow, phase, objective, procedure, or task). The agent's prompt is the context rendered for that agent; a longer body lives in the package's `agents/` domain.

The depth rank names themselves (main, workflow, phase, objective, procedure) are reserved: context meant for every agent at one depth is a depth-bound package prompt (`PROMPT.md` with `binds_to_depth`), not an agent named after the depth.

## Structure Template

```markdown
---
description: Executes discovery over source code and reports findings.
binds_to_depth: objective
agents:
  discovery_source:
    description: Source-code discovery for one scope; reports file and line references.
    agent_depth: objective
---

# Discovery Source

One-sentence description of this agent's objective.

## Objective

<ctxmod_inline path="…/reference/discovery_objective.md" />

## Context

- <ctxmod_path path="…/reference/relevant_topic.md" /> (required)
- <ctxmod_path path="…/reference/additional_topic.md" /> (optional)

## Constraints

- Constraint 1
- Constraint 2
- Constraint 3

## Output

Expected output format or report structure.
```

## Content Guidelines

### Name

The key in the `agents:` map is the agent's name; skills and dispatching agents refer to the agent by it (`discovery_source`).

### Model Selection

Where the agent host lets a definition prefer a model, state the preference with the reason; otherwise state the tier in the dispatch guidance of the skill that launches the agent.

| Tier | Use Case |
|-------|----------|
| small, fast model | Quick, straightforward tasks |
| mid-tier model | Standard complexity tasks |
| strongest model | Complex reasoning, critical decisions; very rarely used, not unless explicitly instructed |

### Objective Section

Inline the objective definition:

```markdown
## Objective

<ctxmod_inline path="…/reference/discovery_repo_source.md" />
```

The objective provides execution instructions. Inline the part the agent needs: a summary when the agent only needs the goal, the core content for ordinary execution, the complete content when every step matters.

### Context Section

Link to required and optional context:

```markdown
## Context

- <ctxmod_path path="…/reference/discovery_objective.md" /> (required)
- <ctxmod_path path="…/rules/orchestration_rule.md" /> (required)
- <ctxmod_path path="…/reference/context_patterns.md" /> (optional)
```

Replace the orchestration rule with the rule category appropriate for your agent. Required context always loads. Optional context loads when relevant.

### Constraints Section

Bound agent behavior with imperative statements:

```markdown
## Constraints

- Modify files only inside the designated directory
- Report file references with line ranges, not content
- Complete within the specified turn limit
- Work alone; launch no sub-agents
```

### Output Section

Specify expected deliverables:

```markdown
## Output

Create a report just in time as a work record
(`ctxmod work new report <title> --parent <work item>`) containing:

1. Summary (50-100 words)
2. Findings with file references and line ranges
3. Recommendations (if applicable)

Return a brief confirmation with the report path.
```

Clear output expectations guide sub-agent behavior.

## Agent Categories

Organize agents by objective domain, one package per domain:

- discovery: information gathering
- analysis: information synthesis
- validation: quality verification
- writing: content generation
- implementation: code modification
- coordination: multi-phase coordination

## Pre-Writing Checklist

Before writing an agent:

- [ ] Identify the objective type and variant
- [ ] Identify the required context files
- [ ] Determine the appropriate model tier
- [ ] Define specific constraints
- [ ] Specify the expected output format

## Post-Writing Checklist

After writing:

- [ ] Declaration complete: name, description, `agent_depth`
- [ ] Objective inlined at the appropriate level of detail
- [ ] Context references appropriate and resolving
- [ ] Constraints are specific and actionable
- [ ] Output format clearly defined
- [ ] Total prose within 100-250 words
- [ ] Agent declared in the package of its domain

## Output

Deliver:

1. The agent declaration (and body, if any) written to its package
2. Brief confirmation: "Wrote agent: {path}"
