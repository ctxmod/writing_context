# Evidence by Example

Every claim about a produced artifact carries an implicit question: how
do you know? Answer it with real generated output when a real instance
exists, and with a marked sketch when it does not. Both are honest — the
difference is that the reader can always tell which one they are looking
at.

## The Principle

> Cite real generated output as evidence for claims about artifacts. When a real file demonstrates the shape being taught or claimed, cite it by path and date; when only a fabricated example exists, mark it in its first line as an illustrative sketch. An unmarked sketch presented as a real artifact is an honesty failure, not a style choice.

A repository's output is its own demonstration corpus. Reports,
validation records, rendered twins, and completed work items accumulate
as work happens, so a claim about what one of them looks like is usually
one path away from a real instance.

Sketches remain legitimate — some shapes have no real instance yet — but
a sketch speaks for itself only when it says so on its first line. This
generalizes a habit one doctrine file already kept: the rule-authoring
reference marks its own worked example with a sketch disclaimer, and that
convention now holds for every artifact claim the doctrine makes.

## What Counts

| Example | When it applies | Handling |
|---|---|---|
| Real artifact | A generated file demonstrating the shape exists | Cite it by path and date; quote at most the lines that carry the point |
| Sketch | No real instance exists; the shape is taught anyway | Mark the first line "Illustrative sketch"; never present it as found output |
| Borrowed example | The demonstration lives in another project or corpus | Attribute the source; never copy its prose into core doctrine files |

The three kinds are not ranked by quality. A marked sketch of a shape
that does not yet exist anywhere is more honest than a strained citation
of a file that only resembles the claim. What is never acceptable is
ambiguity about which kind the reader is looking at.

## Worked Mini-Examples

Each example below is a shape description, not a citation — a core file
cannot depend on paths that consumer repositories cannot see. The real
citation, where one exists, belongs to the file doing the teaching.

**A report citing a prior report.** When a recurring failure shape shows
up again, the finding cites the earlier report's section — path and date
— as evidence that the shape recurs, instead of restaging it:

> Illustrative sketch
> Same failure shape as {reports-base}/{prior-date}/{time}-04-validation.md,
> section "Findings" — third recurrence this program.

**A doctrine file citing a real rule and its rendered twin.** A reference
teaching a rendering behavior cites a real rule file and its rendered
twin rather than inventing a synthetic pair. The pair already exists on
disk, and the citation doubles as a live demonstration of the transform
it describes.

**A work item citing a completed exemplar.** A story that must show what
a conforming report looks like cites an actual completed story's report
— path and date — instead of fabricating a plausible-looking sample. The
exemplar is also maintenance-free: it stays accurate as formats evolve
precisely because it is real.

**A test-tool reference citing a real passing run.** A test-tool guide
points at one real passing run's output — captured path and run date —
before describing the general shape, so readers compare every claim
against evidence that was actually produced.

## Limits

- Cite, never paste. A citation is a pointer; pasting an artifact's body
  into doctrine duplicates content that then drifts away from its source
  and doubles the maintenance surface.
- Work-tree paths are ephemeral and gitignored. Cite them with dates,
  expect rot, and prefer archived paths where they exist.
- Core doctrine files address every consuming repository, so they never
  cite this repository's work tree or any external clone. State the
  pattern self-containedly; when a real citation would be repo-local by
  nature, keep the file abstract rather than leak a path no consumer can
  resolve.

## Related

- Where judgment stays semantic and mechanisms enforce the mechanical — `semantic_vs_invariant` (module `agent_workflows`, profile `orchestration`, package `delegation`)
- Point at sources instead of copying them; a citation is the reference principle applied to evidence — <ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/reference_over_duplication.md" />
- The token economics that make citing cheaper than pasting — <ctxmod_path path="ctx:github.com/ctxmod/writing_context/context::shared::density@core/reference/context_efficiency.md" />
