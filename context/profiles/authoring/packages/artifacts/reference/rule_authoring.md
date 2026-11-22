# Rule Authoring

How to write a rule that costs little and points well, and where the content it points at belongs.

## The Pointer Principle

Rules are pointers. Reference files are content.

A rule exists for one purpose: to make an agent aware that guidance on a subject exists, and to link to where that guidance lives. It states the constraint in a sentence or two and then gets out of the way. The reference file it links to carries the detail — the tables, the worked examples, the edge cases, the rationale — and is read only when the agent judges it relevant to the task at hand.

The asymmetry is economic. A rule is loaded into context speculatively, before anyone knows whether it matters: an unbounded rule pays its full token cost in every session of every repository that consumes the profile, whether or not the session ever touches the subject. A reference file pays its cost only in the sessions that read it. Moving a hundred lines of detail out of a rule and into a reference file does not delete the content — it converts a fixed, universal cost into a variable, earned one.

This is why a rule that has grown into a small manual is a bug even when every line of it is correct. Correctness is not the constraint; unconditional cost is.

The pointer principle in brief, with the referencing principle behind it (point at canonical sources instead of copying them), is the `point_cite_never_paste` rule of this module's `core` profile; the load budget it serves is the `budget_by_load` rule beside it.

## The Four-Tier Body-Line Budget

The budget is keyed to the rule's `paths:` frontmatter property, because `paths:` is the only signal available about how likely the rule is to be relevant when it loads. The tighter the scope, the more often the rule is loaded into a session where it genuinely applies, and the more body it has earned.

In ctxmod, each `paths:` element is a full workspace-relative pattern where `*` and `?` match within one segment, so a pattern matches only paths with its own segment count. A "whole file type" scope is therefore written as one pattern per depth it must reach.

| Tier | Scope shape | Frontmatter `paths` | Body-line ceiling |
|---|---|---|---|
| Unbounded | no path scoping — loads every session | absent | 1–10 |
| Slightly bounded | whole file type or a broad directory (`*.go`, `*/*.go`, `*/*/*.go` …; `docs/*`, `docs/*/*` …) | broad patterns | 10–25 |
| Bounded | specific file patterns (`pkg/go/llmsrv/*.go`, `pkg/go/llmsrv/*/*.go`) | narrow patterns | 25–50 |
| Very bounded | a single package or narrow unambiguous file set where the content is ALWAYS relevant to those files | single narrow pattern or package path | 50–200 |

There is no tier property, and none is being added. The tier is read off the `paths:` property; a declared tier would let a rule claim a budget its scope has not earned.

**Body lines** means every line of the file after the closing `---` of the frontmatter (or every line, for a rule without frontmatter), blank lines included. Blank lines count because they are real tokens in the loaded context, and because excluding them invites padding.

### Even Tier 4 rules link out

A 200-line ceiling is a ceiling, not a target, and it is not a licence to inline a reference file. A very bounded rule earns room to state its constraint precisely, enumerate the non-obvious cases, and give a short example — not room to become the reference file. If the content would stand on its own as a document someone reads deliberately, it is a reference file, and the rule links to it.

### Why scoped rules are not exempt

A path pattern is a weak relevance signal, not a relevance guarantee. The matcher compares patterns against files; it cannot infer from "the agent read a `.go` file" that any particular Go rule bears on the task. A rule scoped to every `.go` file loads for a session that opens one Go file to rename a variable exactly as it loads for a session rewriting the package's concurrency model.

Scoped rules therefore also load speculatively. What a tighter scope buys is a better hit rate — a larger fraction of the sessions that load the rule are sessions the rule helps. That earns a larger budget. It does not earn exemption from the budget.

### Trap: the trailing catch-all widens the scope

A rule that lists several narrow patterns and then a catch-all has the effective scope of the catch-all. For example:

```yaml
paths:
  - "app/jobs/*.py"
  - "app/tasks/*.py"
  - "*.py"
  - "*/*.py"
  - "*/*/*.py"
```

The first two entries are decorative. Any Python file at depths one to three matches the last three, so the rule loads for nearly every Python file and belongs to Tier 2, not Tier 3 — regardless of how specific the narrow entries look.

When such a rule is over its Tier 2 budget, **dropping the catch-all is usually the better remedy than cutting content.** If the narrow patterns genuinely describe where the rule applies, removing the catch-all both fixes the scope and moves the rule to a tier whose budget it already fits. Cut content only when the catch-all is load-bearing.

## Link Mechanics: Inlining Versus Naming

A rule's link form decides whether the target is *inlined* or merely *named*. That decision, not the rule's line count, dominates the rule's real context cost — an 8-line rule can unconditionally inline 700 lines.

| Component | Effect |
|---|---|
| `<ctxmod_inline path="…" />` | The target's content is pulled into the rendered context wherever the component stands — whenever the rule loads. |
| `<ctxmod_path path="…" />`, `<ctxmod_link path="…" />` | The target is named. The agent reads the file only if it judges it relevant. |

**Reference pointers in rules use a naming component.** Inlining a large reference file from a rule re-inflates exactly the cost the pointer discipline exists to remove: the reference file's content arrives in every session the rule loads, which is the same unconditional tax as writing the content into the rule body — only harder to see, because the rule's own line count stays small.

Three audit lessons hold for any link syntax:

- **Know the default.** Where a link form has a mode that defaults to inlining when no keyword is given, a bare link is not neutral; audit by enumerating every link opener and subtracting the explicitly non-inlining ones, never by searching for the inlining keyword alone, which reports a clean tree while bare forms inline heavily.
- **Inlining can be transitive.** A form that inlines its target together with the target's own inlined links pulls in the whole closure; one such link in a rule has been measured pulling more than 1,700 lines across 17 files. Prefer the naming form for anything with links of its own.
- **Position can drop a link silently.** Put the description first and the link last in a list item (`- the field reference — <link>`): a link that opens a list item is the form most likely to be mis-parsed, and a dropped target leaves an orphaned bullet whose description survives while the content it names becomes unreachable.

### Verify on the rendered output

Neither the rule's line count nor its source is sufficient evidence of its cost. Render the selection the rule belongs to and inspect the rendered rule: every inlined block is content that loads whenever the rule loads. A rule is only clean when its rendered form names its references instead of carrying them.

Links resolve against the selected view, not against the file system. A link into a profile or module that the consuming selection does not include does not resolve; `ctxmod vet` reports it (CTX-REF007). Link only into the rule's own profile, the profiles it extends, or required modules that the selection activates; otherwise name the target in prose.

## Reference Taxonomy

Within any `reference/` domain, content files sort into four shapes:

| Shape | Holds |
|---|---|
| a tool's package or files | Documentation for a project-authored tool — anything in a repository's own tools tree. |
| an application's package or files | Documentation for an application. |
| contracts | Contract documentation: schemas, wire formats, API surfaces, interface agreements. |
| a topic | Everything else — principles, procedures, domain topics. |

### Shared vs local

The same tool can have documentation in two places, and the split is by audience:

| Location | Holds |
|---|---|
| the shared module's package for the tool (the `context/` tree other repositories consume) | The portable surface — what another repository consuming the module needs to know to use the tool: its commands, its contracts, its invariants. |
| the repository's own development context (`context.internal/`) | Repo-local implementation detail — internals, local wiring, this-repo-only operational notes. |

A file that mixes the two is split into two files, one in each location. It is not filed wholesale under whichever location holds more of it: a portable file with local detail inside it exports noise to every consuming repository, and a local file holding the portable surface hides it from them entirely.

## Worked Example

*Illustrative sketch, not a real file.* When a real generated file demonstrates the same shape, cite it instead of sketching (see `evidence_by_example.md` in this module's `core` profile).

**Before** — one rule, unbounded, ~340 body lines:

```md
# Config Schema

... 40 lines on file layout ...
... a 90-row table of every field in settings.toml, with types and defaults ...
... 60 lines on validation semantics and strict-mode decoding ...
... 80 lines of worked TOML examples per section ...
... 70 lines on migration from the legacy format ...
```

Every session in every consuming repository pays for all 340 lines. The overwhelming majority of them never touch a config file.

**After** — a ≤10-line pointer plus three named reference files in the tool's package:

```md
# Config Schema

`settings.toml` is strict-mode decoded — an unknown or misspelled key is a hard error, not a silent drop.

- the full field reference — <ctxmod_path path="projconf/reference/schema.md" />
- strict-mode decoding and error reporting — <ctxmod_path path="projconf/reference/validation.md" />
- moving off the legacy format — <ctxmod_path path="projconf/reference/migration.md" />
```

Nothing was deleted. The one fact an agent needs to *know without looking* — that a typo fails loudly — stays in the rule. The 330 lines an agent needs only when actually editing config move behind three named doors, each opened on demand.

## Compliance Is by Convention

This budget is authored policy. There is no mechanical checker: `ctxmod vet` counts no rule body lines and asserts nothing about tier or ceiling. A rule that runs 80 lines over its tier vets cleanly and loads in every session.

Enforcement is therefore review and authorship discipline. Count the body lines when you write or edit a rule, read the tier off its `paths:` property, and cut or relocate content when the two disagree.

## Related Directives

How to read an operator's directive about rules (exhaustiveness, audit-to-remediation, and total-removal defaults) and link counting as a census over a tree are orchestration guidance, kept with the directive-interpretation principle outside this module.
