---
name: 02_stakeholder_risk_framing
description: Execute Stage 2 after Service Goal Definition and before Requirements & Acceptance Criteria to identify stakeholders, role/permission directions, personal or sensitive data, external transfers, administrator powers, audit needs, and early security/privacy risks.
stage: "02 - Stakeholder & Risk Framing"
version: 1.0.0
status: draft
primary_output: "/workflow/02_stakeholders_risk/02_stakeholders.md"
requires_human_approval: true
---

# 02 Stakeholder & Risk Framing SKILL

## 1. Purpose

Execute Stage 2 of the Manual Agentic Coding Workflow.

This SKILL identifies who or what can affect or be affected by the system, and what role, permission, data, privacy, security, compliance, abuse, external-transfer, administrator-power, and operational risks must be considered before requirements are decomposed.

This SKILL creates draft Stage 2 artifacts for human review. It does not approve decisions.

---

## 2. Operating Mode

You are a structured development assistant, not an autonomous decision-maker.

Maintain these distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```

Classify all important findings as one of:

- Approved Decision: explicitly approved by the human developer.
- Decision Candidate: proposed by the agent and awaiting approval.
- Working Assumption: useful but unverified.
- Open Question: unresolved issue affecting later work.
- Risk: possible harm, exposure, abuse, failure, compliance issue, or operational concern.
- Rejected / Superseded Option: explicitly rejected or replaced.

Do not update `/workflow/context/DECISIONS.md` unless explicit human approval already exists.

---

## 3. When to Use

Use this SKILL when:

- Stage 0 Project Intake has provided project context.
- Stage 1 Service Goal Definition has provided a service goal direction.
- Requirements have not yet been decomposed.
- Stakeholder, role, permission, data, privacy, security, external-transfer, or audit framing is needed.

Do not use this SKILL to:

- Write final functional requirements or acceptance criteria.
- Finalize authorization implementation.
- Design architecture, APIs, domain model, database schema, tests, tasks, or implementation.
- Perform final release security review.
- Perform a full formal threat model unless a specialization addendum requires it.

---

## 4. Input Precedence

When inputs conflict, apply this order:

```text
1. Current explicit user instruction
2. /workflow/02_stakeholders_risk/USER_DIRECTIVES.md
3. /workflow/context/APPROVAL_LOG.md and /workflow/context/DECISIONS.md
4. /workflow/context/artifact_manifest.yml
5. /workflow/context/context_packet.md
6. Approved stage artifacts
7. /workflow/context/ASSUMPTIONS.md
8. Agent inference
```

Conflict handling:

- Do not silently resolve conflicts.
- Identify conflicting sources.
- Explain impact.
- Continue only if non-blocking.
- Stop and write a Blocker Report if the conflict affects scope, roles, permissions, privacy, security, external transfer, compliance, or requirements framing.

---

## 5. Required Inputs

### 5.1 Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/00_intake/00_project_intake.md
/workflow/01_goal/01_service_goal.md
```

### 5.2 Read If Applicable

```text
/workflow/00_intake/00_existing_context_review.md
  if brownfield, legacy, integration-heavy, migration, extension, or existing-codebase work

/workflow/00_intake/review_notes.md
  if Stage 0 review comments, corrections, constraints, or approvals exist

/workflow/01_goal/review_notes.md
  if Stage 1 review comments, corrections, goal changes, or approvals exist

/workflow/02_stakeholders_risk/USER_DIRECTIVES.md
  if present; always read before analysis

/workflow_templates/specializations/web_saas.md
  if browser-based, tenant-based, account-based, or multi-user web service

/workflow_templates/specializations/internal_tool.md
  if internal staff, admin, operations, or back-office tool

/workflow_templates/specializations/mobile_app.md
  if mobile app, device permissions, local storage, push notifications, or offline sync

/workflow_templates/specializations/ai_data_product.md
  if AI/ML/LLM, datasets, model outputs, synthetic data, labeling, or human model/data review

/workflow_templates/specializations/regulated_security_sensitive.md
  if regulated, security-sensitive, privacy-sensitive, institutional, legal, healthcare, financial, child-related, or high-risk data

/workflow_templates/specializations/brownfield_legacy.md
  if existing roles, permissions, data flows, integrations, or forbidden change areas exist
```

### 5.3 Do Not Read By Default

- Raw chat history or full agent logs.
- Superseded or rejected artifacts except to understand why they were rejected.
- Draft artifacts from Stage 3 or later.
- Source code unless brownfield risk review requires it.
- Later architecture, data design, test strategy, task breakdown, implementation, or release artifacts.

---

## 6. Missing Input Handling

### Blocking by Default

Stop and write a Blocker Report if any of these occur:

- Missing `/workflow/01_goal/01_service_goal.md`.
- Missing service goal direction.
- Missing project type when it materially affects stakeholder scope, privacy, security, regulation, or external transfer.
- User directive conflicts with approved decisions on roles, permissions, personal data, sensitive data, external transfer, or non-scope.
- A rejected or superseded artifact is referenced as current truth.

Blocker Report structure:

```markdown
# Result: 02 Stakeholder & Risk Framing

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

### Non-Blocking by Default

Proceed with a clearly marked working assumption if these are missing:

- `APPROVAL_LOG.md`
- `REJECTED_OPTIONS.md`
- `review_notes.md`
- optional specialization addendum
- conditional artifact not activated by project profile or context

Record the gap in `result.md` and, if it affects later work, in `OPEN_QUESTIONS.md`.

---

## 7. USER_DIRECTIVES.md Handling

If `/workflow/02_stakeholders_risk/USER_DIRECTIVES.md` exists:

1. Read it before stage analysis.
2. Classify each directive as approval, correction, preference, requirement candidate, rejection, scope change, open question, or constraint.
3. Apply it before agent assumptions.
4. Do not treat every directive as a globally approved decision.
5. Report conflicts with approved decisions.
6. Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

---

## 8. Stage Boundaries

### This Stage Does

- Identify primary, secondary, operational, administrative, external, and affected stakeholders.
- Propose preliminary role and permission directions.
- Identify privileged/admin/support/reviewer/operator powers.
- Identify personal, sensitive, confidential, regulated, logged, uploaded, derived, model, dataset, or externally transferred data.
- Identify external API, LLM, analytics, monitoring, cloud, email/SMS, payment, dataset, vendor, export, or human-review transfer exposure.
- Identify early security, privacy, compliance, abuse, misuse, and operational risks.
- Identify audit and accountability needs.
- Produce Stage 3 implications without writing Stage 3 requirements.

### This Stage Does Not

- Write final functional requirements.
- Write acceptance criteria.
- Finalize RBAC/ABAC, policy engine, or permission implementation.
- Design APIs, architecture, database schema, domain model, test strategy, tasks, or code.
- Treat role, permission, privacy, security, data handling, or external-transfer proposals as approved.
- Claim “no security/privacy risk” without evidence and N/A rationale.

---

## 9. Execution Procedure

### Step 1. Preflight

Record a concise preflight in `result.md`:

```text
[ ] Current SKILL.md read.
[ ] artifact_manifest.yml checked if available.
[ ] context_packet.md checked if available.
[ ] DECISIONS.md checked if available.
[ ] USER_DIRECTIVES.md checked if present.
[ ] Always Read inputs checked.
[ ] Conditional inputs activated or marked N/A.
[ ] Required source artifacts exist or missing inputs recorded.
[ ] Source artifact approval status checked where available.
[ ] Superseded or rejected inputs avoided unless explicitly used for history.
[ ] Conflicts, missing inputs, and assumptions identified.
[ ] Stage 2 task restated.
```

If required sources are drafts, use them only as draft inputs and label Stage 2 outputs as draft.

### Step 2. Restate Current Task

In `result.md`, restate:

- current stage
- service goal source
- active project profile if known
- approved constraints already known
- what this stage will and will not produce

### Step 3. Identify Stakeholders

Consider:

```text
primary users, secondary users, administrators, operators, maintainers, reviewers,
moderators, approvers, support staff, internal business stakeholders,
external organizations, external systems/providers, data subjects,
affected non-users, compliance/legal/audit stakeholders, misuse/abuse actors
```

For each stakeholder, record:

```text
Stakeholder ID:
Name / Category:
Type:
Description:
Goals / Interests:
Main Actions:
Data Access or Exposure:
Risk Relevance:
Status: approved / candidate / assumption / open question
Source:
Stage 3 Implication:
```

Use IDs: `STK-001`, `STK-002`, ...

### Step 4. Identify Role and Permission Candidates

For each role candidate, record:

```text
Role ID:
Role Name:
Actor Type:
Purpose:
Likely Permissions:
Forbidden Actions:
Sensitive Operations:
Data Access Level:
Authentication Need:
Authorization Need:
Audit Need:
Decision Status:
Source:
Stage 3 Implication:
```

Use IDs: `ROLE-001`, `ROLE-002`, ...

Separate business role, technical permission, operational responsibility, approval authority, and support/admin capability.

### Step 5. Review Administrator and Privileged Powers

Check elevated operations such as:

```text
view all records, view sensitive data, delete data, export data, change roles,
approve/reject/moderate, trigger irreversible actions, access logs,
configure integrations, impersonate users, override workflow states,
rerun model/data processing, access system metadata
```

For each power, record:

```text
Power ID:
Description:
Role Candidate:
Affected Data or Object:
Risk:
Audit Required:
Approval Required:
Reversibility:
Recommended Constraint:
Decision Status:
Stage 3 Implication:
```

Use IDs: `POWER-001`, `POWER-002`, ...

Create `02_admin_power_review.md` if privileged operations are meaningful.

### Step 6. Identify Data Categories

Classify data that may be created, viewed, stored, transmitted, logged, exported, processed, inferred, or deleted.

Baseline categories:

```text
account/profile, contact, authentication, user-generated content, uploaded files,
logs/analytics, operational metadata, payment/billing, personal data,
sensitive personal data, confidential business data, regulated data,
research data/dataset records, model input/output, synthetic data, third-party data
```

For each category, record:

```text
Data ID:
Data Category:
Description:
Data Subject:
Source:
Created By:
Viewed By:
Stored Where / Storage Assumption:
Logged or Exported:
External Transfer:
Retention / Deletion Concern:
Privacy Risk:
Security Risk:
Decision Status:
Stage 3 Implication:
```

Use IDs: `DATA-001`, `DATA-002`, ...

Create `02_data_exposure_map.md` if personal, sensitive, confidential, uploaded, logged, model, dataset, or externally transferred data exists.

### Step 7. Screen External Transfer and LLM/API Exposure

Check possible transfer through:

```text
external APIs, LLM providers, embedding/vector databases, cloud storage,
managed databases, auth providers, email/SMS/push providers,
analytics/monitoring/logging, payment providers, file-processing services,
third-party datasets, human review/labeling vendors, exports, BI, dashboards
```

For each transfer, record:

```text
Transfer ID:
External Service / Recipient:
Purpose:
Data Sent:
Data Received:
Sensitive Data Status:
Data Subject:
Retention Concern:
Consent / Notice / Redaction Need:
Risk Level:
Decision Needed:
Stage 3 Implication:
```

Use IDs: `EXT-001`, `EXT-002`, ...

Create `02_external_transfer_register.md` if any external transfer is possible or unresolved.

### Step 8. Identify Early Risks

Screen at least:

```text
unauthorized access, excessive privilege, privilege escalation, data leakage,
sensitive data in logs, external transfer exposure, weak authentication assumptions,
missing authorization boundaries, admin misuse, irreversible destructive actions,
inadequate auditability, retention/deletion ambiguity, abuse/misuse, fraud,
prompt injection or LLM data exfiltration, model output misuse or overreliance,
dataset provenance or consent issues, compliance ambiguity, operational failure,
support workflow leakage
```

For each risk, record:

```text
Risk ID:
Risk Category:
Description:
Affected Stakeholders:
Affected Roles:
Affected Data:
Affected External Transfer:
Impact:
Likelihood: Low / Medium / High / Unknown
Severity: Low / Medium / High / Critical
Early Mitigation Direction:
Later Stage Owner:
Decision Needed:
Status:
Stage 3 Implication:
```

Use IDs: `RISK-001`, `RISK-002`, ...

### Step 9. Identify Audit and Accountability Needs

For each action requiring accountability, record:

```text
Audit ID:
Action:
Actor:
Affected Data / Object:
Reason to Audit:
Candidate Log Fields:
Retention Concern:
Who Can View Audit Log:
Privacy Risk of Logging:
Later Stage Owner:
Decision Status:
Stage 3 Implication:
```

Use IDs: `AUD-001`, `AUD-002`, ...

Create `02_audit_accountability_needs.md` if auditability is non-trivial.

### Step 10. Identify Abuse and Misuse Cases

Create abuse/misuse notes when there is user-generated content, privileged users, public access, AI/LLM output, uploaded files, payments, exports, confidential data, or moderation/review workflows.

For each case, record:

```text
Abuse Case ID:
Actor:
Scenario:
Target:
Potential Harm:
Existing Constraint:
Suggested Early Mitigation:
Requirements Implication:
Risk Link:
Decision Status:
```

Use IDs: `ABUSE-001`, `ABUSE-002`, ...

Create `02_abuse_misuse_cases.md` if abuse/misuse scenarios are meaningful.

### Step 11. Identify Compliance or Policy Concerns

If regulated, privacy-sensitive, institutional, legal, healthcare, financial, child-related, research-data-related, or AI/data-product-related, record:

```text
Compliance Concern ID:
Area:
Reason It May Apply:
Affected Data / Stakeholders:
Known Requirement or Unknown:
Decision Needed:
Later Stage Owner:
Risk Link:
Stage 3 Implication:
```

Use IDs: `COMP-001`, `COMP-002`, ...

Create `02_compliance_risk_notes.md` if applicable.

### Step 12. Produce Artifacts

Create mandatory artifacts. Create conditional artifacts when applicable. Mark artifacts as `draft` unless explicit human approval exists.

If a conditional artifact is not created, add an N/A record to `result.md`:

```markdown
### N/A: [[artifact name]]
- Reason not applicable:
- Evidence or input used:
- Revisit if:
- Impact on later stages:
```

### Step 13. Update Context Files

Update when relevant:

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Do not update `DECISIONS.md` without explicit human approval.

If direct updates are not possible, include exact proposed additions in `result.md` under `Context File Updates Needed`.

### Step 14. Prepare Human Approval Gate

End with human approval items. Do not claim approval unless explicit approval exists.

---

## 10. Output Artifacts

### Mandatory Artifacts

```text
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/02_stakeholders_risk/result.md
/workflow/context/context_packet.md
```

### Update When Relevant

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

### Conditional Artifacts

```text
/workflow/02_stakeholders_risk/02_role_permission_matrix.md
  if multiple roles, permissions, reviewers, admins, or access levels exist

/workflow/02_stakeholders_risk/02_data_exposure_map.md
  if personal, sensitive, confidential, uploaded, logged, model, dataset, or externally transferred data exists

/workflow/02_stakeholders_risk/02_external_transfer_register.md
  if external APIs, LLMs, analytics, email/SMS, payment, cloud, vendors, reviewers, or third-party services exist

/workflow/02_stakeholders_risk/02_admin_power_review.md
  if admin, support, moderator, reviewer, operator, or privileged powers exist

/workflow/02_stakeholders_risk/02_audit_accountability_needs.md
  if auditability, traceability, reversibility, accountability, moderation, or approval evidence is needed

/workflow/02_stakeholders_risk/02_compliance_risk_notes.md
  if regulated, legal, policy, privacy, AI/data governance, or high-risk concerns exist

/workflow/02_stakeholders_risk/02_abuse_misuse_cases.md
  if abuse, fraud, prompt injection, scraping, privilege abuse, model misuse, or external attack scenarios are relevant
```

---

## 11. Required Output Structure

### `02_stakeholders.md`

```markdown
# 02 Stakeholders

Status: draft
Stage: 02 Stakeholder & Risk Framing

## 1. Source Inputs
## 2. Stakeholder Overview
## 3. Stakeholder Register
## 4. User Role Candidates
## 5. Administrator / Privileged Actor Candidates
## 6. External System Stakeholders
## 7. Affected Non-User Stakeholders
## 8. Decision Candidates
## 9. Working Assumptions
## 10. Open Questions
## 11. Requirements Implications for Stage 3
```

### `02_risk_privacy_screening.md`

```markdown
# 02 Risk & Privacy Screening

Status: draft
Stage: 02 Stakeholder & Risk Framing

## 1. Source Inputs
## 2. Screening Summary
## 3. Data Category Register
## 4. External Transfer / LLM/API Exposure Register
## 5. Initial Security Risk Register
## 6. Initial Privacy Risk Register
## 7. Admin Power and Abuse Risk Notes
## 8. Audit / Accountability Needs
## 9. Compliance or Policy Concerns
## 10. N/A Records for Conditional Artifacts
## 11. Decision Candidates
## 12. Working Assumptions
## 13. Open Questions
## 14. Requirements Implications for Stage 3
```

### `result.md`

```markdown
# Result: 02 Stakeholder & Risk Framing

## 1. Task Summary
## 2. Inputs Used
## 3. Outputs Created or Updated
## 4. Stakeholder Findings
## 5. Role / Permission Findings
## 6. Data / Privacy Findings
## 7. External Transfer Findings
## 8. Security / Abuse / Operational Risk Findings
## 9. Audit / Accountability Findings
## 10. Decision Candidates
## 11. Working Assumptions
## 12. Open Questions
## 13. Risks and Constraints
## 14. Rejected or Superseded Options
## 15. Traceability Updates
## 16. N/A Records
## 17. Context File Updates Needed
## 18. Human Approval Required
## 19. Recommended Next Step
```

### Conditional Artifact Structure

```markdown
# [[Artifact Title]]

Status: draft
Stage: 02 Stakeholder & Risk Framing

## 1. Purpose
## 2. Source Inputs
## 3. Register / Findings
## 4. Decision Candidates
## 5. Working Assumptions
## 6. Open Questions
## 7. Requirements Implications for Stage 3
```

---

## 12. Traceability Requirements

Use these ID prefixes:

```text
STK-###     stakeholder
ROLE-###    role candidate
POWER-###   privileged/admin power
DATA-###    data category
EXT-###     external transfer candidate
RISK-###    security/privacy/operational risk
AUD-###     audit/accountability need
ABUSE-###   abuse/misuse case
COMP-###    compliance/policy concern
```

Required links:

```text
Service Goal → Stakeholder
Service Goal → Role Candidate
Stakeholder → Data Category
Role Candidate → Permission Concern
Data Category → Privacy/Security Risk
External Transfer → Privacy/Security Risk
Admin Power → Audit Need
Risk → Requirements Implication for Stage 3
Open Question → Affected Later Stage
```

Do not create detailed requirement IDs unless Stage 3 already defines them.

Suggested traceability table:

```markdown
| Source Goal / Input | Stage 2 ID | Stage 2 Item | Related Risk / Data / Role | Stage 3 Implication | Status |
|---|---|---|---|---|---|
```

---

## 13. Context Packet Update Rules

Update `/workflow/context/context_packet.md` for Stage 3. Keep it concise. Do not copy full registers.

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 02 Stakeholder & Risk Framing completed as draft / approved / partially blocked.
- Completed stages:
- Next recommended stage: 03 Requirements & Acceptance Criteria.

## 2. Approved Decisions
- Only human-approved Stage 2 decisions.

## 3. Working Assumptions
- Stakeholder assumptions.
- Role/permission assumptions.
- Data handling assumptions.
- Risk assumptions.

## 4. Open Questions
- Questions affecting requirements, acceptance criteria, security/privacy requirements, domain rules, architecture, data design, tests, or release.

## 5. Rejected / Superseded Options
- Stakeholders, roles, data flows, risk approaches, or transfer approaches rejected by the human developer.

## 6. Constraints That Must Not Be Violated
- Role/permission constraints.
- Privacy constraints.
- Security constraints.
- External transfer constraints.
- Audit/accountability constraints.
- Scope constraints.

## 7. Key Context for Next Stage
- Stakeholder summary.
- Role candidate summary.
- Personal/sensitive data summary.
- External transfer summary.
- Initial risk summary.
- Audit/accountability summary.

## 8. Required Inputs for Next Stage
- /workflow/01_goal/01_service_goal.md
- /workflow/02_stakeholders_risk/02_stakeholders.md
- /workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- /workflow/02_stakeholders_risk/02_role_permission_matrix.md, if created
- /workflow/02_stakeholders_risk/02_data_exposure_map.md, if created
- /workflow/02_stakeholders_risk/02_external_transfer_register.md, if created
- /workflow/02_stakeholders_risk/02_admin_power_review.md, if created
- /workflow/02_stakeholders_risk/02_audit_accountability_needs.md, if created
- /workflow/02_stakeholders_risk/02_compliance_risk_notes.md, if created
- /workflow/02_stakeholders_risk/02_abuse_misuse_cases.md, if created
- /workflow/context/DECISIONS.md
- /workflow/context/ASSUMPTIONS.md
- /workflow/context/OPEN_QUESTIONS.md
- /workflow/context/REJECTED_OPTIONS.md

## 9. Do Not Do
- Do not treat role candidates as final requirements unless approved.
- Do not ignore personal/sensitive data handling questions.
- Do not assume external API or LLM transfer is allowed unless approved.
- Do not design detailed architecture or database schema in Stage 3.
- Do not convert risk mitigations into requirements without Stage 3 decomposition and human review.
```

---

## 14. Specialization Hooks

Apply specialization addenda after core and Stage 2 rules. Specialization may add inputs, questions, artifacts, risks, validation needs, and approval requirements, but must not replace this SKILL.

- **Web SaaS:** tenant/org roles, account lifecycle, billing/admin roles, resource visibility, sessions, analytics exposure, cross-tenant leakage.
- **Internal Tool:** staff roles, operational overrides, internal access boundaries, support/admin least privilege, manual accountability.
- **Mobile App:** device permissions, local storage, push notifications, offline/sync exposure, platform identity, lost-device risk.
- **AI/Data Product:** dataset subjects, provenance, labeling roles, model input/output, LLM/API transfer, synthetic data, model misuse, human review.
- **Regulated/Security-Sensitive:** compliance assumptions, audit logs, retention/deletion, legal/institutional review, high-severity blockers, separation of duties.
- **Brownfield/Legacy:** existing roles, permissions, data exposure, inherited constraints, forbidden change areas, migration/compatibility risks.

---

## 15. Validation Checklist

Before finishing, verify:

```text
[ ] Stage 0 and Stage 1 inputs were reviewed or missing inputs were handled.
[ ] USER_DIRECTIVES.md was checked if present.
[ ] Stakeholders include users, operators/admins, external systems, and affected non-users where applicable.
[ ] Preliminary roles and permission directions are identified but not treated as final requirements.
[ ] Administrator and privileged powers are explicitly reviewed.
[ ] Personal, sensitive, confidential, regulated, logged, uploaded, model, dataset, or externally transferred data is identified or marked N/A.
[ ] External API, LLM, analytics, cloud, email/SMS, payment, third-party, human-review, or export risks are identified or marked N/A.
[ ] Security risks include unauthorized access, excessive privilege, data leakage, logging exposure, and abuse/misuse where applicable.
[ ] Privacy risks include minimization, retention, deletion, consent, external transfer, logging, and sensitive data handling where applicable.
[ ] Audit and accountability needs are identified or marked N/A.
[ ] Risks are connected to later-stage owners.
[ ] Requirements implications for Stage 3 are listed without writing full Stage 3 requirements.
[ ] Decision candidates, assumptions, open questions, risks, and rejected options are separated.
[ ] Conditional artifacts are created or N/A rationale is recorded.
[ ] Traceability IDs are stable and do not pretend later-stage artifacts already exist.
[ ] context_packet.md is updated for Stage 3.
[ ] Human approval items are listed.
[ ] No unapproved candidate was written as an approved decision.
```

---

## 16. Human Approval Gate

End `result.md` with:

```markdown
## Human Approval Required

### Decisions to Approve
- Stakeholder categories to carry into requirements.
- User role and permission direction.
- Administrator / operator / reviewer / support power direction.
- Personal or sensitive data handling direction.
- External API / LLM / third-party / analytics / logging transfer direction.
- Audit and accountability direction.
- Initial risk assumptions that should constrain Stage 3.
- Conditional artifacts to treat as active Stage 2 handoff inputs.

### Assumptions to Confirm
- ...

### Open Questions to Resolve Before Stage 3
- ...

### Risks to Review
- ...

### Artifacts Ready for Review
- /workflow/02_stakeholders_risk/02_stakeholders.md
- /workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- /workflow/02_stakeholders_risk/result.md
- [[conditional artifacts if created]]

### Recommended Next Step
- Review and approve, revise, or reject the stakeholder/risk framing before running Stage 3 Requirements & Acceptance Criteria.
```

Do not proceed to Stage 3 as if approval has been granted unless the human explicitly approves.

---

## 17. Failure Handling

If completion is unsafe:

1. Produce partial `result.md` rather than pretending completion.
2. Mark the stage as blocked or partially blocked.
3. Identify safe partial work completed.
4. Identify exact human decision needed.
5. Do not create misleading final artifacts.
6. Do not update `context_packet.md` as if Stage 2 completed successfully.

Common failures:

- Service goal missing or contradictory.
- Project type unknown where regulation, privacy, stakeholder scope, or security depends on it.
- Source artifact is rejected, superseded, or unapproved but treated as current truth.
- User directive conflicts with approved decision.
- External transfer, personal data, or sensitive data direction is too ambiguous to proceed safely.
- Brownfield project requires existing-context input that is missing.

---

## 18. Do Not Do

Do not:

- Treat all stakeholders as end users.
- Ignore admins, operators, reviewers, support, maintainers, external systems, or affected non-users.
- Treat proposed roles as approved requirements.
- Design detailed RBAC/ABAC or authorization implementation.
- Ignore personal data, sensitive data, logs, analytics, uploaded files, model inputs/outputs, datasets, exports, or external transfers.
- Claim “no security risk” or “no privacy risk” without evidence.
- Defer all security/privacy thinking to Stage 12.
- Mix requirements decomposition, architecture, database, API, test strategy, task, or implementation design into this stage.
- Use `context_packet.md` as the only source of truth.
- Use rejected or superseded artifacts as current truth.
- Overwrite approved decisions without approval.
- Update `DECISIONS.md` without explicit human approval.
- Skip the human approval gate.

---

## 19. Final Response Requirement

At the end of execution, provide a short summary to the human developer:

```markdown
## Stage 2 Execution Summary

### Created / Updated
- ...

### Main Findings
- ...

### Approval Needed
- ...

### Blockers or Open Questions
- ...

### Recommended Next Step
- ...
```

This summary must not replace the actual artifacts.
