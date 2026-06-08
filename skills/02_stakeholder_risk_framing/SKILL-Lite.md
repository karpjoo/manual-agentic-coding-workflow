---
name: 02_stakeholder_risk_framing
description: Use after Service Goal Definition and before Requirements & Acceptance Criteria to frame stakeholders, roles, permissions, data exposure, external transfers, admin powers, audit needs, and early security/privacy risks.
stage: "02 - Stakeholder & Risk Framing"
version: 1.2.0
status: draft
primary_output: "/workflow/02_stakeholders_risk/02_stakeholders.md"
requires_human_approval: true
---

# 02 Stakeholder & Risk Framing SKILL

## 1. Purpose
Execute Stage 2 of the Manual Agentic Coding Workflow.
This stage identifies:
- who can affect or be affected by the system;
- candidate roles and permission directions;
- personal, sensitive, confidential, regulated, logged, or externally transferred data;
- privileged/admin powers;
- audit/accountability needs;
- early security, privacy, abuse, compliance, and operational risks.
The output constrains Stage 3 Requirements & Acceptance Criteria.
This stage does **not** finalize requirements, authorization design, architecture, database schema, tests, or implementation.

## 2. Operating Contract
You are a structured development assistant, not the final decision-maker.
Preserve these distinctions:
```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```
Classify every important item as one of:
```text
Approved Decision | Decision Candidate | Working Assumption | Open Question | Risk | Rejected/Superseded Option
```
Do not update `/workflow/context/DECISIONS.md` unless explicit human approval already exists.

## 3. When to Use
Use when:
- Stage 0 has provided project context;
- Stage 1 has produced a service goal direction;
- stakeholder, role, permission, data, privacy, security, external-transfer, admin, or audit framing is needed before requirements.
Do not use to:
- write final requirements or acceptance criteria;
- design RBAC/ABAC implementation;
- design architecture, APIs, domain model, database, tests, or release controls;
- perform final security/privacy review;
- perform a formal threat model unless a specialization addendum requires it.

## 4. Input Precedence
When sources conflict, use this order:
```text
1. Current explicit user instruction
2. /workflow/02_stakeholders_risk/USER_DIRECTIVES.md
3. /workflow/context/APPROVAL_LOG.md and DECISIONS.md
4. /workflow/context/artifact_manifest.yml
5. /workflow/context/context_packet.md
6. Approved stage artifacts
7. /workflow/context/ASSUMPTIONS.md
8. Agent inference
```
If conflict affects scope, roles, permissions, personal/sensitive data, external transfer, compliance, privacy, security, or Stage 3 requirements, treat it as blocking unless resolved by the human developer.

## 5. Inputs
### Always Read
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
### Read If Applicable
```text
/workflow/00_intake/00_existing_context_review.md
/workflow/00_intake/review_notes.md
/workflow/01_goal/review_notes.md
/workflow/02_stakeholders_risk/USER_DIRECTIVES.md
/workflow_templates/specializations/web_saas.md
/workflow_templates/specializations/internal_tool.md
/workflow_templates/specializations/mobile_app.md
/workflow_templates/specializations/ai_data_product.md
/workflow_templates/specializations/regulated_security_sensitive.md
/workflow_templates/specializations/brownfield_legacy.md
```
Activate applicable inputs from project profile, `artifact_manifest.yml`, `context_packet.md`, `USER_DIRECTIVES.md`, or explicit user instruction.
### Do Not Read By Default
Do not read raw chat logs, full agent logs, superseded/rejected artifacts, unrelated drafts, source code, or later-stage artifacts unless needed and justified.

## 6. Missing Input Handling
Blocking by default:
- missing `/workflow/01_goal/01_service_goal.md`;
- missing service goal direction;
- missing project type when it affects stakeholder, data, privacy, security, regulatory, or external-transfer framing;
- directive conflicts with approved decision;
- rejected/superseded artifact is referenced as current truth.
Non-blocking by default:
- missing `APPROVAL_LOG.md`, `REJECTED_OPTIONS.md`, review notes, optional specialization, or inactive conditional artifact.
If blocked, stop before final artifacts and write `/workflow/02_stakeholders_risk/result.md` with:
```markdown
# Result: 02 Stakeholder & Risk Framing

## Blocker Report
### Blocking Issue
### Why It Matters
### Affected Artifacts or Stages
### Safe Partial Work Completed
### Human Decision Needed
```
If non-blocking, continue with labeled working assumptions and record gaps in `result.md`; update `OPEN_QUESTIONS.md` when later stages may be affected.

## 7. USER_DIRECTIVES.md Handling
If `/workflow/02_stakeholders_risk/USER_DIRECTIVES.md` exists:
- read it before analysis;
- classify each directive as approval, correction, preference, new requirement, rejection, scope change, or question;
- apply it before assumptions;
- report conflicts with approved decisions;
- do not edit it unless explicitly instructed.

## 8. Output Artifacts
Follow `/skills/02_stakeholder_risk_framing/artifact_contract.md` or `/workflow/02_stakeholders_risk/artifact_contract.md` if present. If no artifact contract exists, use the minimum structures in this SKILL.
### Mandatory
```text
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/02_stakeholders_risk/result.md
/workflow/context/context_packet.md
```
Update when relevant:
```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```
### Conditional
Create only when applicable:
```text
/workflow/02_stakeholders_risk/02_role_permission_matrix.md
/workflow/02_stakeholders_risk/02_data_exposure_map.md
/workflow/02_stakeholders_risk/02_external_transfer_register.md
/workflow/02_stakeholders_risk/02_admin_power_review.md
/workflow/02_stakeholders_risk/02_audit_accountability_needs.md
/workflow/02_stakeholders_risk/02_compliance_risk_notes.md
/workflow/02_stakeholders_risk/02_abuse_misuse_cases.md
```
For skipped conditional artifacts, add to `result.md`:
```markdown
### N/A: [[artifact name]]
- Reason not applicable:
- Evidence or input used:
- Revisit if:
- Impact on later stages:
```

## 9. Execution Procedure
### Step 1. Preflight
Read required inputs, check approval/supersession status, apply directives, activate specialization hooks, identify missing/conflicting inputs, restate the task, and stop with a Blocker Report if safe progress is impossible.
### Step 2. Identify Stakeholders
Identify relevant stakeholder categories:
```text
primary users, secondary users, admins, operators, maintainers, reviewers,
moderators, approvers, business stakeholders, external organizations,
external systems, data subjects, affected non-users, legal/compliance/audit,
support, abuse/misuse actors
```
For each stakeholder, capture: ID, category, goal/interest, main actions, data access/exposure, risk relevance, source, and status.
### Step 3. Identify Roles and Permission Directions
Identify role candidates without finalizing implementation.
For each role, capture: ID, name, actor type, purpose, likely permissions, forbidden actions, sensitive operations, data access level, authn/authz need, audit need, and status.
Keep separate:
```text
business role ≠ technical permission ≠ operational responsibility
```
### Step 4. Review Privileged Powers
Identify admin/operator/support/moderator powers such as global viewing, sensitive-data access, deletion, role changes, export, approval/rejection, moderation, irreversible action, log access, integration configuration, and impersonation.
For each privileged power, capture: actor, action, risk, audit need, approval need, reversibility, recommended constraint, and status.
### Step 5. Identify Data Categories
Identify data created, viewed, stored, transmitted, logged, exported, or processed.
Consider: account/profile, contact, authentication, user-generated content, uploads, logs/analytics, operational metadata, payment/billing, personal data, sensitive data, confidential business data, regulated data, research/dataset records, model input/output, synthetic data, and third-party data.
For each data category, capture: source, subject, access, storage, transfer, retention/deletion concern, privacy risk, security risk, and status.
### Step 6. Screen External Transfers
Identify data leaving the system boundary through APIs, LLMs, vector DBs, cloud storage, managed DBs, auth providers, email/SMS/push, analytics/monitoring/logging, payment, third-party datasets, file processing, or human review vendors.
For each transfer, capture: service, purpose, data sent/received, sensitivity, retention concern, consent/redaction need, risk level, and decision needed.
### Step 7. Identify Early Risks
Screen for unauthorized access, excessive privilege, privilege escalation, data leakage, sensitive data in logs, external transfer exposure, weak authentication, missing authorization boundary, admin misuse, irreversible action, insufficient auditability, retention/deletion ambiguity, abuse/misuse, prompt injection, LLM data exfiltration, model-output misuse, dataset consent/provenance issues, compliance ambiguity, and operational failure.
For each risk, capture: category, affected stakeholders/data/roles, impact, likelihood, severity, mitigation direction, later-stage owner, decision needed, and status.
### Step 8. Identify Audit and Accountability Needs
For each auditable action, capture: actor, affected object/data, reason, candidate log fields, retention concern, log access rules, later-stage owner, and status.
### Step 9. Produce and Update Artifacts
Create mandatory artifacts, create applicable conditional artifacts, add N/A records, use stable IDs, mark outputs as draft unless approval is documented, update context files, and separate approved decisions from candidates and assumptions.
### Step 10. Prepare Human Approval Gate
End with decisions, assumptions, open questions, and risks requiring human review before Stage 3.

## 10. Minimum Artifact Structures
Use detailed `artifact_contract.md` when available. Otherwise, use these minimum sections.
### `02_stakeholders.md`
```markdown
# 02 Stakeholders

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

## 1. Source Inputs
## 2. Screening Summary
## 3. Data Category Register
## 4. External Transfer / LLM/API Exposure Register
## 5. Initial Security Risk Register
## 6. Initial Privacy Risk Register
## 7. Admin Power and Abuse Risk Notes
## 8. Audit / Accountability Needs
## 9. Compliance or Policy Concerns
## 10. Decision Candidates
## 11. Working Assumptions
## 12. Open Questions
## 13. Requirements Implications for Stage 3
```
### `result.md`
```markdown
# Result: 02 Stakeholder & Risk Framing

## 1. Task Summary
## 2. Inputs Used
## 3. Outputs Created or Updated
## 4. Key Findings
## 5. Decision Candidates
## 6. Working Assumptions
## 7. Open Questions
## 8. Risks and Constraints
## 9. Rejected or Superseded Options
## 10. Traceability Updates
## 11. N/A Records
## 12. Human Approval Required
## 13. Recommended Next Step
```

## 11. Traceability
Use stable IDs:
```text
STK-###   stakeholder
ROLE-###  role candidate
DATA-###  data category
EXT-###   external transfer candidate
RISK-###  security/privacy/operational risk
AUD-###   audit/accountability need
```
Maintain links where applicable:
```text
Service Goal → Stakeholder
Service Goal → Role Candidate
Stakeholder → Data Category
Role Candidate → Permission Concern
Data Category → Privacy/Security Risk
External Transfer → Privacy/Security Risk
Admin Power → Audit Need
Risk → Requirements Implication for Stage 3
```
Do not create detailed requirement IDs unless Stage 3 already defines them.

## 12. Context Packet Update
Update `/workflow/context/context_packet.md` for Stage 3 with only minimum operational context:
```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 02 Stakeholder & Risk Framing completed as draft / approved / partially blocked.
- Completed stages:
- Next recommended stage: 03 Requirements & Acceptance Criteria.

## 2. Approved Decisions
- Only human-approved Stage 2 decisions.

## 3. Working Assumptions
- Stakeholder, role, permission, data, external-transfer, audit, and risk assumptions.

## 4. Open Questions
- Questions affecting requirements, security/privacy, domain rules, architecture, or data design.

## 5. Rejected / Superseded Options
- Rejected stakeholders, roles, data flows, external transfers, or risk approaches.

## 6. Constraints That Must Not Be Violated
- Role/permission, privacy, security, external transfer, audit, scope, and operational constraints.

## 7. Key Context for Next Stage
- Stakeholder summary.
- Role/permission summary.
- Personal/sensitive data summary.
- External transfer summary.
- Initial risk summary.
- Audit/accountability summary.

## 8. Required Inputs for Next Stage
- /workflow/01_goal/01_service_goal.md
- /workflow/02_stakeholders_risk/02_stakeholders.md
- /workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- Conditional Stage 2 artifacts actually created.
- /workflow/context/DECISIONS.md
- /workflow/context/ASSUMPTIONS.md
- /workflow/context/OPEN_QUESTIONS.md
- /workflow/context/REJECTED_OPTIONS.md

## 9. Do Not Do
- Do not treat role candidates as final requirements unless approved.
- Do not ignore personal/sensitive data questions.
- Do not assume external API or LLM transfer is allowed unless approved.
- Do not design detailed architecture or database schema in Stage 3.
```

## 13. Human Approval Gate
End with:
```markdown
## Human Approval Required
### Decisions to Approve
- Stakeholder categories to carry into requirements.
- User role and permission direction.
- Administrator/operator power direction.
- Personal or sensitive data handling direction.
- External API/LLM/third-party transfer direction.
- Audit and accountability direction.
- Initial risk assumptions that should constrain Stage 3.
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
- Conditional artifacts created in this run.
### Recommended Next Step
- Review and approve, revise, or reject Stage 2 before running Stage 3.
```
Do not claim Stage 2 is approved unless explicit approval exists.

## 14. Validation Checklist
Verify before finishing:
```text
[ ] Stage 0 and Stage 1 inputs reviewed.
[ ] USER_DIRECTIVES.md checked if present.
[ ] Missing/conflicting inputs reported.
[ ] Stakeholders include users, admins/operators, external systems, and affected non-users where applicable.
[ ] Role/permission candidates identified but not treated as final requirements.
[ ] Privileged/admin powers reviewed.
[ ] Personal/sensitive/confidential/regulated/externally transferred data identified or marked N/A.
[ ] External APIs, LLMs, analytics, cloud, email/SMS, payment, and third-party transfers identified or marked N/A.
[ ] Security, privacy, abuse, operational, audit, and compliance risks screened.
[ ] Risks connected to later-stage implications.
[ ] Decisions, candidates, assumptions, questions, and risks separated.
[ ] Conditional artifacts created or given N/A records.
[ ] Traceability updated or gaps recorded.
[ ] context_packet.md updated for Stage 3.
[ ] Human approval items listed.
[ ] No unapproved candidate recorded as approved decision.
```

## 15. Specialization Hooks
Apply relevant addenda after core Stage 2 rules:
```text
web_saas                     → tenant/org roles, account lifecycle, billing/admin, sessions, analytics
internal_tool                → staff roles, overrides, least privilege, auditability
mobile_app                   → device permissions, local storage, push, offline/sync, platform identity
ai_data_product              → dataset subjects, provenance, model input/output, LLM transfer, labeling, synthetic data, model misuse
regulated_security_sensitive → compliance, audit logs, retention/deletion, institutional/legal review, high-severity blockers
brownfield_legacy            → existing roles, permissions, data exposure, inherited constraints, forbidden change areas
```
Specialization may add inputs, questions, artifacts, risks, and approval requirements. It must not replace this SKILL.

## 16. Do Not Do
Do not:
- treat all stakeholders as end users;
- ignore admins, operators, reviewers, external systems, or affected non-users;
- treat proposed roles as approved requirements;
- design detailed RBAC/ABAC implementation;
- ignore logs, analytics, uploads, model inputs/outputs, or external transfers;
- claim “no security risk” without evidence;
- defer all security/privacy thinking to Stage 12;
- mix detailed requirements, architecture, database, or implementation work into this stage;
- update `DECISIONS.md` without explicit human approval;
- use `context_packet.md` as the only source of truth;
- revive rejected options without explicit instruction;
- skip the human approval gate.
