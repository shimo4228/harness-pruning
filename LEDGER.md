# Retirement ledger

Every removal, dissolution, or shrink in one personal Claude Code harness (canonical tree
`~/.claude`, public copy [claude-harness](https://github.com/shimo4228/claude-harness)) **that
has a decision record behind it**. As of 2026-09-08. Removals made without an ADR are outside
this ledger, so the count is a floor, not a total.

Rules of this ledger:

- One row per retirement event. **No row without evidence** — every row cites an ADR file in
  `~/.claude/docs/adr/` (all of them are published in `claude-harness`).
- The *model generation* column names a generation **only when the ADR itself names one**.
  Where the ADR attributes the removal to the substrate (a built-in feature, a tool, an
  official harness default) rather than to model judgment, the column says so. It is not
  filled in by inference.
- Dates are the ADR's own `## Date`. ADR-0009 has no `Date` section; its commit date is used
  and marked.

| date | component | what was removed or shrunk | why | model generation at which it became unnecessary | evidence |
|---|---|---|---|---|---|
| 2026-03-08 | plugin `claude-mem` | disabled in `settings.json`; plugin files and DB kept | no automatic retrieval, so anything it accumulated was never used | not model-attributed | `~/.claude/docs/adr/0002-disable-claude-mem.md` |
| 2026-03-13 | rule `documentation.md` | moved out of the always-loaded rule set | both of its jobs already had owners — CLAUDE.md upkeep in the `context-sync` skill, external doc standards in the writing skill | not model-attributed | `~/.claude/docs/adr/0004-retire-documentation-rule.md` |
| 2026-03-13 | rule `kimi-delegation.md`, then (2026-04-19) skills `kimi-spec` / `kimi-dispatch`, `bin/` wrappers, one learned note | rule retired first, then every Kimi asset removed and the `bin/` directory deleted | the delegation stopped firing in practice once Claude Code alone was capable enough | Opus 4.7 (1M context) — named in the ADR's 2026-04-19 update | `~/.claude/docs/adr/0005-retire-kimi-delegation-rule.md` |
| 2026-03-29 | ECC plugin (116 skills) | plugin turned off; only hand-picked components imported per project | wholesale import polluted context and left a large tail of components that were never used | not model-attributed | `~/.claude/docs/adr/0008-ecc-local-only-management.md` |
| 2026-05-02 (commit date; ADR has no `Date`) | skills `orchestrate`, `verification-loop`, `python-testing` | deleted; `python-testing`'s 7 Python-specific judgments compressed into a rule | `orchestrate` hardcoded a chain that fought the chain matrix, `verification-loop` fully duplicated `verify`, and ~90% of `python-testing`'s 815 lines was general pytest knowledge the model already has | current generation (not named in the ADR) | `~/.claude/docs/adr/0009-implementation-chain-front-loaded-in-plan.md` |
| 2026-06-10 | skills `code-review`, `security-review`, `verify`, `plan`, `build-fix`, `test-coverage`; rule `performance.md`; the Parallel Task Execution section of `agents.md` | all deleted outright (not archived — `rules/` is loaded recursively, so an archive folder would put retired rules back into context) | four collided with built-ins of the same name, two had become general training knowledge, `performance.md` was written entirely against an "Opus 4.6 + 1M context + MAX Plan" setup, and parallel task execution had moved into the product's own system prompt | premise was Opus 4.6; the ADR does not name the successor generation | `~/.claude/docs/adr/0011-retire-builtin-duplicate-skills-and-version-dependent-rules.md` |
| 2026-06-30 | rule `multi-agent-orchestration.md` | deleted | keeping a local rule that talks about native throughput was itself the source of drift against the official harness | not model-attributed (substrate: official Workflow / Agent harness) | `~/.claude/docs/adr/0014-retire-multi-agent-orchestration-rule.md` |
| 2026-07-19 | rule `authorship-strategy.md` | deleted | the skill of the same name already held the whole content; the rule was a condensed duplicate paying a per-session residency cost | not model-attributed | `~/.claude/docs/adr/0017-retire-authorship-strategy-rule-absorbed-by-skill.md` |
| 2026-07-25 | the resident `rules/` layer as a whole; `rules/python/` (6 files) | 5,789 → 2,314 words, 20 → 14 files; `rules/python/` removed and absorbed into a skill; the Parallel Group notation and the forced summary format retired without a destination | over-constraint written for weaker models turns into a conflict cost for models with better judgment — the reported basis was Anthropic's 2026-07-25 finding that >80% of the Claude Code system prompt could be cut with no measurable eval regression | Claude 5 (Opus 5 / Fable 5) | `~/.claude/docs/adr/0018-rules-rightsize-for-claude5.md` |
| 2026-07-26 | skill `security-scan` | deleted, with 13 live references repointed | five months of zero invocations, stale documentation, a third-party npm supply-chain dependency, and an official plugin that measurably covered the same surface | not model-attributed (substrate: official plugin) | `~/.claude/docs/adr/0020-retire-security-scan-delegate-risk-to-claude-security.md` |
| 2026-07-27 | agent `planner` | dissolved; `architect` narrowed to build-or-not judgment only | planning needs rich context and the human intervention point, neither of which a fresh-context subagent has | not model-attributed (fresh/rich context axis) | `~/.claude/docs/adr/0023-dissolve-planner-narrow-architect-to-essence-evaluation.md` |
| 2026-07-27 | agent `tdd-guide` | dissolved; five references rewritten to point at the main loop | the spec lives in the conversation, so writing tests is main-loop work, not a delegable stage — the agent was an artifact of an older "turn each stage into an agent" design | generation change named as the reason for re-placing the stage, without naming a generation | `~/.claude/docs/adr/0024-dissolve-tdd-guide-and-axis-auxiliary-rationales.md` |
| 2026-07-31 | Signal-first section (with its Output discipline subsection) of rule `akc-cycle.md` | removed from residency; the principle moved into the skills that consume it | the generation now does that confirm-and-filter step by default, so the resident copy was a permanent override-versus-residency friction | Claude 5 | `~/.claude/docs/adr/0026-retire-signal-first-residency.md` |
| 2026-08-02 | hook `review-chain-notice.sh` (Stop branch), 4 advisory scripts, rules `human-gate.md` / `output-register.md` / `patterns.md` / `hooks.md`, and a custom approval gate | hook thinned to a plain "did Review / Verify run?" reminder; Stop branch and 4 advisory scripts retired; 4 rules retired; approval gate deleted | rules were re-scoped to environment-specific facts, wiring, and traps only; commit authority went back to the task request and the substrate | not model-attributed | `~/.claude/docs/adr/0035-commit-review-hook-and-rules-rightsize.md` |
| 2026-08-13 | agent `python-reviewer`, skill `python-review` | retired | lint rules catch the mechanical half, and the remaining semantic half is native to the Claude 5 generation reviewer — an explicit case of downward dissolution | Claude 5 | `~/.claude/docs/adr/0039-retire-python-reviewer-simplify-in-chain.md` |
| 2026-08-15 | chain step `feat` × TDD | demoted from mandatory to conditional (the ordering only, not the tests) | no primary record ever showed the enforced RED→GREEN ordering paid off in this harness; it was inherited from ECC and never measured | current generation (the ADR asks "does this still hold in the current generation" without naming one) | `~/.claude/docs/adr/0040-demote-feat-tdd-to-conditional.md` |
| 2026-08-16 | agent `code-reviewer` | retired; Code Review repointed at the built-in `/code-review`, and Security Review demoted to fire only on threat-surface changes | the built-in covers the same ground, and a permanently-on security review was not tied to anything that actually changed the threat surface | not model-attributed (substrate: built-in `/code-review`) | `~/.claude/docs/adr/0042-retire-code-reviewer-and-scope-security-review-to-threat-surface.md` |
| 2026-08-22 | skill `skill-creator` | 19 files / 5,886 lines → a 96-line SKILL.md plus one 38-line reference; `scripts/`, three sub-agents, `eval-viewer/`, `assets/` deleted | the machinery was old-generation step-by-step scaffolding that did not fire in practice | Fable — named in the ADR as the generation the rewritten SKILL.md is written for (§3), not as the trigger that made the old machinery unnecessary | `~/.claude/docs/adr/0046-skill-creator-shrink-in-place-and-creation-gate.md` |
| 2026-08-23 | `skills/learned/` (11 notes) | directory deleted and the route into it removed from `learn-eval`; saves now go to an existing skill/rule/doc or become a real skill, else Drop | a parking lot that nothing routes back to is not a save destination | not model-attributed | `~/.claude/docs/adr/0047-retire-learned-notes-directory.md` |
| 2026-08-26 | agent `adr-reviewer` | mechanical checks extracted into `adr_lint.py`; the reviewer thinned to semantic checks only | a reviewer spending its judgment on checks a script can decide is paying model cost for a deterministic answer | not model-attributed | `~/.claude/docs/adr/0051-extract-mechanical-adr-checks-into-cross-repo-lint.md` |
| 2026-08-26 | skills `skill-health`, `skill-stocktake` | URL liveness and usage aggregation extracted into evidence scripts | same reason as above, plus the hand-written grep pipeline in the skill body was itself producing wrong verdicts | not model-attributed | `~/.claude/docs/adr/0052-url-liveness-and-usage-aggregation-evidence-scripts.md` |
| 2026-08-26 | skill `context-sync` Phase 4 checklist | extracted into `context_evidence.py`; the checklist thinned to a Step 0 wiring line | same reason | not model-attributed | `~/.claude/docs/adr/0053-extract-context-sync-checklist-into-evidence-script.md` |
| 2026-08-26 | skills `agent-stocktake`, `learn-eval` | mechanical checks extracted into evidence scripts — `agent_evidence.py` for `agent-stocktake`, a new `overlap_candidates.py` for `learn-eval`; self-reported answers replaced by a produced artifact | same reason; self-report is not evidence | not model-attributed | `~/.claude/docs/adr/0054-extract-agent-stocktake-and-learn-eval-mechanical-checks.md` |
| 2026-08-27 | review chain rows: Simplify, Silent-Failure Review, Cross-Model Review, Premise Challenge | deleted from the chain matrix; the standing review reduced to one fresh-context pass plus a conditional security reviewer; per-commit Simplify demoted to batch opt-in | multi-stage review was scaffolding built on the assumption of a weaker build session, and the quality axis is now inside the built-in reviewer | Fable / Opus 5 generation | `~/.claude/docs/adr/0055-review-chain-single-pass-regression.md` |
| 2026-08-28 | writing-harness craft conventions | folded back into a short list of principles; numeric thresholds moved to the reviewer agent, worked examples to `references/` | the enumerated conventions were scaffolding; the principle plus one question per line carries the same instruction | not model-attributed (the ADR lists the next generation as a further-shrink trigger, not this one) | `~/.claude/docs/adr/0058-writing-harness-scaffold-dissolution.md` |
| 2026-09-01 | agent `codemap-writer` chain | freshness gate and header acceptance extracted into `codemap_evidence.py`; the chain thinned to semantic checks | same extraction reason as the 2026-08-26 rows | not model-attributed | `~/.claude/docs/adr/0060-codemap-evidence-script-and-freshness-gate-mechanization.md` |
| 2026-09-05 | skill `update-codemaps` (with the evidence script written four days earlier), agent `codemap-writer`, `context-sync` Phase 0, the `release-doi` regeneration step | all deleted; file-level structure is no longer stored by any skill | the codemap was scaffolding for a generation of reader LLMs that had no symbol index; an LSP tool now derives the same structure on demand, so storing it only created a staleness gate to maintain | generation change named (reader LLMs without a symbol index → LSP era); no model name given | `~/.claude/docs/adr/0062-retire-codemap-machinery.md` |

27 rows. They cover 27 of the 65 ADRs in this harness; the other 38 record decisions that were
not retirements.

## Net change

Counted on 2026-09-08 in `~/.claude`.

**Current size**

| layer | count |
|---|---|
| skills (`skills/*/`) | 60 |
| agents (`agents/*.md`) | 13 |
| rules (`rules/common/*.md`) | 13 |

**Over the whole history of the harness repo** (first commit 2026-02-26 → 2026-09-08), counting
distinct paths added and deleted with rename detection on (`git log -M --diff-filter=A|D`):

| layer | paths added | paths deleted | net |
|---|---|---|---|
| skills (`skills/*/SKILL.md`) | 127 | 68 | +59 |
| agents (`agents/*.md`) | 39 | 26 | +13 |
| rules (`rules/**`, README excluded) | 37 | 24 | +13 |

**The harness did not get smaller. It turned over.** Additions outnumber retirements in every
layer — 1.9:1 for skills, 1.5:1 for agents and rules. 68 skills were deleted and 127 were
created; the tree still grew by 59.
What the ledger above records is churn with a direction — components leaving because the
substrate absorbed them — not a shrinking harness.

Two caveats on these numbers, both of which inflate both columns rather than one:

- A path that was created and later deleted is counted in both columns.
- A shrink-in-place (ADR-0046, ADR-0018, ADR-0055) changes no path count at all, so the
  largest reductions in this ledger are invisible in the table above. ADR-0018 cut the
  resident rule layer by 60% by word count while the file count went 20 → 14.

The one place the two views agree: 127 − 68 = 59 against 60 skill directories present today
(the difference is one skill that is a symlink to an external tool and not tracked here).
