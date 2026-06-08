---
name: 13b_stage_workflow_review
description: Review completed workflow stages, artifact quality, context handoff, approval gates, traceability, validation, DDD continuity, and security/privacy workflow behavior.
stage: 13 Workflow Retrospective & Skill Improvement
parent_skill: /skills/13_workflow_retrospective/SKILL.md
subskill_id: 13b
subskill_order: 2
previous_subskill: /skills/13_workflow_retrospective/13a_retrospective_scope_evidence/SKILL.md
next_subskill: /skills/13_workflow_retrospective/13c_agent_failure_pattern_analysis/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/13_retrospective/13_workflow_retrospective.md
requires_human_approval: true
external_visibility: internal
---

# 13b Stage Workflow Review

## 1. Purpose

This sub-skill reviews how the workflow stages performed as a structured development process.

It evaluates the stages, artifacts, context handoffs, approval gates, and cross-cutting practices without yet turning findings into skill backlog items.

## 2. Core Question

```text
Which stages, artifacts, handoffs, gates, and cross-cutting practices worked well or caused rework, ambiguity, risk, or loss of traceability?
```

## 3. Required Inputs

### Always Read

```text
/workflow/13_retrospective/13_workflow_retrospective.md
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/13_retrospective/USER_DIRECTIVES.md, if it exists
```

Also read the stage result summaries identified by `13a` as in scope:

```text
/workflow/00_intake/result.md
/workflow/01_goal/result.md
/workflow/02_stakeholders_risk/result.md
/workflow/03_requirements/result.md
/workflow/04_domain/result.md
/workflow/05_architecture/result.md
/workflow/06_data/result.md
/workflow/07_mvp_release/result.md
/workflow/08_test_strategy/result.md
/workflow/09_tasks/result.md
/workflow/10_prompts/result.md
/workflow/11_implementation_results/result.md
/workflow/12_review_release_handoff/result.md
```

Read only those that exist and are in scope.

### Read If Applicable

```text
/workflow/03_requirements/03_traceability_matrix.md
/workflow/04_domain/04_domain_traceability_matrix.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/12_review_release_handoff/12_release_readiness.md
/workflow/12_review_release_handoff/12_security_privacy_review.md
/workflow/*/review_notes.md
```

Read these when the corresponding review area is in scope or result summaries are insufficient.

### Do Not Read By Default

```text
- full raw implementation diffs;
- full source code;
- raw logs;
- secrets or environment files;
- every stage artifact if result summaries provide sufficient evidence.
```

## 4. Input Preflight Procedure

```text
[ ] Read the scope and evidence map from 13a.
[ ] Confirm which stages are in scope.
[ ] Confirm which stage result summaries exist.
[ ] Identify stages with missing or weak evidence.
[ ] Identify cross-cutting review areas activated by evidence or USER_DIRECTIVES.
[ ] Avoid reviewing excluded stages unless the user explicitly expands scope.
```

## 5. Execution Procedure

### Step 1. Stage-by-Stage Review

For each included stage, evaluate:

```text
- Was the stage run at the right time?
- Were required inputs available and approved?
- Were outputs concrete, reviewable, and useful?
- Were assumptions separated from decisions?
- Were open questions carried forward?
- Were rejected options preserved?
- Was the context handoff useful to the next stage?
- Was the approval gate clear?
- Did downstream stages use the correct source of truth?
- Did the stage create avoidable ambiguity or rework?
```

Record concise evidence-backed findings.

### Step 2. Artifact Quality Review

Assess:

```text
- concrete artifact structure;
- clarity of required sections;
- excessive verbosity or missing detail;
- source-of-truth clarity;
- reviewability by a human developer;
- consistency with artifact_manifest.yml;
- whether conditional artifacts had N/A records.
```

### Step 3. Context Handoff Review

Assess:

```text
- whether context_packet.md was useful as a navigation layer;
- whether it carried minimal operational context;
- whether it copied too much history;
- whether next-stage required inputs were clear;
- whether session reset tolerance was preserved;
- whether approved decisions were separated from assumptions.
```

### Step 4. Approval Gate Review

Assess:

```text
- gates that prevented mistakes;
- gates that were skipped;
- gates that were vague;
- decisions that were implied but not approved;
- areas where human approval should be earlier, later, stronger, or lighter.
```

### Step 5. Cross-Cutting Practice Review

Evaluate:

```text
- traceability from goals to implementation evidence;
- TDD or test-aware execution;
- DDD language and domain rule continuity;
- security and privacy awareness across stages;
- release and documentation handoff quality;
- context reset tolerance.
```

### Step 6. Prepare Handoff to Agent Failure Pattern Analysis

Summarize possible Agent behavior patterns for `13c`, but do not finalize failure pattern IDs unless clearly evidenced.

## 6. Output Artifact Updates

Update:

```text
/workflow/13_retrospective/13_workflow_retrospective.md
```

Required sections to add or revise:

```markdown
## 4. Stage-by-Stage Retrospective
| Stage | What Worked | Problems | Evidence | Improvement Candidate |
|---|---|---|---|---|

## 5. Artifact Quality Review
| Artifact Area | Strengths | Issues | Improvement |
|---|---|---|---|

## 6. Context Handoff Review
- Useful handoffs:
- Missing context:
- Excess context:
- Confusing source-of-truth cases:
- Context reset tolerance:

## 7. Approval Gate Review
- Gates that worked:
- Gates that were unclear:
- Gates that were skipped or weak:
- Approval rule improvements:

## 8. Traceability Review
- Traceability preserved:
- Traceability gaps:
- Broken or weak links:
- Recommended fixes:

## 9. TDD / Validation Review
- Test-first or test-aware successes:
- Validation gaps:
- Evidence quality:
- Future validation improvements:

## 10. DDD / Domain Continuity Review
- Domain language preserved:
- Domain drift:
- Invariant or rule gaps:
- Future DDD improvements:

## 11. Security / Privacy Review of the Workflow
- Early risks captured:
- Late-discovered issues:
- Security/privacy handoff gaps:
- Future security/privacy workflow improvements:
```

### Conditional Artifact Candidates

Create or mark for finalizer creation when needed:

```text
/workflow/13_retrospective/13_context_management_review.md
- if context handoff, artifact manifest, approval state, or session reset issues are extensive.

/workflow/13_retrospective/13_prompt_ambiguity_report.md
- if prompt ambiguity appears as a major workflow-stage issue.
```

## 7. Traceability Rules

Use or extend retrospective IDs:

```text
RF-001, RF-002      Retrospective Finding
```

Required links:

```text
Retrospective Finding → Evidence Source
Retrospective Finding → Affected Stage
Retrospective Finding → Candidate Improvement Area
```

Mark weakly supported findings as hypotheses.

## 8. Decision / Assumption / Open Question Rules

Do not approve workflow changes.

Classify:

```text
Decision Candidate: Candidate workflow rule or approval gate change.
Working Assumption: Assumption about why a stage issue occurred.
Open Question: Missing evidence or unresolved policy question.
Risk: Workflow risk if the issue repeats.
```

## 9. Validation Checklist

```text
[ ] Stage-by-stage review covers all included stages.
[ ] Excluded stages are not silently reviewed.
[ ] Findings cite evidence sources or are marked as hypotheses.
[ ] Artifact quality is reviewed.
[ ] Context handoff is reviewed.
[ ] Approval gates are reviewed.
[ ] Traceability, TDD, DDD, and security/privacy workflow behavior are reviewed.
[ ] Handoff to 13c identifies possible Agent behavior patterns.
```

## 10. Human Approval Gate

At this sub-skill boundary, ask for review only if stage findings are controversial or evidence is weak:

```markdown
## Human Approval Required

### Stage Review Findings to Check
- ...

### Assumptions to Confirm
- ...

### Evidence Gaps
- ...

### Recommended Next Step
- Run `13c_agent_failure_pattern_analysis`.
```

## 11. Do Not Do

The Agent must not:

```text
- turn workflow findings into approved skill changes;
- blame the human or Agent without evidence;
- read source code or raw logs by default;
- create product feature tasks;
- override approved decisions;
- overgeneralize a one-off stage issue.
```
