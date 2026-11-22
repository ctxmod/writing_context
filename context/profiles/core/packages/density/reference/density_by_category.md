# Density by Category

Different context-content categories (domains) require different content densities. Density aligns with how files are loaded and used.

## Core Principle

Files loaded automatically must be sparse—every token counts against the agent's context budget. Files read deliberately can be dense—comprehensive coverage aids understanding.

## Category Density

| Category | Density | Rationale |
|----------|---------|-----------|
| `reference/` | High | Read once for understanding, not auto-loaded |
| `rules/` | Low | Auto-loaded, must be concise |
| `skills/` | Low | Loaded by name, aggregates references |
| `commands/` | Low | Developer-invoked, orchestration steps only |
| `agents/` | Medium | Sub-agent context, balanced completeness |

ctxmod has no `commands/` domain; a command written as a skill or as a depth-bound prompt keeps the command density below.

## High Density (Reference)

Reference files are comprehensive and self-contained:

- **Word count**: 300-800 words typical
- **Content**: Complete coverage of the topic
- **Structure**: Multiple sections with depth
- **Examples**: Included when they aid understanding
- **Cross-references**: Link to related references

Reference files serve as the single source of truth. Completeness matters more than brevity.

## Low Density (Rules, Skills, Commands)

These categories prioritize brevity:

- **Word count**: 50-150 words (excluding code examples)
- **Content**: Core information only
- **Structure**: Minimal sections
- **Examples**: Brief, illustrative
- **Cross-references**: Link to reference files for depth

These files add to agent context frequently. Every token has high marginal cost. A 200-word rule file loaded 50 times consumes 10,000 tokens. Reducing it to 100 words saves 5,000 tokens across those interactions.

### Rules

State the constraint. Reference rationale:

```markdown
# Rule Name

One-sentence constraint statement.

## Rationale

Brief explanation.

<link to the reference file carrying the rationale>
```

### Skills

Declare capability. Aggregate references:

```markdown
# Skill Name

One-sentence capability.

## Context

- <links to the objective reference files>
```

### Commands

Define orchestration. Name agents:

```markdown
# Command Name

## Workflow

1. agent:first-agent
2. agent:second-agent
```

## Medium Density (Agents)

Agents balance context needs with budget constraints:

- **Word count**: 100-250 words
- **Content**: Enough for execution, no more
- **Structure**: Objective, context, constraints, output
- **Examples**: Only when essential
- **Cross-references**: Required context, selective optional

Agents receive their content as sub-agent prompts. The content must be sufficient for independent execution but not bloated.

## Measuring Density

Assess density by:

1. **Information per word**: High ratio indicates appropriate density
2. **Redundancy**: Zero redundancy indicates optimal density
3. **Completeness**: All necessary information present
4. **Loading frequency**: Higher frequency requires lower density

## Adjusting Density

If a file feels too dense for its category:

- Extract content to reference file
- Replace with link
- Keep only essential summary

If a file feels too sparse for its category:

- Add necessary context
- Expand examples
- Include related information

## Consistency

Within a category, maintain consistent density. Readers develop expectations. Meeting those expectations reduces cognitive load.
