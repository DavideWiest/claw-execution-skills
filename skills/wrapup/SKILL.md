---
name: wrapup
description: Use when a task arc is complete or a project is working and needs evaluation, cleanup, documentation, artifacts, or a publication plan.
---

# Execution Wrapup

## Purpose
Make the completed task arc or project defensible, reproducible, publishable,
and easy to reuse.

## Principles

- Wrap up each completed task arc before treating it as done; keep the scale of
  cleanup, documentation, and dissemination proportional to the arc.
- Do not expand the project's claims or scope during wrapup.
- Readers will usually be unfamiliar with the project. Separate internal
  knowledge, jargon, design choices, and development environment details from
  what a reader needs to understand the result.

## Workflow

### Task Arc Wrapup

- Clean the repository: lint and format as appropriate, remove debug or dead
  code and abandoned outputs, and make small reusability improvements that do
  not expand the project's claims or scope.
- Complete the evaluation required by the specification; for ML projects this
  may include full-scale training/validation.
- Generate plots or visualizations required to interpret or present results,
  storing deliverables and agent-produced artifacts in
  `<project-dir>/docs/<task-arc>/artifacts/`.
- Add missing required metrics and reporting.
- If the arc used iteration on a measurable metric, especially through
  `autoresearch-loop`, create a progress plot from
  `docs/<task-arc>/progress.md`: metric value over iteration time, with time on
  the x axis. Use `sci-scientific-visualization`, store it in
  `docs/<task-arc>/artifacts/`, and link it from the final progress entry. If
  the progress file lacks enough structured metric data, record that limitation
  instead of inventing values.
- Write final README and documentation, including limitations and how claims
  are supported.
- Ensure reproducibility (pinned dependencies, seed values, runnable checks).
- Extract practical, theoretical, or methodological insights from the arc.
  Use `knowledge-organization` only for selective cross-project conclusions,
  research directions, or resources that were both reusable and significantly
  helpful; link to project artifacts rather than copying them into the vault.
- Add or update the top row of
  `$VAULT_PATH/Knowledge/task-arc-reflection-log.md` with: task arc, project,
  status (`DONE`, `FAILED`, `SUPERSEDED`, `PARTIAL`, or `ABANDONED`), start
  time, time spent, feedback, worth it, and one-phrase core learning.

### Project Wrapup

- When wrapping up a whole project rather than one task arc, think about making
  it usable by others, especially if it may be published or become a package.
  The biggest factor is ease of use: installation, first run, configuration,
  examples, and reproducibility should require minimal guesswork.
- Make results, evidence, and work more visible. Upload or link important
  artifacts where appropriate, inspect plots before presenting them, and make
  plots more meaningful or visually clear when the evidence deserves it.
- Polish the README with `write-readme-writing`: put the most important thing for
  newcomers at the top, show the result or improvement rather than merely
  describing it, lead with the strongest material, move secondary details later,
  and omit reader-irrelevant internal history.
- For research-like outputs, consider whether a preprint server, DOI, Zenodo
  archive, or similar durable artifact route exists. Add a citation code block
  near the bottom of the README, but not so far down that readers miss it.
- Give the user a recommended numbered publishing/publicity plan whose scope
  matches the size and maturity of the endeavor. A small internal result may
  warrant a short visibility recommendation; a mature research contribution
  may warrant an article on the personal website, arXiv/preprint release,
  posts on X and LinkedIn, and a dedicated project information website/paper companion website.

## Output

- Code meeting the stated project completion criteria
- Evaluation results with plots
- Complete documentation
- Reproducible environment
- Updated `$VAULT_PATH/Knowledge/task-arc-reflection-log.md`
- A numbered dissemination plan with prerequisites and recommended order

## Rules

1. Do not add new features during wrapup.
2. Run the final verification/evaluation required by the spec and available
   resources; state anything not run.
3. Generate requested or evidence-relevant plots and metrics.
4. Document known limitations honestly.
5. Ensure someone else can reproduce the results.
6. Insert new task-arc reflection rows at the top of the log table.
7. Recommend outward-facing actions, but do not publish or post without the
   user's approval of the content and action.
