---
name: execution-guidance
description: Use for coding, research, or build execution to choose lifecycle stage, execution pattern, and escalation or interaction mode.
---

# Execution Guidance Skill

## Purpose
Provide the decision framework for how to execute tasks: what pattern to use,
how to behave when blocked, and when to escalate vs. self-resolve.

## 0. This Is the Entrypoint

**Read this skill first** for coding, ML research, or build tasks. It is the
source of truth for work-mode selection, project lifecycle, and escalation. If
work is delegated, read
`supervising` for role separation, route selection,
notification, and acceptance responsibilities.

### Reasoning Level

Use **high reasoning effort** by default for all delegated tasks. Both Kimi
(`--thinking`) and OpenClaw (`thinkingDefault: "high"`) are configured for
this. Do not downgrade reasoning unless the user explicitly requests a faster,
cheaper mode.

## 1. Choose a Work Mode

Run this section before coding, research, or build execution.

### Routing Layers

The following layers are compatible; do not force them into one mutually
exclusive choice:

| Layer | Decision |
|-------|----------|
| Project lifecycle | Use Section 4 when initiating, iterating, or wrapping a project. |
| Primary execution pattern | Choose one from the table below for how work runs. |
| Domain overlay | Add `machine` or scientific skills when the domain requires them. |
| Delegation contract | Load `supervising` whenever a worker or subagent is dispatched. |

### Primary Execution Pattern

| Task Type | Pattern |
|-----------|---------|
| Long non-agent shell/I/O operation: download, installation, data preparation, export, sync, or ordinary build | `background-task-execution` |
| Narrow implementation/review with clear acceptance checks and one worker run | Direct supervised execution using `supervising` when delegated |
| Multi-phase implementation/review with milestones or broader risk | `multi-step-execution` |
| Iterative idea testing or optimization with comparable outcomes, including scientific premise testing or blind downstream search such as hyperparameter tuning | `autoresearch-loop` |

### Domain Overlays

| Condition | Add Skill |
|-----------|-----------|
| ML runs, datasets, or computationally heavy work on this machine | `machine` |
| Scientific or ML work intended to support a knowledge claim | `scientific-work` |
| One uncertain empirical comparison requiring a baseline and controlled intervention | `test-hypothesis` |

### Rules For Selection

1. Choose one primary execution pattern; add applicable domain overlays.
2. Read `supervising` before dispatching a worker or subagent.
3. If unsure between coding patterns, prefer `multi-step-execution`.
4. Respect "no escalation" directives: if the user has forbidden escalating,
   prefer patterns that allow self-correction (`autoresearch-loop`,
   `multi-step-execution` with retries) over patterns that assume human
   intervention on failure.

### Cross-Cutting Boundaries

- `background-task-execution` owns launch, status, and completion rules for
  long non-agent commands.
- `supervising` owns communication and acceptance rules for
  workers and subagents.
- Scientific overlay skills own experimental validity and claim boundaries.

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

## 4. Project Lifecycle Routing

Use this section when a coding or research project is starting, stuck,
pivoting, or nearing completion. Route to exactly one stage at a time; never
skip stages.

### Stages

| Stage | Check | Skill |
|-------|-------|-------|
| Initiate | No `docs/spec.md` exists | `exec-initiation` |
| Build | Spec exists, no working code | Pattern from Section 1 → delegate |
| Iterate | Code exists, tests failing or blockers | `exec-iteration` |
| Wrapup | Core done, needs evaluation/plots/docs | `exec-wrapup` |

### Rules

1. One stage at a time. Do not skip.
2. Revisit exploration if iteration reveals the approach was wrong.
