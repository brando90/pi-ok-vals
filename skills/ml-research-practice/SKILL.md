---
name: ml-research-practice
description: "Apply expect-then-verify machine-learning research checks derived from Rylan Schaeffer's CS229 ML advice. Use when designing, launching, or interpreting experiments, benchmark or agent evaluations, judge or reward-model studies; changing prompts, harnesses, scorers, parsers, or datasets behind reported numbers; or investigating surprising results."
---

# Expect-then-verify machine-learning research

**Doc link:** <https://github.com/brando90/pi-ok-vals/blob/main/skills/ml-research-practice/SKILL.md>

**TLDR:** Predict what each measurement should show before running an experiment, including the score of perfect instruction-following. Inspect raw outputs and controls, then explain every difference between expected and observed behavior before trusting the result.

This skill adapts Brando's research workflow based on Rylan Schaeffer's Stanford CS229 lecture. It is not a claim that Rylan authored this skill file. Apply it within the task's existing authorization, data-access rules, and budgets; loading the skill does not authorize new experiments or paid calls.

## Procedure

1. **Write a measurement contract before execution.** For every reported metric, record its definition, exact computing code path, range, and predicted values for the reference answer, intended behavior, literal instruction-following, degenerate submissions, and baselines. If you cannot predict the measurement, inspect its implementation before proceeding.
2. **Check delivered instructions against scoring.** Read the rendered prompts, examples, repair messages, and success criteria that each system actually receives. Following instructions must not lower the score. Keep reference-authoring conventions out of solver prompts; report unequal instructions or budgets as confounds.
3. **Trace one item end to end.** Follow delivered prompt → transcript → captured output → extraction → scorer branch → judge input and parsed response → aggregate result. Verify exact content and hashes between stages, rather than trusting version labels alone.
4. **Run controls before scaling, when execution is authorized.** Use a small set with positive, negative, literal-compliance, and known-bad controls. Require outcomes to match the contract. Change one thing at a time. For a results-only investigation, reuse saved controls and mark missing evidence rather than silently launching new work.
5. **Look at the data.** Inspect raw outputs across zeros, perfect scores, the middle, and outliers. Count concrete behaviors such as placeholders, attempted proofs, and restated implementations. Sample enough to understand the behavior mixture, not just the best-looking examples.
6. **Compare observed with expected.** Investigate discrepancies in either direction before interpreting them. Check whether thresholds, discrete judge outputs, geometric means, or all-or-nothing scoring themselves produce the apparent pattern.
7. **Inspect for metric gaming.** Look at top scorers for empty or vacuous claims, implementation restatements, deleted obligations, custom axioms, or other shortcuts. Distinguish success on the proxy from the behavior the study is meant to measure.
8. **Keep the experiment honest.** Retain failed and missing cells in the declared denominator. Report distributions over existing repetitions rather than only the best run. Changes to tasks, prompts, scoring, or budgets create separately labeled conditions; never retrofit them to rescue an old result.
9. **Use consistency checks.** Recompute tables from saved artifacts. Verify mappings are one-to-one where required, hashes bind outputs to scores, and equivalent implementations agree. Distinguish deterministic checks from stochastic judge repeatability; do not assume independent model calls must match exactly.
10. **Iterate on verified bottlenecks.** Find a concrete problem, make a small change, check it, and repeat. Fast iteration is useful only when the measurement remains trustworthy.

## Measurement contract

Fill predictions before execution and observations afterward. Keep the table with the experiment's protocol or results, not in this reusable skill.

| Metric / range | Code path | Reference | Intended behavior | Literal compliance | Degenerate cases | Baseline | Observed | Explanation of mismatch |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Name and definition | Exact implementation | Predicted | Predicted | Predicted | Empty / vacuous / placeholder | Predicted | Measured or unavailable | Mechanism and evidence |

## Stop interpretation or scaling when

- Literal instruction-following scores below the best achievable result.
- A control misses its predicted range.
- Degenerate submissions score well for the wrong reason.
- Compared systems receive materially different instructions or inputs without disclosure.
- Scores collapse onto suspicious constants or a few discrete values.
- Judge inputs differ from the references or items humans evaluated.
- Missing or failed cells disappear from the reported denominator.
- You cannot trace a reported number back to raw evidence.

Preserve the evidence, name the specific unresolved mechanism, and fix or qualify the affected claim. Do not change frozen protocols or invent measurements.

## Sources and supporting references

- [Full adapted workflow, examples, and checklist](https://github.com/brando90/agents-config/blob/main/workflows/ml-research-practice.md).
- [Rylan Schaeffer's CS229 lecture, 02-19-2025](https://www.youtube.com/watch?v=sl55buSIJPA).
- [Lecture slides](https://docs.google.com/presentation/d/1kTg6SSm4TRbogwz18_CtanJftYsj8Khx6W8UJQbQgYI/edit?usp=sharing).
- [Transcript reference](https://github.com/brando90/agents-config/blob/main/workflows/assets/rylan_schaeffer_cs229_ml_advice_02-19-2025_transcript.md).
- [Slide-to-source index](https://github.com/brando90/agents-config/blob/main/workflows/assets/rylan_schaeffer_cs229_ml_advice_02-19-2025_slide_index.md).
- [Related language-model judge recipe](https://github.com/brando90/agents-config/blob/main/workflows/llm-judge-recipe.md).

The executable procedure above is self-contained. Supporting material is linked rather than duplicating the lecture transcript or private experiment artifacts.
