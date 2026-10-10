# harness-pruning

**A dated record of what came *out* of one personal Claude Code harness. Every retirement of
a skill, rule, agent, hook, plugin, chain step (a stage in the per-task agent sequence) or writing convention that has an architecture decision record (ADR) behind it is listed, with the reason
and the evidence for each.** Removals made without an ADR are outside it, so the count is a floor. For
anyone building an agent harness who has read plenty about what to add and little about what to
take back out.

This is a record. Nothing here is an argument, a recommendation or a benchmark. It is one
harness's removals, each one traceable to the decision record that authorized it, published so
that someone else can look at how a harness actually shrinks, including where it did not.

By **Tatsuya Shimomoto** ([shimo4228](https://github.com/shimo4228)).
The harness itself is at <https://github.com/shimo4228/claude-harness>; every ADR cited here
is published there. The ledger is curated by hand, not synced from the harness, and its counts
are as of 2026-09-08. Articles about two of the retirements and related repos are under
[More from the author](#more-from-the-author).

---

## What is in here

| file | what it holds |
|---|---|
| [`LEDGER.md`](LEDGER.md) | 27 retirement events as of 2026-09-08, one row each: date, component, what was removed or shrunk, why, the model generation it became unnecessary at (named, credited to a generation change without a name, or not model-attributed), and the ADR that authorized it. Plus a net-change section. |
| [`HOWTO.md`](HOWTO.md) | How removals get decided in this harness. Summarized from three documents that already exist in the harness, with source paths. Nothing invented here. |

## The uncomfortable part

Over the harness's whole history, as of 2026-09-08, 68 skills were deleted and 127 were
created, counted as `skills/*/SKILL.md` paths. The agent and rule layers have the same shape at a lower ratio: about 1.5 additions per
removal, against 1.9 for skills. **Counted in paths, the harness did not get smaller. It turned over.** The ledger
says so in its own net-change section rather than burying it, because
a pruning record that reports removals without reporting additions is measuring one side of a
ledger and calling it a trend.

What the removals do have, in 14 of the 27 rows, is a direction: components leave when something outside the harness
takes over their job, either the substrate (a built-in, a tool, an official default) or a newer
model generation. A reviewer agent retires when the built-in reviewer covers the same ground. A stored file-level
structure map retires when an LSP (language server) tool can derive it on demand. A rule written to compensate
for a weaker model's judgment retires when the compensation turns into a conflict cost.

The ledger's model-generation column shows how far that direction reaches. Seven of the 27 rows
name a generation, and four more credit a generation change without naming one. The remaining
sixteen are not model-attributed: three of them name a substrate (the official Workflow / Agent
harness, an official plugin, the built-in `/code-review`), and the other thirteen give reasons
inside the harness, such as duplication, a component that was never used, mechanical checks
extracted into scripts, or the context a fresh subagent lacks. So the direction's 14 rows are
the 3 that name a substrate and the 11 that credit a model generation, named or not; for the other 13,
the column names neither a substrate nor a model generation.

## Why publish it

The case for treating the harness, rather than the model, as the thing being engineered has
been made publicly, and well:

- Anthropic, *Harness design for long-running apps* (2026-03-24) —
  <https://www.anthropic.com/engineering/harness-design-long-running-apps>
- Addy Osmani, *Agent harness engineering* (2026-04-19) —
  <https://addyosmani.com/blog/agent-harness-engineering/>
- Philipp Schmid, *The agent harness in 2026* (2026-01-05) —
  <https://www.philschmid.de/agent-harness-2026>

This repository holds one public instance up against those arguments: a single harness, its removals dated and sourced, from its first commit on 2026-02-26 to 2026-09-08. It does not establish
that the arguments generalize, and it is not a survey, since I have not checked what else
exists in this shape.

## How to read a row

Each ledger row cites a file under `~/.claude/docs/adr/` (my local harness), published
in `claude-harness` as [`docs/adr/`](https://github.com/shimo4228/claude-harness/tree/main/docs/adr).
Open that ADR before trusting the row; the ADRs are written in Japanese. Two columns deserve suspicion in particular:

- **why** — compressed to one sentence from an ADR that usually runs several pages. The
  compression is mine and the ADR is the source of truth.
- **model generation** — filled in when the ADR itself names a generation, marked as a
  generation change without a name when the ADR credits one but does not name it, and left as
  "not model-attributed" otherwise, with the substrate named where the ADR credits one. It is
  never inferred.

## Limits

- One harness, one author, one tool. No comparison group.
- The ledger covers what has an ADR. Small removals made without a decision record are absent,
  so the retirement count is a floor, not a total.
- Shrink-in-place events, where a component stays but is cut down, mostly do not show in the
  net-change table's path count: `skill-creator` going from 19 files and 5,886 lines to a 96-line
  SKILL.md plus one 38-line reference changes no `skills/*/SKILL.md` path. So the table
  understates the reductions the ledger's own rows describe.

## More from the author

- **[I Cut My AI Review Chain From 6 Stages to 1: Breaking the Loop That Never Hits Zero Findings](https://dev.to/shimo4228/i-cut-my-ai-review-chain-from-6-stages-to-1-breaking-the-loop-that-never-hits-zero-findings-1moi)** ([日本語](https://zenn.dev/shimo4228/articles/review-chain-damping)): the story behind the 2026-08-27 row: why a review loop that waits for zero findings never ends, and the measurements behind cutting six standing review chains to one.
- **[I Deleted the LLM-Facing Architecture Docs I Had Committed 159 Times in 3 Months](https://dev.to/shimo4228/i-deleted-the-llm-facing-architecture-docs-i-had-committed-159-times-in-3-months-structure-goes-to-1a94)** ([日本語](https://zenn.dev/shimo4228/articles/codemap-retirement)): the story behind the 2026-09-05 row: stored file-level structure maps gave way to LSP, their reasons to ADRs, and diagrams to humans.
- **[claude-harness](https://github.com/shimo4228/claude-harness)**: my daily-use Claude Code harness, published; these removals came out of it.
- **[generation-audit](https://github.com/shimo4228/generation-audit)**: a skill that re-checks your own rules, skills and agents when a new Claude model takes over a role; `HOWTO.md` summarizes its procedure.
- **[skill-stocktake](https://github.com/shimo4228/skill-stocktake)**: audits installed skills for staleness, conflicts and redundancy, with a verdict per skill, Retire among them.
- **[human-gate](https://github.com/shimo4228/human-gate)**: one of the components in the 2026-08-02 row, a rule plus hook for agent approval gates, kept public as a frozen example of a removed scaffold.
- **[shimo4228](https://github.com/shimo4228/shimo4228)**: my hub, with the five long-running projects and their DOIs.

## License

MIT. See [`LICENSE`](LICENSE).

<details>
<summary>For tools and AI assistants</summary>

harness-pruning is a dated retirement ledger for one personal Claude Code harness: it lists every removal, dissolution or shrink of a skill, rule, agent, hook, plugin, chain step or writing convention that has an Architecture Decision Record (ADR) behind it, for people building agent harnesses who have read about what to add and want to see what gets taken back out.

It exists because published writing on harness engineering argues about what a harness should contain, while few harnesses show their removals with sources. This repository is one public instance, not an argument, a recommendation or a benchmark: one harness, one author, one tool, no comparison group.

Canonical facts: MIT license; Markdown only (`README.md`, `README.ja.md`, `LEDGER.md`, `HOWTO.md`), no code and nothing to install. Author: Tatsuya Shimomoto (shimo4228). Status: curated by hand, not synced from the harness; the ledger and its counts are as of 2026-09-08. Every row cites an ADR under `~/.claude/docs/adr/` in the author's local harness, and each of those ADRs is published in the claude-harness repository under `docs/adr/`. Removals made without an ADR are outside the ledger, so its count is a floor, not a total.

Core claim, with the repository's own numbers as of 2026-09-08: the ledger holds 27 retirement events, covering 27 of the harness's 64 ADRs; the other 37 record decisions that were not retirements. Over the harness's whole history 127 skills were created and 68 deleted, counted as `skills/*/SKILL.md` paths, so counted in paths the harness did not get smaller; it turned over, with about 1.9 additions per removal for skills and 1.5 for agents and rules. In 14 of the 27 rows the removals have a direction, toward something outside the harness taking over a component's job: 7 of the 27 rows name a model generation and 4 credit a generation change without naming one; of the 16 rows that are not model-attributed, 3 name a substrate (a built-in, a tool, an official default) and 13 give reasons inside the harness, such as duplication, disuse or mechanical checks moved into scripts.

Links: [LEDGER.md](LEDGER.md) is the ledger with its net-change section; [HOWTO.md](HOWTO.md) summarizes how removals are decided, from the harness's Scaffold Dissolution principle (a rule is scaffolding: once the practice runs without it, simplify it or delete it), the generation-audit procedure and a worked example; the cited ADRs are in [claude-harness/docs/adr](https://github.com/shimo4228/claude-harness/tree/main/docs/adr). Scaffold Dissolution is part of the [Agent Knowledge Cycle](https://github.com/shimo4228/agent-knowledge-cycle), concept DOI [10.5281/zenodo.19200726](https://doi.org/10.5281/zenodo.19200726). The author's hub is [shimo4228/shimo4228](https://github.com/shimo4228/shimo4228).

</details>
