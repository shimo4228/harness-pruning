# How components come out

Nothing here is new. This is a summary of three documents that already exist in the harness,
with the source path on every claim so you can read the original instead of trusting this page.

## The principle: scaffolding dissolves

Source: `~/.claude/rules/common/akc-cycle.md`, section *Scaffold Dissolution*.

A rule is scaffolding. When the practice runs without it, simplify it or delete it. Two
directions:

- **Inward** — the principle has been absorbed into how the conversation already goes.
- **Downward** — the substrate gained the capability natively, and the hand-written rule is
  now overwriting a newer default with an older one.

A model generation change is a downward trigger. Prohibitions, exhaustive procedures, and
repeated emphasis written for an older generation get re-audited when the generation turns
over (`~/.claude/skills/generation-audit/SKILL.md`).

Two criteria that decide whether something may actually dissolve:

- **Proof of completion is held-out transfer.** If ablating the scaffold is indistinguishable
  in the *same* context, that is necessary evidence, not sufficient. The evidence that lets
  you dissolve it is the behavior reproducing in a *new* context with the scaffold absent.
- **Delete the negative pole actively.** An artifact carrying a negative information delta —
  a drifted rule that overwrites a newer default — must be removed, not left alone. Silence,
  ablation, and transfer can only detect *absence*; all three are blind to a negative delta.
  That is why it takes a generation review to catch one.

The same reading applies to ADRs themselves: an ADR is a dated hypothesis, not a permanent
constraint. Read its `Date` and its `## Review-when` (expiry conditions) first. An ADR whose
premise is gone has no binding force — supersede it and leave a dated note on the old one.

## The procedure: audit against the runtime layer

Source: `~/.claude/skills/generation-audit/SKILL.md`. Fires on explicit invocation only —
generation changes are rare, explicit events.

1. **Collect the runtime layer from a live session.** What counts is what is actually loaded
   at inference time: the system prompt and the tool descriptions. Official blog posts and
   docs state recommendations but are not loaded. Grepping the config tree will not tell you
   what is loaded, because the runtime layer is injected from outside it too. Build the list
   of themes from your own assets first, then ask the live session to quote the runtime text
   for each theme *verbatim* — "dump everything" comes back summarized.
2. **Record the limits of the collection.** Finding nothing is not "no conflict", it is "this
   question did not find one". And the collection is self-report through the model: use it as
   screening, and confirm the same wording reproduces in a separate session before you retire
   anything on it.
3. **Classify each mismatch** as *conflict* (contradictory instructions loaded at the same
   time), *redundancy* (the runtime layer already says it), or *drift* (away from the
   guidance layer, which is not loaded at all).
4. **Judge each on four axes** — intent (was it written to override the product default, or
   did it merely not conflict at the time), grounding (is there an ADR or incident record for
   why it was written), freshness (does the product behavior it assumed still hold), and
   expiry (has its declared `review-when` trigger fired). Write down the *evidence*, not the
   verdict.
5. **Hand the evidence to the per-class stocktakes** for the verdict. The audit does not hold
   the verdict table itself, so that there is only one canonical owner per asset class.

Two traps the skill names explicitly:

- **Misdiagnosing "cut the verification steps".** What the guidance objects to is instructions
  that make the *model* verify itself more. Deterministic verification run by a machine — a
  command, a hook — is not in scope. Ask which of the two is doing the verifying.
- **Deletion is not enough when the direction flipped.** Delete a suppression instruction and
  the framing of suppression survives and keeps acting. Those cases have to be rewritten in
  the opposite direction, not removed.

## The worked example

Source: `~/.claude/docs/adr/0018-rules-rightsize-for-claude5.md`.

The 2026-07-25 pass that cut the resident rule layer from 5,789 to 2,314 words. What it kept
is the useful half of the answer: your own gotchas, wiring, and opinions — the reversibility
gate, the rate-limit-is-a-policy-signal incident, the origin tracking convention, the
production-test prohibition. What it retired was the general material that a reviewer, a hook,
or the model's own training already covers. The identity/values file was kept verbatim and its
token cost accepted on purpose — a deliberate exception, recorded as one.
