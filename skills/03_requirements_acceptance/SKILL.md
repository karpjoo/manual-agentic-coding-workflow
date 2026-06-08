---
name: 03_requirement_acceptance
aliases:
  - 03_requirements_acceptance
description: Use this reusable Stage 3 SKILL to convert approved goals and stakeholder/risk context into testable requirements, acceptance criteria, traceability, and Stage 4 handoff context.
stage: "03 Requirements & Acceptance Criteria"
version: 1.0.0
status: draft
primary_output: /workflow/03_requirements/03_requirements.md
requires_human_approval: true
internal_split: false
---

# 03 Requirement Acceptance SKILL

## 1. Purpose

Convert approved Stage 1–2 context into explicit, testable, traceable Stage 3 artifacts:

```text
functional requirements
non-functional requirements
security/privacy/data requirements
scenarios and edge cases
acceptance criteria
requirement-level traceability
Stage 4 handoff context
```

This is where TDD begins conceptually. Do not write code or test files here. Create requirements and acceptance criteria that later stages can turn into domain models, architecture, validation strategy, task cards, implementation prompts, and tests.

## 2. Core Question

What must the system do, for whom, under which constraints, and how will each requirement be verified?

## 3. Operating Mode

The agent is a structured development assistant, not the final decision-maker.

Maintain these distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```

Do not claim Stage 3 artifacts are approved unless the human explicitly approves them.

## 4. Stage Boundary

### This Stage Does

```text
- Decompose approved goals into requirements.
- Classify requirements by type.
- Define acceptance criteria and validation methods.
- Capture scenarios, negative paths, edge cases, role/permission conditions, and data/security/privacy conditions.
- Preserve non-goals and rejected scope boundaries.
- Update requirement-level traceability.
- Prepare Stage 4 Domain Modeling / DDD context.
```

### This Stage Does Not

```text
- Design domain aggregates, entities, APIs, database schemas, UI components, or implementation tasks.
- Write code or tests.
- Treat assumptions as approved requirements.
- Expand scope silently.
- Convert recommendations into decisions.
```

## 5. When to Use / Not Use

Use this SKILL when Stage 1 service goal and Stage 2 stakeholder/risk artifacts exist and the project needs requirements, acceptance criteria, and traceability.

Do not use this SKILL to define the service goal, perform stakeholder/risk analysis, create DDD/domain models, design architecture/API/database/UI, write implementation tasks, create implementation prompts, or write code/tests.

## 6. Input Precedence

When inputs conflict, use this order:

```text
1. Current explicit user instruction
2. /workflow/03_requirements/USER_DIRECTIVES.md
3. /workflow/context/APPROVAL_LOG.md and /workflow/context/DECISIONS.md
4. /workflow/context/artifact_manifest.yml
5. /workflow/context/context_packet.md
6. Approved upstream artifacts
7. Working assumptions
8. Agent inference
```

Report conflicts. Treat conflicts affecting scope, roles, personal/sensitive data, security/privacy policy, external transfer, compliance, or must-have goals as blocking unless the user resolves them.

## 7. Required Inputs

### Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
/workflow/01_goal/01_service_goal.md
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
```

### Read If Applicable

```text
/workflow/00_intake/00_project_intake.md
  if project profile, fixed stack, delivery constraints, or project type affect requirements

/workflow/00_intake/00_existing_context_review.md
  if brownfield, migration, extension, or existing-system constraints exist

/workflow/01_goal/review_notes.md
/workflow/02_stakeholders_risk/review_notes.md
  if human review comments exist

/workflow/03_requirements/USER_DIRECTIVES.md
  if stage-local instructions exist

/workflow_templates/specializations/*.md
  if a project-type specialization is active
```

### Do Not Read By Default

```text
raw chat history
raw agent logs
superseded drafts
rejected artifacts as current truth
unrelated previous-stage drafts
implementation code
later-stage artifacts unless Stage 3 is being revised after later work
```

## 8. Missing Input Handling

If required input is missing, draft, unapproved, superseded, rejected, or conflicting:

```text
1. Record it in /workflow/03_requirements/result.md under Missing / Conflicting Information.
2. Explain why it matters.
3. Mark it Blocking or Non-blocking.
4. If non-blocking, proceed only with a clearly labeled working assumption.
5. If blocking, stop after safe partial work and request human decision.
```

Default blocking gaps:

```text
no approved or review-ready service goal
no target users / roles / stakeholders
no scope boundary or non-goal context
no risk/privacy/security context when personal, sensitive, regulated, privileged, or externally transferred data exists
conflict between USER_DIRECTIVES.md and approved decisions
```

## 9. USER_DIRECTIVES.md Handling

If `/workflow/03_requirements/USER_DIRECTIVES.md` exists, read it before execution.

Classify each directive as:

```text
approval | correction | preference | new requirement candidate | rejection | scope change | constraint | question | additional input
```

Do not automatically treat every directive as globally approved. Report conflicts with approved decisions. Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

## 10. Preflight Procedure

Before producing artifacts:

```text
[ ] Confirm this is Stage 3: Requirements & Acceptance Criteria.
[ ] Read this SKILL.md.
[ ] Read artifact_manifest.yml, context_packet.md, DECISIONS.md, and APPROVAL_LOG.md if available.
[ ] Check whether /workflow/03_requirements/USER_DIRECTIVES.md exists.
[ ] Identify Always Read and conditional inputs.
[ ] Verify required inputs exist and check approval/supersession/rejection status.
[ ] Identify missing, ambiguous, conflicting, superseded, or rejected inputs.
[ ] Restate the Stage 3 task and boundary in result.md.
```

If preflight reveals a blocking issue, produce a blocker report instead of pretending completion.

## 11. Output Artifacts

### Mandatory Official Stage Artifacts

```text
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/03_requirements/03_traceability_matrix.md
/workflow/03_requirements/result.md
/workflow/context/context_packet.md
```

### Update When Applicable

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Do not update `/workflow/context/DECISIONS.md` unless the current user explicitly approves a decision during this run.

### Conditional Artifacts

Create only if needed:

```text
/workflow/03_requirements/03_nfr_requirements.md
  if NFRs are too large for 03_requirements.md

/workflow/03_requirements/03_security_privacy_requirements.md
  if security/privacy/data requirements require separate review

/workflow/03_requirements/03_scenarios_edge_cases.md
  if scenarios and edge cases are substantial

/workflow/03_requirements/03_scope_candidates.md
  if scope classification needs separate tracking before Stage 7

/workflow/03_requirements/03_requirements_open_questions.md
  if many requirements are blocked by unresolved questions
```

For skipped conditional artifacts, record this N/A entry in `result.md`:

```text
Artifact:
N/A Reason:
Revisit If:
```

## 12. ID Conventions

Use stable IDs. Do not reuse IDs for different meanings.

```text
FR-###       Functional requirement
NFR-###      Non-functional requirement
SEC-###      Security / privacy requirement
DATA-###     Data handling, retention, deletion, or governance requirement
OPS-###      Operational or observability requirement
INT-###      External integration requirement
AC-[RequirementID]-##  Acceptance criterion
OQ-REQ-###   Requirement open question
ASM-REQ-###  Requirement working assumption
RISK-###     Risk inherited from Stage 2 or introduced as requirement concern
ROLE-###     Role inherited from Stage 2 or introduced for traceability mapping
```

If upstream artifacts use different IDs, preserve them and add mappings rather than replacing them. If a requirement is split, merged, rejected, or superseded, preserve the history in `result.md` and `03_traceability_matrix.md`.

## 13. Execution Procedure

### Step 1. Summarize Approved Source Context

Create a concise source summary:

```text
approved service goal
success criteria
target users and stakeholder roles
non-goals / out-of-scope boundaries
risk/privacy/security constraints
role and permission concerns
data handling concerns
open questions affecting requirements
```

Do not copy entire upstream artifacts. Summarize only what is necessary for requirements work.

### Step 2. Extract Requirement Candidates

Extract candidates from goals, stakeholder needs, risks, privacy screening, operational needs, external integrations, data handling needs, non-goals, rejected options, and open questions.

Classify each candidate as:

```text
Functional
Non-Functional
Security / Privacy
Data / Retention / Deletion
Authorization / Role-Based Access
Operational / Observability
Compliance / Audit
External Integration
Out of Scope / Non-Requirement
Open Question
```

### Step 3. Write Requirements

Each requirement must include:

```text
Requirement ID:
Title:
Type:
Source Goal / Stakeholder / Risk:
User Role or Actor:
User Need / Goal:
Description:
Trigger / Preconditions:
Main Scenario:
Alternative / Failure Scenarios:
Edge Cases:
Out-of-Scope Clarifications:
Acceptance Criteria IDs:
Related NFRs:
Security / Privacy / Data Conditions:
Validation Method:
Traceability Links:
Status: Draft | Proposed | Approved | Needs Clarification
```

Requirement rules:

```text
- Describe observable behavior or reviewable constraints.
- Avoid implementation, database, API, UI, and architecture design.
- Mark unconfirmed items as assumptions or open questions.
- Preserve Stage 2 security/privacy/data implications.
```

### Step 4. Write Acceptance Criteria

Each acceptance criterion must include:

```text
Acceptance Criterion ID:
Linked Requirement ID:
Scenario / Behavior:
Given:
When:
Then:
And / But:
Negative Case:
Edge Case:
Data Condition:
Role / Permission Condition:
Security / Privacy Condition:
Expected Evidence:
Validation Type: Unit | Integration | E2E | Manual | Review | Static Analysis | Policy Review
Status: Draft | Proposed | Approved | Needs Clarification
```

Every requirement needs at least one criterion or an explicit reason why criteria cannot yet be written. Criteria must be observable and testable; include happy paths, important negative paths, role/permission boundaries, and data/privacy conditions where relevant.

### Step 5. Identify Scope Boundaries

Classify discovered items as:

```text
Must Have
Should Have
Could Have
Won't / Non-Scope
Later / Future Candidate
Needs Human Decision
```

Stage 3 may propose scope categories, but final MVP scope is approved later in Stage 7. Do not silently expand MVP or project scope.

### Step 6. Review Testability

For every requirement and criterion, ask:

```text
Can a future agent or developer verify this?
What evidence would prove satisfaction?
Are role, state, input, action, and outcome clear?
Does it avoid hidden implementation assumptions?
Is the validation method specific enough for Stage 8 to refine later?
```

Revise unclear items or record them under `Requirements Not Yet Testable`.

### Step 7. Update Traceability

Minimum links:

```text
Service Goal → Requirement
Success Criterion → Requirement
Stakeholder / Role → Requirement
Risk / Privacy Concern → Requirement, if applicable
Requirement → Acceptance Criterion
Requirement → NFR, if applicable
Requirement / Acceptance Criterion → Validation Method
Requirement → Open Question, if unresolved
Requirement → Rejected / Non-Scope Item, if excluded
```

Do not create premature links to domain entities, API endpoints, database tables, implementation tasks, test files, or code modules unless Stage 3 is being revised after those artifacts already exist and the user explicitly requests it.

### Step 8. Classify Review Items

Separate:

```text
decision candidates
working assumptions
open questions
risks and constraints
rejected or superseded requirement candidates
traceability gaps
testability concerns
```

### Step 9. Update Context for Stage 4

Update `/workflow/context/context_packet.md` with only minimal operational context needed for Stage 4 Domain Modeling / DDD. Do not copy full artifacts into the context packet.

### Step 10. Prepare Human Approval Gate

End `result.md` with the approval gate in Section 18. Do not claim approval unless the user explicitly grants it.

## 14. Required Output Structures

### `03_requirements.md`

```markdown
# 03 Requirements

## 1. Document Status
## 2. Source Context Summary
## 3. Requirement Classification Summary
## 4. Functional Requirements
### FR-001: [[Title]]
- Status:
- Source Goal / Stakeholder / Risk:
- Actor / Role:
- User Need / Goal:
- Description:
- Trigger / Preconditions:
- Main Scenario:
- Alternative / Failure Scenarios:
- Edge Cases:
- Out-of-Scope Clarifications:
- Acceptance Criteria IDs:
- Related NFRs:
- Security / Privacy / Data Conditions:
- Validation Method:
- Traceability Links:

## 5. Non-Functional Requirements
## 6. Security / Privacy / Data Requirements
## 7. Operational / Integration Requirements
## 8. Scope Boundary Candidates
## 9. Requirements Needing Clarification
## 10. Requirements Not Yet Testable
```

### `03_acceptance_criteria.md`

```markdown
# 03 Acceptance Criteria

## 1. Document Status
## 2. Acceptance Criteria Summary
## 3. Criteria by Requirement
### AC-FR-001-01: [[Scenario / Behavior]]
- Status:
- Linked Requirement ID:
- Given:
- When:
- Then:
- And / But:
- Negative Case:
- Edge Case:
- Data Condition:
- Role / Permission Condition:
- Security / Privacy Condition:
- Expected Evidence:
- Validation Type:

## 4. Cross-Cutting Acceptance Criteria
## 5. Manual Review Criteria
## 6. Criteria Needing Clarification
```

### `03_traceability_matrix.md`

```markdown
# 03 Requirements Traceability Matrix

## 1. Document Status
## 2. Traceability Matrix
| Source Type | Source ID / Artifact | Requirement ID | Acceptance Criteria ID | Validation Method | Status | Notes |
|---|---|---|---|---|---|---|
## 3. IDs Introduced in This Stage
## 4. Traceability Gaps
## 5. Do Not Trace Yet
```

### `result.md`

```markdown
# Result: 03 Requirements & Acceptance Criteria

## 1. Task Summary
## 2. Inputs Used
## 3. Outputs Created or Updated
## 4. Missing / Conflicting Information
## 5. Requirement Summary
## 6. Acceptance Criteria Summary
## 7. Scope Boundary Candidates
## 8. Requirements Not Yet Testable
## 9. Decision Candidates
## 10. Working Assumptions
## 11. Open Questions
## 12. Risks and Constraints
## 13. Rejected or Superseded Requirement Candidates
## 14. Traceability Updates
## 15. Conditional Artifacts N/A Record
## 16. Split Assessment
## 17. Human Approval Required
## 18. Recommended Next Step
```

## 15. Requirement Quality Rules

A requirement is acceptable only if it is:

```text
necessary for the approved service goal or stakeholder/risk context
stated without hidden implementation design
assigned a stable ID
tied to a role, actor, or system context where relevant
bounded by scope and non-goals
linked to at least one acceptance criterion or a documented testability gap
linked to a validation method or review evidence
explicit about security/privacy/data implications where relevant
clear enough for later domain modeling, architecture, validation strategy, and task breakdown
```

## 16. Acceptance Criteria Quality Rules

Acceptance criteria must be:

```text
observable
verifiable
tied to a requirement
explicit about state, role, input, action, and expected outcome
clear about failure behavior where relevant
clear about security/privacy behavior where relevant
suitable for later automated or manual validation
```

## 17. Security and Privacy Handling

If Stage 2 identifies personal data, sensitive data, privileged roles, external transfer, LLM/API use, audit needs, or compliance risk:

```text
- attach security/privacy conditions to relevant requirements;
- create security, privacy, data, retention, deletion, audit, access control, or consent requirements where applicable;
- include negative acceptance criteria for unauthorized access, improper exposure, privilege misuse, unsafe external transfer, or data retention violations;
- record unresolved policy questions in OPEN_QUESTIONS.md;
- avoid making security architecture decisions prematurely.
```

If security/privacy/data concerns are not applicable, record why and what future change would require reconsideration.

## 18. Human Approval Gate

End `result.md` with:

```markdown
## Human Approval Required

### Requirements to Approve
- Functional requirements:
- Non-functional requirements:
- Security/privacy/data requirements:
- Operational/integration requirements:

### Acceptance Criteria to Approve
- Criteria by requirement:
- Cross-cutting criteria:
- Manual review criteria:

### Non-Scope / Boundary Items to Approve
- Won't / Non-Scope:
- Later / Future Candidate:
- Needs Human Decision:

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Testability Concerns
- ...

### Security / Privacy Concerns
- ...

### Artifacts Ready for Review
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/03_requirements/03_traceability_matrix.md
- /workflow/03_requirements/result.md

### Recommended Next Step
- Approve Stage 3 artifacts, revise them, or resolve blockers before Stage 4 Domain Modeling / DDD.
```

## 19. Context Packet Update Rules

Update `/workflow/context/context_packet.md` for Stage 4 using this structure:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage completed: 03 Requirements & Acceptance Criteria
- Next recommended stage: 04 Domain Modeling / DDD
- Stage 3 artifact status:

## 2. Approved Decisions
- Only human-approved decisions.

## 3. Working Assumptions
- Requirement assumptions Stage 4 must know.

## 4. Open Questions
- Questions affecting domain concepts, rules, roles, permissions, lifecycle, invariants, or scope.

## 5. Rejected / Superseded Options
- Requirement or scope items not to revive unless reopened.

## 6. Constraints That Must Not Be Violated
- Functional:
- Security/privacy:
- Data handling:
- Role/permission:
- Non-goals:

## 7. Key Context for Next Stage
- Core capabilities implied by requirements.
- User roles and actors relevant to domain modeling.
- Business rules, lifecycle hints, state changes, and invariants implied by requirements.
- Requirement IDs to preserve.

## 8. Required Inputs for Next Stage
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/03_requirements/03_traceability_matrix.md
- /workflow/01_goal/01_service_goal.md
- /workflow/02_stakeholders_risk/02_stakeholders.md
- /workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- /workflow/context/DECISIONS.md
- /workflow/context/ASSUMPTIONS.md
- /workflow/context/OPEN_QUESTIONS.md
- /workflow/context/REJECTED_OPTIONS.md

## 9. Do Not Do
- Do not treat draft requirements as approved.
- Do not design database tables before domain modeling.
- Do not convert assumptions into domain rules.
- Do not ignore security/privacy requirements.
- Do not make Stage 4 depend on Stage 3 prompt history.
```

## 20. Decision / Assumption / Open Question Rules

```text
Approved Decision: only explicit human approval.
Decision Candidate: agent recommendation awaiting approval.
Working Assumption: temporary belief needed for progress; never a requirement.
Open Question: unresolved issue that may affect later work.
Rejected Option: explicitly rejected or superseded option; do not revive unless reopened.
Recommendation: suggestion only; not a decision.
```

Do not update `DECISIONS.md` without explicit human approval.

## 21. Specialization Hooks

Apply active specialization addenda after core and Stage 3 rules.

```text
web_saas:
  account lifecycle, auth/authz, tenant boundaries, admin operations, audit logs, APIs, rate limits, abuse handling

internal_tool:
  operator workflows, approvals, organizational constraints, admin overrides, manual correction, privileged-action auditability

mobile_app:
  device permissions, offline/sync, push notifications, platform constraints, app-store-sensitive behavior, local storage privacy

ai_data_product:
  dataset provenance, label trust, model output review, evaluation metrics, human review, reproducibility, failure modes, bias/error analysis

regulated_security_sensitive:
  auditability, access control granularity, retention/deletion, privacy impact, compliance questions, approval workflows, release blockers

brownfield_legacy:
  backward compatibility, migration constraints, regression-sensitive flows, behavior preservation, forbidden change areas, legacy data constraints
```

Specialization may add concerns, conditional artifacts, and review needs. It must not replace Stage 3 rules or approval requirements.

## 22. Failure Handling

If completion is unsafe, produce partial `result.md` with:

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

### Human Decision Needed
- ...
```

Do not pretend completion. Clearly labeled partial work is acceptable.

## 23. Validation Checklist

Before finishing, verify:

```text
[ ] Required sources were read or missing inputs were reported.
[ ] USER_DIRECTIVES.md was checked if present.
[ ] Each approved service goal is covered or explicitly out of scope.
[ ] Each primary stakeholder role is represented or has N/A rationale.
[ ] Stage 2 risk/privacy findings are reflected in requirements, constraints, or open questions.
[ ] Each requirement has acceptance criteria or a documented testability gap.
[ ] Acceptance criteria are observable and testable.
[ ] NFRs use measurable targets or review criteria where possible.
[ ] Requirements avoid architecture, schema, UI, or implementation design.
[ ] Security/privacy/data requirements are not silently deferred.
[ ] Non-goals and rejected options are preserved.
[ ] IDs are stable.
[ ] Traceability links are updated.
[ ] Assumptions and open questions are separated from requirements.
[ ] DECISIONS.md was not updated without explicit human approval.
[ ] context_packet.md is prepared for Stage 4.
[ ] Human approval gate is present.
[ ] Split assessment is recorded in result.md.
```

## 24. Split Policy

Default: keep Stage 3 as one executable SKILL.

```text
/skills/03_requirement_acceptance/SKILL.md
```

Reason: Stage 3 has a clear linear flow from source review to requirement decomposition, acceptance criteria, traceability, and context handoff. A single compact SKILL is usually easier to execute and review.

Split only if execution becomes too large or unreliable. If split, use a nested Stage Facade Pattern and preserve the same official Stage 3 artifact contract.

Recommended optional structure:

```text
/skills/03_requirement_acceptance/
  SKILL.md                         # parent stage entrypoint / orchestrator
  README.md                        # created separately
  artifact_contract.yml            # created separately

  /03a_requirement_source_review/SKILL.md
  /03b_requirement_decomposition/SKILL.md
  /03c_acceptance_criteria_writer/SKILL.md
  /03d_requirements_traceability_finalizer/SKILL.md
```

Suggested responsibilities:

```text
03a_requirement_source_review
- Read approved Stage 1–2 inputs, summarize source context, extract candidates, identify blockers.

03b_requirement_decomposition
- Create 03_requirements.md, assign stable IDs, classify requirements, preserve scope boundaries.

03c_acceptance_criteria_writer
- Create 03_acceptance_criteria.md, ensure observable criteria or testability gaps.

03d_requirements_traceability_finalizer
- Create 03_traceability_matrix.md, consolidate official artifacts, update result.md and context_packet.md, prepare approval gate.
```

Official Stage 3 artifacts must remain stable:

```text
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/03_requirements/03_traceability_matrix.md
/workflow/03_requirements/result.md
/workflow/context/context_packet.md
```

Downstream rule:

```text
Stage 4 depends on approved official Stage 3 artifacts, not on how many skills produced them.
Downstream stages must not depend on internal sub-skill outputs, sub-skill folder names, or prompt history.
```

If split later, the finalizer must consolidate official artifacts and prepare the approval gate before Stage 4 uses the outputs.

## 25. Do Not Do

```text
Do not treat agent-generated requirements as approved.
Do not invent requirements without source rationale.
Do not convert assumptions into requirements.
Do not silently expand scope.
Do not ignore non-goals or rejected options.
Do not ignore Stage 2 risk/privacy findings.
Do not design database schema, APIs, UI, architecture, or implementation tasks.
Do not create implementation prompts.
Do not write code or tests.
Do not use downstream stage artifacts as source of truth.
Do not update DECISIONS.md without explicit human approval.
Do not use context_packet.md as the only source of truth.
Do not make downstream stages depend on internal sub-skill structure.
Do not claim Stage 3 is complete without human review.
Do not create README.md or artifact_contract.yml as part of this SKILL file.
```
