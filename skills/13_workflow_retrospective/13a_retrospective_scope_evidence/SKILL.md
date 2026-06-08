---
name: 13a_retrospective_scope_evidence
description: Define the Stage 13 retrospective scope, evidence map, evidence limits, and initial retrospective frame before any workflow conclusions are drawn.
stage: 13 Workflow Retrospective & Skill Improvement
parent_skill: /skills/13_workflow_retrospective/SKILL.md
subskill_id: 13a
subskill_order: 1
previous_subskill: null
next_subskill: /skills/13_workflow_retrospective/13b_stage_workflow_review/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/13_retrospective/13_workflow_retrospective.md
requires_human_approval: true
external_visibility: internal
---

# 13a Retrospective Scope and Evidence

## 1. Purpose

This sub-skill defines the retrospective scope and evidence map for Stage 13.

It must prevent the Agent from making unsupported workflow conclusions by first establishing:

```text
- retrospective type;
- included and excluded stages;
- release, milestone, or failed run being reviewed;
- evidence sources available;
- evidence sources missing;
- whether conclusions can be findings or only hypotheses.
```

## 2. Core Question

```text
What evidence is available, what workflow period is being reviewed, and how strong can the retrospective conclusions safely be?
```

## 3. Required Inputs

### Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/13_retrospective/USER_DIRECTIVES.md, if it exists
/workflow/12_review_release_handoff/result.md, if it exists
```

### Read If Applicable

```text
/workflow/00_intake/result.md through /workflow/12_review_release_handoff/result.md
- if the retrospective covers all completed stages.

/workflow/*/review_notes.md
- if stage-specific human review feedback exists.

agent_session_logs/*
ci_reports/*
incident_reports/*
cost_or_usage_reports/*
- only if explicitly provided or referenced by the user and safe to inspect.
```

### Do Not Read By Default

```text
- raw source code files;
- secrets or credentials;
- full raw Agent chat transcripts;
- full stage artifacts unless result summaries are missing or insufficient;
- superseded or rejected artifacts unless needed to understand drift;
- product documents unrelated to workflow execution.
```

### Missing Input Handling

If Stage 12 outputs are missing, classify the retrospective as a milestone, mid-project, failed-run, or skill-template evaluation retrospective rather than a final release retrospective.

If approval status is unknown, do not treat artifacts as approved source of truth.

If evidence is too thin, create a partial evidence map and mark later conclusions as hypotheses unless stronger evidence is supplied.

## 4. Input Preflight Procedure

Before writing outputs:

```text
[ ] Confirm this is Stage 13.
[ ] Determine retrospective type.
[ ] Check artifact_manifest.yml if available.
[ ] Check completed, skipped, partial, and approved stages.
[ ] Check USER_DIRECTIVES.md if available.
[ ] Identify available stage result summaries.
[ ] Identify unavailable, draft, superseded, rejected, or conflicting inputs.
[ ] Define evidence strength: Strong, Moderate, Weak, or Insufficient.
[ ] State scope before drawing conclusions.
```

## 5. Execution Procedure

1. Restate the retrospective purpose and scope.
2. Classify the retrospective as one of:
   - final project retrospective;
   - post-release retrospective;
   - post-milestone retrospective;
   - mid-project workflow checkpoint;
   - failed-run retrospective;
   - skill-template evaluation retrospective.
3. Identify included and excluded stages.
4. Identify whether Stage 12 review/release/handoff artifacts are available.
5. Build an evidence source inventory.
6. Classify each evidence source by status:
   - Available / Approved;
   - Available / Draft;
   - Missing;
   - Superseded;
   - Rejected;
   - Conflicting;
   - Unsafe to inspect.
7. Define evidence limitations.
8. Identify retrospective questions that can be answered now.
9. Identify retrospective questions that must remain open.
10. Prepare the initial sections of `/workflow/13_retrospective/13_workflow_retrospective.md`.
11. Update or prepare local handoff notes for `13b_stage_workflow_review`.

## 6. Output Artifacts

### Mandatory Artifact Updates

Update or create:

```text
/workflow/13_retrospective/13_workflow_retrospective.md
```

Required sections to create or update:

```markdown
# 13 Workflow Retrospective

## 1. Retrospective Scope
- Retrospective type:
- Included stages:
- Excluded stages:
- Release or milestone reviewed:
- Evidence level:

## 2. Evidence Sources Reviewed
| Source | Status | Used For | Limitations |
|---|---|---|---|

## 3. Executive Summary
- Initial summary:
- Evidence strength:
- Main evidence gaps:
- Findings that must remain hypotheses:
```

### Internal Handoff

Prepare a concise handoff for the next sub-skill, either in the stage artifact or in the sub-skill result section:

```text
Scope for stage-by-stage review:
Evidence sources to trust:
Evidence sources to treat as draft:
Stages needing deeper review:
Do not infer:
```

## 7. Traceability Rules

Use these IDs if creating findings:

```text
RF-001, RF-002     Retrospective Finding candidates
```

At this stage, findings should usually be preliminary. Link each finding candidate to an evidence source.

Do not create Agent Failure Pattern IDs here unless the evidence clearly belongs to later `13c_agent_failure_pattern_analysis`.

## 8. Decision / Assumption / Open Question Rules

Classify carefully:

```text
Decision Candidate: Recommended retrospective scope or evidence interpretation requiring human approval.
Working Assumption: Temporary assumption about missing evidence or artifact status.
Open Question: Missing information that affects retrospective conclusions.
Risk: A conclusion may be overgeneralized from insufficient evidence.
```

Do not update `/workflow/context/DECISIONS.md` unless explicit human approval exists.

## 9. Validation Checklist

```text
[ ] Retrospective type is stated.
[ ] Included and excluded stages are listed.
[ ] Evidence sources are inventoried.
[ ] Evidence limitations are explicit.
[ ] Missing evidence is listed.
[ ] Draft, superseded, rejected, and conflicting sources are not treated as approved truth.
[ ] Later sub-skills have clear review scope.
```

## 10. Human Approval Gate

Ask the human to review only the scope and evidence frame at this sub-skill boundary if needed:

```markdown
## Human Approval Required

### Retrospective Scope to Confirm
- ...

### Evidence Sources to Accept
- ...

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Recommended Next Step
- Run `13b_stage_workflow_review` after scope is acceptable.
```

## 11. Do Not Do

The Agent must not:

```text
- draw final workflow conclusions before evidence is mapped;
- treat missing logs as proof that work was not done;
- treat draft artifacts as approved source of truth;
- read raw logs, secrets, or full transcripts by default;
- rewrite SKILLs or templates;
- create product requirements, architecture changes, or implementation tasks.
```
