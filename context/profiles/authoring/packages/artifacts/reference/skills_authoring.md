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

## The Agent Skills Format

A skill written here may be rendered for harnesses that read the **Agent Skills** open format (`SKILL.md` with YAML frontmatter; originated by Anthropic, published as an open standard in December 2025, contributed to the Linux Foundation's Agentic AI Foundation in October 2026). This module's skill grammar is ctxmod's, not the format's; where the two differ, write for ctxmod and know what the rendered skill must satisfy.

**What the format requires.** Frontmatter `name` (1-64 characters of lowercase letters, digits, and single hyphens, matching the skill directory) and `description` (1-1024 characters, saying what the skill does and when to use it). Optional: `license`, `compatibility` (environment requirements, at most 500 characters), `metadata` (a string-to-string map for client-specific properties), and an experimental `allowed-tools`. One vendor's runtime adds constraints of its own (no XML tags, reserved words in `name`); name those as vendor specifics when they matter.

**Progressive disclosure is the format's load model**, and it is the information hierarchy of the `core` profile applied to skills: metadata (roughly 100 tokens per skill) is resident for every skill at startup; the body (recommended under 5,000 tokens and 500 lines) loads when the skill activates; bundled files load only when the body points at them. The depth-tier ceilings above sit inside the format's 500-line guidance.

| Concern | ctxmod skill | Agent Skills format |
|---|---|---|
| Directory name | snake_case (`[a-z][a-z0-9_]{0,63}`) | `name` with hyphens, no underscores — a rendered name must map to that charset |
| Gating | `binds_to_depth` / `gated_by` and other ctxmod properties | none in the spec; client-specific properties belong under `metadata` |
| Bundled detail | the skill's own `reference/` | `references/`, `scripts/`, `assets/` by convention |
| Links | `ctxmod_path` / `ctxmod_inline` link components, resolved at render | relative paths from the skill root, kept one level deep |
| Description | output-keyed one-liner (template above) | what it does **and** when to use it, with the keywords a task would contain |

**The description is the selection signal.** When a harness chooses skills itself, it decides from `name` and `description` alone — the body is not loaded until after the choice. A skill invoked by name from an orchestrating skill or command can keep the output-keyed one-liner; a skill meant to be picked up by the model unprompted needs its trigger condition in the description, written in the third person ("Extracts …; use when …"), because dispatch timing written only in the body is invisible at selection time.

**Practices the format's guidance adds** that this guide's density rules already imply: assume the model's general knowledge and add only what it lacks; match the degree of freedom to the task's fragility (heuristics for open work, an exact script for a fragile sequence); prefer bundled scripts for deterministic steps and say whether to run or read each one; keep references one level deep from `SKILL.md`, since nested chains invite partial reads; give long reference files a contents list; and build a few evaluation scenarios from observed failures before writing extensive instructions.

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

## Sources

- https://agentskills.io/specification — Agent Skills format: directory layout, frontmatter fields and limits, progressive-disclosure tiers, one-level file references (accessed 2026-11-22)
- https://www.linuxfoundation.org/press/agentic-ai-foundation-announces-four-new-projects-agent-skills-open-responses-openenv-and-opensandbox — Agent Skills contributed by Anthropic to the Agentic AI Foundation (Linux Foundation press release, 2026-10-22; accessed 2026-11-22)
- https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices — vendor authoring guidance: conciseness, degrees of freedom, third-person what-and-when descriptions, one-level references, contents lists, evaluation-first development (Anthropic docs; accessed 2026-11-22)
- https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills — the progressive-disclosure design rationale and the 2025-12-18 open-standard update (Anthropic Engineering, 2025-10-16; accessed 2026-11-22)
