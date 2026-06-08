# 02 Stakeholder & Risk Framing Skill Template

> Recommended path: `/workflow_templates/stage_templates/02_stakeholder_risk_skill_template.md`  
> This is a **stage-specific SKILL template**, not an executable `SKILL.md`.  
> It extends `/workflow_templates/core/core_skill_template.md` and defines only Stage 2-specific rules.

---

## 0. Template Metadata

```yaml
template_name: 02_stakeholder_risk_skill_template
stage: "02 - Stakeholder & Risk Framing"
template_type: stage_specific_skill_template
intended_reusable_skill: /skills/02_stakeholder_risk_framing/SKILL.md
workflow_stage_folder: /workflow/02_stakeholders_risk
version: 1.0.0
status: draft
extends: /workflow_templates/core/core_skill_template.md
```

---

## 1. Stage Purpose

Stage 2 identifies stakeholders, roles, permission directions, sensitive data, personal data, external data transfers, administrator powers, audit needs, and early security/privacy risks before requirements are decomposed.

This stage does **not** write final requirements, design architecture, design database schema, or implement authorization. It frames the human-approved context that Stage 3 must respect.

---

## 2. Core Question

```text
Who or what can affect or be affected by the system, and what role, permission, data, privacy, security, operational, compliance, or external-transfer risks must be considered before writing requirements?
```

---

## 3. Stage Boundaries

### This Stage Does

- Identify primary, secondary, operational, administrative, external, and affected stakeholders.
- Propose preliminary roles and permission directions.
- Identify privileged/admin powers.
- Identify personal, sensitive, confidential, regulated, or externally transferred data.
- Identify early security, privacy, compliance, abuse, misuse, and operational risks.
- Identify audit/accountability needs.
- Produce decision candidates, assumptions, open questions, and Stage 3 implications.

### This Stage Does Not

- Finalize functional requirements or acceptance criteria.
- Finalize authorization implementation.
- Design architecture, APIs, domain model, database schema, or tests.
- Treat role, permission, privacy, or security proposals as approved decisions.
- Perform a full formal threat model unless a specialization addendum requires it.

---

## 4. Input Contract

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
/workflow/00_intake/00_existing_context_review.md          # brownfield / legacy / integration context
/workflow/00_intake/review_notes.md                       # Stage 0 corrections or constraints
/workflow/01_goal/review_notes.md                         # Stage 1 corrections or user-goal changes
/workflow/02_stakeholders_risk/USER_DIRECTIVES.md          # stage-local human instructions
/workflow_templates/specializations/web_saas.md            # web SaaS or browser multi-user service
/workflow_templates/specializations/internal_tool.md        # internal staff / ops / admin tool
/workflow_templates/specializations/mobile_app.md           # mobile, device permissions, local/offline data
/workflow_templates/specializations/ai_data_product.md      # AI/ML/LLM, datasets, model outputs, labeling
/workflow_templates/specializations/regulated_security_sensitive.md
                                                             # regulated or high-risk privacy/security context
/workflow_templates/specializations/brownfield_legacy.md    # existing roles, permissions, data, integrations
```

### Do Not Read By Default

- Raw chat history or full agent logs.
- Superseded or rejected artifacts unless checking why they were rejected.
- Draft artifacts from Stage 3 or later unless explicitly requested.
- Source code unless brownfield risk review requires it.
- Architecture, data design, test strategy, task breakdown, or implementation artifacts from later stages.

### Missing Input Handling

Blocking by default:

- Missing `/workflow/01_goal/01_service_goal.md`.
- Missing service goal direction.
- Missing project type when it materially affects privacy, security, regulation, or stakeholder scope.

If blocking, produce a Blocker Report in `result.md` and stop before creating final Stage 2 artifacts.

Non-blocking by default:

- Missing `APPROVAL_LOG.md`, `REJECTED_OPTIONS.md`, `review_notes.md`, or non-required specialization addendum.

If non-blocking, continue with clearly marked working assumptions and record the gap in `result.md` and, if relevant, `OPEN_QUESTIONS.md`.

---

## 5. Output Artifact Contract

### Mandatory Artifacts

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

Do **not** update `/workflow/context/DECISIONS.md` unless explicit human approval already exists.

### Conditional Artifacts

```text
/workflow/02_stakeholders_risk/02_role_permission_matrix.md       # multiple roles, permissions, reviewers, admins
/workflow/02_stakeholders_risk/02_data_exposure_map.md            # personal/sensitive/confidential/log/model/dataset data
/workflow/02_stakeholders_risk/02_external_transfer_register.md   # external APIs, LLMs, analytics, email/SMS, payment, cloud
/workflow/02_stakeholders_risk/02_admin_power_review.md           # admin/support/moderator/operator powers
/workflow/02_stakeholders_risk/02_audit_accountability_needs.md   # traceability, reversibility, accountability, moderation
/workflow/02_stakeholders_risk/02_compliance_risk_notes.md        # regulated or high-risk context
/workflow/02_stakeholders_risk/02_abuse_misuse_cases.md           # abuse, fraud, prompt injection, scraping, privilege abuse
```

### N/A Record Rule

For each skipped conditional artifact, record in `result.md`:

```markdown
### N/A: [[artifact name]]
- Reason not applicable:
- Evidence or input used:
- Revisit if:
- Impact on later stages:
```

---

## 6. Stage-Specific Procedure

### Step 1. Preflight

Read inputs, check artifact approval status, apply `USER_DIRECTIVES.md` if present, activate specialization hooks, report missing/draft/superseded/rejected/conflicting inputs, and restate the Stage 2 task.

### Step 2. Identify Stakeholders

Classify stakeholders as applicable:

```text
primary users, secondary users, administrators, operators, maintainers, reviewers,
moderators, approvers, internal business stakeholders, external organizations,
external systems/providers, data subjects, affected non-users, compliance/legal/audit,
support, misuse/abuse actors
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
```

### Step 3. Identify Role and Permission Candidates

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
```

Separate business role, technical permission, and operational responsibility.

### Step 4. Review Administrator / Privileged Powers

Check elevated operations such as viewing all records, viewing sensitive data, deleting data, changing roles, exporting data, approving/rejecting/moderating, triggering irreversible actions, accessing logs, configuring integrations, and impersonating users.

For each power, record: `Power ID`, `Description`, `Role Candidate`, `Risk`, `Audit Required`, `Approval Required`, `Reversibility`, `Recommended Constraint`, `Decision Status`.

### Step 5. Identify Data Categories

Classify data that may be created, viewed, stored, transmitted, logged, exported, or processed.

Baseline categories:

```text
account/profile, contact, authentication, user-generated content, uploaded files,
logs/analytics, operational metadata, payment/billing, personal data,
sensitive personal data, confidential business data, regulated data,
research data/dataset records, model input/output, synthetic data, third-party data
```

For each category, record source, data subject, access, storage, external transfer, retention/deletion concern, privacy risk, security risk, and decision status.

### Step 6. Screen External Transfer and LLM/API Exposure

Check whether data may leave the system boundary through external APIs, LLM providers, embedding/vector DBs, cloud storage, managed databases, auth providers, email/SMS/push providers, analytics/monitoring/logging, payment providers, third-party datasets, file processing, or human review/labeling vendors.

For each transfer, record service, purpose, data sent/received, sensitive data status, retention concern, consent/redaction need, risk level, and decision needed.

### Step 7. Identify Early Risks

Screen at least these categories:

```text
unauthorized access, excessive privilege, privilege escalation, data leakage,
sensitive data in logs, external transfer exposure, weak authentication assumptions,
missing authorization boundaries, admin misuse, irreversible destructive actions,
inadequate auditability, retention/deletion ambiguity, abuse/misuse,
prompt injection or LLM data exfiltration, model output misuse or overreliance,
dataset provenance or consent issues, compliance ambiguity, operational failure
```

For each risk, record category, affected stakeholders/data/roles, impact, likelihood, severity, early mitigation direction, later stage owner, decision needed, and status.

### Step 8. Identify Audit and Accountability Needs

For each audit need, record action, actor, affected data/object, reason, candidate log fields, retention concern, log access, later stage owner, and decision status.

### Step 9. Produce Artifacts

Create mandatory artifacts, create applicable conditional artifacts, record N/A rationales, use stable IDs, mark artifacts as draft unless approval is documented, and separate facts, assumptions, candidates, open questions, and risks.

### Step 10. Prepare Human Approval Gate

List decisions, assumptions, open questions, and risks that require human review before Stage 3.

### Step 11. Update Context for Stage 3

Update `context_packet.md` with only the minimum operational context required for requirements decomposition.

---

## 7. Required Output Structure

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
## 17. Human Approval Required
## 18. Recommended Next Step
```

---

## 8. Traceability Requirements

Recommended ID prefixes:

```text
STK-###   stakeholder
ROLE-###  role candidate
DATA-###  data category
EXT-###   external transfer candidate
RISK-###  security/privacy/operational risk
AUD-###   audit/accountability need
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
```

Do not create detailed requirement IDs unless Stage 3 already defines them.

---

## 9. Validation Checklist

```text
[ ] Stage 0 and Stage 1 inputs were reviewed.
[ ] Stakeholders include users, operators/admins, external systems, and affected non-users where applicable.
[ ] Preliminary roles and permission levels are identified but not treated as final requirements.
[ ] Administrator and privileged powers are explicitly reviewed.
[ ] Personal, sensitive, confidential, regulated, or externally transferred data is identified or marked N/A.
[ ] External API, LLM, analytics, cloud, email/SMS, payment, or third-party transfer risks are identified or marked N/A.
[ ] Security risks include unauthorized access, excessive privilege, data leakage, logging exposure, and abuse/misuse where applicable.
[ ] Privacy risks include minimization, retention, deletion, consent, external transfer, and sensitive data handling where applicable.
[ ] Audit and accountability needs are identified or marked N/A.
[ ] Risks are connected to later-stage owners.
[ ] Decision candidates, assumptions, open questions, and risks are separated.
[ ] Human approval items are listed.
[ ] context_packet.md is updated for Stage 3.
[ ] No unapproved candidate was written as an approved decision.
```

---

## 10. Human Approval Gate

The reusable Stage 2 SKILL must end with:

```markdown
## Human Approval Required

### Decisions to Approve
- Stakeholder categories to carry into requirements.
- User role and permission direction.
- Administrator / operator power direction.
- Personal or sensitive data handling direction.
- External API / LLM / third-party transfer direction.
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
- [[conditional artifacts if created]]
- /workflow/02_stakeholders_risk/result.md

### Recommended Next Step
- Review and approve, revise, or reject the stakeholder/risk framing before running Stage 3 Requirements & Acceptance Criteria.
```

Do not claim Stage 2 is approved unless explicit human approval exists.

---

## 11. Next `context_packet.md` Rules

Update `/workflow/context/context_packet.md` for Stage 3.

Required handoff content:

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
- Questions that may affect requirements, acceptance criteria, security/privacy requirements, domain rules, or architecture.

## 5. Rejected / Superseded Options
- Stakeholders, roles, data flows, or risk approaches rejected by the human developer.

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
- /workflow/context/DECISIONS.md
- /workflow/context/ASSUMPTIONS.md
- /workflow/context/OPEN_QUESTIONS.md
- /workflow/context/REJECTED_OPTIONS.md

## 9. Do Not Do
- Do not treat role candidates as final requirements unless approved.
- Do not ignore personal/sensitive data handling questions.
- Do not assume external API or LLM transfer is allowed unless approved.
- Do not design detailed architecture or database schema in Stage 3.
```

---

## 12. Specialization Hooks

- **Web SaaS:** tenant/org roles, account lifecycle, billing/admin roles, resource visibility, sessions, analytics exposure.
- **Internal Tool:** staff roles, operational overrides, internal access boundaries, support/admin least privilege, auditability.
- **Mobile App:** device permissions, local storage, push notifications, offline/sync exposure, platform identity.
- **AI/Data Product:** dataset subjects, provenance, model input/output, LLM/API transfer, labeling roles, synthetic data, model misuse.
- **Regulated/Security-Sensitive:** compliance assumptions, audit logs, retention/deletion, legal/institutional review, high-severity blockers.
- **Brownfield/Legacy:** existing roles, permissions, data exposure, inherited constraints, forbidden change areas.

---

## 13. Anti-Patterns

Avoid treating all stakeholders as end users; ignoring admins/operators/reviewers/external systems/affected non-users; treating proposed roles as approved requirements; designing detailed RBAC/ABAC too early; ignoring personal data, logs, analytics, uploaded files, model inputs/outputs, or external transfers; claiming “no security risk” without evidence; deferring all security/privacy thinking to Stage 12; mixing requirements, architecture, database design, or implementation into this stage; and recording agent assumptions as approved decisions.

---

## 14. Template Quality Checklist

```text
[ ] Stage 2-specific purpose and core question are clear.
[ ] The template does not repeat the entire core skill template.
[ ] Always Read inputs are defined.
[ ] Conditional inputs and specialization hooks are defined.
[ ] Do Not Read By Default rules are defined.
[ ] Missing input handling is defined.
[ ] Mandatory artifacts are defined.
[ ] Conditional artifacts and N/A record rules are defined.
[ ] Required output structures are defined.
[ ] Stakeholder, role, data, transfer, risk, and audit registers are covered.
[ ] Approved decisions, decision candidates, assumptions, open questions, and risks are separated.
[ ] Traceability links from goals to stakeholders, roles, data, risks, and Stage 3 implications are defined.
[ ] context_packet.md handoff rules for Stage 3 are defined.
[ ] Human approval gate is included.
[ ] Project-specific content is not embedded.
[ ] Implementation, architecture, database, and detailed requirements work are left to later stages.
```
