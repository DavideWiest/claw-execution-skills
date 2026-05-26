---
name: supervising
description: Use when delegating implementation, analysis, or review work to a worker or subagent.
---

# Supervising

This skill owns the delegation contract and supervision mechanics. Use
`execution-guidance` to choose the work mode and escalation policy; do not
redefine those decisions here.

## Ownership Contract

| Concern | Owner | Contract |
|---------|-------|----------|
| Objective, constraints, and acceptance criteria | Claw | Establish before dispatch; a worker cannot silently redefine them. |
| Implementation or delegated analysis | Worker/subagent | Perform only the dispatched scope and report changes, evidence, blockers, and assumptions. |
| Worker-side checks | Worker/subagent | Run requested checks and provide results; these are evidence, not acceptance. |
| Worker handoff report | Worker/subagent | Write or replace `docs/worker-report.md` when a verified bidirectional session route is unavailable; it is the single worker-owned durable handoff file. |
| Durable progress record and accepted milestone log | Claw | Own and update `docs/progress.md` after verifying worker messages and evidence; a worker may propose progress but does not author the accepted record. |
| Acceptance and scientific/technical conclusion | Claw | Inspect actual output critically, rigorously and independently assess evidence before reporting success. |
| User-facing updates and outward actions | Claw | Report accurately and obtain approval where required. |

For project work, `docs/spec.md` holds requirements. Claw maintains
`docs/progress.md` for material verified progress, decisions, and results
when persistent progress is useful. Unless a tested message route is being
used, the worker writes only `docs/worker-report.md` for durable reporting.

## Before Dispatch

1. State the primary task, and label side-questions so they do not silently
   replace the main objective.
2. Provide the worker with goal, relevant spec/files, scope constraints,
   acceptance checks, and the reporting or notification route.
3. Choose the execution route:
   - Use native OpenClaw `sessions_send` for bidirectional steering only after
     a round-trip smoke test has succeeded in the active runtime. The
     2026-05-26 test accepted a send but skipped delivery and returned no
     acknowledgement, so it is not presently a dependable report route.
   - Use `coding-agent` with Codex by default for substantial coding work;
     follow its completion/blocker notification contract rather than assuming
     it exposes an OpenClaw session channel.

## During And After Work

- Prefer event-driven completion and blocker messages; avoid repetitive polls.
- While no tested bidirectional route is available, require a single
  worker-owned `docs/worker-report.md` with milestones, checks, results, and
  blockers. Claw verifies its integrity and evidence before transferring
  accepted facts into `docs/progress.md`.
- If independent tests run in parallel while using that file fallback,
  dispatch one coordinating worker to aggregate their results; never allow
  concurrent workers to write the same handoff file.
- Before accepting a result, inspect the actual work and run or examine the
  relevant verification. Check specification compliance before code quality or
  narrative polish.
- For experimental or research work, separately check methodology,
  implementation fidelity, measurements, uncertainty, and claims.
- Report unresolved risk or needed user decisions explicitly.
