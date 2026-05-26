---
name: execution-guidance
description: Use when orienting coding, research, or build work to choose lifecycle stage and apply escalation or interaction policy.
---

# Execution Guidance Skill

## Purpose

Claw is the manager: it establishes objectives and acceptance criteria,
delegates meaningful implementation or bounded analysis to appropriate
workers, and independently verifies results before reporting success. It does
not silently replace a worker on substantial delegated work merely because it
could make edits itself.

Read this skill when orienting a coding, ML research, or build task. It is the
source of truth for lifecycle selection, interaction modifiers, and
escalation. Use `execution` as the primary implementation and continuation
skill once work is underway.

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

### Step 3: Execute Under The Contract

1. For implementation, repair, validation, or resumed project work, use
   `execution`; it covers direct work and milestone-based delegation.
2. Before dispatching meaningful work, load the delegation contract and give
   the worker scope, acceptance checks, relevant files, and its report route.
3. Respect "no escalation" directives: use a self-correcting loop when
   suitable rather than assuming human intervention after a failure.

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

## 3. Interaction Modes (Key Phrases)

Before execution, actively scan the user's full message for the modifiers
below. They can occur anywhere and still apply unless the user explicitly limits or negates
them. Reporting and escalation modifiers combine as specified below.

**Regardless of mode, always report the final outcome.** The user must always
know what happened — completion, partial completion, or explicit failure with
reason.

- **"fast feedback"** — Claw writes status updates more frequently and seeks
guidance / escalates earlier than default thresholds. Use when the user wants
tight steering.
- **"low escalation"** — Claw makes autonomous decisions and reports only at
natural completion points. Do not escalate early even if "fast feedback" is
also present.
- **"no escalation"** — Claw must self-resolve. Do not ask the user for help.
See Section 2 for full rules.
- **"report milestones"** — Claw explicitly lists all milestones reached so far
before continuing or before the final summary.
- **"evaluate harness"** — Claw performs the requested work while deliberately
observing how skills, system instructions, tools, routing, compaction, and
reporting mechanisms affect its choices and result quality. It records only
concrete, reusable findings or failures in
`$VAULT_PATH/Knowledge/workflow-reflection.md`, using `capture-knowledge`
discipline, and mentions material findings in its final report.

### Default (no phrase)
- Report at natural milestones and on completion.
- Escalate after 3 failed attempts or >60 min blocked.

### "fast feedback" in effect
- Report after every significant sub-step.
- Escalate or seek guidance after **1 failed attempt** or **>20 min blocked**.
- Ask the user on ambiguous decisions rather than guessing.
- If combined with "low escalation", keep reporting frequently but decide
autonomously.

### "low escalation" in effect
- Report at natural milestones only.
- Do not escalate early.
- Make decisions autonomously.
- If combined with "fast feedback", reporting stays high but escalation stays
deferred.
- If combined with "no escalation", "no escalation" wins: do not escalate at
all. Keep reporting frequently.

### "no escalation" in effect
- Report completion, partial completion, or explicit failure with reason.
- If combined with "fast feedback", report frequently. If combined with "low
escalation", report at milestones only.

### "report milestones" in effect
- Before continuing, list all milestones reached in this session.
- Before the final reply, include a "Milestones reached" section.
- This is additive: it layers on top of whatever other mode is active.

### "evaluate harness" in effect
- Continue to prioritize the user's actual task; harness evaluation is an
  observational overlay, not a replacement objective.
- Note specific beneficial behavior, friction, failure, or improvement ideas
  supported by the run rather than writing generic commentary.
- Do not append anything when the run reveals no reusable harness lesson.

---
