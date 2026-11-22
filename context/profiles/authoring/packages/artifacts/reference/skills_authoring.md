# Writing Skill Files

Write sparse skill files that declare capabilities by aggregating references to objectives, rules, and agents. This guide specializes the shared writing objective for the `skills/` domain of a context package.

## Generalization Requirement

Skills in a shared module reach every consumer of that module. Capabilities must apply universally regardless of project type, language, or domain.

**Scope-based exceptions**: only skills whose package or profile declares a narrower scope may assume that context:

- a skill in a Go validation package may assume Go
- a skill in a specification profile may assume specifications
- a skill in a general validation package must work for any artifact type

Skill declarations and purpose statements should describe general capabilities. Avoid references to specific languages, frameworks, or artifact types unless the skill's scope indicates that context.

## Density Requirements

Skill files are **low density**:

- **Budget**: line ceilings keyed to the depth the skill binds to (table below; ceilings, not targets)
- **Content**: Capability declaration + reference aggregation
- **Structure**: Minimal prose sections
- **Examples**: None (reference files provide examples)

Skills load by name. They aggregate context; they don't provide it directly.

Skill body budgets are line ceilings keyed to the skill's depth binding (`binds_to_depth`), the only observable signal of how much orchestration the entry point must carry. There is no line-budget field and none is added; a skill without a depth binding budgets at the procedure ceiling until it declares a depth. Body lines are every line after the closing `---`, blanks included. Ceilings are not targets: skills with a `reference/` subtree keep bulk there; the entry point decides and routes. Count body lines when writing or editing; no mechanical checker exists, so enforcement is authorship discipline.

| Depth tier (`binds_to_depth`) | Skill shape | SKILL.md body-line ceiling |
|---|---|---|
| procedure | fixed step sequence; detail lives in reference/ | ≤ 180 |
| objective | capability entry aggregating objectives, rules, agents | ≤ 340 |
| phase | full workflow orchestration: phase tables, validation dimensions, anti-patterns | ≤ 460 |
| workflow | cross-phase orchestration (reserved; none observed) | ≤ 460 |
| main | main-agent entry points running one capability end to end; the ceiling sits above the observed bodies (131, 162, and 335 lines) | ≤ 350 |

## Structure Template

A skill is a directory `skills/<name>/` holding `SKILL.md`. Its properties are a `description` and a binding (`binds_to_depth`, or another gating constraint), either as `SKILL.md` frontmatter or in a sibling `skill.yaml`. Skill-local detail lives under the skill's own `reference/`.

```markdown
---
description: >-
  Output-keyed one-liner leading with the artifact the reader ends up
  holding (dispatch timing belongs in the body).
binds_to_depth: objective
---

# Skill Name

One-sentence capability description.

## Purpose

When to use this skill (2-3 sentences maximum).

## Context

- <ctxmod_path path="…/reference/discovery_objective.md" /> (required)
- <ctxmod_path path="…/reference/context_patterns.md" /> (optional)

## Agents

Relevant agents:
- `agent_name_1`: brief description
- `agent_name_2`: brief description

## Notes

Additional guidance (only if essential, otherwise omit).
```

## Content Guidelines

### Capability Declaration

The skill's directory name and description declare what the skill enables:

```yaml
# skills/discovery_workflows/skill.yaml
description: Execute discovery objectives for information gathering
binds_to_depth: objective
```

The name is the invocation identifier. The description leads with the artifact the reader ends up holding.

### Purpose Section

Explain when to use the skill in 2-3 sentences:

```markdown
## Purpose

Use when gathering information about code structure, documentation, or
external sources. Appropriate for the discovery phase of any workflow
that requires understanding before action.
```

### Context Section

Aggregate references with link components:

```markdown
## Context

- <ctxmod_path path="…/reference/discovery_objective.md" />
- <ctxmod_path path="…/reference/context_patterns.md" />
- <ctxmod_path path="…/rules/context_rule.md" />
```

Required links provide essential context. Optional links provide supplementary guidance; say which is which in the list.

### Agents Section

Name related agents by their declared name (the key in a package's `agents:` map):

```markdown
## Agents

- `discovery_source`: source code discovery
- `discovery_docs`: documentation discovery
- `discovery_research`: external research
```

## Skill-Agent Relationship

Skills aggregate agents. The skill defines "what can be done"; agents define "how":

```
skill discovery
├── agent discovery_source
├── agent discovery_docs
└── agent discovery_research
```

Multiple agents may implement a single skill's capability.

## Pre-Writing Checklist

Before writing a skill:

- [ ] Identify the capability being provided
- [ ] Identify relevant objective definitions
- [ ] Identify relevant agents (or plan to create them)
- [ ] Check for existing skills with overlapping capability

## Post-Writing Checklist

After writing:

- [ ] Description and depth binding present
- [ ] Purpose section is 2-3 sentences
- [ ] Context references are appropriate and resolve
- [ ] Agents are named correctly
- [ ] Body lines within the depth tier ceiling
- [ ] Skill placed in `profiles/{profile}/packages/{package}/skills/{name}/SKILL.md`

## Output

Deliver:

1. The skill written to `profiles/{profile}/packages/{package}/skills/{name}/SKILL.md`
2. Brief confirmation: "Wrote skill: {path}"
