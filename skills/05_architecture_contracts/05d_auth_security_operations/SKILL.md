---
name: 05d_auth_security_operations
description: Define architecture-level authentication, authorization, security/privacy, operations, and brownfield compatibility policies for Stage 5.
stage: 05 Architecture & Technical Contracts
parent_skill: /skills/05_architecture_contracts/SKILL.md
subskill_id: 05d
subskill_order: 4
previous_subskill: /skills/05_architecture_contracts/05c_technical_contracts/SKILL.md
next_subskill: /skills/05_architecture_contracts/05e_architecture_finalizer/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/05_architecture/05_authn_authz_model.md
requires_human_approval: true
external_visibility: internal
---

# 05d Auth, Security & Operations

## 1. Purpose

Use this sub-skill to define architecture-level authentication, authorization, security/privacy architecture, operational architecture, and brownfield compatibility concerns after system boundaries and contracts have been drafted.

This sub-skill creates conditional artifacts when applicable:

```text
/workflow/05_architecture/05_authn_authz_model.md
/workflow/05_architecture/05_security_privacy_architecture.md
/workflow/05_architecture/05_operational_architecture.md
/workflow/05_architecture/05_brownfield_compatibility_plan.md
```

It also updates cross-cutting technical policy sections in:

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_architecture_decisions.md
```

## 2. When to Use

Use this sub-skill after `05c_technical_contracts` has identified API, integration, event, external data transfer, protected operation, and operational implications.

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
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
```

### Read If Applicable

```text
/workflow/05_architecture/05_api_contracts.md
- if APIs or programmatic operations exist.

/workflow/05_architecture/05_integration_contracts.md
- if external integrations exist.

/workflow/05_architecture/05_event_contracts.md
- if events, background jobs, queues, notifications, or async workflows exist.

/workflow/00_intake/00_existing_context_review.md
- if this is brownfield, migration, or existing-system extension work.

/workflow/04_domain/04_domain_events.md
- if event-driven behavior affects audit, security, or operations.
```

### Do Not Read By Default

```text
- source code unless brownfield compatibility requires targeted inspection
- detailed data schema drafts from Stage 6
- future test/task/implementation artifacts
- raw agent logs
- unapproved security notes from unrelated sessions
```

## 4. USER_DIRECTIVES.md Handling

If this file exists, read it before producing outputs:

```text
/workflow/05_architecture/USER_DIRECTIVES.md
```

Security, privacy, compliance, auth, audit, and operational directives have high impact. If they conflict with approved decisions, stop and report the conflict unless the user explicitly directs exploratory analysis.

## 5. Input Preflight Procedure

Verify:

```text
[ ] stakeholder roles and risk/privacy screening were checked.
[ ] module boundaries were checked.
[ ] contract artifacts were checked if applicable.
[ ] protected operations were identified or marked absent.
[ ] personal/sensitive data handling direction was checked.
[ ] external data transfers were identified or marked absent.
[ ] operational constraints were identified or marked absent.
[ ] brownfield compatibility needs were identified or marked absent.
```

## 6. Missing Input Handling

Blocking issues:

```text
- unclear role/permission direction when protected operations exist
- unclear personal/sensitive data handling direction when such data exists
- unresolved external data transfer policy
- missing risk/privacy screening for security-sensitive or regulated project
- unclear identity provider constraint when authn/authz architecture depends on it
- missing existing-system context for brownfield compatibility decisions
```

Non-blocking issues may be recorded as assumptions only when they do not affect security, privacy, authorization, or irreversible architecture decisions.

## 7. Execution Procedure

### Step 1. Determine Applicable Artifacts

Determine whether each conditional artifact is required:

```text
05_authn_authz_model.md
- required if user accounts, roles, permissions, administrators, protected resources, protected operations, sensitive data, or access-controlled resources exist.

05_security_privacy_architecture.md
- required if personal data, sensitive data, external data transfer, LLM/API exposure, compliance concerns, audit needs, or security-sensitive workflows exist.

05_operational_architecture.md
- required if deployment, hosting, reliability, observability, environment management, secrets, scaling, background jobs, or operations are significant architecture concerns.

05_brownfield_compatibility_plan.md
- required if the project modifies, extends, migrates, integrates with, or must remain compatible with an existing system.
```

Record N/A rationale for non-applicable artifacts.

### Step 2. Define Authentication and Authorization Model If Applicable

Define:

```text
- identity source
- user/account model at architecture level
- roles
- permissions
- protected resources
- protected operations
- authorization decision points
- authorization enforcement points
- admin capability boundaries
- audit requirements
- privilege escalation risks
- open questions
```

This is architecture-level auth design, not database security rule design.

### Step 3. Define Security and Privacy Architecture If Applicable

Define:

```text
- personal/sensitive data flows
- trust boundaries
- external data transfer points
- LLM/API exposure points if applicable
- data minimization implications
- authentication and authorization dependencies
- audit logging architecture
- secret handling direction
- logging redaction rules
- abuse/rate limiting concerns
- threat/risk assumptions
- security and privacy open questions
```

### Step 4. Define Operational Architecture If Applicable

Define:

```text
- deployment/runtime assumptions
- environment boundaries
- configuration and environment variable policy
- secret management direction
- logging strategy
- metrics/observability strategy
- error reporting strategy
- background job operations
- retry/failure/recovery expectations
- reliability/scaling assumptions
- manual operations and runbook implications
```

### Step 5. Define Brownfield Compatibility Plan If Applicable

For brownfield or migration projects, define:

```text
- existing system boundaries to preserve
- compatibility constraints
- migration or adapter strategy candidates
- rollback considerations
- regression risk areas
- forbidden change areas
- integration with existing data or APIs
- operational transition concerns
```

### Step 6. Update Cross-Cutting Policies in Architecture Plan

Update `/workflow/05_architecture/05_architecture_plan.md` with:

```text
- error handling policy
- validation responsibility
- logging policy
- audit logging policy
- observability policy
- configuration / environment policy
- secret handling policy
- rate limiting policy
- caching policy if applicable
- background job handling policy
- transaction / consistency strategy
- failure and recovery strategy
```

### Step 7. Update Architecture Decisions

Update `/workflow/05_architecture/05_architecture_decisions.md` with decision candidates related to:

```text
- identity provider
- authorization model
- audit approach
- logging/observability approach
- secret handling
- operational runtime
- brownfield migration/compatibility approach
```

Mark as `Proposed` unless explicitly approved.

### Step 8. Prepare Handoff to Finalizer

Identify:

```text
- artifacts created
- artifacts marked N/A
- open questions affecting final Stage 5 approval
- assumptions Stage 6 must not treat as approved
- risks requiring human review
- traceability gaps to resolve in finalizer
```

## 8. Output Artifacts

### Conditional Outputs

Create if applicable:

```text
/workflow/05_architecture/05_authn_authz_model.md
/workflow/05_architecture/05_security_privacy_architecture.md
/workflow/05_architecture/05_operational_architecture.md
/workflow/05_architecture/05_brownfield_compatibility_plan.md
```

### Mandatory Updates

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_architecture_decisions.md
```

### Context Updates If Needed

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
```

## 9. Required Output Structure

### 9.1 `05_authn_authz_model.md`

Use this structure if authn/authz applies:

```markdown
# 05 Authentication and Authorization Model

## 1. Status
- Draft / Needs Review / Approved

## 2. Approved Inputs Used

## 3. Identity Model

## 4. Role Inventory

| Role ID | Role Name | Description | Allowed Capabilities | Forbidden Capabilities |
|---|---|---|---|---|

## 5. Protected Resource Inventory

| Resource | Operation | Allowed Roles | Authorization Rule | Audit Required |
|---|---|---|---|---|

## 6. Authorization Decision Points

## 7. Authorization Enforcement Points

## 8. Admin Capability Boundaries

## 9. Audit Logging Requirements

## 10. Security Risks

## 11. Open Questions

## 12. Human Approval Required
```

### 9.2 `05_security_privacy_architecture.md`

Use this structure if security/privacy architecture applies:

```markdown
# 05 Security and Privacy Architecture

## 1. Status

## 2. Approved Inputs Used

## 3. Security / Privacy Drivers

## 4. Trust Boundaries

## 5. Personal / Sensitive Data Flow Summary

## 6. External Data Transfer Points

## 7. Access Control Architecture Notes

## 8. Audit Logging Architecture

## 9. Secrets and Configuration Security

## 10. Logging Redaction and Data Minimization

## 11. Abuse, Rate Limiting, and Misuse Concerns

## 12. Security / Privacy Risks

## 13. Open Questions

## 14. Human Approval Required
```

### 9.3 `05_operational_architecture.md`

Use this structure if operational architecture applies:

```markdown
# 05 Operational Architecture

## 1. Status

## 2. Approved Inputs Used

## 3. Runtime / Deployment Assumptions

## 4. Environment and Configuration Policy

## 5. Secret Handling Direction

## 6. Logging and Observability

## 7. Metrics and Alerting Candidates

## 8. Background Jobs and Scheduled Work

## 9. Failure, Retry, and Recovery Strategy

## 10. Scaling and Performance Assumptions

## 11. Operational Risks

## 12. Open Questions

## 13. Human Approval Required
```

### 9.4 `05_brownfield_compatibility_plan.md`

Use this structure if brownfield compatibility applies:

```markdown
# 05 Brownfield Compatibility Plan

## 1. Status

## 2. Approved Inputs Used

## 3. Existing System Boundaries

## 4. Compatibility Constraints

## 5. Migration / Adapter Strategy Candidates

## 6. Forbidden Change Areas

## 7. Regression Risk Areas

## 8. Rollback Considerations

## 9. Operational Transition Concerns

## 10. Open Questions

## 11. Human Approval Required
```

## 10. Traceability Rules

Link auth, security, privacy, and operations architecture to:

```text
- stakeholder roles
- security/privacy risks
- requirements
- acceptance criteria
- protected modules
- API/integration/event contracts
- domain invariants
- operational constraints
```

Use stable IDs:

```text
AUTHZ-001, AUTHZ-002
SEC-001, SEC-002
OPS-001, OPS-002
BRW-001, BRW-002
```

## 11. Decision / Assumption / Open Question Rules

- Auth/security/operations recommendations are decision candidates unless explicitly approved.
- Never treat security/privacy assumptions as approved policy.
- Unresolved authorization or sensitive data handling issues are open questions or blockers.
- Do not update `DECISIONS.md` without explicit approval.

## 12. Validation Checklist

```text
[ ] Risk/privacy screening was checked.
[ ] Module boundaries were checked.
[ ] Contract artifacts were checked if applicable.
[ ] Authn/authz artifact was created or marked N/A.
[ ] Security/privacy artifact was created or marked N/A.
[ ] Operational architecture artifact was created or marked N/A.
[ ] Brownfield compatibility artifact was created or marked N/A.
[ ] Cross-cutting policies were updated in architecture plan.
[ ] Architecture decisions were updated if needed.
[ ] Open questions and blockers were recorded.
[ ] Handoff to finalizer was prepared.
```

## 13. Human Approval Gate

Interim approval may be requested for:

```text
- identity provider direction
- role and permission model
- admin capability boundaries
- external data transfer handling
- audit logging direction
- operational runtime direction
- brownfield compatibility strategy
```

Full Stage 5 approval happens after finalizer execution.

## 14. Handoff to Finalizer

At the end of each created artifact or architecture plan, include:

```markdown
## Handoff to 05e Architecture Finalizer

### Artifacts Created or Updated

### N/A Artifacts and Rationale

### Decision Candidates

### Working Assumptions

### Open Questions

### Risks Requiring Human Review

### Traceability Gaps
```

## 15. Do Not Do

Do not:

- design database security rules in detail; Stage 6 handles data security rules
- implement auth or security code
- treat auth/security/privacy assumptions as approved decisions
- ignore external data transfer risks
- ignore audit implications for admin or sensitive operations
- make operational promises without evidence
- skip N/A rationale for non-applicable conditional artifacts
