# Clarity Principles

All writing prioritizes clarity over impressiveness. Write to inform, not persuade.

For writing an agent consumes, the agent takes the same process every run: the document is a specification of that process, not a persuasion piece.

## Core Principles

### Precision Over Obfuscation

Use technical terms only when they add precision. Prefer simple language that conveys meaning equally well.

**Examples**:
- *Bad*: "We delve into the intricate realm of context management to illuminate its pivotal role."
- *Good*: "We study context management to understand its contribution."

### Direct Communication

State claims directly. Give readers "random access"—they should understand content without reading everything preceding it.

**Examples**:
- *Bad*: "It is important to note that the agent achieves high accuracy."
- *Good*: "The agent achieves 90% accuracy."

### Active Voice

Use active voice for directness. Reserve passive for emphasis on object or unknown agent.

| Passive | Active |
|---------|--------|
| "The file is read by the agent." | "The agent reads the file." |
| "Context was managed efficiently." | "The system managed context efficiently." |

**Target**: 80% active, 20% passive.

## Sentence Construction

### Length Distribution

Target: 70% medium (15-25 words), 20% short (8-14), 10% long (26-35). Avoid excessive short sentences (choppy), excessive long sentences (hard to parse), and uniform length (mechanical rhythm). The writing anti-patterns reference covers additional burstiness guidelines.

<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::basics@core/reference/anti_patterns.md" />

### Sentence Types

**Simple** (one independent clause):
> "The agent reads the file."

**Compound** (two independent clauses):
> "The agent reads the file, and the main agent orchestrates the response."

**Complex** (independent + dependent clause):
> "Although the agent reads the file, it does not modify content."

Mix all types. Emphasize simple and compound for clarity.

### Varied Openings

Mix opening patterns:
- **Transitional**: "In this workflow, agents coordinate..."
- **Adverbial**: "Because context is limited, agents summarize..."
- **Prepositional**: "Despite these constraints, performance remains..."
- **Subject-first**: "The algorithm processes input data..."

## Word Choice

### Technical Terms

Use when: audience consists of specialists, terms are standard in the domain, precision requires specialized vocabulary, and terms are defined on first use. Avoid when: simpler language conveys meaning equally, or terms signal group membership rather than precision.

Define terms on first use: "We employ sub-agents—specialized processes that execute focused objectives—to distribute work efficiently."

### Hedging

Use for uncertain claims: approximators ("approximately," "roughly") and shields ("may," "might," "suggests," "tends to"). Target ~1 hedging term per 50 words for uncertain claims. Avoid hedging certain claims.

## Paragraph Structure

Standard length: 3-6 sentences (100-200 words). Minimum 3 (develops idea), maximum 8 (risks rambling).

Components: topic sentence (main idea, relates to section purpose), supporting sentences (evidence, explanation, elaboration), optional concluding sentence (reinforces or transitions). Each paragraph focuses on a single main idea. New idea = new paragraph.

## Transitions

| Relationship | Transitions |
|--------------|-------------|
| Addition | additionally, also, beyond that |
| Contrast | however, in contrast, nevertheless |
| Causation | therefore, consequently, thus |
| Evidence | for example, specifically |
| Conclusion | in summary, overall |

Never repeat the same transition consecutively. Within paragraphs, move from old information to new, use pronouns to connect sentences, and create logical flow without explicit markers.

## Titles and Headings

Headings must be specific (indicates scope), informative (sets expectations), concise (efficient), and parallel (consistent formatting within documents).

Guidelines: main headings 4-8 words, subheadings 3-6 words, avoid vague terms ("General," "Various," "Miscellaneous"), maximum three heading levels.

See also `[@writing_context_sources_ctxmod_source_example_example, writing principles]`.
