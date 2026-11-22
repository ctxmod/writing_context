# Information Density

Density measures meaningful information per token in an artifact. Match density to usage frequency and audience expertise. Mismatched density either wastes cognitive resources or leaves critical information gaps.

## Core Principle

Information density is signal-to-noise ratio applied to artifact content. High density means each token carries meaning; low density means filler, redundancy, or irrelevant content dilutes useful information. Every low-value token displaces a high-value one, whether the consumer is human (limited working memory) or machine (fixed token limits constraining reasoning depth).

The central trade-off: high density enables efficient processing for experts with domain chunking structures, but overwhelms consumers who lack them. An expert reads a configuration schema as three logical groups; a novice reads thirty isolated fields. Same content, different perceived density.

Optimization requires knowing how often the artifact loads and who processes it. Frequent consumption by diverse audiences demands sparsity. Rare deep consultation by specialists permits comprehensiveness.

## Cognitive Foundations

Cowan (2001) revised Miller's estimate: humans process roughly four chunks simultaneously, not seven. Experts transcend this limit through chunking—organizing elements into larger perceptual units. A specialist perceives dense content as organized patterns; a newcomer perceives unconnected details.

Cognitive Load Theory (Sweller) distinguishes intrinsic load (content complexity), extraneous load (presentation problems), and germane load (building understanding). Redundancy, verbosity, and scattered information increase extraneous load without improving comprehension. Density optimization minimizes extraneous load, freeing capacity for content processing.

Structure enables density. Well-organized dense content outperforms disorganized sparse content because predictable structure becomes chunkable with repeated exposure.

## Density Dimensions

Three dimensions interact. When they conflict, prioritize in this order:

**Loading frequency** (first priority). Token cost multiplies across operations. Automatically loaded artifacts must be sparse; infrequently accessed artifacts can be dense. Context efficiency covers this relationship in detail.

<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/context_efficiency.md" />

**Audience expertise** (second priority). Broad audiences require sparse content with scaffolding. Specialists possess chunking structures that make density efficient. For mixed audiences, progressive disclosure separates sparse overviews from dense details.

**Artifact purpose** (adjusts within bounds set by above). Quick decision support benefits from scannable content. Reproducibility and traceability demand comprehensive coverage. Learning artifacts progress from sparse to dense incrementally.

## Application Guidance

| Favor Density | Favor Sparsity |
|---------------|----------------|
| Infrequent loading for deep understanding | Automatic or frequent loading |
| Expert consumers with chunking structures | Varying expertise levels |
| Completeness and traceability primary | Quick decision-making primary |
| Token cost amortizes over rare access | Token cost multiplies across operations |

**Adjustment strategies**: progressive disclosure (sparse summary followed by dense details), layered structure (overview for scanning, depth for reference), external references (link to dense content rather than inlining), and consistent organization (predictable structure becomes chunkable with exposure).

Avoid uniform density across artifacts. Same density applied to auto-loaded configuration and deep reference wastes resources in both directions.

## Indicators

| Appropriate | Problematic |
|-------------|-------------|
| Consumers find information without excessive searching | Consumers ask questions already answered in the artifact |
| Questions answered within the artifact | Sparse reference forces cross-referencing for basic understanding |
| Experts find comprehensive coverage | Dense auto-loaded content consumes budget on every operation |
| Newcomers locate overview sections first | Inconsistent density within similar types breaks expectations |

Three metrics: signal-to-noise ratio (relevant tokens / total tokens), redundancy (zero is optimal, per SSOT), and completeness (all necessary information present for the artifact's purpose).

## Anti-Patterns

| Anti-Pattern | Effect |
|--------------|--------|
| **Information dumping** | All data presented without importance signaling; critical indistinguishable from peripheral |
| **Redundancy loops** | Content restated across sections; violates SSOT, creates maintenance burden |
| **Abrupt density shifts** | Inconsistent density forces recalibration; cognitive resources spent on presentation |
| **Filler accumulation** | Tokens added without information; each filler phrase displaces meaningful content |
| **Audience mismatch** | Expert density for general audiences (incomprehension) or scaffolding for specialists (redundant explanation) |

## Related

Density implements context efficiency at the artifact level. SSOT eliminates redundancy (a primary source of low density). Reference-over-duplication reduces token consumption by pointing to sources.

<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/context_efficiency.md" />
`ssot` (module `engineering`, profile `principles`, package `design`)
<ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/reference_over_duplication.md" />
