---
name: 13_workflow_retrospective
description: Stage 13 entrypoint and orchestrator for a post-project, post-release, post-milestone, or mid-project retrospective that evaluates the Manual Agentic Coding Workflow and prepares approved skill improvement work.
stage: 13 Workflow Retrospective & Skill Improvement
version: 1.0.0
status: draft
primary_output: /workflow/13_retrospective/result.md
requires_human_approval: true
internal_split: true
---

# 13 Workflow Retrospective Stage Entrypoint

## 1. Purpose

This parent `SKILL.md` is the stage-level entrypoint for Stage 13: Workflow Retrospective & Skill Improvement.

The purpose of Stage 13 is to review the completed project, release, milestone, failed run, or workflow experiment and convert evidence-backed observations into reusable lessons and skill improvement backlog items.

This stage evaluates the workflow itself. It must not redesign the product, rewrite implementation code, or silently revise reusable `SKILL.md` files.

Core question:

```text
Which workflow, prompt, context, artifact, approval, validation, and Agent-behavior issues should be preserved, fixed, split, merged, removed, or promoted into reusable rules for future projects?
```

Key distinction:

```text
Agent retrospective finding ≠ approved workflow change
Agent improvement suggestion ≠ approved SKILL revision
```

## 2. Public Stage Contract

The public stage package is:

```text
/skills/13_workflow_retrospective/
```

This parent `SKILL.md` orchestrates internal sub-skills. Downstream workflow improvement work, future project intake, or archival handoff must depend only on approved official Stage 13 artifacts under `/workflow/13_retrospective/`, not on internal sub-skill folders, prompt history, or raw chat logs.

Official Stage 13 artifacts are not considered approved until the human developer explicitly approves them.

## 3. Internal Sub-Skill Sequence

Run the sub-skills in this order:

```text
13a_retrospective_scope_evidence
→ 13b_stage_workflow_review
→ 13c_agent_failure_pattern_analysis
→ 13d_skill_improvement_backlog
→ 13e_retrospective_finalizer
```

Sub-skill responsibilities:

```text
13a_retrospective_scope_evidence
- Define retrospective scope, evidence level, included/excluded stages, and evidence map.

13b_stage_workflow_review
- Review workflow stages, artifact quality, context handoff, approval gates, traceability, validation, DDD continuity, and security/privacy workflow behavior.

13c_agent_failure_pattern_analysis
- Identify Agent strengths, repeated failure patterns, one-off issues, insufficient evidence items, and human judgment points.

13d_skill_improvement_backlog
- Convert evidence-backed findings into reusable lessons, skill lifecycle recommendations, and prioritized skill improvement backlog items.

13e_retrospective_finalizer
- Consolidate all official artifacts, update `result.md`, prepare context handoff, record N/A cases, and present the final human approval gate.
```

## 4. Official Stage Artifacts

The Stage 13 package creates or updates these official artifacts:

```text
/workflow/13_retrospective/13_workflow_retrospective.md
/workflow/13_retrospective/13_agent_failure_patterns.md
/workflow/13_retrospective/13_skill_improvement_backlog.md
/workflow/13_retrospective/13_reusable_lessons.md
/workflow/13_retrospective/result.md
/workflow/context/context_packet.md
```

Conditional artifacts may be created by the relevant sub-skill or finalizer when applicable:

```text
/workflow/13_retrospective/13_prompt_ambiguity_report.md
/workflow/13_retrospective/13_context_management_review.md
/workflow/13_retrospective/13_human_intervention_log.md
/workflow/13_retrospective/13_tooling_limits.md
/workflow/13_retrospective/13_skill_split_candidates.md
/workflow/13_retrospective/13_next_workflow_experiment_plan.md
```

If a conditional artifact is not applicable, record an N/A entry in `/workflow/13_retrospective/result.md`.

## 5. Required Inputs

### Always Read at Stage Entry

When they exist, the stage must check:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/13_retrospective/USER_DIRECTIVES.md
/workflow/12_review_release_handoff/result.md
```

The sub-skills define additional always-read and conditional-read inputs for their local responsibilities.

### Read If Applicable at Stage Entry

```text
/workflow/00_intake/result.md through /workflow/12_review_release_handoff/result.md
- if the retrospective covers the full workflow or needs stage-by-stage analysis.

/workflow/11_implementation_results/11_task_result_*.md
/workflow/11_implementation_results/11_test_evidence_*.md
- if implementation behavior, TDD evidence, or validation discipline is in scope.

/workflow/*/review_notes.md
- if human review comments exist.

agent_session_logs/*
ci_reports/*
incident_reports/*
cost_or_usage_reports/*
- only if explicitly provided or referenced by the user and safe to inspect.
```

### Do Not Read By Default

Do not read these by default:

```text
- raw source code files;
- secrets, credentials, environment variable files, or private keys;
- full raw Agent chat logs;
- superseded artifacts unless needed for drift analysis;
- rejected artifacts unless reviewing why they were rejected;
- full stage artifacts when approved stage `result.md` summaries are sufficient;
- unrelated product documentation not used by the workflow.
```

## 6. USER_DIRECTIVES.md Handling

If `/workflow/13_retrospective/USER_DIRECTIVES.md` exists, every sub-skill must read it before execution.

Classify directives as:

```text
explicit approval
correction
retrospective focus area
skill improvement request
workflow policy preference
rejection
scope limitation
question to answer
additional evidence source
```

Rules:

```text
- Apply USER_DIRECTIVES before Agent assumptions.
- Do not treat every directive as a globally approved workflow change.
- If a directive conflicts with approved decisions or approval logs, report the conflict.
- Do not modify USER_DIRECTIVES.md unless explicitly instructed.
```

## 7. Execution Policy

This stage uses the Stage Facade Pattern.

Rules:

```text
1. The parent SKILL is an orchestrator, not the full retrospective procedure.
2. Sub-skills are internal execution units.
3. Sub-skill outputs remain draft until consolidated by the finalizer and reviewed by the human developer.
4. The finalizer must run before Stage 13 is considered ready for approval.
5. Official Stage 13 artifacts must remain under `/workflow/13_retrospective/`.
6. Do not create project-specific product requirements, architecture changes, database changes, implementation tasks, or code.
7. Do not revise reusable SKILL files unless the user explicitly asks for a separate revision task after approving the backlog.
```

## 8. Finalizer Requirement

The stage is not ready for downstream use until `13e_retrospective_finalizer` has run.

The finalizer must:

```text
- read the outputs from 13a through 13d;
- consolidate official Stage 13 artifacts;
- detect contradictions or unsupported claims;
- mark weak findings as hypotheses;
- ensure every P0/P1 backlog item has evidence and validation method;
- record N/A cases for skipped conditional artifacts;
- update `/workflow/13_retrospective/result.md`;
- update `/workflow/context/context_packet.md` for the next action;
- prepare the human approval gate.
```

## 9. Human Approval Gate

Human approval is required before:

```text
- accepting retrospective findings as official;
- prioritizing skill improvement backlog items;
- revising any reusable `SKILL.md`;
- changing a stage-specific template;
- modifying artifact contracts;
- deleting, merging, splitting, or creating SKILLs;
- applying lessons to the next project as required rules.
```

The final approval gate must list:

```text
Retrospective Findings to Accept
Skill Improvement Priorities to Approve
SKILL Revision Candidates to Approve
New SKILL Creation Candidates to Approve
Skill Split / Merge / Deprecation Candidates to Approve
Workflow Policy Changes to Approve
Assumptions to Confirm
Open Questions to Resolve
Risks to Review
Artifacts Ready for Review
Recommended Next Step
```

## 10. Downstream Handoff Rule

After human approval, the next action is one of:

```text
- execute approved SKILL improvement tasks;
- revise selected workflow templates;
- start the next project intake with approved lessons;
- archive the project workflow artifacts;
- run another retrospective iteration after missing evidence is supplied.
```

Do not let downstream work depend on:

```text
- internal sub-skill outputs not consolidated by the finalizer;
- unapproved improvement suggestions;
- raw Agent logs;
- prompt history;
- private user notes;
- unverified assumptions.
```

## 11. Do Not Do

The Agent must not:

```text
- collapse all sub-skills into one uncontrolled retrospective;
- rewrite SKILL.md files during this stage unless explicitly instructed;
- treat recommendations as approved workflow changes;
- infer repeated failure patterns from one weak example;
- create new product requirements from retrospective observations;
- change product scope, architecture, database, release, or implementation decisions;
- expose secrets or private data from logs;
- read all raw logs or chat transcripts by default;
- ignore missing evidence;
- update DECISIONS.md without explicit human approval;
- claim the workflow is improved merely because a backlog was created.
```
