---
name: execution
description: Use as the primary execution skill for implementing, resuming, fixing, refactoring, or validating project work, including milestone-based delegated execution.
---

# Execution

## Purpose

Implement or resume work on a project and carry it through verified
milestones. Use `entrypoint` for lifecycle selection and escalation policy;
use this skill as the ordinary working path once implementation, repair, or
validation is underway.

## Workflow

### 1. Identify Project And State

- Project name or path from user input
- Default lookup: `~/main/workspace/<project-name>`
- Verify directory exists
- Use the task arc selected by `entrypoint`; ensure its
  `docs/<task-arc>/spec.md` and `progress.md` exist before any project work
- Read `docs/<task-arc>/spec.md` for requirements; it is the user-derived
  specification and should not be edited by default.
- Read `docs/<task-arc>/exploration.md` when present for prior findings
- Read `docs/<task-arc>/progress.md` for durable execution results
- Read `docs/<task-arc>/worker-report.md` when delegated work used the worker-owned
  handoff fallback; verify it before accepting or transferring results
- Read `README.md` for current state
- Check `git status` / `git log --oneline -10`
- Check native OpenClaw session state when delegated work may be running
- Check for `TODO.md`, `ROADMAP.md`, or issue trackers

### 2. Establish The Next Verified Milestone

- Compare spec features against implementation
- Note completed items in progress
- Identify next milestone or blocker
- State the next milestone from the spec and record accepted material outcomes
  in `docs/<task-arc>/progress.md`.
- Milestones record completed phases, meaningful verification, blockers, and
  final results, not a stream of command output.

### 3. Order Work 

- The user's specifications may not be in executable order. Follow task
  dependencies first: identify which assumptions, components, or results
  must work before later work is meaningful.
- Fail fast on pivotal premises and dependencies. Prefer a bounded test that
  validates or invalidates an approach before expensive implementation.
- Prefer existing, working solutions over writing a custom implementation by
  default. If an existing solution is hard to set up and the custom version is
  not too hard to get right, conservatively prefer the custom solution.
- For hyperparameter sweeps, prefer Optuna (`https://optuna.readthedocs.io/`)
  unless the project already has a working tool. Predefine the search space,
  target metric, seeds/folds, and fixed budget (`n_trials` or timeout) before
  running; run the sweep once rather than extending it ad hoc. Before choosing
  the budget, search previous work or practitioner norms for the closest
  comparable model, dataset, and compute setting. Report the best trial,
  uncertainty/significance from repeats or folds when available, parameter
  importances, and relevant plots/tables.
- Prioritize foundational and structure-determining work over polish or
  optimization: do high-temperature decisions first, then low-temperature
  tuning within a validated structure.
- Use bounded experiments where evidence is needed; load `test-hypothesis`
  when it fits. One or two well-motivated retries are acceptable, but do not
  continue from sunk cost alone.

### 4. Execute Or Delegate

- For narrow direct work, implement, test, and update state yourself.
- For meaningful delegated work, apply `supervising` to define acceptance
  checks, worker scope, and notification route.
- Follow `supervising` when selecting Codex or Kimi. For file-based delegated
  work, ask the worker to maintain one worker-owned
  `docs/<task-arc>/worker-report.md` and send a completion notification with
  outcome, verification, and blockers.
- Use `sessions_send` instead of the handoff file only after a live round-trip
  test has passed in the current runtime.
- When resuming delegated work, check native session state and ask the worker
  to resume prior context when useful.
- Commit and push frequently after every major task completion.

### 5. Review And Iterate

- Fix bugs and failing tests
- Remove dead code from pivots
- Refactor for clarity or performance
- Resolve blockers from progress logs
- Continue implementation toward next milestone
- Inspect worker results and verification before accepting delegated output.
- Retry only after identifying a specific transient or fixable cause.
- Commit incrementally with clear messages. Commit under the user's name.

### 6. Record And Report

- Preserve `docs/<task-arc>/spec.md`; amend it only when the user changes or
  approves requirements.
- After checking evidence, update Harness-owned `docs/<task-arc>/progress.md`
  with material verified outcomes.
- Store generated project artifacts in `docs/<task-arc>/artifacts/`; use
  `knowledge-organization` only for durable structured knowledge worth linking
  beyond project working state
- Use `sci-scientific-visualization` when creating, polishing, or reviewing
  project figures.
- When the selected task arc reaches its completion criteria, load `wrapup`
  before reporting final success.
- Report start, meaningful milestones when requested, and final outcome.

#### `progress.md` Layout

- Use reverse chronological bullets by default; insert new entries at the top.
- Each entry should include type, time, and information, e.g.
  `- IMPLEMENTATION (2026-05-29 14:30): ...`. Allowed types
  include `USER`, `INITIATION`, `PIVOT`, `DECISION`, `EXPERIMENT`, `IMPLEMENTATION`, `VERIFICATION`,
  `BLOCKER`, `ARTIFACT`, `MILESTONE`, `WRAPUP`. `USER` is for logging every
  user message. `MILESTONE` is for noting a
  milestone has been reached, `DECISION` for notable design decisions.
- Record important metrics, verification status, decisions, next actions, and
  links to important artifacts so a later session can resume quickly and the
  results can be published if needed. Store more rather than less, especially
  if it's not saved anywhere else.
- Use tables when they make metrics, comparisons, or artifact indexes
  clearer than bullets. 

## Failure Modes

- **Unowned slowness**: if a run/program is slow, slower than expected, or a
  computational part becomes prohibitively slow, expensive, unreliable, or a
  significant bottleneck, attribute it first to Harness's design decisions.
  Frequent causes: bad design decisions, lazy implementation, or failure to
  follow the specification or implied approach in the user's request.
- **Complexification**: do not add elaborate machinery when a simpler faithful
  test or implementation answers the question.
- **Narrow-sighted design decisions**: do not optimize a local metric or
  convenient component while ignoring the actual objective, constraints, or
  later dependencies.
- **Sunk cost**: do not keep a failing line of work alive merely because time
  or compute has already been spent on it.
- **Cheating**: do not drift from the agreed plan, replace hard requirements
  with easier proxies, or present simulated activity as verified progress.
- **Stupid design decisions**: Design decisions that are obviously stupid when
  reflecting, such as implementations are the vastly less performant then 
  proper ones.

## Rules

1. Always read or establish the selected arc's `spec.md` and `progress.md`
   before making changes.
2. Never assume state from conversation alone.
3. Commit at coherent verified milestones.
4. Remove dead code promptly.
5. Update tests to match new behavior.
6. If stuck, follow workspace `AGENTS.md` escalation and no-escalation policy.
7. Use `wrapup` before closing a completed task arc.
8. Escalation policy and alternative-approach rules are defined in workspace `AGENTS.md`.
