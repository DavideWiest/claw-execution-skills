---
name: exec-initiation
description: "Start new project: explore, spec, scaffold."
---

# Execution Initiation

## Purpose

Establish a lean project-local source of truth before implementation.

## Workflow

1. Write `<project-dir>/docs/spec.md`, preserving user requirements and
   recording unresolved questions rather than silently choosing scope. The user
   probably gave you a spec file or specification notes.
2. Identify the goal, constraints, target directory (default
   `~/main/code/<name>`), and only the stack decisions needed to begin.
3. Add `docs/exploration.md` only when prior-work review, alternatives, or
   premise validation materially informs the project. For scientific work use
   `scientific-work`; for a controlled empirical premise use `test-hypothesis`.
4. Create only the scaffold needed for the next work mode. Add
   `docs/progress.md` for multi-stage or delegated work that benefits from
   Claw-maintained durable milestones and verification; add
   `docs/worker-report.md` when a delegated worker needs its single durable
   handoff surface.
5. Store generated project deliverables and agent artifacts under
   `<project-dir>/docs/artifacts/` when they are created.
6. Initialize or publish Git only when requested or already part of the
   agreed project workflow; never publish without approval.
7. Use `capture-knowledge` only for enduring insight, not to
   log project creation or running status.

## Rules

1. Write the spec before implementation.
2. Keep exploration and scaffolding proportional to the task.
3. If delegating, apply `supervising` and provide the worker
   the spec and relevant exploration evidence.
4. Use native session state for active delegation and `docs/progress.md` for
   durable project progress where it adds value.
