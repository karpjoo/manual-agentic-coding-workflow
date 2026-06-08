---
name: 05c_technical_contracts
description: Define API, integration, and event/async contracts for Stage 5 when applicable.
stage: 05 Architecture & Technical Contracts
parent_skill: /skills/05_architecture_contracts/SKILL.md
subskill_id: 05c
subskill_order: 3
previous_subskill: /skills/05_architecture_contracts/05b_system_module_boundaries/SKILL.md
next_subskill: /skills/05_architecture_contracts/05d_auth_security_operations/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/05_architecture/05_api_contracts.md
requires_human_approval: true
external_visibility: internal
---

# 05c Technical Contracts

## 1. Purpose

Use this sub-skill to define architecture-level technical contracts after module boundaries have been drafted.

This sub-skill creates conditional artifacts when applicable:

```text
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_event_contracts.md
```

If one or more of these contract types are not applicable, record N/A rationale for the finalizer.

## 2. When to Use

Use this sub-skill after `05b_system_module_boundaries` has produced module boundaries and contract handoff notes.

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
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
```

### Read If Applicable

```text
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if contracts expose personal data, sensitive data, protected operations, external data transfer, or LLM/API data exposure.

/workflow/04_domain/04_bounded_contexts.md
- if contract boundaries must preserve bounded context boundaries.

/workflow/00_intake/00_existing_context_review.md
- if existing APIs, integrations, messaging, or compatibility constraints exist.
```

### Do Not Read By Default

```text
- implementation source code unless existing contracts must be inspected in a brownfield project
- database schema drafts
- later-stage test/task/implementation artifacts
- raw agent logs
- unapproved contract drafts from unrelated sessions
```

## 4. USER_DIRECTIVES.md Handling

If this file exists, read it before producing outputs:

```text
/workflow/05_architecture/USER_DIRECTIVES.md
```

Respect explicit user constraints on API style, integration approach, eventing, compatibility, security, and external services. Report conflicts with approved decisions.

## 5. Input Preflight Procedure

Verify:

```text
[ ] 05b module boundaries exist or the user explicitly instructed this sub-skill to proceed without them.
[ ] modules requiring public contracts are identified.
[ ] external systems are identified or marked absent.
[ ] domain events or async workflows are identified or marked absent.
[ ] role/security implications are noted for contract-level authorization.
[ ] rejected API/integration/event options are not revived.
```

## 6. Missing Input Handling

Blocking issues:

```text
- no usable module boundary artifact
- unclear requester roles for protected APIs
- unclear external system ownership for required integration contracts
- unresolved domain workflow that prevents defining required contract boundaries
- conflict between approved technology decisions and requested contract style
```

Non-blocking issues may be recorded as assumptions if contract shape can be drafted safely at architecture level.

## 7. Execution Procedure

### Step 1. Determine Applicable Contract Types

Decide whether each artifact is applicable:

```text
05_api_contracts.md
- applicable if the system exposes APIs, service operations, RPC calls, GraphQL operations, server actions, or explicit programmatic interfaces.

05_integration_contracts.md
- applicable if the system communicates with external systems, third-party APIs, identity providers, LLM/model APIs, webhooks, data providers, external storage, or external queues.

05_event_contracts.md
- applicable if the system uses domain events, async messaging, queues, pub/sub, background jobs, webhooks, notifications, scheduled jobs, or event-driven workflows.
```

Record N/A rationale for non-applicable artifacts.

### Step 2. Define API Contracts If Applicable

For each API or operation, define:

```text
- API ID
- operation name
- method / interaction type
- path / operation name if known
- requester role
- purpose
- owning module
- request summary
- response summary
- authorization rule
- validation rules
- error cases
- idempotency / retry notes
- pagination/filtering/sorting if relevant
- related requirements
- related domain concepts
- test implications
```

Keep this architecture-level. Do not write framework-specific code.

### Step 3. Define Integration Contracts If Applicable

For each external integration, define:

```text
- integration ID
- external system
- purpose
- direction of data flow
- data exchanged
- authentication/authorization mechanism
- failure handling
- retry/idempotency expectations
- rate limits or quotas if known
- privacy/security concerns
- logging/audit expectations
- fallback/degradation behavior
- ownership of integration errors
- related requirements
- test implications
```

### Step 4. Define Event / Async Contracts If Applicable

For each event or async workflow, define:

```text
- event ID
- event name
- producer
- consumer
- trigger
- payload summary
- delivery expectations
- ordering requirements
- idempotency requirements
- retry/dead-letter handling
- observability expectations
- related domain event
- related requirement
- test implications
```

### Step 5. Update Architecture Plan

Update `/workflow/05_architecture/05_architecture_plan.md` with:

```text
- contract boundary summary
- data flow implications
- error handling implications
- security/privacy implications
- test strategy implications
```

### Step 6. Update Architecture Decisions

Update `/workflow/05_architecture/05_architecture_decisions.md` if contract style, external integration approach, eventing, API versioning, or compatibility creates a decision candidate.

### Step 7. Prepare Handoff to Auth/Security/Operations

Identify contract-level issues that `05d_auth_security_operations` must handle:

```text
- protected operations
- sensitive data exposure
- external data transfer
- authentication dependencies
- audit-relevant actions
- retry/failure/observability concerns
- rate limiting or abuse concerns
- background job operational concerns
```

## 8. Output Artifacts

### Conditional Outputs

Create if applicable:

```text
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_event_contracts.md
```

### Mandatory Updates

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_architecture_decisions.md
```

### N/A Notes for Finalizer

If a contract artifact is not applicable, add N/A notes to a clearly marked section in the most relevant Stage 5 artifact or a temporary finalizer handoff section.

## 9. Required Output Structure

### 9.1 `05_api_contracts.md`

Use this structure if APIs exist:

```markdown
# 05 API Contracts

## 1. Status
- Draft / Needs Review / Approved

## 2. Approved Inputs Used

## 3. API Design Principles

## 4. API Inventory

| API ID | Operation | Requester Role | Purpose | Related Requirement | Related Module |
|---|---|---|---|---|---|

## 5. API Contract Details

### API-001 [[Operation Name]]
#### Purpose
#### Method / Interaction Type
#### Path / Operation Name
#### Owning Module
#### Requester Role
#### Authorization Rule
#### Request Summary
#### Response Summary
#### Validation Rules
#### Error Cases
#### Idempotency / Retry Notes
#### Pagination / Filtering / Sorting
#### Related Requirements
#### Related Domain Concepts
#### Test Implications

## 6. API-Level Error Policy

## 7. API-Level Security / Privacy Notes

## 8. Open Questions

## 9. Human Approval Required
```

### 9.2 `05_integration_contracts.md`

Use this structure if external integrations exist:

```markdown
# 05 Integration Contracts

## 1. Status

## 2. Approved Inputs Used

## 3. Integration Inventory

| Integration ID | External System | Direction | Purpose | Data Exchanged | Risk Level |
|---|---|---|---|---|---|

## 4. Integration Details

### INT-001 [[External System]]
#### Purpose
#### Direction of Data Flow
#### Data Exchanged
#### Authentication / Authorization
#### Failure Handling
#### Retry / Idempotency
#### Rate Limits / Quotas
#### Privacy / Security Concerns
#### Logging / Audit Expectations
#### Fallback / Degradation Behavior
#### Related Requirements
#### Test Implications

## 5. Integration Risks

## 6. Open Questions

## 7. Human Approval Required
```

### 9.3 `05_event_contracts.md`

Use this structure if events or async workflows exist:

```markdown
# 05 Event Contracts

## 1. Status

## 2. Approved Inputs Used

## 3. Event / Async Design Principles

## 4. Event Inventory

| Event ID | Event Name | Producer | Consumer | Trigger | Related Domain Event |
|---|---|---|---|---|---|

## 5. Event Details

### EVT-001 [[Event Name]]
#### Producer
#### Consumer
#### Trigger
#### Payload Summary
#### Delivery Expectations
#### Ordering Requirements
#### Idempotency Requirements
#### Retry / Dead-Letter Handling
#### Observability Expectations
#### Related Requirements
#### Related Domain Concepts
#### Test Implications

## 6. Async Failure Handling

## 7. Open Questions

## 8. Human Approval Required
```

## 10. Traceability Rules

Use stable IDs:

```text
API-001, API-002
INT-001, INT-002
EVT-001, EVT-002
```

Each contract must link to at least one:

```text
- requirement
- acceptance criterion
- domain concept
- domain event
- module
- risk/security constraint
```

If a contract has no traceable source, mark it as a proposed addition requiring human approval.

## 11. Decision / Assumption / Open Question Rules

- Contract recommendations are decision candidates.
- Unknown request/response details may be summarized as assumptions only if architecture-level boundaries are clear.
- Unknown authorization rules for protected operations are open questions or blockers, not assumptions.
- Do not update `DECISIONS.md` without explicit approval.

## 12. Validation Checklist

```text
[ ] 05b module boundaries were checked.
[ ] Applicable contract artifacts were identified.
[ ] N/A rationale was recorded for non-applicable contract artifacts.
[ ] API contracts link to modules and requirements.
[ ] Integration contracts identify data flow and failure handling.
[ ] Event contracts link to domain events or workflows.
[ ] Authorization implications are captured for 05d.
[ ] Security/privacy implications are captured for 05d.
[ ] Test implications are recorded.
[ ] Architecture decisions were updated if needed.
```

## 13. Human Approval Gate

Interim approval may be requested for:

```text
- API contract style
- external integration approach
- event/async design approach
- compatibility-impacting contract decisions
- exposed sensitive data or protected operation contracts
```

Full Stage 5 approval happens after finalizer execution.

## 14. Context Handoff to Next Sub-Skill

At the end of the relevant contract artifact or architecture plan, include:

```markdown
## Handoff to 05d Auth, Security & Operations

### Protected Operations

### Sensitive Data Exposures

### External Data Transfers

### Authn/Authz Dependencies

### Audit-Relevant Actions

### Operational Concerns

### Open Questions Affecting Security or Operations
```

## 15. Do Not Do

Do not:

- implement API code
- create database schema
- create tests
- over-specify framework-specific handlers
- ignore authorization for protected contracts
- hide external data transfer risks
- create contracts unrelated to requirements, modules, or domain workflows
- treat draft contracts as approved
