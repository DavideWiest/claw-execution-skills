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
- Default lookup: `~/main/code/<project-name>`
- Verify directory exists
- Read `docs/spec.md` for requirements
- Read `docs/exploration.md` for prior findings
- Read `docs/progress.md` when it exists for durable execution results
- Read `docs/worker-report.md` when delegated work used the worker-owned
  handoff fallback; verify it before accepting or transferring results
- Read `README.md` for current state
- Check `git status` / `git log --oneline -10`
- Check native OpenClaw session state when delegated work may be running
- Check for `TODO.md`, `ROADMAP.md`, or issue trackers

### 2. Establish The Next Verified Milestone

- Compare spec features against implementation
- Check off completed items
- Identify next milestone or blocker
- For multi-phase builds, large refactors, or work expected to take more than
  a few minutes, state milestones in `docs/spec.md` and decide whether Claw
  should maintain `docs/progress.md` for verified outcomes.
- Milestones record completed phases, meaningful verification, blockers, and
  final results, not a stream of command output.

### 3. Order Work By Dependencies

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
  work, ask the worker to maintain one worker-owned `docs/worker-report.md`
  and send a completion notification with outcome, verification, and blockers.
- Use `sessions_send` instead of the handoff file only after a live round-trip
  test has passed in the current runtime.
- When resuming delegated work, check native session state and ask the worker
  to resume prior context when useful.

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

- Update `docs/spec.md` with completed features
- After checking evidence, update Claw-owned `docs/progress.md` with material
  verified outcomes when progress is persisted.
- Store generated project artifacts in `docs/artifacts/`; use
  `capture-knowledge` only for durable structured knowledge worth linking
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
- **"evaluate harness"** — While doing the actual task, record only concrete,
  reusable harness findings or failures in
  `$VAULT_PATH/Knowledge/workflow-reflection.md` using `capture-knowledge`
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

## Context Loading Priority

1. `docs/spec.md`
2. `docs/exploration.md`
3. `docs/progress.md` (when present)
4. `README.md`
5. `git log --oneline -20`
6. Native session state (if delegated work is running)
7. TODO comments in code

## Dead Code Removal

```bash
git rm <dead_files>
git commit -m "chore: remove dead code after pivot"
```

## Rules

1. Always read `docs/spec.md` before making changes.
2. Never assume state from conversation alone.
3. Commit at coherent verified milestones.
4. Remove dead code promptly.
5. Update tests to match new behavior.
6. If stuck for >60 min, escalate to user.
7. Escalation policy and alternative-approach rules are defined in the `entrypoint` skill.
