# 05 Architecture & Technical Contracts Skill Template

> Template file: `/workflow_templates/stage_templates/05_architecture_skill_template.md`
> Target reusable skill: `/skills/05_architecture_contracts/SKILL.md`
> Target project artifact folder: `/workflow/05_architecture`

---

## 0. Template Scope

This is a **Stage-Specific Skill Template** for Stage 5: Architecture & Technical Contracts.

It is not an executable `SKILL.md` by itself.

Use this template to create a reusable executable skill at:

```text
/skills/05_architecture_contracts/SKILL.md
```

This template defines only Stage 5-specific extensions.

It assumes the reusable skill will also follow the core skill template, including:

* agent-as-assistant operating mode
* input precedence rules
* `USER_DIRECTIVES.md` handling
* artifact status checks
* decision / assumption / open question separation
* context packet update rules
* human approval gate
* failure handling
* do-not-do rules

---

## 1. Stage Purpose

Stage 5 translates approved requirements and approved domain modeling outputs into a concrete architecture direction and technical contracts.

The purpose is to define:

* architecture style and major technical structure
* frontend / backend / service boundaries
* module boundaries
* API contracts, if APIs exist
* integration contracts, if external systems exist
* authentication and authorization model, if roles or permissions exist
* event / async contracts, if domain events or messaging exist
* system data flow at the architecture level
* error handling, logging, observability, and operational policies
* major architecture decisions and trade-offs
* architecture-level security and privacy constraints
* handoff context for Stage 6 Data Design

This stage does not implement code, design database schema in detail, or create task cards.

---

## 2. Core Question

The core question for this stage is:

```text
Given the approved service goal, requirements, stakeholder/risk context, and domain model, what system architecture and technical contracts should guide data design, test strategy, task breakdown, and implementation?
```

Secondary questions:

```text
- What are the system boundaries?
- What are the module boundaries?
- Which responsibilities belong to frontend, backend, database, external services, or infrastructure?
- Which API, integration, auth, event, and operational contracts are needed?
- Which architecture decisions require explicit human approval?
- Which architecture assumptions are safe to carry forward, and which are blocking?
```

---

## 3. Stage Type

This is a planning and design stage.

It is:

```text
- architecture-design
- contract-design
- integration-boundary-design
- security/privacy-aware
- test-aware
- data-design-preparatory
```

It is not:

```text
- implementation
- database physical schema design
- detailed UI design
- task breakdown
- test implementation
- deployment execution
```

---

## 4. Stage Folder

Project artifacts for this stage should be created or updated under:

```text
/workflow/05_architecture
```

Stage-local human instructions may be provided at:

```text
/workflow/05_architecture/USER_DIRECTIVES.md
```

---

## 5. Always Read Inputs

The generated reusable `SKILL.md` must require the Agent to read these inputs when available.

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
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/03_requirements/03_traceability_matrix.md
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
```

If Stage 4 was split internally, the Agent must read only approved official Stage 4 artifacts, not internal sub-skill files or prompt history.

---

## 6. Read If Applicable Inputs

Read these only when project profile, `context_packet.md`, `DECISIONS.md`, `USER_DIRECTIVES.md`, or artifact manifest indicates they apply.

```text
/workflow/00_intake/00_existing_context_review.md
- Read if the project is brownfield, legacy, migration, or extension of an existing system.

/workflow/00_intake/00_project_intake.md
- Read if project type, fixed technology choices, repository constraints, hosting constraints, or forbidden change areas are not already summarized in context_packet.md.

/workflow/04_domain/04_domain_traceability_matrix.md
- Read if Stage 4 produced a separate domain traceability matrix.

/workflow/04_domain/result.md
- Read if the approved Stage 4 summary contains architecture-relevant warnings, unresolved modeling risks, or handoff notes.

/workflow/03_requirements/result.md
- Read if requirements contain unresolved architecture implications not reflected in the requirements or acceptance criteria artifacts.

/workflow/02_stakeholders_risk/result.md
- Read if stakeholder/risk outputs include unresolved security, privacy, compliance, or operational constraints.

/workflow/context/REJECTED_OPTIONS.md
- Read if previous architecture, technology, platform, API, integration, or data storage options were rejected or superseded.

/workflow/context/APPROVAL_LOG.md
- Read if approval status is unclear or if Stage 4/Stage 5 boundary decisions need verification.
```

Specialization addenda may activate additional conditional inputs.

Examples:

```text
web_saas
- hosting constraints
- identity provider constraints
- browser/client constraints

mobile_app
- platform constraints
- offline/sync constraints
- device permission constraints

ai_data_product
- dataset source notes
- model/evaluation risk notes
- human review requirements

regulated_security_sensitive
- threat model notes
- audit/compliance constraints
- privacy impact constraints

brownfield_legacy
- existing architecture notes
- compatibility constraints
- regression baseline
```

---

## 7. Do Not Read By Default

The generated reusable `SKILL.md` must instruct the Agent not to read these by default:

```text
- raw chat history
- raw agent logs
- unapproved draft artifacts
- superseded architecture drafts
- rejected options as if they were current options
- full implementation source code unless brownfield architecture review is explicitly required
- detailed database schemas from later stages
- task breakdown artifacts from later stages
- implementation prompt artifacts from later stages
- test evidence from later stages
```

If implementation source code must be inspected in a brownfield project, the skill must treat that as a conditional input and limit the inspection to architecture-relevant files.

---

## 8. Missing Input Handling

The generated reusable `SKILL.md` must classify missing inputs as blocking or non-blocking.

### Blocking Missing Inputs

Treat the following as blocking unless the user explicitly requests exploratory architecture drafting:

```text
- missing or unapproved service goal
- missing or unapproved requirements
- missing or unapproved acceptance criteria
- missing or unapproved domain model
- missing or unresolved role/permission direction when authz architecture is required
- missing or unresolved personal/sensitive data handling direction when personal/sensitive data exists
- conflicting approved decisions about technology stack, architecture style, hosting, or data ownership
```

### Non-Blocking Missing Inputs

The following may be handled with clearly labeled assumptions if they do not affect irreversible architecture choices:

```text
- incomplete observability details
- incomplete deployment target details
- missing exact API field names when API resource boundaries are still clear
- unresolved non-critical external integration details
- incomplete performance targets for a prototype or early MVP
```

### Required Blocker Report

If blocked, produce a `Blocker Report` in `result.md` with:

```markdown
## Blocker Report

### Blocking Issue
### Why It Matters
### Affected Architecture Areas
### Affected Downstream Stages
### Safe Partial Work Completed
### Human Decision Needed
```

---

## 9. Stage-Specific Procedure

The generated reusable `SKILL.md` must instruct the Agent to follow this procedure.

### Step 1. Confirm Stage Context

Restate:

```text
- current stage: Stage 5 Architecture & Technical Contracts
- previous approved stage artifacts used
- next stage: Stage 6 Data Design
- whether the work is greenfield, brownfield, prototype, MVP production, or regulated/security-sensitive
- whether project-type specialization addenda apply
```

### Step 2. Run Architecture Preflight

Check:

```text
- required inputs exist
- required inputs are approved or explicitly allowed as draft inputs
- no superseded or rejected artifacts are used as current truth
- USER_DIRECTIVES.md exists and has been read if present
- current user instruction does not conflict with approved decisions
- unresolved questions that may block architecture are identified
```

### Step 3. Extract Architecture Drivers

From approved inputs, identify:

```text
- business goals that shape architecture
- critical functional requirements
- non-functional requirements
- security and privacy constraints
- role and permission constraints
- domain boundaries and bounded contexts
- invariants and consistency boundaries
- expected data ownership boundaries
- integration needs
- operational constraints
- deployment or hosting constraints
- testability and validation constraints
```

### Step 4. Define System Context and Boundaries

Describe:

```text
- system under design
- users / actors
- administrators / operators
- external systems
- identity providers
- data providers
- third-party APIs
- LLM/model services, if applicable
- out-of-scope systems
```

Use a textual system context diagram if visual diagrams are not required.

### Step 5. Propose Architecture Options

Identify 2–4 viable architecture options when meaningful.

For each option, capture:

```text
- summary
- fit with approved requirements
- fit with domain model
- security/privacy implications
- operational complexity
- implementation complexity
- testability
- scalability and performance implications
- major risks
- why it should be selected or rejected
```

If only one architecture option is realistic because of approved constraints, state why.

### Step 6. Recommend Architecture Direction

Create a recommended architecture direction.

Important rule:

```text
The recommendation is a decision candidate, not an approved decision.
```

The recommendation should include:

```text
- architecture style
- runtime components
- frontend/backend/service boundaries
- module organization
- major dependencies
- authn/authz approach
- contract boundaries
- integration approach
- error handling policy
- logging/observability policy
- operational assumptions
- data design implications
```

### Step 7. Define Module Boundaries

For each module or component, define:

```text
- stable module/component ID
- name
- responsibility
- owned domain concepts
- public interface
- internal responsibilities
- dependencies
- forbidden dependencies
- related requirements
- related domain concepts
- security/privacy notes
- testability notes
```

Module boundaries should preserve domain meaning and avoid leaking infrastructure concerns into domain concepts.

### Step 8. Define API Contracts If Applicable

If the system exposes APIs, define API contracts at the architecture level.

Include:

```text
- API group/resource
- endpoint or operation name
- method or interaction type
- requester role
- request summary
- response summary
- authorization rule
- validation rule
- error cases
- idempotency rule if relevant
- pagination/filtering/sorting if relevant
- related requirements
- related domain concepts
```

Do not over-specify implementation framework code.

### Step 9. Define Integration Contracts If Applicable

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
- fallback or degradation behavior
- ownership of integration errors
```

### Step 10. Define Authentication and Authorization Model If Applicable

If roles, permissions, user accounts, administrators, sensitive data, or protected operations exist, define:

```text
- identity source
- user/account model at architecture level
- roles
- permissions
- protected resources
- authorization decision points
- authorization enforcement points
- admin capabilities
- audit requirements
- privilege escalation risks
- open questions
```

This is architecture-level auth design, not database security rule design.

### Step 11. Define Event / Async Contracts If Applicable

If domain events, asynchronous workflows, queues, pub/sub, background jobs, webhooks, or notifications exist, define:

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
```

### Step 12. Define Data Flow and Data Ownership at Architecture Level

Describe architecture-level data flow:

```text
- data enters the system from where
- data is validated where
- data is transformed where
- data is stored where conceptually
- data is read by which modules
- data is exposed through which contracts
- sensitive data crosses which boundaries
- audit-relevant actions occur where
```

Do not design detailed schema here.

Detailed schema belongs to Stage 6 Data Design.

### Step 13. Define Cross-Cutting Technical Policies

At minimum, define or mark N/A for:

```text
- error handling
- validation responsibility
- logging
- audit logging
- observability
- metrics
- configuration / environment variables
- secret handling
- rate limiting
- caching
- background job handling
- transaction / consistency strategy
- performance-sensitive paths
- failure and recovery strategy
```

### Step 14. Identify Architecture Decisions

Create architecture decision records or a decision table.

Each decision candidate must include:

```text
- decision ID
- title
- status: Proposed / Approved / Rejected / Superseded
- context
- options considered
- recommendation
- consequences
- risks
- required human approval
- related requirements
- related domain concepts
```

Only explicitly approved decisions may be marked `Approved`.

### Step 15. Update Traceability

Update architecture traceability so that downstream stages can connect:

```text
Requirement
→ Acceptance Criteria
→ Domain Concept / Invariant / Event
→ Architecture Component / Module
→ API Contract / Integration Contract / Event Contract
→ Data Design Implication
→ Future Test Strategy
```

If traceability cannot be completed, record the gap.

### Step 16. Prepare Stage 6 Data Design Handoff

Identify what Stage 6 must know:

```text
- data ownership boundaries
- conceptual storage needs
- persistence expectations
- query patterns implied by contracts
- access control implications
- audit requirements
- retention/deletion implications
- migration implications if brownfield
- consistency/transaction boundaries
- unresolved data design questions
```

Do not design the detailed schema.

### Step 17. Produce Human Approval Gate

List:

```text
- architecture decisions to approve
- API contracts to approve
- authorization model to approve
- integration approach to approve
- assumptions to confirm
- open questions to resolve
- risks to review
- artifacts ready for review
```

---

## 10. Mandatory Artifacts

The generated reusable `SKILL.md` must create or update these mandatory artifacts.

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/05_architecture/05_architecture_traceability_matrix.md
/workflow/05_architecture/result.md
/workflow/context/context_packet.md
```

The skill must also update or prepare these context files when applicable:

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

The skill must not update `DECISIONS.md` unless explicit human approval is already present.

---

## 11. Conditional Artifacts

The generated reusable `SKILL.md` must create these artifacts when applicable.

```text
/workflow/05_architecture/05_api_contracts.md
- Required if the system exposes APIs, service operations, RPC calls, GraphQL operations, server actions, or other explicit programmatic interfaces.

/workflow/05_architecture/05_integration_contracts.md
- Required if the system communicates with external systems, third-party APIs, identity providers, payment providers, LLM/model APIs, webhooks, data providers, or external storage.

/workflow/05_architecture/05_authn_authz_model.md
- Required if the system has user accounts, roles, permissions, administrators, protected operations, sensitive data, or access-controlled resources.

/workflow/05_architecture/05_event_contracts.md
- Required if the system uses domain events, async messaging, queues, pub/sub, background jobs, webhooks, notifications, or event-driven workflows.

/workflow/05_architecture/05_security_privacy_architecture.md
- Required if Stage 2 or Stage 3 identified personal data, sensitive data, compliance concerns, external data transfer, LLM/API exposure, audit requirements, or security-sensitive workflows.

/workflow/05_architecture/05_operational_architecture.md
- Required if deployment, hosting, scaling, reliability, observability, environment management, secrets, or operations are significant architecture concerns.

/workflow/05_architecture/05_brownfield_compatibility_plan.md
- Required if the project modifies, extends, migrates, or integrates with an existing system.
```

If a conditional artifact is not applicable, the skill must record an N/A item in `result.md`.

---

## 12. N/A Record Rules

For every conditional artifact not created, record:

```markdown
## N/A Items

| Artifact | Why Not Applicable | Revisit If |
|---|---|---|
| 05_api_contracts.md | No APIs or programmatic interfaces are exposed. | The system adds backend endpoints, service operations, or integrations. |
```

Do not silently omit conditional artifacts.

---

## 13. Required Output Structure

### 13.1 `05_architecture_plan.md`

Required sections:

```markdown
# 05 Architecture Plan

## 1. Status
- Draft / Needs Review / Approved

## 2. Architecture Summary

## 3. Approved Inputs Used

## 4. Architecture Drivers
### 4.1 Functional Drivers
### 4.2 Non-Functional Drivers
### 4.3 Security / Privacy Drivers
### 4.4 Domain Drivers
### 4.5 Operational Drivers

## 5. System Context
### 5.1 Actors
### 5.2 External Systems
### 5.3 System Boundary
### 5.4 Out-of-Scope Systems

## 6. Architecture Options Considered

## 7. Recommended Architecture Direction
- Mark as Decision Candidate unless explicitly approved.

## 8. Runtime / Container View

## 9. Frontend / Backend / Service Boundary

## 10. Data Flow at Architecture Level

## 11. Cross-Cutting Policies
### 11.1 Error Handling
### 11.2 Validation Responsibility
### 11.3 Logging
### 11.4 Observability
### 11.5 Configuration and Secrets
### 11.6 Caching
### 11.7 Background Jobs
### 11.8 Consistency / Transaction Strategy

## 12. Security and Privacy Architecture Notes

## 13. Data Design Implications for Stage 6

## 14. Test Strategy Implications for Stage 8

## 15. Risks and Trade-Offs

## 16. Open Questions

## 17. Human Approval Required
```

---

### 13.2 `05_module_boundaries.md`

Required sections:

```markdown
# 05 Module Boundaries

## 1. Status

## 2. Boundary Principles

## 3. Module / Component Inventory

| Module ID | Name | Responsibility | Owned Domain Concepts | Public Interface | Dependencies | Forbidden Dependencies |
|---|---|---|---|---|---|---|

## 4. Module Details

### MOD-001 [[Name]]
#### Responsibility
#### Inputs
#### Outputs
#### Public Interface
#### Internal Responsibilities
#### Related Requirements
#### Related Domain Concepts
#### Security / Privacy Notes
#### Testability Notes
#### Data Design Implications

## 5. Dependency Rules

## 6. Boundary Risks

## 7. Human Approval Required
```

---

### 13.3 `05_api_contracts.md`

Required if APIs exist.

```markdown
# 05 API Contracts

## 1. Status

## 2. API Design Principles

## 3. API Inventory

| API ID | Operation | Requester Role | Purpose | Related Requirement | Related Module |
|---|---|---|---|---|---|

## 4. API Contract Details

### API-001 [[Operation Name]]
#### Purpose
#### Method / Interaction Type
#### Path / Operation Name
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

## 5. API-Level Error Policy

## 6. API-Level Security / Privacy Notes

## 7. Open Questions

## 8. Human Approval Required
```

---

### 13.4 `05_integration_contracts.md`

Required if external integrations exist.

```markdown
# 05 Integration Contracts

## 1. Status

## 2. Integration Inventory

| Integration ID | External System | Direction | Purpose | Data Exchanged | Risk Level |
|---|---|---|---|---|---|

## 3. Integration Details

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

## 4. Integration Risks

## 5. Human Approval Required
```

---

### 13.5 `05_authn_authz_model.md`

Required if roles, permissions, accounts, administrators, or protected resources exist.

```markdown
# 05 Authentication and Authorization Model

## 1. Status

## 2. Identity Model

## 3. Role Inventory

| Role ID | Role Name | Description | Allowed Capabilities | Forbidden Capabilities |
|---|---|---|---|---|

## 4. Protected Resource Inventory

| Resource | Operation | Allowed Roles | Authorization Rule | Audit Required |
|---|---|---|---|---|

## 5. Authorization Decision Points

## 6. Authorization Enforcement Points

## 7. Admin Capability Boundaries

## 8. Audit Logging Requirements

## 9. Security Risks

## 10. Open Questions

## 11. Human Approval Required
```

---

### 13.6 `05_event_contracts.md`

Required if events, async workflows, webhooks, queues, pub/sub, notifications, or background jobs exist.

```markdown
# 05 Event Contracts

## 1. Status

## 2. Event / Async Design Principles

## 3. Event Inventory

| Event ID | Event Name | Producer | Consumer | Trigger | Related Domain Event |
|---|---|---|---|---|---|

## 4. Event Details

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

## 5. Async Failure Handling

## 6. Open Questions

## 7. Human Approval Required
```

---

### 13.7 `05_architecture_decisions.md`

Required sections:

```markdown
# 05 Architecture Decisions

## 1. Status

## 2. Decision Table

| Decision ID | Title | Status | Recommendation | Requires Approval | Related Requirements |
|---|---|---|---|---|---|

## 3. Decision Records

### ADR-001 [[Decision Title]]
#### Status
- Proposed / Approved / Rejected / Superseded

#### Context

#### Options Considered

#### Recommendation

#### Consequences

#### Risks

#### Related Requirements

#### Related Domain Concepts

#### Human Approval Needed
```

Only mark a decision as `Approved` when explicit human approval exists.

---

### 13.8 `05_architecture_traceability_matrix.md`

Required sections:

```markdown
# 05 Architecture Traceability Matrix

## 1. Status

## 2. Traceability Summary

## 3. Requirement to Architecture Mapping

| Requirement ID | Acceptance Criteria | Domain Concept | Architecture Component | Contract | Data Design Implication | Test Implication |
|---|---|---|---|---|---|---|

## 4. Domain to Architecture Mapping

| Domain Concept / Invariant / Event | Architecture Component | Contract / Policy | Notes |
|---|---|---|---|

## 5. Traceability Gaps

## 6. Human Approval Required
```

---

### 13.9 `result.md`

Required sections:

```markdown
# Result: 05 Architecture & Technical Contracts

## 1. Task Summary

## 2. Inputs Used

## 3. Outputs Created or Updated

## 4. Approved Decisions Used

## 5. Architecture Summary

## 6. New Decision Candidates

## 7. Working Assumptions

## 8. Open Questions

## 9. Risks and Constraints

## 10. Rejected or Superseded Options

## 11. Traceability Updates

## 12. N/A Items

## 13. Stage 6 Data Design Handoff

## 14. Validation Checklist Result

## 15. Human Approval Required

## 16. Recommended Next Step
```

---

## 14. Traceability Requirements

The generated reusable `SKILL.md` must preserve or improve these links:

```text
Goal
→ Requirement
→ Acceptance Criteria
→ Domain Concept / Invariant / Event
→ Architecture Component / Module
→ API Contract / Integration Contract / Event Contract
→ Data Design Implication
→ Test Strategy Implication
```

Use stable IDs.

Recommended ID conventions:

```text
Architecture components: ARC-001, ARC-002
Modules: MOD-001, MOD-002
API contracts: API-001, API-002
Integration contracts: INT-001, INT-002
Auth rules: AUTHZ-001, AUTHZ-002
Event contracts: EVT-001, EVT-002
Architecture decisions: ADR-001, ADR-002
Architecture risks: ARISK-001, ARISK-002
Open questions: AQ-001, AQ-002
```

Traceability rules:

```text
- Do not break existing requirement IDs.
- Do not rename domain concept IDs without explanation.
- Link every major architecture component to at least one requirement, domain concept, risk, or operational constraint.
- Link every API/integration/event contract to at least one requirement or domain workflow.
- If a component or contract has no traceable source, mark it as a proposed addition and require human approval.
- If a requirement has no architecture support, record it as a traceability gap.
```

---

## 15. Stage-Specific Validation Checklist

The generated reusable `SKILL.md` must include this checklist.

```text
[ ] artifact_manifest.yml was checked if available.
[ ] context_packet.md was checked.
[ ] DECISIONS.md and APPROVAL_LOG.md were checked if available.
[ ] USER_DIRECTIVES.md was checked if present.
[ ] Required Stage 1, 2, 3, and 4 artifacts were checked.
[ ] Only approved artifacts were used as source of truth unless exploratory work was explicitly requested.
[ ] Missing, draft, superseded, rejected, or conflicting inputs were reported.
[ ] Architecture drivers were extracted from approved inputs.
[ ] System boundary was defined.
[ ] Module boundaries were defined.
[ ] API contracts were created or marked N/A.
[ ] Integration contracts were created or marked N/A.
[ ] Authn/authz model was created or marked N/A.
[ ] Event contracts were created or marked N/A.
[ ] Security/privacy architecture concerns were addressed or marked N/A with reason.
[ ] Cross-cutting policies were addressed.
[ ] Architecture decisions were recorded as proposed unless explicitly approved.
[ ] Rejected options were not revived.
[ ] Traceability matrix was created or updated.
[ ] Data Design handoff was prepared.
[ ] Assumptions, open questions, risks, and recommendations were separated.
[ ] Human approval gate was prepared.
```

---

## 16. Stage-Specific Human Approval Gate

Stage 5 must end with a human approval gate.

Required approval items:

```markdown
## Human Approval Required

### Decisions to Approve
- Architecture style and direction
- Major technical choices
- Frontend/backend/service boundary
- Module boundaries
- API contracts, if applicable
- Integration contracts, if applicable
- Authentication and authorization model, if applicable
- Event/async contracts, if applicable
- Security/privacy architecture direction, if applicable
- Operational architecture direction, if applicable

### Assumptions to Confirm
- Technology stack assumptions
- Deployment/hosting assumptions
- Integration availability assumptions
- Performance/scalability assumptions
- Auth provider assumptions
- Data ownership assumptions
- Observability/logging assumptions

### Open Questions to Resolve
- Architecture questions that affect Stage 6 Data Design
- Contract questions that affect Stage 8 Test Strategy
- Security/privacy questions that affect implementation safety
- Operational questions that affect deployment or release

### Risks to Review
- Architecture complexity risks
- Security/privacy risks
- Data consistency risks
- Integration reliability risks
- Vendor lock-in risks
- Maintainability risks
- Testability risks

### Artifacts Ready for Review
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/05_architecture/05_module_boundaries.md
- /workflow/05_architecture/05_architecture_decisions.md
- /workflow/05_architecture/05_architecture_traceability_matrix.md
- /workflow/05_architecture/result.md
- Conditional artifacts created for this project

### Recommended Next Step
- Human reviews Stage 5 artifacts.
- After explicit approval, proceed to Stage 6 Data Design.
```

The Agent must not claim that Stage 5 is approved unless the human explicitly approves it.

---

## 17. Next Context Packet Rules

The generated reusable `SKILL.md` must update or prepare:

```text
/workflow/context/context_packet.md
```

The update must be concise and must prepare Stage 6 Data Design.

Required sections:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 05_architecture_contracts
- Completed stages:
- Next recommended stage: 06_data_design

## 2. Approved Decisions
- Only human-approved decisions relevant to Stage 6.

## 3. Working Assumptions
- Architecture assumptions that Stage 6 must be aware of.

## 4. Open Questions
- Questions affecting data design, security rules, schema, query patterns, or migration.

## 5. Rejected / Superseded Options
- Architecture or technology options not to revive unless reopened.

## 6. Constraints That Must Not Be Violated
- Technology constraints
- Security constraints
- Privacy constraints
- Scope constraints
- Operational constraints

## 7. Key Context for Next Stage
- Architecture style
- Module boundaries
- Contract boundaries
- Data ownership implications
- Auth/access implications
- Integration implications
- Event/async implications
- Audit/logging implications
- Consistency/transaction implications

## 8. Required Inputs for Next Stage
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/05_architecture/05_module_boundaries.md
- /workflow/05_architecture/05_architecture_decisions.md
- /workflow/05_architecture/05_architecture_traceability_matrix.md
- Conditional Stage 5 artifacts that were created and approved
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/04_domain/04_domain_model.md
- /workflow/04_domain/04_business_rules_invariants.md

## 9. Do Not Do
- Do not design schema from unapproved architecture.
- Do not ignore auth/access rules when designing data.
- Do not treat architecture recommendations as approved decisions.
- Do not use internal sub-skill outputs as source of truth.
```

Important rule:

```text
context_packet.md is a navigation layer, not the sole source of truth.
```

---

## 18. Stage-Specific Do Not Do

The generated reusable `SKILL.md` must include these Stage 5 anti-patterns.

```text
Do not implement code.
Do not design detailed database schema.
Do not create migration scripts.
Do not create task cards.
Do not write implementation prompts.
Do not treat a recommended architecture as approved.
Do not silently choose a technology stack if it conflicts with approved decisions.
Do not ignore role/permission requirements.
Do not defer all security/privacy architecture to final review.
Do not create API contracts that are not linked to requirements or domain workflows.
Do not create modules that have no traceable responsibility.
Do not read all previous artifacts by default.
Do not rely on prompt history.
Do not use rejected architecture options unless explicitly reopened.
Do not make Stage 6 depend on unapproved architecture drafts.
Do not collapse domain model and database design into architecture.
```

---

## 19. Specialization Hooks

The generated reusable `SKILL.md` must allow project-type specialization addenda.

### web_saas

May add:

```text
- browser/client-server boundary
- authentication provider integration
- tenant/account boundary
- API versioning
- rate limiting
- audit logging
- deployment/runtime assumptions
```

### internal_tool

May add:

```text
- operator workflow boundaries
- admin permissions
- organizational data access rules
- manual process integration
- audit or approval workflow
```

### mobile_app

May add:

```text
- offline/sync architecture
- device permission boundaries
- local storage boundary
- push notification contracts
- platform release constraints
```

### ai_data_product

May add:

```text
- dataset ingestion boundary
- model service boundary
- inference/evaluation contract
- human review workflow
- reproducibility and experiment tracking architecture
- model output risk controls
```

### regulated_security_sensitive

May add:

```text
- threat model interface
- audit trail architecture
- data minimization architecture
- privacy impact constraints
- stronger release blockers
- stronger approval logging
```

### brownfield_legacy

May add:

```text
- existing architecture review
- migration strategy boundary
- compatibility constraints
- strangler or adapter pattern considerations
- regression and rollback architecture
```

Specialization addenda must not replace the Stage 5 template.

---

## 20. Tool Wrapper Hooks

Tool-specific wrappers may define:

```text
- where the generated SKILL.md is stored
- how the Agent is invoked
- file creation conventions
- sandbox or permission rules
- review UI conventions
- artifact save behavior
```

Tool wrappers must not define:

```text
- architecture decisions
- domain model decisions
- data design decisions
- requirements
- API semantics
- security policy decisions
```

---

## 21. Acceptance Criteria for the Generated Reusable SKILL.md

A reusable `/skills/05_architecture_contracts/SKILL.md` generated from this template is acceptable only if:

```text
[ ] It follows the core skill template.
[ ] It identifies Stage 5 as Architecture & Technical Contracts.
[ ] It defines Always Read inputs.
[ ] It defines Read If Applicable inputs.
[ ] It defines Do Not Read By Default.
[ ] It defines missing input handling.
[ ] It checks USER_DIRECTIVES.md.
[ ] It checks artifact_manifest.yml.
[ ] It creates or updates all mandatory Stage 5 artifacts.
[ ] It creates conditional artifacts or records N/A rationale.
[ ] It defines required sections for each artifact.
[ ] It preserves requirement → domain → architecture traceability.
[ ] It prepares Stage 6 Data Design handoff.
[ ] It separates approved decisions, decision candidates, assumptions, open questions, risks, and recommendations.
[ ] It does not update DECISIONS.md without explicit human approval.
[ ] It includes a human approval gate.
[ ] It is context-reset tolerant.
[ ] It contains no project-specific architecture choices.
[ ] It does not mix tool-specific wrapper rules into architecture reasoning.
```

---

## 22. Recommended File Name

Save this template as:

```text
/workflow_templates/stage_templates/05_architecture_skill_template.md
```

Use it later to generate:

```text
/skills/05_architecture_contracts/SKILL.md
```
