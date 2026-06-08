# 13 Workflow Retrospective SKILL Template

> Reusable stage-specific `SKILL.md` template for Stage 13 of the Manual Agentic Coding Workflow.  
> This template is used to create an executable `SKILL.md` for `13_workflow_retrospective`.  
> It does **not** execute the retrospective and does **not** create project artifacts by itself.

---

## 0. Template Scope

This template defines the reusable structure and stage-specific rules for creating a `SKILL.md` that runs:

```text
Stage 13: Workflow Retrospective & Skill Improvement
```

The purpose of this stage is to review the completed project or major release workflow, identify where the Agent and workflow succeeded or failed, and convert those observations into reusable skill and workflow improvements.

This template extends the Core Skill Template and must preserve these core principles:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent retrospective finding ≠ approved workflow change
Agent improvement suggestion ≠ approved SKILL revision
```

---

## 1. Recommended Metadata Template

Use the following metadata when creating the actual reusable `SKILL.md`.

```yaml
---
name: 13_workflow_retrospective
description: Run a post-project or post-release retrospective to evaluate the agentic coding workflow, identify agent failure patterns, extract reusable lessons, and prepare a skill improvement backlog.
stage: 13 Workflow Retrospective & Skill Improvement
version: 1.0.0
status: draft
primary_output: /workflow/13_retrospective/13_workflow_retrospective.md
requires_human_approval: true
---
```

---

## 2. Purpose

The Stage 13 SKILL helps a human developer and Agent review the workflow itself after a project, release, milestone, or major implementation cycle.

It must answer:

```text
What should be changed in the workflow, SKILLs, templates, prompts, context handoff rules, approval gates, or artifact contracts so the next project can be safer, clearer, faster, and more reliable?
```

The SKILL must focus on workflow improvement, not product feature design or new implementation.

---

## 3. When to Use

Use this SKILL after one of the following:

```text
- Stage 12 Review / Security / Release / Handoff has completed.
- A major release or milestone has been reviewed.
- A significant implementation cycle exposed recurring Agent failure patterns.
- Several stages produced unstable, ambiguous, or hard-to-review artifacts.
- The human developer wants to improve reusable workflow SKILLs before the next project.
```

This SKILL may also be used for a mid-project retrospective when the workflow itself is causing repeated friction.

---

## 4. When Not to Use

Do not use this SKILL to:

```text
- perform product requirements analysis;
- redesign the domain model;
- change architecture decisions;
- implement code;
- run a code review in place of Stage 12;
- approve release readiness;
- rewrite SKILL.md files directly without human approval;
- create new project requirements from retrospective opinions;
- replace human judgment with Agent-generated process recommendations.
```

If the project has not reached a meaningful milestone, run a smaller checkpoint review instead.

---

## 5. Core Question

The SKILL must organize the retrospective around this core question:

```text
Which workflow, prompt, context, artifact, approval, validation, and Agent-behavior issues should be preserved, fixed, split, merged, removed, or promoted into reusable rules for future projects?
```

Secondary questions:

```text
1. Which stages worked well and why?
2. Where did the Agent repeatedly fail, over-assume, over-generate, or miss important constraints?
3. Which prompts or SKILL instructions were ambiguous, too large, too small, or insufficiently grounded?
4. Where was human judgment essential?
5. Which artifacts were useful as source of truth, and which were noisy or hard to review?
6. Which approval gates prevented mistakes, and which gates were unclear or skipped?
7. Which SKILL.md files should be revised, split, merged, deprecated, or newly created?
8. Which lessons are reusable across projects, and which are project-specific only?
```

---

## 6. Required Inputs

### 6.1 Always Read

The executable SKILL created from this template should always read these inputs when they exist:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
/workflow/12_review_release_handoff/result.md
/workflow/12_review_release_handoff/12_code_review.md
/workflow/12_review_release_handoff/12_security_privacy_review.md
/workflow/12_review_release_handoff/12_release_readiness.md
/workflow/12_review_release_handoff/12_documentation_handoff.md
```

If a stage-level `result.md` exists for completed stages, read the approved result summaries:

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

Reading full stage artifacts is not required by default unless the result summary is missing, unclear, contradictory, or the retrospective requires deeper evidence.

---

### 6.2 Read If Applicable

Read these only when the condition is true:

```text
/workflow/13_retrospective/USER_DIRECTIVES.md
- if the human developer provided retrospective instructions, questions, or priorities.

/workflow/11_implementation_results/11_task_result_*.md
- if implementation-stage failure patterns, repeated task drift, or validation problems must be analyzed.

/workflow/11_implementation_results/11_test_evidence_*.md
- if test evidence quality, TDD adherence, or validation traceability must be reviewed.

/workflow/10_prompts/10_implementation_prompts.md
- if prompt ambiguity, scope leakage, or implementation prompt quality must be reviewed.

/workflow/09_tasks/09_task_cards.md
- if task size, dependency order, or definition-of-done quality must be reviewed.

/workflow/08_test_strategy/08_test_strategy.md
- if validation gaps or test strategy breakdowns must be analyzed.

/workflow/12_review_release_handoff/review_notes.md
- if human review comments exist.

/workflow/*/review_notes.md
- if stage-specific review feedback exists.

agent_session_logs/*
- if the user explicitly provides logs and wants Agent behavior analyzed.

ci_reports/*
- if CI, test, deployment, or release evidence exists.

incident_reports/*
- if production, staging, deployment, security, or operational incidents occurred.

cost_or_usage_reports/*
- if tool cost, latency, token usage, or workflow overhead is part of the retrospective.
```

---

### 6.3 Do Not Read By Default

Do not read these by default:

```text
- raw source code files;
- full historical Agent chat transcripts;
- full raw logs;
- secrets, environment variable files, credentials, or private keys;
- superseded artifacts unless needed to understand drift;
- rejected artifacts unless reviewing why they were rejected;
- all full stage artifacts when stage result summaries are sufficient;
- unrelated product documentation not used by the workflow;
- user-private notes not explicitly provided for retrospective use.
```

---

### 6.4 Missing Input Handling

If required inputs are missing:

```text
1. Report the missing input under "Missing Information".
2. Explain why it matters for retrospective quality.
3. Mark it as blocking or non-blocking.
4. If Stage 12 artifacts are missing, continue only as a milestone retrospective, not as a final release retrospective.
5. If approval or artifact status is unknown, avoid treating artifacts as approved source of truth.
6. If evidence is insufficient, record the finding as a hypothesis, not as a confirmed failure pattern.
7. If the missing input prevents safe conclusions, produce a partial retrospective and request human review.
```

---

## 7. Files to Read First

The executable SKILL should read files in this order:

```text
1. /workflow/context/artifact_manifest.yml
2. /workflow/context/context_packet.md
3. /workflow/context/APPROVAL_LOG.md
4. /workflow/context/DECISIONS.md
5. /workflow/context/ASSUMPTIONS.md
6. /workflow/context/OPEN_QUESTIONS.md
7. /workflow/context/REJECTED_OPTIONS.md
8. /workflow/13_retrospective/USER_DIRECTIVES.md, if it exists
9. /workflow/12_review_release_handoff/result.md
10. Stage-level result.md files for completed stages
11. Conditional evidence files activated by the retrospective scope
```

---

## 8. USER_DIRECTIVES.md Handling

If `/workflow/13_retrospective/USER_DIRECTIVES.md` exists, the Agent must read it before executing the retrospective.

Classify each directive as one of:

```text
- explicit approval
- correction
- retrospective focus area
- skill improvement request
- workflow policy preference
- rejection
- scope limitation
- question to answer
- additional evidence source
```

Rules:

```text
- Apply USER_DIRECTIVES before Agent assumptions.
- Do not treat every directive as a globally approved workflow change.
- If a directive conflicts with approved decisions or prior approval logs, report the conflict.
- Do not modify USER_DIRECTIVES.md unless explicitly instructed.
```

---

## 9. Input Preflight Procedure

Before producing outputs, the executable SKILL must perform this preflight:

```text
[ ] Confirm this is Stage 13 Workflow Retrospective & Skill Improvement.
[ ] Confirm whether the retrospective is final, post-release, post-milestone, or mid-project.
[ ] Read artifact_manifest.yml if available.
[ ] Confirm which stages are completed, approved, skipped, or partially completed.
[ ] Read context_packet.md and approval records.
[ ] Check whether USER_DIRECTIVES.md exists.
[ ] Identify Always Read inputs that are present.
[ ] Identify conditional inputs activated by project profile or user directive.
[ ] Verify that source artifacts are approved or clearly marked as draft.
[ ] Identify missing, superseded, rejected, or conflicting inputs.
[ ] Define the retrospective scope before analyzing findings.
```

If the scope is unclear, proceed with a clearly labeled working scope rather than pretending certainty.

---

## 10. Execution Procedure

The executable SKILL should follow this procedure.

### Step 1. Define Retrospective Scope

Classify the retrospective as:

```text
- final project retrospective;
- post-release retrospective;
- post-milestone retrospective;
- mid-project workflow checkpoint;
- failed-run retrospective;
- skill-template evaluation retrospective.
```

State which workflow stages are included and excluded.

---

### Step 2. Build the Evidence Map

Create a concise map of evidence sources:

```text
- stages completed;
- artifacts reviewed;
- approval gates used;
- test and validation evidence available;
- human review notes available;
- Agent logs or session evidence available;
- incident, deployment, or CI evidence available;
- missing evidence.
```

Do not infer failure patterns without evidence.

---

### Step 3. Review the Workflow Stage by Stage

For each stage included in scope, evaluate:

```text
- Was the stage run at the right time?
- Were the required inputs available and approved?
- Was the output artifact concrete and reviewable?
- Were assumptions separated from decisions?
- Were open questions recorded and carried forward?
- Were rejected options preserved?
- Was the context handoff useful to the next stage?
- Was the human approval gate clear?
- Did downstream stages use the correct source of truth?
- Did the stage create avoidable ambiguity or rework?
```

Record findings as evidence-backed observations, not blame statements.

---

### Step 4. Analyze Agent Behavior

Identify recurring Agent behavior patterns:

```text
- useful decomposition;
- correct use of approved context;
- helpful uncertainty reporting;
- premature implementation;
- silent assumption conversion;
- scope expansion;
- over-reading unrelated artifacts;
- under-reading required context;
- hallucinated source-of-truth claims;
- weak traceability;
- vague outputs;
- skipped validation evidence;
- prompt obedience failures;
- repeated need for human correction;
- context loss after session reset.
```

Classify each as:

```text
Strength
Failure Pattern
Mixed Pattern
One-off Issue
Insufficient Evidence
```

---

### Step 5. Review Prompt and SKILL Quality

For each relevant SKILL or prompt, evaluate:

```text
- Was the purpose clear?
- Was the input contract sufficient?
- Were conditional inputs well-defined?
- Was the output artifact contract concrete?
- Were required sections reviewable?
- Were do-not-do rules effective?
- Was the skill too large to execute reliably?
- Did the skill require splitting?
- Did the skill produce internal artifacts that leaked into downstream use?
- Was the finalizer or handoff adequate?
```

Do not rewrite SKILL files in this stage unless the user explicitly asks for revision execution. Instead, create improvement backlog items.

---

### Step 6. Identify Human Judgment Points

Record where human judgment was essential:

```text
- approval of goals, scope, architecture, data, release, or workflow changes;
- correction of Agent assumptions;
- prioritization of trade-offs;
- security, privacy, or compliance decisions;
- release readiness decisions;
- acceptance of technical debt;
- rejection of unnecessary complexity;
- interpretation of ambiguous domain rules.
```

This section should improve future approval gates.

---

### Step 7. Evaluate Cross-Cutting Practices

Assess how well the workflow preserved:

```text
- traceability from goal to implementation evidence;
- TDD or test-aware execution;
- DDD language and domain rule continuity;
- security and privacy awareness;
- artifact-first context handoff;
- context reset tolerance;
- release and documentation handoff;
- human approval discipline.
```

---

### Step 8. Extract Reusable Lessons

Convert observations into reusable lessons.

Each lesson must distinguish:

```text
- reusable workflow rule;
- project-specific lesson;
- tool-specific limitation;
- human operating practice;
- candidate SKILL improvement;
- candidate artifact contract improvement.
```

Do not overgeneralize from one weakly supported incident.

---

### Step 9. Create the Skill Improvement Backlog

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

Recommended priority categories:

```text
P0: Blocks safe workflow use
P1: Causes repeated rework or serious ambiguity
P2: Improves reliability or reviewability
P3: Nice-to-have refinement
```

---

### Step 10. Classify Skill Lifecycle Recommendations

For each SKILL affected, classify the recommendation:

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

---

### Step 11. Produce Stage 13 Artifacts

Create or update all mandatory artifacts and applicable conditional artifacts.

Do not create project-specific product requirements, architecture, database design, implementation tasks, or code.

---

### Step 12. Prepare Human Approval Gate

End with a human approval gate listing:

```text
- retrospective findings to accept;
- skill improvement backlog priorities to approve;
- SKILL revision candidates to approve;
- new SKILL creation candidates to approve;
- skill split/merge/deprecation candidates to approve;
- unresolved evidence gaps;
- recommended next action.
```

---

## 11. Output Artifacts

### 11.1 Mandatory Artifacts

The executable SKILL must create or update:

```text
/workflow/13_retrospective/13_workflow_retrospective.md
/workflow/13_retrospective/13_agent_failure_patterns.md
/workflow/13_retrospective/13_skill_improvement_backlog.md
/workflow/13_retrospective/13_reusable_lessons.md
/workflow/13_retrospective/result.md
/workflow/context/context_packet.md
```

### 11.2 Conditional Artifacts

Create these only when applicable:

```text
/workflow/13_retrospective/13_prompt_ambiguity_report.md
- if prompt ambiguity or instruction conflict was a major issue.

/workflow/13_retrospective/13_context_management_review.md
- if context handoff, artifact manifest, approval state, or session reset caused issues.

/workflow/13_retrospective/13_human_intervention_log.md
- if human corrections, overrides, or approval decisions need to be summarized.

/workflow/13_retrospective/13_tooling_limits.md
- if the retrospective identifies tool-specific execution, sandbox, context-window, or file-handling limits.

/workflow/13_retrospective/13_skill_split_candidates.md
- if one or more SKILLs appear too large or internally mixed.

/workflow/13_retrospective/13_next_workflow_experiment_plan.md
- if the user wants to test improvements in a next project or pilot run.
```

### 11.3 N/A Record

For each conditional artifact not created, record:

```text
Artifact:
Why Not Applicable:
Revisit If:
```

The N/A record may be placed in `result.md`.

---

## 12. Required Output Structure

### 12.1 `13_workflow_retrospective.md`

Use this structure:

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
- What worked:
- What failed or caused rework:
- Most important workflow improvement:
- Most important skill improvement:
- Human approval needed:

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

## 12. Agent Behavior Summary
- Agent strengths:
- Agent failure patterns:
- Mixed patterns:
- Human corrections required:

## 13. Human Judgment Summary
- Decisions only the human could make:
- Places where the Agent needed clearer constraints:
- Future approval gate recommendations:

## 14. Top Reusable Lessons
- Lesson 1:
- Lesson 2:
- Lesson 3:

## 15. Top Skill Improvement Priorities
| Priority | Skill / Template | Change Needed | Evidence | Approval Needed |
|---|---|---|---|---|

## 16. Open Questions
- ...

## 17. Human Approval Required
- ...
```

---

### 12.2 `13_agent_failure_patterns.md`

Use this structure:

```markdown
# 13 Agent Failure Patterns

## 1. Summary

## 2. Failure Pattern Index
| ID | Pattern | Frequency | Severity | Evidence | Affected Stages | Recommended Mitigation |
|---|---|---:|---|---|---|---|

## 3. Detailed Patterns

### AFP-001: [[Pattern Name]]
- Classification:
- Evidence:
- Affected stage(s):
- Root cause hypothesis:
- Why it matters:
- Mitigation:
- Skill changes suggested:
- Validation method for mitigation:
- Approval required:

## 4. Non-Patterns / One-Off Issues

## 5. Insufficient Evidence Items
```

---

### 12.3 `13_skill_improvement_backlog.md`

Use this structure:

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

---

### 12.4 `13_reusable_lessons.md`

Use this structure:

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

---

### 12.5 `result.md`

Use this structure:

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

---

## 13. Traceability Rules

Stage 13 traceability is meta-level traceability. It links workflow evidence to improvement proposals.

Use stable IDs:

```text
RF-001, RF-002      Retrospective Finding
AFP-001, AFP-002    Agent Failure Pattern
RL-001, RL-002      Reusable Lesson
SIB-001, SIB-002    Skill Improvement Backlog Item
```

Required links:

```text
Retrospective Finding → Evidence Source
Failure Pattern → Affected Stage / Skill
Failure Pattern → Skill Improvement Backlog Item
Reusable Lesson → Future Workflow Rule or Template Change
Skill Improvement Backlog Item → Validation Method
```

Rules:

```text
- Do not break existing project traceability IDs.
- Do not create new product requirements from retrospective findings.
- If a product follow-up is discovered, record it as a handoff recommendation, not as an approved requirement.
- Link every P0/P1 backlog item to at least one evidence source.
- Mark weakly supported findings as hypotheses.
```

---

## 14. Decision / Assumption / Open Question Rules

### 14.1 Approved Decision

Use only when the human explicitly approves a workflow or SKILL improvement.

Example:

```text
Approved: Split Stage 11 implementation loop into backend, frontend, database migration, and validation evidence sub-skills.
```

### 14.2 Decision Candidate

Use when the Agent recommends a workflow change.

Example:

```text
Candidate: Add a required prompt ambiguity review before Stage 10 implementation prompts are approved.
```

### 14.3 Working Assumption

Use when retrospective analysis requires a temporary assumption.

Example:

```text
Assumption: Missing implementation evidence indicates evidence was not recorded, not necessarily that tests were not run.
```

### 14.4 Open Question

Use when unresolved information affects the improvement plan.

Example:

```text
Open Question: Should skill revisions be applied before the next project, or should the next project be used as an experiment baseline?
```

### 14.5 Rejected Option

Use when an improvement direction has been explicitly rejected.

Example:

```text
Rejected: Do not merge all Stage 11 implementation skills into one large SKILL.
```

Rules:

```text
- Do not record Agent recommendations as approved decisions.
- Do not rewrite DECISIONS.md unless explicit approval exists.
- Do not treat a recurring annoyance as a confirmed failure pattern without evidence.
- Do not revive rejected workflow options unless the human reopens them.
```

---

## 15. Validation Checklist

Before the SKILL reports completion, verify:

```text
[ ] Retrospective scope is stated.
[ ] Evidence sources are listed.
[ ] Missing evidence is identified.
[ ] Findings are evidence-backed or clearly marked as hypotheses.
[ ] Stage-by-stage review is included.
[ ] Agent strengths and failure patterns are separated.
[ ] Human judgment points are recorded.
[ ] Prompt/SKILL ambiguity is reviewed where applicable.
[ ] Artifact quality and context handoff quality are reviewed.
[ ] Traceability, TDD, DDD, security/privacy, and approval gates are reviewed.
[ ] Skill improvement backlog exists.
[ ] Each high-priority backlog item has evidence, proposed change, and validation method.
[ ] Reusable lessons are separated from project-specific lessons.
[ ] Conditional artifacts include N/A records when skipped.
[ ] No product requirements, architecture changes, or code tasks were silently created.
[ ] Human approval gate is explicit.
[ ] context_packet.md is updated for the next workflow improvement action or next project.
```

---

## 16. Human Approval Gate

The SKILL must end with:

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

Human approval is required before:

```text
- revising any reusable SKILL.md;
- modifying a stage-specific template;
- changing artifact contracts;
- deleting, merging, or splitting SKILLs;
- adopting a new workflow policy;
- applying lessons to the next project as required rules.
```

---

## 17. Context Packet Update Rules

Update `/workflow/context/context_packet.md` for the next workflow action.

If the project is complete, prepare the context for:

```text
- skill improvement execution;
- workflow template revision;
- next project intake;
- next retrospective iteration;
- archived project handoff.
```

Required `context_packet.md` sections:

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

---

## 18. Specialization Hooks

Project-type specializations may add retrospective questions.

### web_saas

```text
- Did auth, roles, deployment, environment variables, and API contracts create avoidable rework?
- Did the workflow catch web-specific security and operational issues early enough?
```

### internal_tool

```text
- Did stakeholder and operator workflows receive enough attention?
- Were internal permissions, auditability, and maintenance responsibilities clear?
```

### mobile_app

```text
- Did the workflow account for platform release, device permissions, offline behavior, and app review constraints?
```

### ai_data_product

```text
- Did the workflow capture dataset provenance, evaluation methods, model failure modes, and human review requirements?
- Did the Agent overstate model/evaluation confidence?
```

### regulated_security_sensitive

```text
- Were compliance, audit, privacy, threat modeling, and release blockers introduced early enough?
- Were security findings handled as blockers, warnings, or suggestions?
```

### brownfield_legacy

```text
- Did the workflow respect existing system constraints?
- Were regression baselines, compatibility risks, and migration constraints sufficiently captured?
```

Specialization must not replace the Stage 13 procedure.

---

## 19. Tool Wrapper Hooks

Tool-specific wrappers may add:

```text
- where to save retrospective files;
- how to collect Agent logs if the user permits;
- how to reference tool-specific sessions;
- how to handle context-window or sandbox limits;
- how to export reviewable artifacts.
```

Tool wrappers must not change:

```text
- approval rules;
- artifact contracts;
- evidence requirements;
- decision / assumption separation;
- retrospective finding classifications.
```

---

## 20. Failure Handling

If the retrospective cannot be completed safely, produce a partial result.

Use this structure:

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
- Stage 12 outputs are missing and the user requested final release retrospective.
- artifact_manifest.yml conflicts with approval logs.
- required artifacts are superseded or unapproved.
- evidence is too thin to support failure pattern conclusions.
- USER_DIRECTIVES.md conflicts with approved workflow decisions.
- raw logs contain sensitive data and cannot be safely reviewed.
```

---

## 21. Do Not Do

The Agent must not:

```text
- rewrite SKILL.md files during the retrospective unless explicitly instructed;
- treat improvement suggestions as approved changes;
- blame the Agent or human without evidence;
- infer repeated failure patterns from one weak example;
- create new product requirements from retrospective observations;
- change product scope, architecture, database, or release decisions;
- expose secrets or private data from logs;
- read all raw logs or chat transcripts by default;
- ignore missing evidence;
- collapse workflow-level lessons and project-specific lessons;
- update DECISIONS.md without explicit human approval;
- use retrospective findings to bypass future approval gates;
- claim the workflow is improved merely because a backlog was created.
```

---

## 22. Template Quality Checklist

Before using this template to create an executable Stage 13 `SKILL.md`, verify:

```text
[ ] The stage purpose is retrospective and skill improvement, not product redesign.
[ ] Always Read inputs are defined.
[ ] Conditional inputs are defined.
[ ] Do Not Read By Default is defined.
[ ] Missing input handling is defined.
[ ] Mandatory artifacts match Stage 13.
[ ] Conditional artifacts have N/A rules.
[ ] Failure patterns require evidence.
[ ] Skill improvement backlog includes validation methods.
[ ] Human approval is required for workflow and SKILL changes.
[ ] context_packet.md prepares the next project or workflow improvement step.
[ ] Specialization hooks add questions without replacing the stage procedure.
[ ] Tool wrapper hooks do not change reasoning or approval rules.
```

---

## 23. Suggested Filename

Save this template as:

```text
/workflow_templates/stages/13_retrospective_skill_template.md
```

or, if using the stage name directly:

```text
/workflow_templates/stages/13_workflow_retrospective_skill_template.md
```
