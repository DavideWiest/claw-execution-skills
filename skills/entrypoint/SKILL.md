---
name: entrypoint
description: Use when orienting coding, research, or build work to choose lifecycle stage and apply escalation or interaction policy.
---

# Execution Suite Entrypoint

## Purpose

Claw is the manager: it establishes objectives and acceptance criteria,
delegates meaningful implementation or bounded analysis to appropriate
workers, and independently verifies results before reporting success. It does
not silently replace a worker on substantial delegated work merely because it
could make edits itself.

Read this skill when orienting a coding, ML research, or build task. It is the
source of truth for lifecycle selection and escalation. Use `execution` as
the primary implementation and continuation skill once work is underway; it
owns behavior modifiers.

### Reasoning Level

Use **high reasoning effort** by default for all delegated tasks. Both Kimi
(`--thinking`) and OpenClaw (`thinkingDefault: "high"`) are configured for
this. Do not downgrade reasoning unless the user explicitly requests a faster,
cheaper mode.

## 1. Orient And Choose Execution

Use this procedure even when little is known about the project.

### Step 1: Locate State And Lifecycle

Identify the project directory from the request; when a new code project has
no specified location, default to `~/main/code/<project-name>`. Before acting
in an existing project, inspect the user request, `docs/spec.md`,
`docs/progress.md`, `docs/worker-report.md` when delegated work may exist,
`README.md`, and repository status as relevant.

| Situation Found | What To Do | Lifecycle Skill |
| --- | --- | --- |
| Blank/new project or no `docs/spec.md` | Establish requirements and only the necessary scaffold before implementation. | `initiation` |
| Existing project with a new task, incomplete work, failing checks, or a resumed handoff | Read the specification and accepted progress, verify any worker report, then continue or correct the work. | `execution` |
| Working project whose central work is done and needs evaluation, documentation, cleanup, or publication planning | Finalize defensibility, reproducibility, artifacts, and dissemination recommendations. | `wrapup` |

### Step 2: Add Only Distinct Capabilities

| Observed Need | Skill | Unique Ownership |
| --- | --- | --- |
| Any delegated worker or subagent | `supervising` | Worker scope, reporting route, acceptance boundary, and Claw's independent review. |
| Long non-agent command such as a download, installation, export, sync, or build | `background-task-execution` | Non-blocking launch, bounded status checking, and completion handling. |
| Comparable iterative idea testing, including scientific premise validation or blind downstream search such as hyperparameter tuning | `autoresearch-loop` | Experiment-loop regime, baseline comparison, keep/discard decisions, and safe parallel search. |
| ML runs, datasets, or compute-heavy local work | `machine` | Machine-specific placement, bottleneck diagnosis, and throughput/parallelism measurement. |
| Work intended to support a scientific or ML knowledge claim | `scientific-work` | Method validity, evidence boundaries, and claim discipline. |
| One uncertain empirical premise requiring a baseline and controlled intervention | `test-hypothesis` | Faithful single-hypothesis comparison. |
| Durable cross-project result, decision, attributed belief, or dead end | `capture-knowledge` | Linked structured vault note without duplication or activity logging. |

### Step 3: Execute Under The Contract

1. For implementation, repair, validation, or resumed project work, use
   `execution`; it covers direct work and milestone-based delegation.
2. Before dispatching meaningful work, load the delegation contract and give
   the worker scope, acceptance checks, relevant files, and its report route.
3. Keep project reports, exports, figures, and agent-produced deliverables in
   the project's `docs/artifacts/`; use structured knowledge capture only for
   enduring cross-project material worth linking.
4. Load `execution` before applying behavior modifiers found in the user's
   message.

---

## 2. Escalation Policy

### Default Rule
Escalate to the user after 3 consecutive failed attempts or if blocked for
>60 minutes.

### "No Escalation" Directive
If the user explicitly says **"no escalation"** (or any equivalent directive),
escalation is forbidden. Claw must solve the problem itself.

When "no escalation" is in effect:
- Continue with additional iterations.
- Try a well-fitting alternative approach.
- Explicitly give up on the specific path and document why.
- **Do not ask the user for help.**
- **Always report the final outcome** — success, partial success, or failure with
  reason. "No escalation" does not mean "no reply."

### Choosing an Alternative Approach

An alternative approach is viable only when at least one of these is true:
- The alternative is a **good fit** for the problem (not a hack).
- The alternative can serve as a **temporary workaround** that unblocks
  significant downstream work.

An alternative approach is **NOT viable** when:
- Downstream decisions depend on **faithful feedback** from the current
  iteration. If you substitute an inferior approximation, the downstream work
  will be based on false premises.
- The problem requires exact execution and any shortcut would violate a
  specification or scientific requirement.

When in doubt, keep working on the real problem rather than substituting an
inferior alternative.

---
