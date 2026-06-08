# 04_domain_modeling Skill Template

> Type: Stage-Specific SKILL Template  
> Target executable SKILL: `/skills/04_domain_modeling/SKILL.md`  
> Target project stage folder: `/workflow/04_domain`  
> This template is used to create a reusable executable `SKILL.md`. It is not itself the executable SKILL, README, artifact contract, or project artifact.

---

## 0. Scope

This template defines the Stage 4 extension for the Manual Agentic Coding Workflow.

It must be combined with the separate Core Skill Template when creating the executable `SKILL.md`.

This template defines Stage 4-specific:

- purpose and core question;
- input contract;
- DDD/domain modeling procedure;
- official artifacts;
- required artifact sections;
- traceability rules;
- approval gate;
- context handoff to Stage 5.

It must not include tool-specific commands, project-specific domain content, database schema design, API design, architecture decisions, implementation tasks, or test execution commands.

---

## 1. Stage Identity

```yaml
stage_number: "04"
stage_name: "domain_modeling"
stage_title: "Domain Modeling / DDD"
skill_folder: "/skills/04_domain_modeling"
skill_file: "/skills/04_domain_modeling/SKILL.md"
project_stage_folder: "/workflow/04_domain"
previous_stage: "03_requirements_acceptance"
next_stage: "05_architecture_contracts"
requires_human_approval: true
```

---

## 2. Stage Purpose

Model the domain before architecture, data design, API design, UI design, or implementation.

Stage 4 converts approved goals, stakeholders, requirements, acceptance criteria, and relevant risk constraints into a domain model that preserves:

- ubiquitous language;
- core domain concepts;
- entities and value objects;
- aggregates and consistency boundaries;
- business rules and invariants;
- state transitions and lifecycle rules;
- domain events;
- bounded contexts and context relationships;
- traceability from requirements to domain concepts and forward to architecture, data design, and tests.

DDD in this workflow is about domain meaning, business rules, and boundaries. It is not database table extraction.

---

## 3. Core Question

> What domain language, concepts, rules, consistency boundaries, events, and bounded contexts must the system preserve so that later architecture, data design, testing, and implementation remain aligned with the approved requirements?

Sub-questions:

1. Which terms must be used consistently across artifacts, code, APIs, UI, and tests?
2. Which concepts are entities, value objects, aggregates, domain services, policies, events, states, or external actors?
3. Which business rules and invariants must always hold?
4. Which state transitions are valid, invalid, or unresolved?
5. Which domain events matter to workflows, audit, integration, or tests?
6. Which bounded contexts exist, and where do language/rule boundaries appear?
7. Which requirements cannot yet be mapped to domain concepts, rules, events, or contexts?

---

## 4. When to Use

Use this stage after Stage 3 has produced requirements and acceptance criteria.

Use it when the project has domain terminology, workflows, roles, policies, permissions, reviews, approvals, scoring, scheduling, payments, lifecycle states, data governance, external systems, or other business rules that must be preserved in implementation.

For a small prototype, produce a lightweight domain model but still record terminology, assumptions, open questions, and rule gaps.

---

## 5. When Not to Use

Do not use this stage to:

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

---

## 6. Input Contract

### 6.1 Always Read

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

### 6.2 Read If Applicable

```text
/workflow/00_intake/00_project_intake.md
- if project type, fixed constraints, or non-changeable areas affect domain modeling

/workflow/00_intake/00_existing_context_review.md
- if brownfield, legacy, migration, extension, or compatibility constraints exist

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if roles, permissions, sensitive data, compliance, audit, security, or privacy affect domain rules

/workflow/03_requirements/03_traceability_matrix.md
- if Stage 3 produced a traceability matrix

/workflow/context/APPROVAL_LOG.md
- if approval status is ambiguous

/workflow/04_domain/USER_DIRECTIVES.md
- if present; read before execution

/workflow/04_domain/review_notes.md
- if revising a prior Stage 4 draft

/workflow_templates/specializations/*.md
- if project profile activates a specialization addendum
```

### 6.3 Do Not Read By Default

```text
- implementation source code, except for brownfield domain extraction
- database schemas, except as supporting evidence for existing-system terminology
- downstream architecture, API, or data design drafts
- full historical agent logs
- superseded or rejected artifacts
- unrelated draft artifacts
```

### 6.4 Missing Input Handling

Blocking if missing or unapproved:

- service goal;
- requirements;
- acceptance criteria;
- current artifact status/approval information;
- stakeholder roles when role semantics drive the domain.

Non-blocking with explicit assumptions:

- detailed privacy/risk screening;
- Stage 3 traceability matrix;
- brownfield context for greenfield projects;
- specialization addendum that does not materially change Stage 4.

Record missing inputs in `result.md`:

```markdown
## Missing Information

| Missing Input | Blocking? | Why It Matters | Safe Assumption | Human Decision Needed |
|---|---:|---|---|---|
```

---

## 7. Stage-Specific Procedure

The executable SKILL must follow the core runtime procedure and add these Stage 4 steps.

### Step 1. Confirm Boundary

Restate the stage goal, approved inputs, artifact status, and exclusions.

Required statement:

```text
This stage models domain meaning and rules. It does not design database tables, API endpoints, UI screens, architecture, or implementation tasks.
```

### Step 2. Build Ubiquitous Language

Extract domain terms from goals, stakeholders, requirements, and acceptance criteria.

For each important term:

- define preferred term;
- define meaning;
- identify source requirement/stakeholder;
- identify synonyms or deprecated terms;
- flag ambiguity or conflicts.

### Step 3. Identify Domain Concepts

Classify concepts as appropriate:

- actor / role;
- entity;
- value object;
- aggregate root;
- aggregate member;
- domain service;
- policy / rule;
- workflow / process;
- state;
- domain event;
- external system;
- unclear concept.

Do not force every noun into entity/value-object form.

### Step 4. Distinguish Entities and Value Objects

For each candidate:

- decide whether identity matters over time;
- decide whether equality is value-based;
- describe lifecycle only when domain-relevant;
- capture validation rules at the domain level;
- avoid database-driven attributes unless they are true domain identities.

### Step 5. Define Aggregates and Consistency Boundaries

For each aggregate candidate:

- identify aggregate root;
- list members;
- define protected invariants;
- identify commands/operations that modify it;
- describe consistency expectations;
- record cross-aggregate references and eventual consistency assumptions.

Aggregates are consistency boundaries, not data containers.

### Step 6. Define Business Rules and Invariants

For each rule or invariant:

- assign stable ID;
- state it in domain language;
- link it to requirements and acceptance criteria;
- identify invalid state or prohibited action;
- identify future test target where possible;
- record unresolved details as open questions.

### Step 7. Define State Transitions

For lifecycle-bearing concepts:

- list valid states;
- define allowed transitions;
- define triggers;
- define guards/preconditions;
- define invalid transitions;
- link transitions to acceptance criteria and future scenario tests.

### Step 8. Define Domain Events

For each event:

- use a past-tense business event name when appropriate;
- identify source concept or aggregate;
- define trigger and significance;
- identify interested contexts, actors, audit logs, integrations, or tests;
- reject UI-only or technical notifications as domain events.

### Step 9. Define Bounded Contexts

Identify one or more bounded contexts.

For each context:

- define purpose;
- define owned language;
- define owned concepts;
- define inbound/outbound relationships;
- identify translation or contract needs;
- record context split candidates requiring human approval.

If one context is enough, record single-context rationale.

### Step 10. Update Traceability

Create or update links:

```text
Requirement → Acceptance Criteria → Domain Term / Concept / Rule / Invariant / Event / Context
```

Record gaps when:

- a requirement has no domain concept;
- a concept has no linked requirement;
- an acceptance criterion has no rule, transition, or event;
- a rule lacks validation implications;
- a role/permission requirement lacks domain representation.

### Step 11. Prepare Stage 5 Handoff

Summarize what architecture must preserve:

- bounded contexts that may influence module boundaries;
- aggregates that may influence transaction boundaries;
- invariants that need enforcement points;
- domain events that may influence integration design;
- role/permission concepts that affect authorization;
- domain terms that should appear consistently in APIs, UI, tests, and code;
- unresolved issues that block architecture decisions.

---

## 8. Output Artifact Contract

### 8.1 Mandatory Artifacts

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

### 8.2 Conditional Artifacts

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

### 8.3 N/A Record

If a conditional artifact is skipped, record in `result.md`:

```markdown
## Conditional Artifacts Not Created

| Artifact | Why Not Applicable | Revisit If |
|---|---|---|
```

---

## 9. Required Output Structure

The executable SKILL should define concise structures for each artifact.

### `04_ubiquitous_language.md`

Required sections:

```text
1. Status
2. Language Scope
3. Preferred Domain Terms
4. Synonyms and Deprecated Terms
5. Ambiguous or Conflicting Terms
6. Terms to Preserve in Later Stages
```

Required table fields:

```text
Term ID | Preferred Term | Definition | Source Requirement / Stakeholder | Notes
```

### `04_domain_model.md`

Required sections:

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

Required table fields:

```text
Concept ID | Name | Type | Definition | Linked Requirements | Notes
Entity ID | Name | Identity | Lifecycle Summary | Linked Requirements | Notes
Value Object ID | Name | Value Equality / Validation | Linked Requirements | Notes
Aggregate ID | Root | Members | Protected Invariants | Consistency Boundary | Linked Requirements
```

### `04_business_rules_invariants.md`

Required sections:

```text
1. Status
2. Business Rules
3. Invariants
4. State Transition Rules
5. Rule Conflicts or Gaps
```

Required table fields:

```text
Rule ID | Rule | Applies To | Linked Requirement | Acceptance Criteria | Enforcement Notes
Invariant ID | Invariant | Protected By | Invalid State Prevented | Linked Requirement | Future Test Target
Transition ID | Concept | From State | To State | Trigger | Guard / Precondition | Invalid Transitions
```

### `04_domain_events.md`

Required sections:

```text
1. Status
2. Domain Events
3. Event Ordering or Causality Notes
4. Events Rejected as Technical or UI Events
5. Event Open Questions
```

Required table fields:

```text
Event ID | Event Name | Source Concept / Aggregate | Trigger | Why It Matters | Interested Contexts / Actors | Linked Requirement
```

### `04_bounded_contexts.md`

Required sections:

```text
1. Status
2. Context Strategy Summary
3. Bounded Contexts
4. Context Relationships
5. Single-Context Rationale, if Applicable
6. Context Split Candidates Requiring Approval
```

Required table fields:

```text
Context ID | Name | Purpose | Owned Language | Owned Concepts | Linked Requirements
Relationship ID | Upstream Context | Downstream Context | Relationship Type | Translation / Contract Need | Notes
```

### `04_domain_traceability_matrix.md`

Required sections:

```text
1. Status
2. Requirement to Domain Links
3. Domain to Future Stage Links
4. Traceability Gaps
```

Required table fields:

```text
Requirement ID | Acceptance Criteria IDs | Domain Terms | Concepts | Rules / Invariants | Events | Bounded Contexts | Gaps
Domain Item ID | Type | Architecture Implication | Data Design Implication | Test Implication | Notes
```

### `result.md`

Required sections:

```text
1. Task Summary
2. Inputs Used
3. Outputs Created or Updated
4. Domain Modeling Summary
5. Key Domain Findings
6. Decision Candidates
7. Working Assumptions
8. Open Questions
9. Risks and Constraints
10. Rejected or Superseded Options
11. Traceability Updates
12. Conditional Artifacts Not Created
13. Human Approval Required
14. Recommended Next Step
```

---

## 10. ID Conventions

Use stable IDs.

```text
Domain terms: TERM-001
Concepts: DC-001
Entities: ENT-001
Value objects: VO-001
Aggregates: AGG-001
Business rules: BR-001
Invariants: INV-001
State transitions: ST-001
Domain events: EVT-001
Bounded contexts: BC-001
Traceability gaps: TG-001
```

Preserve Stage 3 requirement and acceptance-criteria IDs.

---

## 11. Traceability Rules

Required links:

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

Prohibited premature links:

```text
Domain Concept → final Database Table
Aggregate → final Microservice
Domain Event → final Message Broker Topic
Bounded Context → final Deployment Unit
Entity → final ORM Model
```

These belong to later architecture, data design, or implementation stages.

---

## 12. Validation Checklist

Before human review, verify:

```text
[ ] Inputs are approved or clearly labeled as draft.
[ ] Domain language is explicit and consistent.
[ ] Ambiguous terms are flagged.
[ ] Entities and value objects are distinguished by domain meaning.
[ ] Aggregates are consistency boundaries.
[ ] Invariants link to requirements or acceptance criteria.
[ ] State transitions exist where lifecycle matters.
[ ] Domain events are business-significant, not merely technical notifications.
[ ] Bounded contexts are defined, or single-context rationale is recorded.
[ ] Security/privacy/audit/permission domain rules are not ignored.
[ ] Major requirements link to domain terms, concepts, rules, events, or contexts.
[ ] Traceability gaps are recorded.
[ ] Outputs are not database/API/UI/architecture documents in disguise.
[ ] Decision candidates, assumptions, open questions, and risks are separated.
[ ] Stage 5 handoff is concise and actionable.
[ ] Human approval gate is present.
```

---

## 13. Human Approval Gate

The executable SKILL must end with:

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

---

## 14. Context Packet Update Rules

Update `/workflow/context/context_packet.md` for Stage 5.

Include only minimal operational context. Do not copy entire Stage 4 artifacts.

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

Stage 5 handoff must include:

```text
- bounded contexts that may influence module boundaries
- aggregates that may influence transaction boundaries
- invariants that need enforcement points
- domain events that may influence integration design
- role/permission concepts that affect authorization
- terms that should be preserved in APIs, UI, tests, and code
- unresolved issues that block architecture decisions
```

Required Stage 5 inputs to list:

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

Do not update `/workflow/context/DECISIONS.md` without explicit human approval.

---

## 15. Specialization Hooks

Specialization addenda may add inputs, questions, risks, or conditional artifacts. They must not replace Stage 4 rules or change the official artifact contract unless explicitly approved.

Suggested hooks:

```text
web_saas:
- account, tenant, organization, workspace, role, permission, invitation, subscription, billing, audit concepts

internal_tool:
- operator workflows, approval chains, exception handling, organizational role language

mobile_app:
- device/user/session concepts, offline state, synchronization only when domain-relevant

ai_data_product:
- dataset, sample, label, annotation, model output, review, evaluation, confidence, explanation, human override, provenance

regulated_security_sensitive:
- consent, retention, access grant, audit event, policy, review, approval, risk status, compliance evidence

brownfield_legacy:
- current terminology extraction, implementation-name vs domain-name distinction, compatibility constraints, migration-safe context candidates
```

---

## 16. Failure Handling

If the SKILL cannot complete safely, produce partial `result.md` with:

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

---

## 17. Do Not Do

The executable SKILL must prohibit:

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
```

---

## 18. Split Recommendation If Executable SKILL Becomes Too Large

The stage template can remain one file. If the executable `SKILL.md` becomes too large or unreliable for agent execution, split Stage 4 into smaller reusable SKILLs while preserving the same official Stage 4 artifacts.

Recommended split:

```text
/skills/04a_ubiquitous_language/SKILL.md
- Produces or updates 04_ubiquitous_language.md.

/skills/04b_domain_concepts_entities_values/SKILL.md
- Produces or updates core parts of 04_domain_model.md.

/skills/04c_aggregates_rules_lifecycle/SKILL.md
- Produces or updates aggregate, invariant, rule, and lifecycle sections.
- Produces optional 04_state_lifecycle.md.

/skills/04d_events_bounded_contexts/SKILL.md
- Produces or updates 04_domain_events.md and 04_bounded_contexts.md.
- Produces optional 04_context_map.md.

/skills/04e_domain_modeling_finalizer/SKILL.md
- Consolidates official artifacts.
- Updates 04_domain_traceability_matrix.md, result.md, context_packet.md, and the human approval gate.
```

Downstream Stage 5 must depend only on approved official Stage 4 artifacts, not on the internal SKILL split.

---

## 19. Template Quality Checklist

```text
[ ] Extends the core template instead of replacing it.
[ ] Defines Stage 4 purpose and core question.
[ ] Defines Always Read, Read If Applicable, and Do Not Read By Default inputs.
[ ] Defines missing input handling.
[ ] Defines mandatory and conditional artifacts.
[ ] Requires N/A records for skipped conditional artifacts.
[ ] Defines required output structures.
[ ] Includes DDD-specific procedure steps.
[ ] Prevents domain modeling from becoming database/API/architecture design.
[ ] Defines traceability from requirements to domain elements.
[ ] Prepares Stage 5 handoff.
[ ] Separates decision candidates, assumptions, open questions, risks, and rejected options.
[ ] Requires human approval before downstream reliance.
[ ] Leaves project-type concerns to specialization addenda.
[ ] Leaves tool-specific behavior to wrappers.
[ ] Is context-reset tolerant.
```

---

## 20. Prompt to Generate Executable SKILL.md

```text
You are creating an executable reusable SKILL.md for Stage 04 Domain Modeling / DDD in a Manual Agentic Coding Workflow.

Use these source documents:
- /workflow_templates/core/core_skill_template.md
- /workflow_templates/stage_templates/04_domain_modeling_skill_template.md
- agentic-coding-workflow-concept-and-design.md
- skill-template-design-principles.md
- workflow_folder_structure_guide.md

Target output:
- /skills/04_domain_modeling/SKILL.md

Create a reusable SKILL.md that an agent can actually execute.

Rules:
1. Follow the core skill template.
2. Implement the Stage 4 template.
3. Do not include project-specific domain content.
4. Do not create README.md or artifact_contract.yml yet.
5. Do not execute the workflow stage.
6. Define required inputs, conditional inputs, output artifacts, required sections, procedure, traceability rules, context handoff, failure handling, and human approval gate.
7. Make the SKILL context-reset tolerant.
8. Keep the SKILL compact enough for agent execution.
9. If the SKILL becomes too large, propose the split structure from the template instead of creating an oversized file.
```
