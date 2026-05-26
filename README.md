# Claw Execution Skills

Execution-oriented skills for the Kimi-Claw harness, kept outside the core
configuration repository so execution policy can evolve as a coherent
extension.

## Skills

| Source Skill | Visible Runtime Name | Purpose |
| --- | --- | --- |
| `execution` | `exec-execution` | Primary implementation, repair, validation, continuation, and milestone workflow. |
| `execution-guidance` | `exec-guidance` | Select lifecycle, interaction modifiers, and escalation policy. |
| `supervising` | `exec-supervising` | Establish ownership, reporting routes, and independent acceptance. |
| `autoresearch-loop` | `exec-autoresearch-loop` | Explore scientific premise-testable ideas or blind downstream-search candidates reproducibly. |
| `initiation` | `exec-initiation` | Establish lean project-local specification and scaffolding. |
| `wrapup` | `exec-wrapup` | Clean, validate, document, package artifacts, and recommend publication paths. |

`single-step-execution` is intentionally omitted: narrow work is covered
directly by `execution` plus `supervising`, and the
former skill contained no domain-specific guidance.

Delegated workers currently report through one worker-owned
`docs/worker-report.md` file; Claw verifies it before recording accepted
progress. A live OpenClaw `sessions_send` round trip on May 26, 2026 skipped
delivery, so session-message reporting remains conditional on a later
successful runtime test.

## Integration

The `kimi-claw` repository generates full-content namespaced runtime copies
from this sibling checkout and loads those through OpenClaw's
`skills.load.extraDirs` setting. This repository stores no credentials or
project-specific output.
