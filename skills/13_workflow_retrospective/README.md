# 13 Workflow Retrospective & Skill Improvement

## What this SKILL package is for

This reusable Stage 13 package reviews a completed project, release, milestone, failed run, or workflow experiment and turns evidence-backed observations into reusable lessons and skill improvement backlog items.

It evaluates the Manual Agentic Coding Workflow itself. It does not revise product requirements, implementation code, or reusable `SKILL.md` files directly.

## When to use it

Use this package after Stage 12 review/release/handoff, after a major milestone, after a failed workflow run, or when you want to improve the workflow and reusable skills from real execution evidence.

It is also appropriate for a mid-project checkpoint when the workflow process is unstable and needs evidence-based adjustment.

## When not to use it

Do not use this package to perform code review, security review, deployment, product redesign, requirements rewriting, or direct SKILL editing. Those actions belong to earlier workflow stages or to a separate approved skill-revision task after Stage 13 findings are approved.

## Required inputs before running

At minimum, the Agent should check:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`
- `/workflow/12_review_release_handoff/result.md`, if this is a final or post-release retrospective
- `/workflow/13_retrospective/USER_DIRECTIVES.md`, if it exists

Only approved artifacts should be treated as source of truth. Draft artifacts may be used as evidence only when labeled as draft.

## Optional or conditional inputs

Use these only when relevant to the retrospective scope:

- `/workflow/00_intake/result.md` through `/workflow/12_review_release_handoff/result.md`
- `/workflow/*/review_notes.md`
- `/workflow/11_implementation_results/11_task_result_*.md`
- `/workflow/11_implementation_results/11_test_evidence_*.md`
- `agent_session_logs/*`, only if explicitly provided and safe to inspect
- `ci_reports/*`, `incident_reports/*`, or `cost_or_usage_reports/*`, if available and relevant

Do not inspect secrets, credentials, private keys, or raw private logs.

## Sub-SKILL execution order

Run the sub-SKILLs in this order:

13a. `13a_retrospective_scope_evidence` — Defines retrospective scope, included and excluded stages, evidence sources, and evidence strength before conclusions are drawn.
13b. `13b_stage_workflow_review` — Reviews completed workflow stages, artifact quality, context handoff, approval gates, traceability, validation, DDD continuity, and security/privacy workflow behavior.
13c. `13c_agent_failure_pattern_analysis` — Identifies evidence-backed Agent strengths, repeated failure patterns, mixed patterns, one-off issues, insufficient evidence items, and human judgment points.
13d. `13d_skill_improvement_backlog` — Converts evidence-backed retrospective findings and Agent behavior patterns into reusable lessons, prioritized skill improvement backlog items, and skill lifecycle recommendations.
13e. `13e_retrospective_finalizer` — Consolidates Stage 13 retrospective artifacts, validates evidence-backed findings, prepares result.md and context_packet.md, records N/A cases, and presents the final human approval gate.

The parent `SKILL.md` is the stage entrypoint and orchestrator. The finalizer must run before Stage 13 artifacts are considered ready for human approval.

## Outputs created when the SKILL is executed

Mandatory official Stage 13 outputs:

- `/workflow/13_retrospective/13_workflow_retrospective.md` — Workflow retrospective scope, evidence map, stage-by-stage review, and cross-cutting findings.
- `/workflow/13_retrospective/13_agent_failure_patterns.md` — Evidence-backed analysis of Agent strengths, failure patterns, one-off issues, and human judgment points.
- `/workflow/13_retrospective/13_skill_improvement_backlog.md` — Prioritized skill improvement backlog and skill lifecycle recommendations.
- `/workflow/13_retrospective/13_reusable_lessons.md` — Reusable lessons for future workflow, prompt, artifact, context, approval, testing, DDD, security, privacy, and tooling improvements.
- `/workflow/13_retrospective/result.md` — Final Stage 13 summary, N/A records, traceability updates, and approval gate.
- `/workflow/context/context_packet.md` — Minimal context for approved skill revision work, workflow experiments, or the next project intake.

Conditional outputs:

- `/workflow/13_retrospective/13_prompt_ambiguity_report.md` — if Prompt ambiguity or SKILL wording ambiguity repeatedly affected execution.
- `/workflow/13_retrospective/13_context_management_review.md` — if Context reset, handoff, or context_packet problems affected execution.
- `/workflow/13_retrospective/13_human_intervention_log.md` — if Human correction, rejection, approval, or intervention patterns require focused analysis.
- `/workflow/13_retrospective/13_tooling_limits.md` — if Tool limits, sandbox constraints, context limits, or command failures affected outcomes.
- `/workflow/13_retrospective/13_skill_split_candidates.md` — if A SKILL should be split, merged, deleted, or created based on retrospective findings.
- `/workflow/13_retrospective/13_next_workflow_experiment_plan.md` — if Workflow changes should be tested before becoming reusable rules.

Conditional artifacts that are not applicable must be recorded with an N/A rationale in `result.md`.

## Human approval requirements

Human approval is required before any Stage 13 finding becomes an approved workflow decision or before any SKILL is revised, split, merged, deleted, or created.

The approval gate should include:

- retrospective findings to approve
- skill improvement priorities to approve
- assumptions to confirm
- open questions to resolve
- risks to review
- artifacts ready for review
- recommended next action

## How to run the SKILL in an Agentic Coding tool

1. Start from `/skills/13_workflow_retrospective/SKILL.md`.
2. Confirm the retrospective scope and available evidence.
3. Run sub-SKILLs `13a` through `13e` in order.
4. Keep all project artifacts under `/workflow/13_retrospective/` and `/workflow/context/`.
5. Do not depend on chat history; use files as the source of truth.
6. After `13e`, review the approval gate before executing any skill improvement work.

## Relationship to previous and next stages

Previous stage: `12_review_release_handoff`.

Stage 13 consumes release, handoff, implementation, validation, approval, and workflow evidence. It prepares the next workflow improvement action, a follow-up skill-revision task, or the next project intake. There is no normal Stage 14.

Downstream improvement work must depend on approved official Stage 13 artifacts, not internal sub-SKILL outputs.

## How to interpret status values

- `Draft`: created by the Agent and not yet approved.
- `Needs Review`: ready for human inspection but not approved.
- `Approved`: explicitly approved by the human developer.

Agent output is not approval.

## Common mistakes to avoid

- Treating retrospective suggestions as approved skill revisions.
- Updating reusable `SKILL.md` files during the retrospective.
- Reading all historical artifacts by default.
- Drawing conclusions before defining evidence scope.
- Overgeneralizing one-off Agent behavior into a repeated failure pattern.
- Confusing tool limitations with SKILL design failures.
- Letting downstream work depend on internal sub-SKILL artifacts.

## Troubleshooting / blocker cases

If Stage 12 outputs are missing, run Stage 13 as a milestone, failed-run, or skill-template retrospective instead of a final release retrospective.

If approval status is unclear, label sources as draft or uncertain and avoid treating findings as approved.

If evidence is insufficient, produce a partial retrospective with hypotheses, evidence gaps, and human decision points.

If sub-SKILL outputs conflict, stop at the finalizer and report the conflict instead of merging them silently.

## Recommended next step after successful execution

After human approval, use the approved `13_skill_improvement_backlog.md` and `13_reusable_lessons.md` to plan a separate skill revision, split/merge, or workflow experiment task.
