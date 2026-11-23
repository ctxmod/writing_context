---
name: write_phase
description: >-
  Context content writing phase: produce context content files
  (reference, rule, skill, agent, tool, command, and documentation
  variants) through discovery, research, planning, writing, and
  multi-dimension validation with a bounded remediation loop.
binds_to_depth: phase
---

# Write Context Phase

Context content writing phase: produce the content files that define
agent behavior in a context module (reference files, rules, skills,
agents, tool declarations, commands, documentation). It is one of the
sibling writing phases (report, work item, context, intent); they share
the same writing methodology and the same objective- and
procedure-depth writing guidance.

Context content writing is a **phase, not a workflow**. The main agent
invokes it directly for one artifact (a "write a reference file", "write
a rule", "write a skill", "write an agent", "write a command", or "write
docs" request, or a general "write" request routed here), and any other
domain's workflow may use this phase as its "write context content"
sub-step.

## Variants

Seven content variants share this one phase. The variant is determined
by the artifact type requested; each takes the arguments below.

### Reference variant

Create a reference file following the module's conventions.

| Argument | Required | Description |
|----------|----------|-------------|
| `package` | Yes | The profile and package the file belongs to |
| `name` | Yes | Reference file name (snake_case) |
| `description` | Yes | Brief description of the reference's purpose |

Output: `profiles/{profile}/packages/{package}/reference/{name}.md`. Density: 300-800 words.

### Rule variant

Create a rule file defining a behavioral constraint.

| Argument | Required | Description |
|----------|----------|-------------|
| `package` | Yes | The profile and package the rule belongs to |
| `name` | Yes | Rule file name (snake_case) |
| `constraint` | Yes | Behavioral constraint description |

Output: `profiles/{profile}/packages/{package}/rules/{name}.md`. Density: 50-150 words.

### Skill variant

Create a skill that aggregates agent capabilities.

| Argument | Required | Description |
|----------|----------|-------------|
| `package` | Yes | The profile and package the skill belongs to |
| `name` | Yes | Skill name (snake_case) |
| `description` | Yes | Skill purpose |

Output: `profiles/{profile}/packages/{package}/skills/{name}/SKILL.md` (frontmatter `description` and a binding such as `binds_to_depth`, or a sibling `skill.yaml`). Density: the line budget of the depth the skill binds to.

### Agent variant

Create an agent definition: the context template a sub-agent starts from.

| Argument | Required | Description |
|----------|----------|-------------|
| `package` | Yes | The profile and package that declares the agent |
| `name` | Yes | Agent name (snake_case) |
| `objective` | Yes | Agent objective description |

Output: the package's `agents` declaration (an entry in the package entrypoint's `agents:` map, or a file under the package's `agents/`). Density: 100-250 words. The rank names main, workflow, phase, objective, and procedure are reserved for depths; an agent meant to run at one of those depths is a depth-bound package prompt (`PROMPT.md` with `binds_to_depth`), not an agent named after the depth.

### Tool variant

Declare a tool the module carries.

| Argument | Required | Description |
|----------|----------|-------------|
| `name` | Yes | Tool name (snake_case) |
| `purpose` | Yes | What the tool does and when an agent runs it |

Output: `tools/{name}.yaml` or `tools/{name}/tool.yaml`, at module or package level. Density: as the declaration schema requires.

### Command variant

Write a command: an orchestration template that runs a workflow through workflow design, agent creation, writing, and validation phases. ctxmod has no command domain; express a command as a skill (or as a depth-bound package prompt), or write it for the agent host's own command mechanism when the host supports slash commands.

| Argument | Required | Description |
|----------|----------|-------------|
| `name` | Yes | Command name |
| `orchestration_description` | Yes | Orchestration/workflow description |

### Docs variant

Orchestrate documentation creation with research, writing, and validation phases.

| Argument | Required | Description |
|----------|----------|-------------|
| `type` | Yes | Documentation type: `general`, `technical`, or `specification` |
| `description` | Yes | Brief description of documentation purpose |

Documentation is written to the artifacts of the most specific work item in context (a work-store artifact record), or to a general artifacts location when there is no work item. Override the default by specifying an explicit output path.

## Orchestration Context

The main agent orchestrates: it dispatches sub-agents, passes report
paths between them, and never reads intermediate report bodies into its
own context. The dispatch parameters each sub-agent needs (variant,
target location, report path, work item context) travel in its dispatch
prompt.

## When to Use

Use this phase when:

- Producing context content files (reference, rule, skill, agent, tool, command)
- Schema compliance and density targets matter
- Cross-references must resolve (`ctxmod vet` passes)
- Shared (published) files must be project-agnostic

## Variant Dispatch

The variant determines output location, density target, and schema
reference. All variants share the same phase structure below;
variant-specific differences are noted per phase.

| Variant | Output location | Density |
|---------|-----------------|---------|
| `reference` | `profiles/{profile}/packages/{package}/reference/{name}.md` | 300-800 words |
| `rule` | `profiles/{profile}/packages/{package}/rules/{name}.md` | 50-150 words |
| `skill` | `profiles/{profile}/packages/{package}/skills/{name}/SKILL.md` | line budget of the bound depth |
| `agent` | the package's `agents` declaration | 100-250 words |
| `tool` | `tools/{name}.yaml` or `tools/{name}/tool.yaml` | declaration schema |
| `command` | a skill, a depth-bound prompt, or the host's command file | variable (workflow design) |
| `docs` | the work item's artifacts, or a general artifacts location | variable (type-driven) |

### Documentation Types (docs variant only)

When the variant is `docs`, the `type` argument determines procedures
and schema references:

| Type | Purpose | Procedures |
|------|---------|------------|
| `general` | User guides, conceptual docs, process docs | the general procedures of the `writing` module's `documentation` profile (`procedures` package) |
| `technical` | API references, runbooks, architecture docs | the technical procedures of the same package |
| `specification` | Requirements, design specs, technical specs | the `procedures` package of the `writing` module's `specification` profile |

## Phase Orchestration

This phase dispatches objective-depth sub-agents carrying the shared
writing objective guidance, with the content-specific reference
material below scoping each dispatch. The shared writing methodology
carries the variant-selection reference (model choice, coordination
pattern, transition criteria, anti-patterns).

```
Phase 1: Discovery (mid-tier model)
         |
Phase 2: Research (optional)
         |
Phase 3: Planning (mid-tier model)
         |
Phase 4: Writing (strongest model)
         |
Phase 5: Validation (mid-tier model)
         |
Phase 6: Remediation (conditional loop)
```

### Phase 1: Discovery

Gather context for content creation. Launch these sub-agents:

- Existing-content discovery: scan the target package and profile for overlaps
- Related-content discovery: identify cross-reference opportunities

Dispatch these one at a time, in the foreground, waiting for each,
unless this phase has been granted concurrent dispatch; read-only
discovery sub-agents may then share a single message.

- Reports: one discovery report per sub-agent (existing, related), each created just in time as a work-store report (`ctxmod work new report …`)

**Workflow-specific notes**:

- Discovery only; do not write the content file
- For rules: discover reference files providing rationale
- For skills: discover agents that aggregate to this skill
- For agents: discover the objectives the agent dispatches
- For commands: discover workflow patterns and dispatch prompts

### Phase 2: Research (Optional)

Research best practices when the topic warrants external knowledge.

- Report: one research report

**Workflow-specific notes**:

- Skip when the topic is internal to the context system itself
- Skip when the user provides a comprehensive specification
- Skip when the topic is well defined by existing module conventions

### Phase 3: Planning

Plan the content file structure.

- Report: one planning report

**Workflow-specific notes**:

- Plan structure only; do not write the content file
- Define sections and a content outline
- Identify cross-references (ctxmod link components in the body; frontmatter is not a cross-reference channel in ctxmod)
- Plan density targets appropriate to the variant
- For rules: identify the reference file for the rationale link
- For skills: identify agent references

### Phase 4: Writing (strongest model)

Produce the content file.

- Output: the variant-specific output location (see Variant Dispatch)

**Workflow-specific notes**:

- Write the content file only
- Follow the structure from the planning report
- Include exactly the metadata the domain interprets: a rule's `paths:` when it is scoped; a package entrypoint's or skill's `description` and binding; nothing on reference files, whose frontmatter is not interpreted (the description becomes the opening sentence)
- Match the density target for the variant
- Shared files must be project-agnostic
- Use ctxmod link components (`ctxmod_path`, `ctxmod_link`, `ctxmod_inline`) for internal references
- Where the content claims something about produced artifacts, cite one real generated example by path when one exists; mark fabricated sketches as sketches

### Phase 5: Validation

Verify content file quality. Launch these sub-agents:

- Structure validation: metadata, sections, heading hierarchy, and a clean `ctxmod vet --root <repository root>`
- Content validation: anti-patterns, clarity, density; evidence claims are real-cited or sketch-marked
- Reference validation: cross-references resolve

Dispatch these one at a time, in the foreground, waiting for each,
unless this phase has been granted concurrent dispatch; read-only
validation sub-agents may then share a single message.

- Reports: one validation report per dimension (structure, content, references)

### Phase 6: Remediation (Conditional Loop)

Execute only if any Phase 5 validation report contains failures.
Maximum 3 iterations.

**Loop execution**:

1. All Phase 5 validations pass: skip Phase 6, workflow complete
2. Any failures: launch the remediation agent
3. After remediation: re-launch all three Phase 5 validation agents
4. All re-validations pass: workflow complete
5. Failures remain and iterations < 3: return to step 2
6. Iterations = 3: proceed with the best-effort file, report unresolved issues

## Information Flow

```
Phase 1: Discovery
- Receives: variant, package, name, description
- Produces: discovery reports (existing, related)

Phase 2: Research (optional)
- Receives: Phase 1 outputs
- Produces: research report

Phase 3: Planning
- Receives: Phase 1 outputs, Phase 2 output (if run)
- Produces: planning report

Phase 4: Writing
- Receives: Phase 3 output
- Produces: the variant-specific output location

Phase 5: Validation
- Receives: content file path
- Produces: validation reports (structure, content, references)

Phase 6: Remediation (conditional)
- Receives: validation reports, content file path
- Produces: one remediation report per iteration
```

The main agent passes report **paths** between phases, never report
content. Each report is a work-store record (`ctxmod work new report
<title> --owner <owning work item>`), created just in time by the
sub-agent that writes it.

## Execution Strategy

1. **Resolve variant**: determine reference/rule/skill/agent/tool/command/docs from the request
2. **Discovery**: launch the discovery sub-agents (one at a time by default); wait
3. **Research** (optional): launch a research sub-agent if external knowledge is needed
4. **Planning**: launch the planning sub-agent; wait
5. **Writing**: launch the writing sub-agent (strongest model); wait
6. **Validation**: launch the validation sub-agents (one at a time by default); wait
7. **Conditional remediation**: if failures, remediate and re-validate (max 3)
8. **Complete**: return the content file path and a validation summary

## Workflow Variants

### Lightweight Rule

Skip Phase 2 (research) for rules internal to the context system. Skip
Phase 5 reference validation when the rule has no cross-references.

### Research-Heavy Reference

Expand Phase 2 for reference files covering external best practices.
Use one research sub-agent per domain for multi-domain topics.

### Command with Workflow Design

Commands require additional workflow design in Phase 3 (planning), and
may require authoring agent definitions alongside the command. Skip
Phase 2 (research); commands are internal to the context system.

### Documentation (docs variant)

Documentation uses the artifacts output (not a context domain) and
follows the type-specific procedures named under Documentation Types.
Discovery (Phase 1) adds a further sub-agent for documentation
standards and conventions discovery (the `writing` module's
`documentation` profile).

## Error Handling

| Situation | Response |
|-----------|----------|
| Discovery finds conflicting content | Report the conflict, await a decision |
| Validation exceeds iterations | Report persistent issues, await a decision |
| Writing fails | Check the planning output, await a decision |
| Cross-reference target missing | Report the missing reference, await a decision |

Error handling follows the stop-report-propose-await pattern.

## Quality Criteria

| Criterion | Validation Method |
|-----------|-------------------|
| Metadata complete and interpreted | Phase 5 checks required properties per domain |
| Density within target | Phase 5 verifies the word count range |
| Cross-references resolve | Phase 5 runs `ctxmod vet` and checks every link component |
| Project-agnostic | Phase 5 checks for project-specific content |
| Anti-pattern free | Phase 5 applies the clarity principles |

## Anti-Patterns

| Avoid | Why | Instead |
|-------|-----|---------|
| Skipping discovery | Uninformed content | Gather existing content first |
| Writing without planning | Incoherent structure | Plan before writing |
| Single validation pass | Unverified quality | Use the validation loop |
| Project-specific content in shared files | Breaks portability | Keep shared files project-agnostic |
| Returning content | Bloats the orchestrator | Return the path only |
| Duplicating rationale | Bloats the file | Reference principles instead |

## Sub-Layer Launch

When this phase requires objective-depth execution, launch an
objective-depth writing agent; the objective in turn launches a
procedure-depth writing agent for step mechanics. The dispatch prompt:

```text
Execute <phase-name> within context content writing.
Artifact category: <reference|rule|skill|agent|tool|command>
Variant: <content-type>
Phase-specific instructions:
  <phase-specific parameters>
Write to {OUTPUT_PATH}, or create a report just in time
(`ctxmod work new report <title> --owner <work item>`) and write there.
```

## Cross-Workflow Reference

Other domains' workflows may use this phase directly to "write context
content" as a sub-step: launch a phase-depth agent with this skill from
any workflow that needs context content created. The phase-selection
reference of the shared writing methodology (model choice, coordination
pattern, transition criteria, anti-patterns) applies to every writing
phase variant.

## Cross-Cutting Reference

- Parallel and fan-out/fan-in orchestration patterns, the main-agent orchestration discipline, and work-store-first record keeping (the `agentic` module and ctxmod's builtin work discipline)
- The KISS, DRY, and single-source-of-truth principles (the `engineering` module's `principles` profile)
- Context efficiency and agent-facing writing: `context_efficiency.md` and `agent_facing_writing.md` in the `density` package of this module's `core` profile
- The authoring guides for each artifact type in this package: `reference_authoring.md`, `rules_authoring.md`, `skills_authoring.md`, `agents_authoring.md`, `commands_authoring.md`, and `rule_authoring.md`

Depth-scoped writing guidance for the sub-agents this phase launches
(the `writing_objective` and `writing_procedure` skills), the shared
writing methodology (the `writing_phase` skill) and the sibling report
writing phase (`write_report_phase`) live in the `agentic` module's
`workflows` profile.
