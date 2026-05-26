---
name: multi-step-execution
description: Manage milestone-based coding work delegated through the native coding-agent skill.
---

# Multi-Step Execution

## Purpose

Apply the contract in `supervising`. This skill adds only the
multi-phase project workflow: milestones, persistent progress, and completion
handling.

## Workflow

1. Write or update the concrete project requirements in `docs/spec.md`, and
   decide whether Claw should maintain `docs/progress.md` for verified
   milestones.
2. Apply `supervising` to define acceptance checks, worker
   scope, and notification route.
3. Use `coding-agent` to launch a background Codex worker by default. Ask it
   to maintain one worker-owned `docs/worker-report.md` and send a completion
   notification with the outcome, verification, and any blocker requiring a
   decision.
4. Use `sessions_send` instead of the handoff file only after a live
   round-trip test has passed in the current runtime. After checking evidence,
   Claw records useful durable state in `docs/progress.md` when applicable.
5. Return from the initiating chat turn after acknowledging that work started.
6. On completion notification, inspect results and verification, update state,
   and report completion or a concrete failure.

## Milestone Guidance

Use milestones for multi-phase builds, large refactors, or work expected to
take more than a few minutes. They should identify completed phases, meaningful
verification, blockers, and the final result, not stream command output.

## Rules

1. Record milestones and blockers, not a stream of command output.
2. Retry only after identifying a specific transient or fixable cause.
3. Report start, meaningful milestones when requested, and final outcome.
