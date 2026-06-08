---
name: 13e_retrospective_finalizer
description: Consolidate Stage 13 retrospective artifacts, validate evidence-backed findings, prepare result.md and context_packet.md, record N/A cases, and present the final human approval gate.
stage: 13 Workflow Retrospective & Skill Improvement
parent_skill: /skills/13_workflow_retrospective/SKILL.md
subskill_id: 13e
subskill_order: 5
previous_subskill: /skills/13_workflow_retrospective/13d_skill_improvement_backlog/SKILL.md
next_subskill: null
version: 1.0.0
status: draft
primary_output: /workflow/13_retrospective/result.md
requires_human_approval: true
external_visibility: internal
---

# 13e Retrospective Finalizer

## 1. Purpose

This sub-skill finalizes Stage 13.

It consolidates the outputs from `13a` through `13d`, checks consistency, records N/A cases, updates `result.md`, updates `context_packet.md` for the next workflow action, and presents the final human approval gate.

It does not approve workflow changes and does not revise reusable SKILL files.

## 2. Core Question

```text
Are the Stage 13 retrospective artifacts complete, evidence-backed, internally consistent, ready for human review, and safe to use as the basis for approved workflow improvement work?
```

## 3. Required Inputs

### Always Read

```text
/workflow/13_retrospective/13_workflow_retrospective.md
/workflow/13_retrospective/13_agent_failure_patterns.md
/workflow/13_retrospective/13_skill_improvement_backlog.md
/workflow/13_retrospective/13_reusable_lessons.md
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/13_retrospective/USER_DIRECTIVES.md, if it exists
```

### Read If Applicable

```text
/workflow/13_retrospective/13_prompt_ambiguity_report.md
/workflow/13_retrospective/13_context_management_review.md
/workflow/13_retrospective/13_human_intervention_log.md
/workflow/13_retrospective/13_tooling_limits.md
/workflow/13_retrospective/13_skill_split_candidates.md
/workflow/13_retrospective/13_next_workflow_experiment_plan.md
```

Read conditional artifacts if prior sub-skills created them or marked them as required.

### Do Not Read By Default

```text
- raw logs;
- source code;
- secrets or credentials;
- all workflow artifacts beyond those already used;
- all reusable SKILL files unless needed to check an explicitly referenced affected skill path.
```

## 4. Input Preflight Procedure

```text
[ ] Confirm 13a through 13d have run or equivalent artifacts exist.
[ ] Check mandatory Stage 13 artifacts exist.
[ ] Check conditional artifacts that were triggered.
[ ] Identify missing artifacts and decide whether finalization can proceed.
[ ] Check that high-priority backlog items are evidence-backed.
[ ] Check that weak findings are marked as hypotheses.
[ ] Check that recommendations are not recorded as approved decisions.
[ ] Check that no product requirements, architecture changes, or code tasks were created.
```

## 5. Execution Procedure

### Step 1. Consolidate Official Artifacts

Review and align:

```text
/workflow/13_retrospective/13_workflow_retrospective.md
/workflow/13_retrospective/13_agent_failure_patterns.md
/workflow/13_retrospective/13_skill_improvement_backlog.md
/workflow/13_retrospective/13_reusable_lessons.md
```

Check that:

```text
- scope and evidence level are consistent;
- findings match evidence level;
- failure patterns are not overclaimed;
- reusable lessons are separated from project-specific lessons;
- backlog items link to evidence and validation methods;
- skill lifecycle recommendations are marked as needing approval;
- open questions and assumptions are not hidden.
```

### Step 2. Resolve Internal Contradictions

If artifacts conflict:

```text
1. Identify the conflicting sections.
2. State the conflict.
3. Prefer approved evidence over assumptions.
4. If conflict cannot be resolved safely, mark it as an open question.
5. Do not silently delete inconvenient evidence.
```

### Step 3. Record N/A Cases

For each conditional artifact not created, record:

```text
Artifact:
Why Not Applicable:
Revisit If:
```

N/A records may be placed in `result.md`.

### Step 4. Prepare `result.md`

Create or update:

```text
/workflow/13_retrospective/result.md
```

Use the required structure in Section 6.

### Step 5. Update Context Files

Update or prepare:

```text
/workflow/context/context_packet.md
/workflow/context/ASSUMPTIONS.md, if needed
/workflow/context/OPEN_QUESTIONS.md, if needed
/workflow/context/REJECTED_OPTIONS.md, if needed
/workflow/context/TRACEABILITY_MATRIX.md, if meta-level traceability links were introduced
```

Do not update `/workflow/context/DECISIONS.md` unless the human has explicitly approved a workflow improvement decision.

### Step 6. Prepare Next Action

Classify the recommended next action as one of:

```text
- execute approved skill improvement tasks;
- revise selected workflow templates;
- start next project intake with approved lessons;
- archive project workflow artifacts;
- gather missing evidence and rerun part of Stage 13;
- run a next workflow experiment.
```

### Step 7. Present Final Human Approval Gate

List all items requiring approval.

## 6. Output Artifacts

### Mandatory Artifacts to Finalize

```text
/workflow/13_retrospective/13_workflow_retrospective.md
/workflow/13_retrospective/13_agent_failure_patterns.md
/workflow/13_retrospective/13_skill_improvement_backlog.md
/workflow/13_retrospective/13_reusable_lessons.md
/workflow/13_retrospective/result.md
/workflow/context/context_packet.md
```

### `result.md` Required Structure

```markdown
# Result: 13 Workflow Retrospective

## 1. Task Summary

## 2. Inputs Used

## 3. Outputs Created or Updated

## 4. Retrospective Scope

## 5. Key Findings

## 6. Agent Failure Patterns Identified

## 7. Reusable Lessons Extracted

## 8. Skill Improvement Backlog Summary

## 9. Decision Candidates

## 10. Working Assumptions

## 11. Open Questions

## 12. Risks and Constraints

## 13. N/A Records for Conditional Artifacts

## 14. Traceability Updates

## 15. Human Approval Required

## 16. Recommended Next Step
```

### `context_packet.md` Required Structure

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 13 Workflow Retrospective & Skill Improvement
- Completed stages:
- Next recommended action:

## 2. Approved Decisions
- Only human-approved workflow or project decisions.

## 3. Working Assumptions
- Retrospective assumptions not yet confirmed.

## 4. Open Questions
- Questions affecting future workflow or skill revision.

## 5. Rejected / Superseded Options
- Workflow or skill options that should not be reused unless reopened.

## 6. Constraints That Must Not Be Violated
- Workflow:
- Skill design:
- Artifact contract:
- Security/privacy:
- Tooling:
- Project-specific:

## 7. Key Context for Next Action
- Minimal context needed to revise skills or start the next project.

## 8. Required Inputs for Next Action
- Approved retrospective artifacts.
- Approved skill improvement priorities.
- Affected SKILL.md or template files.

## 9. Do Not Do
- Do not treat unapproved improvement suggestions as approved workflow changes.
- Do not modify reusable skills without explicit approval.
```

## 7. Traceability Rules

Verify meta-level links:

```text
Retrospective Finding → Evidence Source
Failure Pattern → Affected Stage / Skill
Failure Pattern → Skill Improvement Backlog Item
Reusable Lesson → Future Workflow Rule or Template Change
Skill Improvement Backlog Item → Validation Method
```

Use stable IDs:

```text
RF-001, RF-002      Retrospective Finding
AFP-001, AFP-002    Agent Failure Pattern
RL-001, RL-002      Reusable Lesson
SIB-001, SIB-002    Skill Improvement Backlog Item
```

Do not break existing product traceability IDs.

## 8. Decision / Assumption / Open Question Rules

In the final result, clearly separate:

```text
Approved Decision: Only explicit human-approved workflow or project decisions.
Decision Candidate: Proposed workflow or skill change awaiting approval.
Working Assumption: Temporary retrospective assumption.
Open Question: Missing evidence or unresolved policy issue.
Rejected Option: Explicitly rejected or superseded workflow option.
Recommendation: Suggested next action not yet approved.
```

Do not write skill improvement decisions into `DECISIONS.md` without explicit approval.

## 9. Validation Checklist

```text
[ ] All mandatory Stage 13 artifacts exist or missing artifacts are reported.
[ ] Conditional artifacts have either been created or recorded as N/A.
[ ] Retrospective scope is stated.
[ ] Evidence sources and limitations are listed.
[ ] Findings are evidence-backed or marked as hypotheses.
[ ] Agent strengths and failure patterns are separated.
[ ] P0/P1 backlog items have evidence and validation methods.
[ ] Reusable lessons and project-specific lessons are separated.
[ ] Skill lifecycle recommendations require approval.
[ ] context_packet.md prepares the next action.
[ ] No product requirements, architecture changes, or implementation tasks were silently created.
[ ] No reusable SKILL.md files were modified.
[ ] Final human approval gate is present.
```

## 10. Failure Handling

If finalization cannot be completed safely, produce a blocker report in `result.md`:

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
- ...

### Affected Artifacts or Stages
- ...

### Safe Partial Work Completed
- ...

### Retrospective Findings That Are Only Hypotheses
- ...

### Human Decision Needed
- ...
```

Common blockers:

```text
- mandatory Stage 13 artifacts are missing;
- Stage 12 outputs are missing but final release retrospective was requested;
- artifact_manifest.yml conflicts with approval logs;
- high-priority findings lack evidence;
- USER_DIRECTIVES.md conflicts with approved workflow decisions;
- raw logs contain sensitive data and cannot be safely reviewed.
```

## 11. Human Approval Gate

The final output must end with:

```markdown
## Human Approval Required

### Retrospective Findings to Accept
- ...

### Skill Improvement Priorities to Approve
- ...

### SKILL Revision Candidates to Approve
- ...

### New SKILL Creation Candidates to Approve
- ...

### Skill Split / Merge / Deprecation Candidates to Approve
- ...

### Workflow Policy Changes to Approve
- ...

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Risks to Review
- ...

### Artifacts Ready for Review
- /workflow/13_retrospective/13_workflow_retrospective.md
- /workflow/13_retrospective/13_agent_failure_patterns.md
- /workflow/13_retrospective/13_skill_improvement_backlog.md
- /workflow/13_retrospective/13_reusable_lessons.md
- /workflow/13_retrospective/result.md

### Recommended Next Step
- ...
```

## 12. Do Not Do

The Agent must not:

```text
- claim retrospective artifacts are approved;
- claim workflow improvements have been implemented;
- revise SKILLs, templates, or artifact contracts;
- update DECISIONS.md without explicit human approval;
- hide evidence gaps;
- overclaim weak findings;
- create product requirements or implementation tasks;
- let future stages depend on internal sub-skill outputs;
- skip the final human approval gate.
```
