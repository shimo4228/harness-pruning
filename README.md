# harness-pruning

**A dated record of what came *out* of one personal Claude Code harness — every retirement of
a skill, rule, agent, or hook that has a decision record behind it, with the reason and the
evidence for each.** Removals made without an ADR are outside it, so the count is a floor. For
anyone building an agent harness who has read plenty about what to add and little about what to
take back out.

This is a record, not an argument. Nothing here is a recommendation or a benchmark. It is one
harness's removals, each one traceable to the decision record that authorized it, published so
that someone else can look at how a harness actually shrinks — including where it did not.

By **Tatsuya Shimomoto (shimo4228)** — <https://github.com/shimo4228>.
The harness itself is at <https://github.com/shimo4228/claude-harness>; every ADR cited here
is published there.

---

## What is in here

| file | what it holds |
|---|---|
| [`LEDGER.md`](LEDGER.md) | 27 retirement events as of 2026-09-08, one row each: date, component, what was removed or shrunk, why, the model generation it became unnecessary at (where the source names one), and the ADR that authorized it. Plus a net-change section. |
| [`HOWTO.md`](HOWTO.md) | How removals get decided in this harness. Summarized from three documents that already exist in the harness, with source paths. Nothing invented here. |

## The uncomfortable part

Over the harness's whole history, as of 2026-09-08, 68 skill files were deleted — and 127 were
created. The agent and rule layers have the same shape at a lower ratio: about 1.5 additions per
removal, against 1.9 for skills. **The harness did not get smaller. It turned over.** The ledger
says so in its own net-change section rather than burying it, because
a pruning record that reports removals without reporting additions is measuring one side of a
ledger and calling it a trend.

What the removals do have is a direction: components leave when the substrate absorbs them. A
reviewer agent retires when the built-in reviewer covers the same ground. A stored file-level
structure map retires when an LSP tool can derive it on demand. A rule written to compensate
for a weaker model's judgment retires when the compensation turns into a conflict cost.

## Why publish it

The case for treating the harness — not the model — as the thing being engineered has been
made publicly, and well:

- Anthropic, *Harness design for long-running apps* (2026-03-24) —
  <https://www.anthropic.com/engineering/harness-design-long-running-apps>
- Addy Osmani, *Agent harness engineering* (2026-04-19) —
  <https://addyosmani.com/blog/agent-harness-engineering/>
- Philipp Schmid, *The agent harness in 2026* (2026-01-05) —
  <https://www.philschmid.de/agent-harness-2026>

Those are arguments. This repository is one public instance held up against them: a single
harness, its removals dated and sourced, over about six and a half months. It does not establish
that the arguments generalize, and it is not a survey — I have not checked what else exists in
this shape.

## How to read a row

Each ledger row cites a file under `~/.claude/docs/adr/`, published in `claude-harness`. Open
that ADR before trusting the row. Two columns deserve suspicion in particular:

- **why** — compressed to one sentence from an ADR that usually runs several pages. The
  compression is mine and the ADR is the source of truth.
- **model generation** — filled in when the ADR itself names a generation, and left as
  "not model-attributed" when it credits the substrate (a built-in, a tool, an official
  default) instead. It is never inferred. Six of the 27 rows name a generation; five more
  credit a generation change without naming one; the remaining sixteen credit the substrate.
  That split is itself a finding: most of these components were not made obsolete by a
  smarter model, they were made obsolete by the product growing a feature.

## Limits

- One harness, one author, one tool. No comparison group.
- The ledger covers what has an ADR. Small removals made without a decision record are absent,
  so the retirement count is a floor, not a total.
- Shrink-in-place events (`skill-creator` going from 5,886 lines to 96) change no file count, so
  the net-change table understates the reductions the ledger's own rows describe.

## License

MIT. See [`LICENSE`](LICENSE).
