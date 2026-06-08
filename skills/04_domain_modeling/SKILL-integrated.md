---
name: 04_domain_modeling
description: Use after Stage 3 to create a reusable DDD-oriented domain model from approved requirements and acceptance criteria, preserving domain language, concepts, rules, invariants, events, bounded contexts, traceability, and Stage 5 architecture handoff context.
stage: 04 Domain Modeling / DDD
version: 1.0.0
status: draft
primary_output: /workflow/04_domain/result.md
requires_human_approval: true
---

# 04 Domain Modeling / DDD SKILL

## 1. Purpose

Model the domain before architecture, data design, API design, UI design, implementation, or testing commands.

This SKILL converts approved goals, stakeholders, requirements, acceptance criteria, and relevant risk constraints into Stage 4 domain artifacts covering:

- ubiquitous language;
- domain concepts, entities, value objects, services, policies, and external actors;
- aggregates and consistency boundaries;
- business rules, invariants, state transitions, and lifecycle rules;
- domain events;
- bounded contexts and context relationships;
- traceability from requirements to domain model elements;
- concise handoff context for Stage 5 Architecture & Technical Contracts.

DDD here means domain language, meaning, rules, and boundaries. It does not mean database table extraction.

## 2. Core Question

What domain language, concepts, rules, consistency boundaries, events, and bounded contexts must the system preserve so that later architecture, data design, testing, and implementation remain aligned with the approved requirements?

## 3. Operating Rules

The agent is a structured development assistant, not the final decision-maker.

Maintain these distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```

Only explicit human approval creates an approved decision. Do not update `/workflow/context/DECISIONS.md` unless explicit approval exists.

## 4. When to Use

Use this SKILL after Stage 3 has produced requirements and acceptance criteria.

Use it when the project has domain terminology, workflows, roles, permissions, policies, approvals, scoring, scheduling, payments, lifecycle states, data governance, external systems, audit needs, or other domain rules that must be preserved.

For a small prototype, create lightweight artifacts but still record terminology, assumptions, open questions, N/A records, and traceability gaps.

## 5. When Not to Use

Do not use this SKILL to:

- design database tables;
- choose architecture style;
- design API endpoints;
- design UI screens;
- create implementation tasks;
- write test commands;
- implement code;
- invent requirements;
- approve product scope;
- treat agent-generated domain proposals as final decisions.

## 6. Input Precedence

When inputs conflict, use this order:

```text
1. Current explicit user instruction
2. /workflow/04_domain/USER_DIRECTIVES.md
3. /workflow/context/APPROVAL_LOG.md and /workflow/context/DECISIONS.md
4. /workflow/context/artifact_manifest.yml
5. /workflow/context/context_packet.md
6. Approved stage artifacts
7. Working assumptions
8. Agent inference
```

Conflict rule: report the conflict, identify sources, explain impact, and stop for human decision if it affects scope, role semantics, security, privacy, domain boundaries, architecture handoff, or approval status.

## 7. Required Inputs

### 7.1 Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/01_goal/01_service_goal.md
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
```

### 7.2 Read If Applicable

```text
/workflow/00_intake/00_project_intake.md
- if project type, fixed constraints, or non-changeable areas affect domain modeling

/workflow/00_intake/00_existing_context_review.md
- if brownfield, legacy, migration, extension, or compatibility constraints exist

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if roles, permissions, sensitive data, compliance, audit, security, or privacy affect domain rules

/workflow/03_requirements/03_traceability_matrix.md
- if Stage 3 produced it

/workflow/context/APPROVAL_LOG.md
- if approval status is ambiguous

/workflow/04_domain/USER_DIRECTIVES.md
- if present

/workflow/04_domain/review_notes.md
- if revising a prior Stage 4 draft

/workflow_templates/specializations/*.md
- if project profile activates specialization rules
```

### 7.3 Do Not Read By Default

```text
- implementation source code, except for brownfield domain extraction
- database schemas, except as supporting evidence for existing-system terminology
- downstream architecture, API, or data design drafts
- full historical agent logs
- superseded or rejected artifacts
- unrelated draft artifacts
```

## 8. USER_DIRECTIVES.md Handling

If `/workflow/04_domain/USER_DIRECTIVES.md` exists, read it before execution.

Classify each directive as approval, correction, preference, rejection, scope change, constraint, question, or new input.

Rules:

- Apply user directives before agent assumptions.
- Do not treat every directive as a globally approved decision.
- Report conflicts with approved decisions.
- Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

## 9. Input Preflight

Before drafting outputs, verify:

```text
[ ] This SKILL.md was read.
[ ] artifact_manifest.yml was checked if available.
[ ] context_packet.md was checked if available.
[ ] DECISIONS.md was checked if available.
[ ] ASSUMPTIONS.md, OPEN_QUESTIONS.md, REJECTED_OPTIONS.md, and TRACEABILITY_MATRIX.md were checked if available.
[ ] USER_DIRECTIVES.md was checked if present.
[ ] Always Read inputs were identified.
[ ] Conditional inputs were activated when applicable.
[ ] Required inputs exist or missing inputs are recorded.
[ ] Source artifacts are approved or clearly marked as draft.
[ ] Superseded or rejected artifacts are not used as current truth.
[ ] Missing, ambiguous, or conflicting information is reported.
```

Required boundary statement:

```text
This stage models domain meaning and rules. It does not design database tables, API endpoints, UI screens, architecture, or implementation tasks.
```

## 10. Missing Input Handling

Blocking if missing or unapproved:

- service goal;
- requirements;
- acceptance criteria;
- current artifact status or approval information;
- stakeholder roles when role semantics drive the domain.

Non-blocking with explicit assumptions:

- detailed privacy/risk screening;
- Stage 3 traceability matrix;
- brownfield context for greenfield projects;
- specialization addendum that does not materially change Stage 4.

Record missing inputs in `/workflow/04_domain/result.md`:

```markdown
## Missing Information

| Missing Input | Blocking? | Why It Matters | Safe Assumption | Human Decision Needed |
|---|---:|---|---|---|
```

If a blocker prevents safe completion, produce a partial `result.md` with a Blocker Report.

## 11. Execution Procedure

### Step 1. Confirm Stage Boundary

Restate current stage, approved inputs, draft inputs, known conflicts, and exclusions.

### Step 2. Build Ubiquitous Language

Extract domain terms from goals, stakeholders, requirements, and acceptance criteria.

For each important term, define:

```text
TERM ID | Preferred Term | Definition | Source Requirement / Stakeholder | Synonyms / Deprecated Terms | Ambiguity / Notes
```

Flag terms that must be preserved in APIs, UI, tests, and code.

### Step 3. Identify Domain Concepts

Classify concepts as actor/role, entity, value object, aggregate root/member, domain service, policy/rule, workflow/process, state, domain event, external system, or unclear concept.

Do not force every noun into entity/value-object form.

### Step 4. Distinguish Entities and Value Objects

For each candidate, decide by domain meaning:

- whether identity matters over time;
- whether equality is value-based;
- whether lifecycle matters;
- what domain validation rules apply;
- whether uncertainty remains.

Avoid database-driven attributes unless they are true domain identities.

### Step 5. Define Aggregates and Consistency Boundaries

For each aggregate candidate:

```text
AGG ID | Root | Members | Protected Invariants | Commands / Operations | Consistency Boundary | Cross-Aggregate References | Linked Requirements
```

Treat aggregates as consistency boundaries, not data containers.

### Step 6. Define Business Rules and Invariants

For each rule or invariant:

```text
BR/INV ID | Rule or Invariant | Applies To | Linked Requirement | Acceptance Criteria | Invalid State Prevented | Future Test Target | Notes
```

Record unresolved details as open questions.

### Step 7. Define State Transitions

For lifecycle-bearing concepts:

```text
ST ID | Concept | From State | To State | Trigger | Guard / Precondition | Invalid Transitions | Linked Acceptance Criteria | Future Scenario Test Target
```

If not applicable, record N/A rationale for `04_state_lifecycle.md`.

### Step 8. Define Domain Events

For each business-significant event:

```text
EVT ID | Past-Tense Event Name | Source Concept / Aggregate | Trigger | Why It Matters | Interested Contexts / Actors | Linked Requirement
```

Reject UI-only or technical notifications as domain events.

### Step 9. Define Bounded Contexts

For each context:

```text
BC ID | Name | Purpose | Owned Language | Owned Concepts | Inbound / Outbound Relationships | Translation / Contract Need | Linked Requirements
```

If one context is enough, record single-context rationale. If context splits require approval, record them as decision candidates.

### Step 10. Update Traceability

Create or update:

```text
Requirement → Acceptance Criteria → Domain Term / Concept / Rule / Invariant / Event / Context
```

Record gaps when a requirement, concept, acceptance criterion, rule, role, or permission cannot be mapped clearly.

### Step 11. Prepare Stage 5 Handoff

Summarize what Stage 5 must preserve:

- bounded contexts that may influence module boundaries;
- aggregates that may influence transaction boundaries;
- invariants that need enforcement points;
- domain events that may influence integration design;
- role/permission concepts that affect authorization;
- terms that should appear consistently in APIs, UI, tests, and code;
- unresolved issues that block architecture decisions.

## 12. Output Artifacts

### 12.1 Mandatory Artifacts

Create or update:

```text
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_domain_traceability_matrix.md
/workflow/04_domain/result.md
/workflow/context/context_packet.md
```

### 12.2 Conditional Artifacts

Create only when applicable:

```text
/workflow/04_domain/04_state_lifecycle.md
- if lifecycle-bearing concepts or meaningful state transitions exist

/workflow/04_domain/04_context_map.md
- if multiple contexts, external contexts, or brownfield context relationships exist

/workflow/04_domain/04_domain_risk_notes.md
- if security, privacy, compliance, audit, sensitive data, or model risk affects domain rules

/workflow/04_domain/04_domain_model_diagrams.md
- if diagrams clarify aggregates, contexts, or state transitions

/workflow/04_domain/04_domain_open_questions.md
- if domain open questions are substantial enough to need a stage-local file
```

### 12.3 N/A Record

If a conditional artifact is skipped, record in `result.md`:

```markdown
## Conditional Artifacts Not Created

| Artifact | Why Not Applicable | Revisit If |
|---|---|---|
```

## 13. Required Artifact Sections

Every artifact must include a `Status` section with one of: `Draft`, `Needs Review`, or `Approved`.

### `04_ubiquitous_language.md`

```text
1. Status
2. Language Scope
3. Preferred Domain Terms
4. Synonyms and Deprecated Terms
5. Ambiguous or Conflicting Terms
6. Terms to Preserve in Later Stages
```

### `04_domain_model.md`

```text
1. Status
2. Domain Overview
3. Core Domain Concepts
4. Entities
5. Value Objects
6. Aggregates
7. Domain Services / Policies
8. External Domain Actors or Systems
9. Modeling Uncertainties
```

### `04_business_rules_invariants.md`

```text
1. Status
2. Business Rules
3. Invariants
4. State Transition Rules
5. Rule Conflicts or Gaps
```

### `04_domain_events.md`

```text
1. Status
2. Domain Events
3. Event Ordering or Causality Notes
4. Events Rejected as Technical or UI Events
5. Event Open Questions
```

### `04_bounded_contexts.md`

```text
1. Status
2. Context Strategy Summary
3. Bounded Contexts
4. Context Relationships
5. Single-Context Rationale, if Applicable
6. Context Split Candidates Requiring Approval
```

### `04_domain_traceability_matrix.md`

```text
1. Status
2. Requirement to Domain Links
3. Domain to Future Stage Links
4. Traceability Gaps
```

### `result.md`

```text
1. Task Summary
2. Inputs Used
3. Outputs Created or Updated
4. Missing Information
5. Domain Modeling Summary
6. Key Domain Findings
7. Decision Candidates
8. Working Assumptions
9. Open Questions
10. Risks and Constraints
11. Rejected or Superseded Options
12. Traceability Updates
13. Conditional Artifacts Not Created
14. Human Approval Required
15. Recommended Next Step
```

## 14. ID Conventions

Preserve Stage 3 requirement and acceptance criteria IDs. Use stable Stage 4 IDs:

```text
TERM-001   Domain terms
DC-001     Domain concepts
ENT-001    Entities
VO-001     Value objects
AGG-001    Aggregates
BR-001     Business rules
INV-001    Invariants
ST-001     State transitions
EVT-001    Domain events
BC-001     Bounded contexts
TG-001     Traceability gaps
A-001      Assumptions
Q-001      Open questions
R-001      Risks
```

## 15. Traceability Rules

### Required Links

Create or preserve where applicable:

```text
Goal → Requirement → Acceptance Criteria → Domain Term
Requirement → Domain Concept
Requirement → Business Rule / Invariant
Acceptance Criteria → State Transition / Rule / Event
Domain Concept → Bounded Context
Aggregate → Invariant
Invariant → Future Unit or Scenario Test Target
State Transition → Future Scenario Test Target
Domain Event → Future Integration or Audit Test Target
Bounded Context → Future Module / Architecture Boundary Candidate
Aggregate → Future Transaction Boundary Candidate
```

### Prohibited Premature Links

Do not create as final decisions in Stage 4:

```text
Domain Concept → final Database Table
Aggregate → final Microservice
Domain Event → final Message Broker Topic
Bounded Context → final Deployment Unit
Entity → final ORM Model
```

Those belong to later stages.

## 16. Classification Rules

### Approved Decision

Use only when explicit human approval exists.

### Decision Candidate

Use for domain recommendations awaiting approval, including preferred terms, entity/value object classifications, aggregate roots, invariants, domain events, bounded contexts, and single-context rationale.

### Working Assumption

Use when progress requires a temporary belief. Keep assumptions out of `DECISIONS.md`.

### Open Question

Use when unresolved information may affect domain meaning, rules, boundaries, architecture, data design, tests, or implementation.

### Rejected Option

Record rejected or superseded terms, concepts, events, rules, aggregate boundaries, or context splits in `REJECTED_OPTIONS.md` when applicable. Do not revive them unless explicitly reopened.

### Risk

Record risks affecting domain correctness, security/privacy domain rules, auditability, authorization semantics, or Stage 5 architecture decisions.

## 17. Context Packet Update Rules

Update `/workflow/context/context_packet.md` for Stage 5. Keep it concise; do not copy entire Stage 4 artifacts.

Required sections:

```text
1. Current Project State
2. Approved Decisions
3. Working Assumptions
4. Open Questions
5. Rejected / Superseded Options
6. Constraints That Must Not Be Violated
7. Key Context for Next Stage
8. Required Inputs for Next Stage
9. Do Not Do
```

Include Stage 5 handoff notes for:

```text
- bounded contexts
- aggregates and transaction-boundary implications
- invariants and enforcement implications
- domain events and integration/audit implications
- role/permission domain concepts
- terms to preserve in APIs, UI, tests, and code
- unresolved architecture blockers
```

List these required Stage 5 inputs:

```text
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_domain_traceability_matrix.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Also update, when applicable:

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Do not update `/workflow/context/DECISIONS.md` without explicit approval.

## 18. Specialization Hooks

Specialization addenda may add inputs, questions, risks, or conditional artifacts, but must not replace Stage 4 rules or change the official artifact contract unless explicitly approved.

Suggested hooks:

```text
web_saas: account, tenant, organization, workspace, role, permission, invitation, subscription, billing, audit
internal_tool: operator workflows, approval chains, exception handling, organizational role language
mobile_app: device/user/session concepts, offline state, synchronization only when domain-relevant
ai_data_product: dataset, sample, label, annotation, model output, review, evaluation, confidence, explanation, human override, provenance
regulated_security_sensitive: consent, retention, access grant, audit event, policy, review, approval, risk status, compliance evidence
brownfield_legacy: current terminology extraction, implementation-name vs domain-name distinction, compatibility constraints, migration-safe context candidates
```

## 19. Validation Checklist

Before human review, verify:

```text
[ ] Inputs are approved or clearly labeled as draft.
[ ] Missing, draft, superseded, rejected, and conflicting inputs are reported.
[ ] Domain language is explicit and consistent.
[ ] Ambiguous terms are flagged.
[ ] Entities and value objects are distinguished by domain meaning.
[ ] Aggregates are consistency boundaries.
[ ] Invariants link to requirements or acceptance criteria.
[ ] State transitions exist where lifecycle matters, or N/A is recorded.
[ ] Domain events are business-significant, not merely technical notifications.
[ ] Bounded contexts are defined, or single-context rationale is recorded.
[ ] Security/privacy/audit/permission domain rules are not ignored.
[ ] Major requirements link to domain terms, concepts, rules, events, or contexts.
[ ] Traceability gaps are recorded.
[ ] Outputs are not database/API/UI/architecture documents in disguise.
[ ] Decision candidates, assumptions, open questions, risks, and rejected options are separated.
[ ] Stage 5 handoff is concise and actionable.
[ ] Human approval gate is present.
```

## 20. Human Approval Gate

End `result.md` with:

```markdown
## Human Approval Required

### Decisions to Approve
- Preferred ubiquitous language terms
- Entity and value object classifications
- Aggregate roots and aggregate boundaries
- Business rules and invariants
- State lifecycle model, if applicable
- Domain events
- Bounded contexts and context relationships
- Single-context rationale, if applicable

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Risks to Review
- ...

### Artifacts Ready for Review
- /workflow/04_domain/04_ubiquitous_language.md
- /workflow/04_domain/04_domain_model.md
- /workflow/04_domain/04_bounded_contexts.md
- /workflow/04_domain/04_business_rules_invariants.md
- /workflow/04_domain/04_domain_events.md
- /workflow/04_domain/04_domain_traceability_matrix.md
- /workflow/04_domain/result.md

### Recommended Next Step
- Review and approve or revise Stage 4 artifacts before running Stage 5 Architecture & Technical Contracts.
```

Stage 5 must not treat Stage 4 artifacts as source of truth until approved.

## 21. Failure Handling

If the SKILL cannot complete safely, produce partial `/workflow/04_domain/result.md` with:

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

Typical blockers:

```text
- requirements are missing or contradictory
- acceptance criteria are too vague to infer business rules
- stakeholder roles are missing but role semantics drive the domain
- approved scope is unclear
- privacy/security constraints conflict with domain operations
- existing-system terminology conflicts with approved terminology
- current source artifact cannot be identified
```

## 22. Do Not Do

```text
- Do not design database tables first.
- Do not convert every noun into an entity.
- Do not treat value objects as entities merely because they may be stored later.
- Do not treat aggregates as data containers.
- Do not equate bounded contexts with microservices.
- Do not equate domain events with message broker topics.
- Do not create final API contracts.
- Do not create final database schema.
- Do not choose architecture style.
- Do not invent requirements.
- Do not treat assumptions as approved domain decisions.
- Do not revive rejected terms, concepts, or boundaries unless reopened.
- Do not ignore security, privacy, audit, or permission-related domain rules.
- Do not update DECISIONS.md without explicit human approval.
- Do not proceed to Stage 5 as if draft artifacts were approved.
- Do not use context_packet.md as the only source of truth.
- Do not read all historical artifacts by default.
- Do not claim approval or finality without explicit human approval.
```

## 23. Split Recommendation If Execution Becomes Too Large

This file is designed as a compact single-stage SKILL. If execution becomes unstable, split Stage 4 internally while preserving the same official Stage 4 artifacts.

Recommended nested Stage Facade structure:

```text
/skills/04_domain_modeling/
  SKILL.md
  README.md                         # separate file, not created by this SKILL
  artifact_contract.yml             # separate file, not created by this SKILL

  /04a_ubiquitous_language/SKILL.md
  /04b_domain_concepts_entities_values/SKILL.md
  /04c_aggregates_rules_lifecycle/SKILL.md
  /04d_events_bounded_contexts/SKILL.md
  /04e_domain_modeling_finalizer/SKILL.md
```

Recommended responsibilities:

```text
04a_ubiquitous_language
- Produces or updates /workflow/04_domain/04_ubiquitous_language.md.

04b_domain_concepts_entities_values
- Produces or updates core parts of /workflow/04_domain/04_domain_model.md.

04c_aggregates_rules_lifecycle
- Produces or updates aggregate, invariant, rule, and lifecycle sections.
- Produces optional /workflow/04_domain/04_state_lifecycle.md.

04d_events_bounded_contexts
- Produces or updates /workflow/04_domain/04_domain_events.md and /workflow/04_domain/04_bounded_contexts.md.
- Produces optional /workflow/04_domain/04_context_map.md.

04e_domain_modeling_finalizer
- Consolidates official artifacts.
- Updates /workflow/04_domain/04_domain_traceability_matrix.md.
- Updates /workflow/04_domain/result.md.
- Updates /workflow/context/context_packet.md for Stage 5.
- Prepares the human approval gate.
```

Downstream Stage 5 must depend only on approved official Stage 4 artifacts, not internal sub-skill paths, prompt history, or unapproved draft outputs.

## 24. Completion Criteria

This SKILL execution is complete only when:

```text
[ ] Mandatory Stage 4 artifacts are created or safely updated.
[ ] Conditional artifacts are created or N/A is recorded.
[ ] Traceability links and gaps are recorded.
[ ] Context packet is prepared for Stage 5.
[ ] ASSUMPTIONS.md, OPEN_QUESTIONS.md, REJECTED_OPTIONS.md, and TRACEABILITY_MATRIX.md are updated when applicable.
[ ] DECISIONS.md is not updated unless explicit human approval exists.
[ ] Human approval gate is presented.
[ ] Stage 5 is clearly instructed not to rely on draft Stage 4 artifacts.
```
