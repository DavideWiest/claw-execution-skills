---
name: initiation
description: "Start new project: explore, spec, scaffold."
---

# Execution Initiation

## Purpose

Establish a lean project-local source of truth before implementation.

## Workflow

1. Identify the goal, constraints, target directory (default
   `~/main/workspace/<name>`), and only the stack decisions needed to begin.
2. Select a concise first task arc and create
   `<project-dir>/docs/<task-arc>/spec.md` and `progress.md`. Preserve user
   requirements in the spec, record unresolved questions rather than silently
   choosing scope, and initialize progress with the established current state.
3. Add `docs/<task-arc>/exploration.md` only when prior-work review, alternatives, or
   premise validation materially informs the project. For scientific work use
   `scientific-work`; for a controlled empirical premise use `test-hypothesis`.
4. Create only the scaffold needed for the next work mode. Add
   `docs/<task-arc>/worker-report.md` only when a delegated worker needs its
   single durable handoff surface.
5. Store generated project deliverables and agent artifacts under
   `<project-dir>/docs/<task-arc>/artifacts/` when they are created.
6. Initialize or publish Git only when requested or already part of the
   agreed project workflow; never publish without approval.
7. Use `knowledge-organization` only for enduring insight, not to
   log project creation or running status.

## Rules

1. Write the task-arc spec and progress files before implementation.
2. Keep exploration and scaffolding proportional to the task.
3. If delegating, apply `supervising` and provide the worker
   the spec and relevant exploration evidence.
4. Use native session state for active delegation and the selected arc's
   `progress.md` for durable project progress.
