---
name: autoresearch-loop
description: Use for iterative idea testing and optimization, distinguishing premise-testable scientific experiments from blind downstream-performance search.
---

# Autoresearch Loop

## Purpose

Explore candidate improvements reproducibly while choosing the feedback regime
that can honestly evaluate them.

## Choose A Regime

### Scientific Setting

Use the scientific setting when an idea rests on a claim about the problem
that can be tested faithfully with richer feedback, diagnostics, or
simulation before downstream evaluation.

Examples:
- A data-loader rewrite is expected to reduce CPU/I/O starvation: validate
  profiler and throughput behavior before measuring training outcome.
- A model component is meant to improve a known capability: test the claimed
  capability with an appropriate diagnostic or controlled simulation before a
  full benchmark.

First state the premise and test it with `test-hypothesis` and applicable
scientific skills. Only ideas whose premises survive faithful testing should
advance to downstream evaluation. Prefer brainstorming candidate ideas in
this regime by looking for explicit mechanisms and valid diagnostics.

### Blind Setting

Use the blind setting when no faithful intermediate test is available, or the
only meaningful criterion is downstream performance.

Examples:
- Learning-rate, batch-size, dropout, or other hyperparameter sweeps.
- Comparing candidate prompts or heuristic variants whose value is defined by
  task success on the target evaluation.

Evaluate each idea directly against the downstream objective and do not invent
a proxy story after the fact. Blind evaluations are often independent; run
them in parallel when resources, reproducibility, and the `machine` guidance
permit. While the `docs/worker-report.md` fallback is active, one delegated
experiment worker must coordinate and aggregate parallel runs so that the
handoff file has a single writer.

## Setup

Create `.claw-autoresearch.md` with the target file, experiment command,
metric name/parser/direction, time budget, and read-only files. Before any
experiment, record a clean baseline and use a dedicated experiment branch or
worktree so existing user changes cannot be discarded.
Apply `supervising` when dispatching an experiment worker.

## Loop

1. Classify the idea as scientific or blind and record the justification.
2. In the scientific setting, state and test the underlying premise using
   faithful rich feedback before running the downstream comparison. In the
   blind setting, define the downstream evaluation directly.
3. Dispatch experiment workers under the supervision contract. Each worker
   records its measurement in the worker-owned `docs/worker-report.md`
   handoff unless a tested bidirectional session route has been configured.
4. Arrange the configured completion route and return from an interactive
   initiating turn while the experiment runs.
5. When each result arrives, inspect it, compare it with the baseline, log the
   decision in `.claw/experiments/results.tsv`, and record accepted durable
   progress in `docs/progress.md` if useful.
6. Keep an improved change by committing it. Discard a non-improving change
   only inside the dedicated clean experiment branch/worktree and only after
   confirming there are no unrelated modifications.
7. Repeat until the budget is exhausted or progress no longer warrants more
   runs. In blind settings, parallelize independent candidate tests when
   resource measurements support it, using one report-owning worker while the
   file handoff is required.

## Rules

1. Keep each comparison attributable: one candidate intervention per run and
   a common baseline; parallel runs may test distinct candidates independently.
2. Record baseline, metric, outcome, and keep/discard decision for every run.
3. Do not claim a premise is validated from downstream improvement alone when
   richer faithful testing was available.
4. Do not replace the downstream objective with an unfaithful proxy.
5. Respect configured read-only files, compute capacity, and time budgets.
6. Do not dispatch concurrent writers to `docs/worker-report.md`.
7. Never destroy existing user work when discarding an experiment.
8. Report meaningful results, crashes, and diminishing returns.
