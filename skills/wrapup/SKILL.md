---
name: wrapup
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
  `<project-dir>/docs/<task-arc>/artifacts/`.
- Add missing required metrics and reporting.
- Write final README and documentation, including limitations and how claims
  are supported.
- Ensure reproducibility (pinned dependencies, seed values, runnable checks).
- Use `knowledge-organization` to capture durable cross-project conclusions or
  research directions, linking to project artifacts rather than copying them
  into the vault.
- Give the user a recommended numbered publishing/publicity plan whose scope
  matches the size and maturity of the endeavor. A small internal result may
  warrant a short visibility recommendation; a mature research contribution
  may warrant an article on the personal website, arXiv/preprint release,
  posts on X and LinkedIn, and a dedicated project information website like
  the paper companion websites referenced in the Kimi-Claw documentation.

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

## Writing text and documentation

Always be aware that readers will usually be unfamiliar with the project. 
Separate internal knowledge, jargon, internal design choices and development 
environment, from things relevant to the reader.
For `REAMDE.md`, use a pyramidal structure (most relevant things first, 
progressively add more detail in dedicated sections), since the reader has 
limited attention and time. Hence, the core message (finding, story, 
relevance) should be at the top. Do not overuse tables. 1-2 in the README 
should suffice. Do not use tables or text-based artifacts as a replacement 
for clear writing and a clear red thread. Instead, treat them as place for 
concrete numbers and evidence. Make them minimal, i.e. delete unnecessary
columns. 
See the other writing skills for more information.
