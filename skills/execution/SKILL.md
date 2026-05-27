---
name: execution
description: Use as the primary execution skill for implementing, resuming, fixing, refactoring, or validating project work, including milestone-based delegated execution.
---

# Execution

## Purpose

Implement or resume work on a project and carry it through verified
milestones. Use `entrypoint` for lifecycle selection and escalation policy;
use this skill as the ordinary working path and source of truth for behavior
modifiers once implementation, repair, or validation is underway.

## Workflow

### 1. Identify Project And State

- Project name or path from user input
- Default lookup: `~/main/workspace/<project-name>`
- Verify directory exists
- Use the task arc selected by `entrypoint`; ensure its
  `docs/<task-arc>/spec.md` and `progress.md` exist before any project work
- Read `docs/<task-arc>/spec.md` for requirements
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
- Check off completed items
- Identify next milestone or blocker
- State the next milestone in `docs/<task-arc>/spec.md` as needed and record
  accepted material outcomes in `docs/<task-arc>/progress.md`.
- Milestones record completed phases, meaningful verification, blockers, and
  final results, not a stream of command output.

### 3. Order Work 

- The user's specifications may not be in executable order. Follow task
  dependencies first: identify which assumptions, components, or results
  must work before later work is meaningful.
- Fail fast on pivotal premises and dependencies. Prefer a bounded test that
  validates or invalidates an approach before expensive implementation.
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

- Update `docs/<task-arc>/spec.md` with completed requirements
- After checking evidence, update Claw-owned `docs/<task-arc>/progress.md`
  with material verified outcomes.
- Store generated project artifacts in `docs/<task-arc>/artifacts/`; use
  `knowledge-organization` only for durable structured knowledge worth linking
  beyond project working state
- Report start, meaningful milestones when requested, and final outcome.

## Behavior Modifiers

Before execution, actively scan the user's full message for these modifiers.
They can occur anywhere and apply unless explicitly limited or negated.
Regardless of mode, always report the final outcome.

- **"verify approach"** (also accept the literal typo **"veriy approach"**) —
  Before beginning substantive execution, respond once with this fixed
  structure and wait for feedback:

  ```markdown
  **Partial** - Verifying approach before execution.

  Approach: <one short sentence or paragraph describing the planned approach>

  Key things to look out for:
  - Fork: <important alternative or decision point, or "none identified">
  - Possible blocker: <dependency, uncertainty, or "none identified">

  Feedback requested: confirm this approach or identify a correction.
  ```

- **"fast feedback"** — Report after every significant sub-step and escalate
  or seek guidance after 1 failed attempt or more than 20 minutes blocked.
- **"low escalation"** — Report at natural milestones and make autonomous
  decisions; do not escalate early.
- **"no escalation"** — Self-resolve without asking the user for help; follow
  the no-escalation policy in `entrypoint`.
- **"report milestones"** — Before continuing and before the final reply,
  list milestones reached in this session.
- **"evaluate harness"** — While doing the actual task, record concrete,
  reusable harness findings or failures in
  `$VAULT_PATH/Knowledge/workflow-reflection.md` using `knowledge-organization`
  discipline; do not write filler.

If `fast feedback` and `low escalation` are combined, report frequently while
deciding autonomously. If `no escalation` is present, it wins for escalation.

## Failure Biases

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
6. If stuck for >60 min, escalate to user.
7. Escalation policy and alternative-approach rules are defined in the `entrypoint` skill.
