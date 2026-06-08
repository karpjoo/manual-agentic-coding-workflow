# 07 MVP Release Slicing Skill Template

```yaml
---
template_name: 07_mvp_release_skill_template
template_type: stage_specific_skill_template
target_stage: "07 MVP Scope & Release Slicing"
target_reusable_skill: "/skills/07_mvp_release_slicing/SKILL.md"
recommended_template_path: "/workflow_templates/stage_templates/07_mvp_release_skill_template.md"
recommended_skill_folder: "/skills/07_mvp_release_slicing"
default_project_profile: "Greenfield MVP Production"
version: "1.0.0"
status: "draft"
---
```

---

# 07 MVP Scope & Release Slicing Skill Template

## 1. Template Purpose

This template defines the stage-specific rules for creating a reusable `SKILL.md` for Stage 7: MVP Scope & Release Slicing.

Stage 7 exists to prevent uncontrolled scope expansion by deciding:

* what belongs in the MVP;
* what should be deferred to later releases;
* what is explicitly out of scope;
* how approved requirements, architecture, and data design should be sliced into coherent, testable release increments.

This template must be used together with the Core Skill Template. It defines only Stage 7-specific extensions and must not duplicate the full core template.

---

## 2. Stage Purpose

The reusable Stage 7 SKILL created from this template must guide the Agent to:

1. read approved requirements, acceptance criteria, architecture, and data design artifacts;
2. classify requirements and capabilities into MVP, later release, and out-of-scope categories;
3. define release slices that are coherent, testable, and implementation-ready;
4. preserve traceability from goals and requirements to release slices;
5. expose trade-offs, risks, assumptions, and scope conflicts;
6. prepare the next Stage 8 Test Strategy & Validation Harness with clear scope boundaries.

The stage must not implement features, write tests, rewrite architecture, or create task cards.

---

## 3. Core Question

The Stage 7 SKILL must answer this central question:

```text
Given the approved service goal, requirements, domain model, architecture, and data design, what is the smallest coherent MVP that delivers validated user value, what should be deferred, what is explicitly out of scope, and in what release order should the remaining capabilities be delivered?
```

Supporting questions:

```text
1. Which requirements are essential for the MVP value proposition?
2. Which requirements are necessary dependencies but not visible user features?
3. Which requirements are important but can safely move to a later release?
4. Which requirements should be explicitly excluded from the current product scope?
5. What release slices are small enough for Agent-driven implementation planning?
6. What acceptance criteria must remain attached to each MVP item?
7. What architecture, data, security, privacy, or operational dependencies constrain release order?
8. What risks are introduced by deferring each requirement?
9. What must Stage 8 know in order to design validation around the approved MVP scope?
```

---

## 4. Stage Boundary

### This Stage Does

The Stage 7 SKILL should:

```text
- classify requirements into MVP / later / out-of-scope categories;
- identify dependency-driven sequencing constraints;
- define release slices;
- identify thin vertical slices where possible;
- link release slices to requirements and acceptance criteria;
- identify scope risks and deferral risks;
- identify validation implications for Stage 8;
- update traceability;
- prepare human approval gate for MVP scope and release order.
```

### This Stage Does Not

The Stage 7 SKILL must not:

```text
- create new product goals;
- rewrite approved requirements unless explicitly instructed;
- create new domain concepts unless an unresolved gap is discovered;
- redesign architecture;
- redesign database schema;
- create detailed test plans;
- create implementation task cards;
- write implementation prompts;
- implement code;
- treat Agent-proposed MVP scope as approved;
- treat deferred items as rejected unless explicitly marked as out of scope.
```

### Boundary with Previous Stage

Stage 6 Data Design defines data structures, query patterns, migrations, retention, deletion, and access rules. Stage 7 uses those decisions to sequence scope and releases. It must not redesign them.

### Boundary with Next Stage

Stage 8 Test Strategy & Validation Harness will design validation only after Stage 7 clarifies MVP scope, later release scope, and non-scope items. Stage 7 must hand off clear release-slice boundaries and requirement mappings.

---

## 5. Required Inputs

The reusable Stage 7 SKILL must define this input contract.

### 5.1 Always Read

The Stage 7 SKILL must always read these files when available:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md

/workflow/01_goal/01_service_goal.md

/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/03_requirements/03_traceability_matrix.md

/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md

/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md

/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/result.md
```

### 5.2 Read If Applicable

The Stage 7 SKILL must read these files only when the project context indicates they apply:

```text
/workflow/02_stakeholders_risk/02_stakeholders.md
- if user roles, stakeholders, operational actors, or value priority affect MVP scope.

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if security, privacy, compliance, sensitive data, personal data, external API, or LLM transfer concerns affect release order.

/workflow/04_domain/04_ubiquitous_language.md
- if terminology consistency affects release slice names or scope descriptions.

/workflow/04_domain/04_bounded_contexts.md
- if release slices cross bounded contexts or context boundaries.

/workflow/04_domain/04_domain_events.md
- if event-driven workflows affect release sequencing.

/workflow/05_architecture/05_api_contracts.md
- if APIs exist or API exposure affects MVP scope.

/workflow/05_architecture/05_integration_contracts.md
- if external integrations affect MVP feasibility or release sequencing.

/workflow/05_architecture/05_authz_model.md
- if roles, permissions, or authorization affect MVP scope.

/workflow/05_architecture/05_event_contracts.md
- if async messaging, events, queues, or background workflows exist.

/workflow/06_data/06_logical_schema.md
- if persistent data exists.

/workflow/06_data/06_physical_schema.md
- if implementation-facing storage choices affect release sequencing.

/workflow/06_data/06_indexes.md
- if query performance, search, filtering, reporting, or analytics affect MVP feasibility.

/workflow/06_data/06_migration_plan.md
- if schema or data migration affects release order.

/workflow/06_data/06_data_security_rules.md
- if data access control, row-level rules, document rules, or storage permissions affect MVP scope.

/workflow/00_intake/00_existing_context_review.md
- if this is a brownfield, migration, extension, or existing-codebase project.

/workflow/00_intake/00_project_intake.md
- if project profile, fixed stack, deadline, deployment target, or constraints affect MVP slicing.

/workflow/06_data/06_data_retention_deletion_policy.md
- if data retention, deletion, archival, or privacy lifecycle affects release scope.
```

### 5.3 Do Not Read By Default

The Stage 7 SKILL must not read these by default:

```text
- full historical agent logs;
- raw brainstorming notes from previous stages;
- superseded artifacts unless needed to understand a conflict;
- rejected artifacts unless checking REJECTED_OPTIONS.md;
- implementation source code unless this is explicitly a brownfield or migration project;
- test files unless Stage 7 is explicitly revising an existing release plan;
- draft artifacts not approved as source of truth;
- unrelated later-stage artifacts, such as task cards, implementation prompts, or implementation results.
```

---

## 6. Missing Input Handling

The Stage 7 SKILL must classify missing inputs as blocking or non-blocking.

### 6.1 Blocking Missing Inputs

The following are normally blocking:

```text
- missing approved service goal;
- missing approved requirements;
- missing acceptance criteria;
- missing approved architecture plan;
- missing Stage 6 data design result when persistent data exists;
- missing DECISIONS.md or approval log when scope-critical decisions are unclear;
- missing artifact_manifest.yml when artifact approval status cannot otherwise be determined.
```

If a blocking input is missing, the Agent must produce a Blocker Report and stop before producing final MVP scope.

### 6.2 Non-Blocking Missing Inputs

The following may be non-blocking if clearly recorded:

```text
- missing optional integration contracts when no integrations are in scope;
- missing data security rules when the system has no persistent user data or access control concerns;
- missing bounded contexts when the project is too simple for explicit context mapping;
- missing migration plan for a greenfield project with no existing data.
```

The Agent must record an N/A rationale or working assumption.

### 6.3 Missing Input Report Format

The reusable SKILL should require this format:

```markdown
## Missing Information

| Missing Input | Blocking? | Why It Matters | Safe Assumption, if Any | Required Human Action |
|---|---:|---|---|---|
|  | Yes/No |  |  |  |
```

---

## 7. Input Preflight Procedure

Before producing outputs, the Stage 7 SKILL must instruct the Agent to perform this preflight:

```text
[ ] Confirm current stage is Stage 7 MVP Scope & Release Slicing.
[ ] Read artifact_manifest.yml if available.
[ ] Read context_packet.md.
[ ] Read DECISIONS.md and APPROVAL_LOG.md if available.
[ ] Check USER_DIRECTIVES.md in /workflow/07_mvp_release/.
[ ] Identify approved source artifacts.
[ ] Identify draft, superseded, rejected, or conflicting artifacts.
[ ] Confirm requirements and acceptance criteria are available.
[ ] Confirm architecture and data design constraints are available.
[ ] Identify security/privacy constraints that affect release order.
[ ] Identify unresolved open questions that could affect MVP scope.
[ ] Restate the current task and scope boundary.
[ ] Report blocking inputs before proceeding.
```

---

## 8. Output Artifact Contract

The Stage 7 SKILL must define the following output artifacts.

### 8.1 Mandatory Artifacts

```text
/workflow/07_mvp_release/07_mvp_scope.md
- Defines the approved-candidate MVP scope, requirement classification, must-have capabilities, and exclusion rationale.

/workflow/07_mvp_release/07_release_slices.md
- Defines release slices, release order, slice goals, linked requirements, dependencies, risks, and validation implications.

/workflow/07_mvp_release/07_out_of_scope.md
- Defines explicit non-scope and deferred items, with rationale and conditions for reconsideration.

/workflow/07_mvp_release/07_scope_traceability_matrix.md
- Links goals, requirements, acceptance criteria, architecture/data dependencies, and release slices.

/workflow/07_mvp_release/result.md
- Summarizes Stage 7 execution, inputs used, outputs created, decisions needed, assumptions, risks, and next step.
```

### 8.2 Conditional Artifacts

```text
/workflow/07_mvp_release/07_release_risk_register.md
- Create if release sequencing introduces significant business, technical, security, privacy, operational, migration, or delivery risks.

/workflow/07_mvp_release/07_dependency_map.md
- Create if release slices have non-trivial dependencies across requirements, bounded contexts, modules, APIs, integrations, data models, or migrations.

/workflow/07_mvp_release/07_scope_tradeoff_analysis.md
- Create if multiple plausible MVP boundaries exist and need human comparison.

/workflow/07_mvp_release/07_specialization_scope_notes.md
- Create if project-type specialization adds scope concerns, such as AI evaluation, mobile app release constraints, regulated compliance gates, or brownfield migration constraints.
```

### 8.3 N/A Record Rule

If a conditional artifact is not created, the Agent must record:

```markdown
## N/A Records

| Conditional Artifact | Why Not Applicable | Revisit If |
|---|---|---|
| 07_release_risk_register.md |  |  |
| 07_dependency_map.md |  |  |
| 07_scope_tradeoff_analysis.md |  |  |
| 07_specialization_scope_notes.md |  |  |
```

---

## 9. Required Output Structure

### 9.1 `07_mvp_scope.md`

The reusable SKILL must require this structure:

```markdown
# 07 MVP Scope

## 1. Stage Status
- Status: Draft / Needs Review / Approved
- Source artifacts:
- Approval required:

## 2. MVP Definition Summary
- MVP purpose:
- Primary user value:
- Minimum success outcome:
- What the MVP proves:
- What the MVP intentionally does not prove:

## 3. Scope Classification Method
- Classification categories:
  - Must
  - Should
  - Could
  - Later
  - Won't / Non-scope
- Decision criteria used:
- Constraints considered:

## 4. MVP Must-Have Scope

| Scope Item ID | Linked Requirement IDs | Capability | User / Actor | Acceptance Criteria Links | Rationale | Dependency Notes |
|---|---|---|---|---|---|---|

## 5. MVP Supporting / Enabling Scope

| Scope Item ID | Linked Requirement IDs | Enabling Capability | Why Needed for MVP | Architecture/Data Dependency | User-visible? |
|---|---|---|---|---|---|

## 6. Should-Have Candidates

| Scope Item ID | Linked Requirement IDs | Capability | Why Not Must | Risk If Deferred | Reconsideration Trigger |
|---|---|---|---|---|---|

## 7. Could-Have Candidates

| Scope Item ID | Linked Requirement IDs | Capability | Value | Deferral Rationale | Reconsideration Trigger |
|---|---|---|---|---|---|

## 8. Later Release Items

| Scope Item ID | Linked Requirement IDs | Capability | Proposed Release | Deferral Rationale | Dependency Notes |
|---|---|---|---|---|---|

## 9. Won't / Non-Scope Items

| Scope Item ID | Linked Requirement IDs | Capability / Idea | Reason Excluded | Reopen Only If |
|---|---|---|---|---|

## 10. Security / Privacy / Compliance Scope Notes
- Required in MVP:
- Deferred:
- Must not defer:
- Open concerns:

## 11. Operational / Deployment Scope Notes
- Required in MVP:
- Deferred:
- Must not defer:
- Open concerns:

## 12. Scope Risks
| Risk ID | Risk | Affected Scope | Severity | Mitigation | Human Review Needed? |
|---|---|---|---|---|---|

## 13. Decision Candidates
- Candidate decisions requiring approval.

## 14. Working Assumptions
- Assumptions used to classify scope.

## 15. Open Questions
- Questions that may change MVP scope.

## 16. Human Approval Required
```

### 9.2 `07_release_slices.md`

The reusable SKILL must require this structure:

```markdown
# 07 Release Slices

## 1. Release Strategy Summary
- Release strategy:
- Release slicing principle:
- Smallest coherent vertical slice:
- Validation dependency:

## 2. Release Slice Overview

| Release ID | Release Name | Goal | Scope Summary | Primary Users | Validation Focus | Status |
|---|---|---|---|---|---|---|

## 3. Release Slice Details

### Release R0 / Foundation, if applicable
- Purpose:
- Included scope items:
- Linked requirements:
- Architecture dependencies:
- Data dependencies:
- Security/privacy dependencies:
- Validation implications:
- Not included:

### Release R1 / MVP
- Purpose:
- Included scope items:
- Linked requirements:
- Acceptance criteria included:
- Architecture dependencies:
- Data dependencies:
- Security/privacy dependencies:
- Manual validation implications:
- Automated validation implications:
- Exit criteria:
- Not included:

### Release R2 / Post-MVP
- Purpose:
- Included scope items:
- Linked requirements:
- Dependencies:
- Validation implications:
- Reconsideration triggers:

## 4. Dependency-Driven Ordering

| Dependency | Source | Affected Release | Why It Affects Order | Alternative |
|---|---|---|---|---|

## 5. Deferred Requirement Impact

| Requirement ID | Deferred To | Impact | Risk | Mitigation |
|---|---|---|---|---|

## 6. Release Risks

| Risk ID | Release | Risk | Severity | Mitigation | Approval Needed |
|---|---|---|---|---|---|

## 7. Stage 8 Validation Handoff
- Requirements Stage 8 must validate:
- Scope items Stage 8 should not validate yet:
- Security/privacy behavior requiring tests:
- Manual validation likely needed:
- Automated validation likely needed:
- Known validation gaps:

## 8. Human Approval Required
```

### 9.3 `07_out_of_scope.md`

The reusable SKILL must require this structure:

```markdown
# 07 Out of Scope

## 1. Purpose
This artifact records what must not be built in the MVP or current release plan unless explicitly reopened.

## 2. Explicit Non-Scope Items

| Non-Scope ID | Item | Related Requirement / Idea | Reason | Reopen Only If | Notes |
|---|---|---|---|---|---|

## 3. Deferred but Not Rejected Items

| Deferred ID | Item | Deferred To | Reason | Reconsideration Trigger | Risk If Forgotten |
|---|---|---|---|---|---|

## 4. Rejected Options to Record

| Rejected Option | Source | Reason Rejected | Must Not Reappear Unless |
|---|---|---|---|

## 5. Scope Creep Watchlist

| Watch Item | Why It May Reappear | How To Handle |
|---|---|---|

## 6. Human Approval Required
```

### 9.4 `07_scope_traceability_matrix.md`

The reusable SKILL must require this structure:

```markdown
# 07 Scope Traceability Matrix

| Goal ID | Requirement ID | Acceptance Criteria ID | Domain Concept | Architecture / Module | Data Artifact | Scope Category | Release Slice | Validation Handoff |
|---|---|---|---|---|---|---|---|---|
```

### 9.5 `result.md`

The reusable SKILL must require this structure:

```markdown
# Result: 07 MVP Scope & Release Slicing

## 1. Task Summary

## 2. Inputs Used

## 3. Outputs Created or Updated

## 4. MVP Scope Summary

## 5. Release Slice Summary

## 6. Out-of-Scope Summary

## 7. Decision Candidates

## 8. Working Assumptions

## 9. Open Questions

## 10. Risks and Constraints

## 11. Rejected or Superseded Options

## 12. Traceability Updates

## 13. N/A Items

## 14. Stage 8 Handoff Notes

## 15. Human Approval Required

## 16. Recommended Next Step
```

---

## 10. Stage-Specific Procedure

The reusable Stage 7 SKILL must instruct the Agent to follow this procedure.

### Step 1. Confirm Stage Context

```text
- Confirm this is Stage 7 MVP Scope & Release Slicing.
- Confirm Stage 6 is complete or identify why partial execution is being requested.
- Confirm whether the project profile is prototype, MVP production, regulated/security-sensitive, AI/data product, mobile app, internal tool, or brownfield.
```

### Step 2. Read Approved Source Artifacts

```text
- Read only approved artifacts as source of truth.
- If using draft artifacts, label them clearly and explain why.
- Check whether any requirement, architecture decision, or data design item is marked rejected or superseded.
```

### Step 3. Build Requirement Inventory for Scope Decisions

```text
- Extract all requirement IDs.
- Extract acceptance criteria.
- Identify user roles and business value.
- Identify security/privacy requirements.
- Identify non-functional requirements.
- Identify data, architecture, and integration dependencies.
```

### Step 4. Define Scope Classification Criteria

The Agent must define and apply criteria such as:

```text
- essential to primary service goal;
- essential to primary user value;
- required for legal/security/privacy correctness;
- required for data integrity;
- required dependency for another MVP item;
- needed for meaningful validation;
- can be simulated manually;
- can be deferred without invalidating MVP;
- high implementation complexity relative to MVP value;
- high uncertainty requiring later discovery;
- explicitly rejected or non-scope.
```

### Step 5. Classify Requirements and Capabilities

Use these categories:

```text
Must
- Required for MVP value, correctness, or safe operation.

Should
- Important, but MVP can still validate core value without it.

Could
- Useful enhancement with limited MVP necessity.

Later
- Valid product direction but intentionally deferred.

Won't / Non-scope
- Explicitly excluded unless reopened by human approval.
```

The Agent must explain each classification.

### Step 6. Identify MVP Thin Slice

The Agent must define the smallest coherent MVP slice:

```text
- user-visible workflow;
- required supporting backend/data/security pieces;
- minimum acceptance criteria;
- excluded enhancements;
- validation implication;
- risks of being too small.
```

### Step 7. Define Release Slices

The Agent must define release slices that are:

```text
- coherent;
- value-oriented;
- traceable to requirements;
- feasible given architecture and data dependencies;
- small enough for Stage 9 task breakdown;
- testable by Stage 8 validation strategy.
```

Preferred release slice pattern:

```text
R0 Foundation / Setup, if needed
R1 MVP
R2 Post-MVP Enhancements
R3 Advanced / Scale / Optimization, if needed
```

The Agent must not create too many releases unless justified.

### Step 8. Check Dependency Order

The Agent must identify dependencies across:

```text
- requirements;
- acceptance criteria;
- domain invariants;
- modules;
- APIs;
- integrations;
- authentication/authorization;
- data models;
- migrations;
- indexes;
- security rules;
- privacy rules;
- operations or deployment.
```

If a dependency blocks the proposed release order, the Agent must revise the release order or record a decision candidate.

### Step 9. Identify Deferral Risks

For every deferred item, the Agent must record:

```text
- what is deferred;
- why it is deferred;
- what risk is introduced;
- how to mitigate the risk;
- what trigger should reopen the item;
- whether the deferral needs human approval.
```

### Step 10. Identify Out-of-Scope Items

The Agent must separate:

```text
Deferred Later
≠ Rejected
≠ Explicit Non-Scope
≠ Unknown / Open Question
```

Only items explicitly excluded should be recorded as non-scope or rejected.

### Step 11. Prepare Stage 8 Handoff

The Agent must prepare Stage 8 with:

```text
- MVP requirements to validate;
- release slices to validate separately;
- non-scope items that should not receive tests yet;
- manual validation candidates;
- likely automated validation candidates;
- security/privacy behavior that must be validated;
- acceptance criteria that are deferred;
- validation gaps caused by unresolved questions.
```

### Step 12. Update Traceability

The Agent must update traceability so that:

```text
Goal
→ Requirement
→ Acceptance Criteria
→ Scope Category
→ Release Slice
→ Stage 8 Validation Handoff
```

If domain, architecture, or data dependencies affect scope, include those links.

### Step 13. Prepare Human Approval Gate

The Agent must list:

```text
- MVP scope decisions to approve;
- out-of-scope items to approve;
- release order to approve;
- assumptions to confirm;
- open questions to resolve;
- risks to review;
- artifacts ready for review.
```

---

## 11. Traceability Requirements

The Stage 7 SKILL must preserve and improve traceability.

### 11.1 Required Links

At minimum, Stage 7 must link:

```text
Service Goal → Requirement
Requirement → Acceptance Criteria
Requirement → Scope Category
Requirement → Release Slice
Release Slice → Validation Handoff for Stage 8
```

Where applicable, also link:

```text
Requirement → Domain Invariant
Requirement → Module / API / Integration
Requirement → Data Model / Security Rule / Migration
Requirement → Release Dependency
```

### 11.2 Stable ID Conventions

The reusable SKILL should use stable IDs such as:

```text
SCOPE-001, SCOPE-002
REL-001, REL-002
NON-SCOPE-001, NON-SCOPE-002
DEF-001, DEF-002
RISK-001, RISK-002
```

The SKILL must not rename existing requirement IDs unless explicitly instructed.

### 11.3 Traceability Gaps

If links cannot be completed, record:

```markdown
## Traceability Gaps

| Gap ID | Missing Link | Why Missing | Risk | Required Human / Upstream Action |
|---|---|---|---|---|
```

---

## 12. Decision / Assumption / Open Question Rules

The Stage 7 SKILL must apply these classification rules.

### 12.1 Approved Decisions

Only explicit human approval can create approved decisions.

Examples:

```text
Approved: MVP includes email/password login only.
Approved: Public sharing is out of scope for MVP.
Approved: Release 1 excludes analytics dashboards.
```

### 12.2 Decision Candidates

Agent recommendations must remain decision candidates.

Examples:

```text
Candidate: Move advanced reporting to Release 2.
Candidate: Include audit logging in MVP because role-based access affects sensitive data.
Candidate: Exclude mobile app support from MVP.
```

### 12.3 Working Assumptions

Assumptions must remain assumptions until confirmed.

Examples:

```text
Assumption: The MVP is intended for production pilot use, not only internal demo.
Assumption: Manual admin setup is acceptable for Release 1.
Assumption: Advanced analytics can be deferred without invalidating MVP success.
```

### 12.4 Open Questions

Open questions must be recorded when unresolved issues can change scope.

Examples:

```text
Open Question: Is third-party payment integration required for MVP validation?
Open Question: Must user deletion be self-service in MVP, or can it be handled manually by admins?
Open Question: Does compliance require audit logs before any production pilot?
```

### 12.5 Rejected Options

Rejected options must not be revived unless explicitly reopened.

Examples:

```text
Rejected: Do not include social login in MVP unless reopened by the human developer.
Rejected: Do not support native mobile app release in the first MVP.
```

---

## 13. Stage-Specific Validation Checklist

The generated reusable SKILL must include this checklist.

```text
[ ] Stage 7 purpose and boundary are clear.
[ ] Only approved source artifacts were used as source of truth, or drafts were labeled.
[ ] Requirements were classified into Must / Should / Could / Later / Won't.
[ ] Each MVP item links to requirement IDs.
[ ] Each MVP item links to acceptance criteria where available.
[ ] MVP supporting/enabling scope is separated from user-visible scope.
[ ] Deferred items are not treated as rejected.
[ ] Non-scope items are explicitly justified.
[ ] Release slices are coherent and testable.
[ ] Release slices respect architecture and data dependencies.
[ ] Security/privacy/compliance items that cannot be deferred are identified.
[ ] Data migration or data security dependencies affecting release order are identified.
[ ] Scope risks and deferral risks are recorded.
[ ] Traceability matrix was updated.
[ ] Stage 8 validation handoff is clear.
[ ] context_packet.md was prepared for Stage 8.
[ ] Human approval gate is explicit.
[ ] No implementation tasks were created.
[ ] No test strategy was fully designed.
[ ] No architecture or data design was rewritten.
```

---

## 14. Human Approval Gate

The Stage 7 SKILL must end with this approval gate.

```markdown
## Human Approval Required

### Decisions to Approve
- MVP scope items.
- Supporting/enabling scope items.
- Deferred requirements.
- Explicit out-of-scope items.
- Release slice order.
- Scope trade-offs.
- Security/privacy/compliance items that must be included in MVP.

### Assumptions to Confirm
- MVP target user and usage context.
- Acceptable manual workarounds.
- Acceptable deferrals.
- Release timeline assumptions, if any.
- Operational assumptions.

### Open Questions to Resolve
- Questions that may change MVP scope.
- Questions that may block Stage 8 validation planning.
- Questions that may affect security, privacy, data, or compliance.

### Risks to Review
- Deferral risks.
- Scope creep risks.
- Architecture/data dependency risks.
- Security/privacy risks.
- Operational readiness risks.
- Validation risks.

### Artifacts Ready for Review
- /workflow/07_mvp_release/07_mvp_scope.md
- /workflow/07_mvp_release/07_release_slices.md
- /workflow/07_mvp_release/07_out_of_scope.md
- /workflow/07_mvp_release/07_scope_traceability_matrix.md
- /workflow/07_mvp_release/result.md
- Conditional artifacts, if created.

### Recommended Next Step
- Human reviews and approves or revises MVP scope and release order.
- After approval, run Stage 8 Test Strategy & Validation Harness.
```

The Agent must not proceed as if Stage 7 is approved until the human explicitly approves it.

---

## 15. Context Packet Update Rules

The Stage 7 SKILL must update or prepare `/workflow/context/context_packet.md` for Stage 8.

### 15.1 Required Context Packet Sections

The Stage 7 update must include:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 07 MVP Scope & Release Slicing
- Completed stages:
- Next recommended stage: 08 Test Strategy & Validation Harness
- Stage 7 status: Draft / Needs Review / Approved

## 2. Approved Decisions
- Only human-approved Stage 7 decisions.
- If Stage 7 is not approved, state that scope is pending approval.

## 3. Working Assumptions
- MVP assumptions.
- Release sequencing assumptions.
- Deferral assumptions.

## 4. Open Questions
- Questions that could affect Stage 8 validation design.
- Questions that could change MVP scope.

## 5. Rejected / Superseded Options
- Explicit non-scope or rejected scope items.
- Superseded release order options.

## 6. Constraints That Must Not Be Violated
- Scope constraints.
- Security/privacy constraints.
- Architecture constraints.
- Data constraints.
- Operational constraints.
- Schedule constraints, if approved.

## 7. Key Context for Next Stage
- MVP scope summary.
- Release slice summary.
- Non-scope items.
- Validation-sensitive risks.
- Requirements to prioritize in Stage 8.

## 8. Required Inputs for Next Stage
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/06_data/result.md
- /workflow/07_mvp_release/07_mvp_scope.md
- /workflow/07_mvp_release/07_release_slices.md
- /workflow/07_mvp_release/07_out_of_scope.md
- /workflow/07_mvp_release/07_scope_traceability_matrix.md

## 9. Do Not Do
- Do not validate out-of-scope items as MVP requirements.
- Do not create tests for deferred items unless explicitly needed as regression guards.
- Do not treat unapproved Stage 7 scope as final.
- Do not revive rejected scope items unless reopened by the human developer.
```

### 15.2 Context Packet Principles

The Agent must:

```text
- keep context_packet.md concise;
- point to Stage 7 artifacts rather than copying them;
- include only context needed by Stage 8;
- clearly mark unapproved scope as pending approval;
- avoid recording Agent proposals as approved decisions.
```

---

## 16. Specialization Hooks

The reusable SKILL created from this template must support specialization addenda without embedding project-type-specific logic into the core Stage 7 procedure.

### 16.1 Web SaaS

May add:

```text
- subscription tier slicing;
- admin/user/organization release boundaries;
- auth and billing deferral rules;
- tenant isolation and data access constraints;
- public launch versus private beta scope.
```

### 16.2 Internal Tool

May add:

```text
- operator workflow priority;
- manual workaround acceptability;
- internal admin-only MVP;
- organizational rollout slices;
- spreadsheet/manual process replacement criteria.
```

### 16.3 Mobile App

May add:

```text
- platform-specific release slicing;
- offline/sync deferral decisions;
- app store release constraints;
- device permission scope;
- push notification deferral decisions.
```

### 16.4 AI / Data Product

May add:

```text
- dataset availability as release dependency;
- evaluation metric readiness;
- model-in-the-loop versus human-in-the-loop MVP boundary;
- model output review requirements;
- baseline model versus advanced model release slicing.
```

### 16.5 Regulated / Security-Sensitive

May add:

```text
- compliance-driven MVP minimums;
- audit logging required in MVP;
- privacy controls that cannot be deferred;
- security release blockers;
- approval evidence requirements.
```

### 16.6 Brownfield / Legacy

May add:

```text
- migration-first release slice;
- compatibility scope;
- regression-sensitive slicing;
- legacy data conversion dependencies;
- rollout and rollback constraints.
```

Specialization must not weaken:

```text
- human approval rules;
- artifact contract;
- assumption handling;
- traceability rules;
- stage boundary;
- context handoff rules.
```

---

## 17. Tool Wrapper Hook

Tool-specific wrappers may define:

```text
- where to save generated SKILL.md;
- command invocation convention;
- sandbox or permission rules;
- file creation conventions;
- review workflow;
- artifact validation automation.
```

Tool wrappers must not define:

```text
- MVP scope decisions;
- release order decisions;
- requirement priority;
- architecture trade-offs;
- data design decisions;
- security or privacy policy.
```

---

## 18. Anti-Patterns to Avoid

The reusable Stage 7 SKILL must warn against these anti-patterns:

```text
- treating every requirement as MVP;
- treating every deferred item as rejected;
- creating a feature list without requirement IDs;
- creating release slices that cannot be validated;
- ignoring architecture or data dependencies;
- deferring security/privacy requirements that are required for safe MVP operation;
- using MoSCoW categories without rationale;
- treating Agent priority recommendations as human-approved scope;
- expanding MVP to include all attractive enhancements;
- creating implementation tasks prematurely;
- writing detailed tests before Stage 8;
- rewriting upstream requirements instead of recording conflicts;
- using unapproved draft artifacts as source of truth;
- failing to update context_packet.md for Stage 8.
```

---

## 19. Failure Handling

If Stage 7 cannot be completed safely, the reusable SKILL must require a partial result with this structure:

```markdown
## Blocker Report

### Blocking Issue
- Describe the issue.

### Why It Matters
- Explain how it affects MVP scope or release slicing.

### Affected Artifacts or Stages
- List affected source artifacts and downstream stages.

### Safe Partial Work Completed
- List any non-final inventory or analysis completed.

### Human Decision Needed
- State the specific decision needed.

### Recommended Recovery Step
- State what should be fixed before rerunning or continuing Stage 7.
```

Blocking examples:

```text
- requirements are not approved;
- acceptance criteria are missing;
- architecture or data design conflicts with MVP requirements;
- security/privacy constraints are unresolved;
- all scope classifications depend on unresolved business decisions;
- artifact approval status cannot be determined.
```

---

## 20. Minimum Acceptance Criteria for the Generated SKILL.md

A reusable Stage 7 `SKILL.md` generated from this template is acceptable only if:

```text
[ ] It follows the Core Skill Template.
[ ] It clearly identifies Stage 7 MVP Scope & Release Slicing.
[ ] It defines Always Read inputs.
[ ] It defines Read If Applicable inputs.
[ ] It defines Do Not Read By Default inputs.
[ ] It defines missing input handling.
[ ] It defines mandatory Stage 7 artifacts.
[ ] It defines conditional Stage 7 artifacts.
[ ] It defines N/A record rules.
[ ] It defines the Stage 7 execution procedure.
[ ] It defines scope classification criteria.
[ ] It defines release slicing rules.
[ ] It preserves requirement and acceptance criteria traceability.
[ ] It identifies architecture and data dependency effects.
[ ] It includes security/privacy awareness.
[ ] It prepares Stage 8 validation handoff.
[ ] It includes context_packet.md update rules.
[ ] It separates approved decisions, decision candidates, assumptions, open questions, risks, and rejected options.
[ ] It includes a human approval gate.
[ ] It does not create implementation tasks.
[ ] It does not write test strategy details that belong to Stage 8.
[ ] It does not include project-specific product content.
[ ] It can be executed from files only after context reset.
```

---

## 21. Prompt to Generate the Executable Reusable SKILL.md

Use this prompt after saving this template:

```text
You are creating an executable reusable SKILL.md for a Manual Agentic Coding Workflow.

Use the following source documents:
- /workflow_templates/core/core_skill_template.md
- /workflow_templates/stage_templates/07_mvp_release_skill_template.md
- agentic-coding-workflow-concept-and-design.md
- skill-template-design-principles.md

Target output:
- /skills/07_mvp_release_slicing/SKILL.md

Create a reusable SKILL.md that an Agent can actually execute.

The SKILL.md must:
1. follow the Core Skill Template;
2. implement the Stage 7 MVP Scope & Release Slicing template;
3. define required inputs and conditional inputs;
4. define output artifacts and required sections;
5. define the execution procedure;
6. define traceability rules;
7. define decision / assumption / open question handling;
8. define context_packet.md update rules;
9. include a human approval gate;
10. avoid project-specific details.

Rules:
- This SKILL.md is reusable across projects.
- Project-specific information must come from approved artifacts, context_packet.md, artifact_manifest.yml, and USER_DIRECTIVES.md.
- Do not assume missing information.
- Mark assumptions explicitly.
- Do not treat Agent proposals as approved decisions.
- Do not create project artifacts under /workflow while generating the reusable SKILL.
- The final file must be saved as /skills/07_mvp_release_slicing/SKILL.md.
```

---

## 22. Template Design Notes

This template intentionally treats Stage 7 as a planning and scoping stage, not as a task breakdown, testing, or implementation stage.

Official Stage 7 artifacts are designed to become the source for Stage 8 Test Strategy and Stage 9 Task Breakdown only after human approval.

The downstream stages should depend on approved official Stage 7 artifacts, not on chat history or unapproved Agent recommendations.
