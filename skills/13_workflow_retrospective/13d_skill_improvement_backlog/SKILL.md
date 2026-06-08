---
name: 13d_skill_improvement_backlog
description: Convert evidence-backed retrospective findings and Agent behavior patterns into reusable lessons, prioritized skill improvement backlog items, and skill lifecycle recommendations.
stage: 13 Workflow Retrospective & Skill Improvement
parent_skill: /skills/13_workflow_retrospective/SKILL.md
subskill_id: 13d
subskill_order: 4
previous_subskill: /skills/13_workflow_retrospective/13c_agent_failure_pattern_analysis/SKILL.md
next_subskill: /skills/13_workflow_retrospective/13e_retrospective_finalizer/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/13_retrospective/13_skill_improvement_backlog.md
requires_human_approval: true
external_visibility: internal
---

# 13d Skill Improvement Backlog

## 1. Purpose

This sub-skill converts Stage 13 findings into reusable lessons and a prioritized improvement backlog for workflow SKILLs, templates, artifact contracts, context rules, approval gates, and tool wrappers.

It does not execute the improvements. It prepares them for human review and approval.

## 2. Core Question

```text
Which evidence-backed findings should become reusable lessons, workflow rules, SKILL revisions, split/merge/deprecation candidates, or new SKILL creation backlog items?
```

## 3. Required Inputs

### Always Read

```text
/workflow/13_retrospective/13_workflow_retrospective.md
/workflow/13_retrospective/13_agent_failure_patterns.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/13_retrospective/USER_DIRECTIVES.md, if it exists
```

### Read If Applicable

```text
/skills/*/SKILL.md
- only for affected reusable skills explicitly identified by findings or USER_DIRECTIVES.

/workflow_templates/stages/*_skill_template.md
- only for affected templates explicitly identified by findings or USER_DIRECTIVES.

/workflow_templates/core/core_skill_template.md
- if findings affect core rules.

/workflow_templates/specializations/*.md
- if findings affect project-type specialization hooks.

/workflow_templates/tool_wrappers/*.md
- if findings affect tool-specific execution behavior.
```

Only inspect the relevant reusable skill or template files needed to identify affected locations. Do not rewrite them in this sub-skill.

### Do Not Read By Default

```text
- all skill files;
- all workflow templates;
- source code files;
- raw Agent logs;
- secrets or private notes;
- product artifacts not connected to a retrospective finding.
```

## 4. Input Preflight Procedure

```text
[ ] Read retrospective findings.
[ ] Read Agent failure patterns.
[ ] Identify evidence-backed findings vs hypotheses.
[ ] Identify affected skills/templates/contracts.
[ ] Check rejected workflow options before proposing improvements.
[ ] Avoid proposing improvements that revive rejected options unless reopened.
[ ] Decide whether affected reusable skill files need inspection.
```

## 5. Execution Procedure

### Step 1. Extract Reusable Lessons

Convert observations into lessons and classify each as:

```text
- reusable workflow rule;
- reusable prompt / SKILL design rule;
- reusable artifact contract lesson;
- reusable context management lesson;
- reusable approval gate lesson;
- reusable validation lesson;
- reusable DDD/domain lesson;
- reusable security/privacy lesson;
- project-specific lesson not yet generalized;
- tool-specific lesson.
```

Do not overgeneralize weak evidence.

### Step 2. Identify Candidate Improvements

For each evidence-backed issue, identify possible improvement type:

```text
- revise existing SKILL;
- split large SKILL;
- merge overlapping SKILLs;
- deprecate obsolete SKILL;
- create new SKILL;
- revise stage template;
- revise artifact contract;
- revise context_packet rules;
- revise approval gate;
- add specialization hook;
- add tool wrapper note;
- add human operating practice.
```

### Step 3. Create Backlog Items

For each improvement item, include:

```text
Backlog ID:
Affected Skill or Template:
Problem Observed:
Evidence Source:
Root Cause Hypothesis:
Recommended Change:
Expected Benefit:
Risk of Change:
Priority:
Effort:
Owner:
Validation Method:
Approval Required:
```

Priority definitions:

```text
P0: Blocks safe workflow use
P1: Causes repeated rework or serious ambiguity
P2: Improves reliability or reviewability
P3: Nice-to-have refinement
```

### Step 4. Create Skill Lifecycle Recommendations

Classify affected skills as:

```text
Keep
Revise
Split
Merge
Deprecate
Create New
Needs More Evidence
```

A recommendation to revise, split, merge, delete, or create a SKILL is not approved until the human explicitly approves it.

### Step 5. Define Validation Method for Each Improvement

Examples:

```text
- apply to one pilot project and compare review friction;
- rerun affected stage with revised SKILL and check artifact quality;
- validate that required inputs are clearer;
- confirm conditional artifacts and N/A records are generated;
- measure reduction in human correction count;
- verify no downstream dependency on sub-skill internals.
```

### Step 6. Prepare Finalizer Handoff

Identify:

```text
- top P0/P1 backlog items;
- items requiring human approval;
- items needing more evidence;
- possible skill split candidates;
- reusable lessons ready for approval;
- project-specific lessons not yet generalized.
```

## 6. Output Artifacts

Create or update:

```text
/workflow/13_retrospective/13_skill_improvement_backlog.md
/workflow/13_retrospective/13_reusable_lessons.md
```

### `13_skill_improvement_backlog.md` Structure

```markdown
# 13 Skill Improvement Backlog

## 1. Backlog Summary

## 2. Priority Definitions
- P0:
- P1:
- P2:
- P3:

## 3. Backlog Items
| ID | Priority | Affected Skill / Template | Problem | Recommended Change | Validation Method | Approval Required |
|---|---|---|---|---|---|---|

## 4. Detailed Backlog Items

### SIB-001: [[Short Title]]
- Priority:
- Affected skill/template:
- Related stage:
- Problem observed:
- Evidence source:
- Root cause hypothesis:
- Recommended change:
- Expected benefit:
- Risk of change:
- Effort:
- Owner:
- Validation method:
- Approval required:

## 5. Skill Lifecycle Recommendations
| Skill | Recommendation | Reason | Evidence | Approval Required |
|---|---|---|---|---|
```

### `13_reusable_lessons.md` Structure

```markdown
# 13 Reusable Lessons

## 1. Reusable Workflow Rules

## 2. Reusable Prompt / SKILL Design Rules

## 3. Reusable Artifact Contract Lessons

## 4. Reusable Context Management Lessons

## 5. Reusable Approval Gate Lessons

## 6. Reusable Testing / Validation Lessons

## 7. Reusable DDD / Domain Lessons

## 8. Reusable Security / Privacy Lessons

## 9. Project-Specific Lessons Not Yet Generalized

## 10. Tool-Specific Lessons
```

Also update:

```text
/workflow/13_retrospective/13_workflow_retrospective.md
```

Required sections:

```markdown
## 14. Top Reusable Lessons
- Lesson 1:
- Lesson 2:
- Lesson 3:

## 15. Top Skill Improvement Priorities
| Priority | Skill / Template | Change Needed | Evidence | Approval Needed |
|---|---|---|---|---|

## 16. Open Questions
- ...
```

### Conditional Artifact Candidates

Create or mark for finalizer creation when applicable:

```text
/workflow/13_retrospective/13_skill_split_candidates.md
- if one or more SKILLs appear too large or internally mixed.

/workflow/13_retrospective/13_next_workflow_experiment_plan.md
- if improvements should be validated in a next pilot project.
```

## 7. Traceability Rules

Use IDs:

```text
RL-001, RL-002      Reusable Lesson
SIB-001, SIB-002    Skill Improvement Backlog Item
```

Required links:

```text
Reusable Lesson → Retrospective Finding or Agent Failure Pattern
Skill Improvement Backlog Item → Evidence Source
Skill Improvement Backlog Item → Affected Skill / Template
Skill Improvement Backlog Item → Validation Method
P0/P1 Backlog Item → At least one evidence source
```

Do not create product requirements or implementation tasks from retrospective findings.

## 8. Decision / Assumption / Open Question Rules

Classify:

```text
Decision Candidate: Proposed workflow or skill change requiring human approval.
Working Assumption: Root cause hypothesis or expected benefit not yet proven.
Open Question: Missing evidence or unresolved improvement policy.
Rejected Option: Improvement direction previously rejected by the human.
Recommendation: Suggested action not yet approved.
```

Do not update `DECISIONS.md` unless explicit human approval exists.

## 9. Validation Checklist

```text
[ ] Reusable lessons are separated from project-specific lessons.
[ ] Every P0/P1 backlog item has evidence and validation method.
[ ] Skill lifecycle recommendations are explicit.
[ ] Rejected options are not revived.
[ ] No SKILL files were modified.
[ ] No product requirements or implementation tasks were created.
[ ] Each recommended change requires approval unless already explicitly approved.
```

## 10. Human Approval Gate

```markdown
## Human Approval Required

### Reusable Lessons to Accept
- ...

### Skill Improvement Backlog Priorities to Approve
- ...

### Skill Lifecycle Recommendations to Approve
- ...

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Recommended Next Step
- Run `13e_retrospective_finalizer`.
```

## 11. Do Not Do

The Agent must not:

```text
- edit reusable SKILL.md files;
- edit templates or artifact contracts;
- treat backlog priority as approved;
- revive rejected options;
- create product work items;
- overgeneralize weak evidence;
- claim workflow improvement has occurred before approved changes are implemented and validated.
```
