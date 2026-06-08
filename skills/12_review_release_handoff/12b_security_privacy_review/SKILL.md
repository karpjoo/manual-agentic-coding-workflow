---
name: 12b_security_privacy_review
description: Review authentication, authorization, data access, privacy, secrets, logging, external transfer, and security/privacy release blockers.
stage: 12 Review / Security / Release / Handoff
parent_skill: /skills/12_review_release_handoff/SKILL.md
subskill_id: 12b
subskill_order: 2
previous_subskill: /skills/12_review_release_handoff/12a_code_review/SKILL.md
next_subskill: /skills/12_review_release_handoff/12c_release_deployment_readiness/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/12_review_release_handoff/12_security_privacy_review.md
requires_human_approval: true
external_visibility: internal
---

# 12b Security / Privacy Review

## 1. Purpose

This sub-SKILL performs final security and privacy review for the release candidate.

It verifies whether the implementation and release plan respect approved security and privacy constraints.

This is a final verification gate, not the first security design stage.

## 2. Core Question

```text
Does the release candidate have unresolved security or privacy risks that should block, warn against, or require explicit human risk acceptance before release?
```

## 3. Required Inputs

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

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/09_tasks/09_task_cards.md
/workflow/11_implementation_results/
/workflow/12_review_release_handoff/12_code_review.md
```

If `02_risk_privacy_screening.md` does not exist, classify whether that is blocking based on whether the project handles users, roles, personal data, sensitive data, integrations, or external transfer.

### Read If Applicable

```text
/workflow/05_architecture/05_architecture_plan.md
- if architecture affects auth, integration, deployment, trust boundaries, or data flow.

/workflow/05_architecture/05_api_contracts.md
- if APIs exist.

/workflow/05_architecture/05_integration_contracts.md
- if external systems exist.

/workflow/06_data/06_logical_schema.md
- if persistent data exists.

/workflow/06_data/06_data_security_rules.md
- if access control is data-dependent.

/workflow/06_data/06_migration_plan.md
- if migration affects security/privacy.

/workflow/08_test_strategy/08_manual_test_plan.md
- if security-sensitive manual validation exists.

/workflow/11_implementation_results/11_test_evidence_*.md
- if security/privacy test evidence exists.

Project environment variable documentation
- if secret handling or deployment readiness is in scope.

Dependency manifest or package files
- if dependency risk review is required.
```

### Do Not Read By Default

```text
- raw agent logs;
- unrelated implementation files;
- superseded/rejected artifacts;
- production secret values;
- private credentials;
- real user data dumps;
- logs containing personal or sensitive data.
```

If secrets must be reviewed, inspect names, presence, storage policy, and access policy only. Never copy or expose secret values.

## 4. USER_DIRECTIVES.md Handling

Check:

```text
/workflow/12_review_release_handoff/USER_DIRECTIVES.md
```

Classify directives related to security, privacy, deployment, compliance, risk acceptance, or data handling. Report conflicts with approved decisions.

## 5. Input Preflight Procedure

```text
[ ] Identify whether the project handles roles, permissions, personal data, sensitive data, external APIs, LLM transfer, file uploads, payments, regulated data, or admin powers.
[ ] Identify approved security/privacy decisions.
[ ] Identify security/privacy requirements and acceptance criteria.
[ ] Review 12a code findings for security/privacy clues.
[ ] Check whether security/privacy test evidence exists.
[ ] Check whether data access/security rules exist if needed.
[ ] Check whether environment/secret documentation exists if deployment is in scope.
[ ] Identify missing or conflicting inputs.
```

Blocking preflight issues:

```text
- personal/sensitive data exists but no handling policy or review input exists;
- role/permission behavior exists but no authz model or evidence exists;
- external transfer exists but no transfer policy exists;
- deployment is in scope but secret handling is unknown;
- security blocker found in code review with no mitigation.
```

## 6. Execution Procedure

### Step 1. Confirm Security / Privacy Review Scope

Record:

```text
data types handled
roles and permission levels
external integrations
LLM/API transfer if any
admin powers
audit/logging needs
release target
security/privacy assumptions
```

### Step 2. Review Authentication and Authorization

Check:

```text
authentication flow
role enforcement
permission boundaries
admin-only behavior
unauthorized access behavior
session/token handling if applicable
auth-related tests or manual validation
```

### Step 3. Review Data Access and Data Security Rules

Check:

```text
ownership rules
read/write restrictions
row/document/object access rules
file/storage access
migration access
backups or exports
least privilege
test evidence for access denial
```

### Step 4. Review Personal / Sensitive Data Handling

Check:

```text
personal data collected
sensitive data collected
data minimization
retention/deletion
consent or notice assumptions
data export
logs and error messages
analytics or tracking
manual review workflows
```

### Step 5. Review External Transfer and Third Parties

Check:

```text
external API transfer
LLM provider transfer
webhooks
email/SMS/push providers
storage providers
analytics providers
payment providers
data sent, purpose, retention assumptions
```

### Step 6. Review Secrets and Environment Variables

Check:

```text
required secret names
storage location expectations
local vs production handling
secret exposure in logs/errors
rotation/revocation assumptions
missing env documentation
```

Do not copy secret values.

### Step 7. Review Logging, Observability, and Error Exposure

Check:

```text
sensitive values in logs
personal data in logs
debug traces
error messages exposing internals
audit logs where required
security-relevant events
```

### Step 8. Classify Findings

Use:

```text
Security Blocker
Privacy Blocker
Security Warning
Privacy Warning
Compliance Warning
Recommendation
Not Applicable
Open Question
```

Each finding must include:

```text
Finding ID
Type
Severity
Affected Requirement / Task / File / Artifact
Evidence
Impact
Recommended Action
Risk Acceptance Needed
```

### Step 9. Write `12_security_privacy_review.md`

## 7. Output Artifacts

### Mandatory Artifacts

```text
/workflow/12_review_release_handoff/12_security_privacy_review.md
```

### Conditional Artifacts

```text
/workflow/12_review_release_handoff/12_compliance_review.md
- if regulated, audit-sensitive, privacy-sensitive, or compliance-sensitive constraints apply and require separate treatment.
```

If the conditional artifact is not created, record N/A rationale for finalizer.

## 8. Required Output Structure

```markdown
# 12 Security and Privacy Review

## 1. Review Scope
## 2. Inputs Reviewed
## 3. Approved Security / Privacy Constraints
## 4. Authentication Review
## 5. Authorization Review
## 6. Data Access Review
## 7. Personal / Sensitive Data Handling
## 8. Secrets and Environment Variables
## 9. Logging and Error Exposure
## 10. External API / LLM / Third-Party Transfer
## 11. Retention, Deletion, and Audit Concerns
## 12. Security Blockers
## 13. Privacy Blockers
## 14. Warnings
## 15. Recommendations
## 16. Assumptions
## 17. Open Questions
## 18. Conditional Artifact N/A Notes
## 19. Review Conclusion
## 20. Handoff to 12c Release / Deployment Readiness
```

## 9. Traceability Requirements

Preserve links:

```text
Security/Privacy Requirement → Acceptance Criteria → Task → Test Evidence → Review Finding
```

Use finding IDs:

```text
SEC-001, SEC-002, ...
PRIV-001, PRIV-002, ...
COMP-001, COMP-002, ...
```

## 10. Validation Checklist

```text
[ ] Security/privacy scope was identified.
[ ] Role and permission behavior was reviewed where applicable.
[ ] Personal/sensitive data handling was reviewed where applicable.
[ ] External transfer was reviewed where applicable.
[ ] Secret values were not exposed.
[ ] Logging and error exposure were checked.
[ ] Security/privacy test evidence was reviewed where available.
[ ] Blockers and warnings were separated.
[ ] Risk acceptance candidates were clearly marked.
[ ] Handoff notes for deployment readiness were included.
```

## 11. Human Approval Gate

This sub-SKILL does not approve security/privacy risk acceptance.

End with:

```markdown
## Human Review Needed

### Security Blockers
- ...

### Privacy Blockers
- ...

### Risk Acceptance Candidates
- ...

### Open Questions
- ...

### Recommended Next Sub-SKILL
- Run `/skills/12_review_release_handoff/12c_release_deployment_readiness/SKILL.md`.
```

## 12. Context Handoff to Next Sub-SKILL

At the end of `12_security_privacy_review.md`, include:

```markdown
## Handoff to 12c Release / Deployment Readiness

### Security / Privacy Blockers Affecting Release
### Environment or Secret Handling Issues
### Deployment Constraints
### Rollback / Recovery Security Concerns
### Open Questions Affecting Release Approval
```

## Decision / Assumption / Open Question Rules

Use these classifications consistently:

```text
Approved Decision
- Only explicit human approval may create this.

Decision Candidate
- A recommended release, security, deployment, operations, or documentation decision awaiting human approval.

Working Assumption
- A temporary belief used only to continue safe partial work.

Open Question
- An unresolved issue that may affect release, deployment, security, privacy, operations, documentation, or retrospective.

Rejected Option
- An option explicitly rejected or superseded. Do not revive it unless the human reopens it.

Recommendation
- Agent advice. It is not a decision.
```

Do not update `DECISIONS.md` unless explicit human approval exists.

## Failure Handling

If the SKILL cannot be completed safely, create a partial output with:

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

Do not pretend completion when required evidence is missing.

## Do Not Do

The agent must not:

- approve release, deployment, or risk acceptance on behalf of the human developer;
- silently turn assumptions into decisions;
- treat unapproved drafts as source of truth;
- use superseded or rejected artifacts as current truth;
- expose secret values;
- claim tests passed without evidence;
- mark a blocker as resolved without evidence;
- update `DECISIONS.md` without explicit human approval;
- create README.md or artifact_contract.yml unless explicitly requested.
