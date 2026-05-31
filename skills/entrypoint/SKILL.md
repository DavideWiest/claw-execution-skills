---
name: entrypoint
description: Use when orienting coding, research, or build work to choose lifecycle stage and execution interaction policy.
---

# Execution Suite Entrypoint

## Principles

Claw is the manager: it establishes objectives and acceptance criteria,
delegates meaningful implementation or bounded analysis to appropriate
workers, and independently verifies results before reporting success. It does
not silently replace a worker on substantial delegated work merely because it
could make edits itself.

Read this skill when orienting a coding, ML research, or build task. It is the
source of truth for lifecycle selection. Use `execution` as the primary
implementation and continuation skill once work is underway. Escalation and
blocker policy lives in workspace `AGENTS.md`.

When a task arc reaches its completion criteria, use `wrapup` before treating
the arc as finished.

## Workflow

Use this procedure even when little is known about the project.

### Step 1: Locate The Project

Identify the project directory from the request; when a new project has no
specified location, default to `~/main/workspace/<project-name>`. Inspect the
user request, repository state, README, and existing `docs/` task-arc
directories before deciding the mode of work.

### Step 2: Select Or Create A Task Arc

A task arc is a coherent objective represented by
`docs/<task-arc>/spec.md` and `docs/<task-arc>/progress.md`. The spec is the
user-derived requirement record; preserve it by default and put running results
in progress.

1. If an existing task arc covers the same objective or the new request is a
   repair, extension, or verification of that objective, reuse that arc.
2. If the request introduces a materially distinct objective, create a concise
   descriptive task-arc directory.
3. If existing project work has no arc yet, create an arc that describes the
   current objective rather than treating the repository as a blank project.
4. For every project task, ensure the selected arc has `spec.md` and
   `progress.md` before working; preserve and incorporate existing
   requirements or accepted results, including small fixes.

Use `docs/<task-arc>/worker-report.md` for a file-based delegated handoff and
`docs/<task-arc>/artifacts/` for deliverables produced in that arc.

### Step 3: Identify The Lifecycle Stage

| Situation Found | What To Do | Lifecycle Skill |
| --- | --- | --- |
| Blank/new project | Establish its first task arc, requirements, and only the necessary scaffold before implementation. | `initiation` |
| Existing project with a selected new or existing task arc, incomplete work, failing checks, or resumed handoff | Read or establish the arc specification and progress, verify any worker report, then continue or correct the work. | `execution` |
| Selected task arc whose central work is done and needs evaluation, documentation, cleanup, or publication planning | Finalize defensibility, reproducibility, artifacts, and dissemination recommendations. | `wrapup` |

### Step 4: Add Only Distinct Capabilities

| Observed Need | Skill | Unique Ownership |
| --- | --- | --- |
| Any delegated worker or subagent | `supervising` | Worker scope, reporting route, acceptance boundary, and Claw's independent review. |
| Comparable iterative idea testing, including scientific premise validation or blind downstream search such as hyperparameter tuning | `autoresearch-loop` | Experiment-loop regime, baseline comparison, keep/discard decisions, and safe parallel search. |
| ML runs, datasets, or compute-heavy local work | `machine` | Machine-specific placement, bottleneck diagnosis, and throughput/parallelism measurement. |
| UI implementation or review | `web-design-guidelines` | Accessibility, interaction, layout, and web interface guideline checks. |
| Work intended to support a scientific or ML knowledge claim | `scientific-work` | Method validity, evidence boundaries, and claim discipline. |
| One uncertain empirical premise requiring a baseline and controlled intervention | `test-hypothesis` | Faithful single-hypothesis comparison. |
| Durable cross-project result, decision, attributed belief, or dead end | `knowledge-organization` | Linked structured vault note without duplication or activity logging. |

### Step 5: Execute Under The Contract

1. For implementation, repair, validation, or resumed project work, use
   `execution`; it covers direct work and milestone-based delegation.
2. Before dispatching meaningful work, load the delegation contract and give
   the worker scope, acceptance checks, relevant files, and its report route.
3. Keep project reports, exports, figures, and agent-produced deliverables in
   the selected arc's `docs/<task-arc>/artifacts/`; use structured knowledge
   capture only for enduring cross-project material worth linking.
4. Load `execution` before applying project directives found in the user's
   message.

## User Interaction During Execution

- Show, do not tell: surface concrete artifacts, diffs, screenshots, plots,
  tables, logs, or checks instead of describing progress abstractly.
- Upload or link important artifacts when the channel supports it; embed plots
  in PDF responses when possible.
- If the spec/progress does not already define the next step, suggest a small
  number of next-step options rather than a single vague continuation.

---

## Rules

Escalation, no-escalation, blocker, and alternative-approach policy lives in
workspace `AGENTS.md`.
