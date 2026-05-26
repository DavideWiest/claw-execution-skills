---
name: exec-iteration
description: "Resume existing project: fix, refactor, continue."
---

# Execution Iteration

## Purpose
Resume work on an existing project and improve it.

## Workflow

### 1. Identify Project

- Project name or path from user input
- Default lookup: `~/main/code/<project-name>`
- Verify directory exists

### 2. Load Context

- Read `docs/spec.md` for requirements
- Read `docs/exploration.md` for prior findings
- Read `docs/progress.md` when it exists for durable execution results
- Read `docs/worker-report.md` when delegated work used the worker-owned
  handoff fallback; verify it before accepting or transferring results
- Read `README.md` for current state
- Check `git status` / `git log --oneline -10`
- Check native OpenClaw session state when delegated work may be running
- Check for `TODO.md`, `ROADMAP.md`, or issue trackers

### 3. Assess Progress

- Compare spec features against implementation
- Check off completed items
- Identify next milestone or blocker

### 4. Resume Delegated Work

- Check native OpenClaw session state for existing worker context when relevant.
- Apply `supervising` when dispatching or resuming a worker.
- Ask the worker to resume prior context when useful and report completion.
- Update project state after reviewing delegated results.

### 5. Iterate

- Fix bugs and failing tests
- Remove dead code from pivots
- Refactor for clarity or performance
- Resolve blockers from progress logs
- Continue implementation toward next milestone
- Commit incrementally with clear messages. Commit under the user's name.

### 6. Wrap Up

- Update `docs/spec.md` with completed features
- Update `docs/progress.md` with material outcomes when progress is persisted
- Store generated project artifacts in `docs/artifacts/`; use
  `capture-knowledge` only for durable structured knowledge worth linking
  beyond project working state
- Summarize progress

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
7. Escalation policy and alternative-approach rules are defined in the `execution-guidance` skill.
