---
name: exec-wrapup
description: Use when a project is working and needs evaluation, cleanup, documentation, artifacts, or a publication plan.
---

# Execution Wrapup

## Purpose
Make the project defensible, reproducible, publishable, and easy to reuse.

## Activities

- Clean the repository: lint and format as appropriate, remove debug or dead
  code and abandoned outputs, and make small reusability improvements that do
  not expand the project's claims or scope.
- Complete the evaluation required by the specification; for ML projects this
  may include full-scale training/validation.
- Generate plots or visualizations required to interpret or present results,
  storing deliverables and agent-produced artifacts in
  `<project-dir>/docs/artifacts/`.
- Add missing required metrics and reporting.
- Write final README and documentation, including limitations and how claims
  are supported.
- Ensure reproducibility (pinned dependencies, seed values, runnable checks).
- Use `capture-knowledge` to capture durable cross-project conclusions or
  research directions, linking to project artifacts rather than copying them
  into the vault.
- Give the user a recommended numbered publishing/publicity plan appropriate
  to the result. Consider, rather than automatically selecting: an article on
  the personal website; an arXiv/preprint release for mature research; posts
  on X and LinkedIn; and a dedicated project information website like the
  paper companion websites referenced in the Kimi-Claw documentation.

## Output

- Code meeting the stated project completion criteria
- Evaluation results with plots
- Complete documentation
- Reproducible environment
- A numbered dissemination plan with prerequisites and recommended order

## Rules

1. Do not add new features during wrapup.
2. Run the final verification/evaluation required by the spec and available
   resources; state anything not run.
3. Generate requested or evidence-relevant plots and metrics.
4. Document known limitations honestly.
5. Ensure someone else can reproduce the results.
6. Recommend outward-facing actions, but do not publish or post without the
   user's approval of the content and action.
