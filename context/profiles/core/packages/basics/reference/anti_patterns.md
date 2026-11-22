# Writing Anti-Patterns

Patterns that signal AI-generated text and reduce documentation quality. Eliminate systematically.

In agent-facing documentation these patterns are noise the agent pays for on every load; the revision checklist at the end is the standing pass.

## Negation-for-Drama

The most persistent AI tell: creating false depth through "It's not X, it's Y" constructions.

| Avoid | Use Instead |
|-------|-------------|
| "It's not about compliance. It's about trust." | "Trust requires genuine compliance." |
| "This isn't a technical problem." | "This is a leadership problem requiring technical solutions." |
| "It's not just efficiency—it's empowerment." | "The system increases both efficiency and user autonomy." |

**Search-and-replace protocol**: After drafting, search for "not just", "not merely", "is not", "it's not". Replace with direct affirmative statements.

## Steering-Level Negation

The prose tell above is stylistic. A second negation failure is behavioral: steering an agent by prohibition. A line like "Never edit generated files" drags the banned action into the agent's attention and makes it more available, so the ban half-reads as an invitation. State the target behavior instead ("treat everything under `generated/` as build output; regenerate rather than edit"), and reserve a bare prohibition for hard guardrails, paired with the positive target. The agent-facing writing doctrine carries the full treatment of this failure mode beside the other steering levers.

<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/agent_facing_writing.md" />

## Formulaic Expressions

### Corporate Jargon

| Avoid | Use Instead |
|-------|-------------|
| "Leverage" | use, apply, employ |
| "Streamline" | simplify, optimize |
| "Synergy" | cooperation, interaction |
| "Game-changer" | significant advancement |
| "Paradigm shift" | fundamental change |
| "Revolutionize" | substantially improve |

### Academic Formalism Markers

**Epistemic verbs to minimize**:
- "delve" → examine, investigate, study
- "underscore" → emphasize, show
- "illuminate" → clarify, explain
- "facilitate" → enable, help
- "bolster" → strengthen, support

**Evaluative adjectives to use sparingly**:
- "crucial" → important, key (or be specific)
- "paramount" → primary, main
- "invaluable" → useful, essential
- "transformative" → changes, alters

**Metaphorical nouns that signal AI**:
- "tapestry" → network, combination
- "landscape" → field, domain
- "symphony" → integration
- "realm" → area, field

## Filler Phrases

Eliminate entirely:
- "In the ever-evolving landscape of X..."
- "It is crucial to recognize that..."
- "What sets X apart is..."
- "At its core, X represents..."
- "When it comes to Y, it's important to consider Z..."

Replace with direct statements:
- "In the ever-evolving landscape of agent orchestration..." → "Agent orchestration..."
- "It is crucial to recognize that..." → [Delete and state point directly]
- "At its core, the problem represents..." → "The problem is..."

## Structural Predictability

### Middle School Essay Architecture

Signs of AI structure:
- Lockstep three-part structures (intro, 3-4 identical body paragraphs, conclusion)
- Predictable topic sentence placement (always first sentence)
- Uniform paragraph lengths lacking organic variability

All writing should have:
- Variable paragraph lengths (2-8 sentences)
- Topic sentences at beginning, end, or implied
- Structure reflects content complexity

### Sentence-Level Templates

**High-risk patterns**:
1. Participial phrase formula: "The system analyzes data, revealing insights" → "The system analysis reveals insights."
2. Correlative conjunction overuse: "Not just X but Y" → Use direct statements
3. Semicolon overconnection: Joining simple clauses → Use natural conjunctions or separate sentences

## Transition Dependency

AI overuses formal connectors. Vary transitions naturally:

| AI Preference | Alternatives |
|---------------|--------------|
| Furthermore | Additionally, Also, Plus |
| Moreover | What's more, Beyond that |
| Therefore | So, Consequently, Thus |
| Nonetheless | Still, However, Even so |

**Rule**: Do not use the same transition word more than once per section.

## Low Burstiness

AI text shows unnatural uniformity.

### Sentence Length

**AI pattern**: Most sentences 15-25 words
**Target pattern**: 70% medium (15-25), 20% short (8-14), 10% long (26-35)

### Lexical Diversity

AI repeats favorite words ("demonstrate," "highlight," "underscore"). Use varied vocabulary contextually.

### Emotional Calibration

- *AI*: "This represents a transformative breakthrough."
- *Human*: "The approach shows promise, though testing remains necessary."

Match claims to evidence strength. Express measured assessment.

## Revision Checklist

After drafting, verify:

**Negation patterns**:
- [ ] No "not just X, but Y" constructions
- [ ] No "it's not X, it's Y" formulations
- [ ] Concepts defined by what they are, not what they're not

**Formulaic expressions**:
- [ ] No leverage, streamline, synergy, game-changer, paradigm shift
- [ ] No delve, underscore, illuminate, facilitate, bolster
- [ ] No crucial, paramount, invaluable, transformative (or used sparingly)
- [ ] No tapestry, landscape, symphony, realm

**Filler phrases**:
- [ ] No "In the ever-evolving landscape of..."
- [ ] No "It is crucial to recognize that..."
- [ ] No "What sets X apart is..."
- [ ] No "At its core, X represents..."

**Sentence variety**:
- [ ] Mix of short, medium, and long sentences
- [ ] Varied sentence openings
- [ ] Mix of simple, compound, and complex structures

**Claims**:
- [ ] Proportional to evidence
- [ ] No overstatement
- [ ] Measured, specific language
- [ ] No invented values — unknowns are marked as unknown, never filled in

See also `[@writing_context_sources_ctxmod_source_example_example, writing principles]`.
