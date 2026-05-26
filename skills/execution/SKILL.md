---
name: execution
description: Use as the primary execution skill for implementing, resuming, fixing, refactoring, or validating project work, including milestone-based delegated execution.
---

# Execution

## Purpose

Implement or resume work on a project and carry it through verified
milestones. Use `entrypoint` for lifecycle selection, interaction
modifiers, and escalation policy; use this skill as the ordinary working path
once implementation, repair, or validation is underway.

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

### 3. Execute Or Delegate

- For narrow direct work, implement, test, and update state yourself.
- For meaningful delegated work, apply `supervising` to define acceptance
  checks, worker scope, and notification route.
- Use `coding-agent` to launch a background Codex worker by default. Ask it to
  maintain one worker-owned `docs/worker-report.md` and send a completion
  notification with the outcome, verification, and any blocker requiring a
  decision.
- Use `sessions_send` instead of the handoff file only after a live round-trip
  test has passed in the current runtime.
- When resuming delegated work, check native session state and ask the worker
  to resume prior context when useful.

### 4. Review And Iterate

- Fix bugs and failing tests
- Remove dead code from pivots
- Refactor for clarity or performance
- Resolve blockers from progress logs
- Continue implementation toward next milestone
- Inspect worker results and verification before accepting delegated output.
- Retry only after identifying a specific transient or fixable cause.
- Commit incrementally with clear messages. Commit under the user's name.

### 5. Record And Report

- Update `docs/spec.md` with completed features
- After checking evidence, update Claw-owned `docs/progress.md` with material
  verified outcomes when progress is persisted.
- Store generated project artifacts in `docs/artifacts/`; use
  `capture-knowledge` only for durable structured knowledge worth linking
  beyond project working state
- Report start, meaningful milestones when requested, and final outcome.

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
