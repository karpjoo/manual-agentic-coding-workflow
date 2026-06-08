---
name: 04b_domain_concepts_entities_values
description: Identify domain concepts, actors, entities, value objects, domain services, policies, identifiers, and key relationships from approved requirements and ubiquitous language.
stage: 04 Domain Modeling / DDD
parent_skill: /skills/04_domain_modeling/SKILL.md
subskill_id: 04b
subskill_order: 2
previous_subskill: /skills/04_domain_modeling/04a_ubiquitous_language/SKILL.md
next_subskill: /skills/04_domain_modeling/04c_aggregates_rules_lifecycle/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/04_domain/04_domain_model.md
requires_human_approval: true
external_visibility: internal
---

# 04b Domain Concepts, Entities, and Value Objects SKILL

## 1. Purpose

Create or update the core domain model artifact by identifying domain concepts and classifying them as appropriate.

This sub-skill focuses on:

- actors and roles;
- core domain concepts;
- entities;
- value objects;
- domain services;
- policies and rules as concept candidates;
- external domain actors or systems;
- important identifiers and relationships.

It does not define final aggregate boundaries, final invariants, final state transition tables, domain events, bounded contexts, database tables, API contracts, or architecture modules.

## 2. Core Question

Which domain concepts must the system preserve, and which of them have identity, value-based equality, policy behavior, or external-system meaning?

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
/workflow/01_goal/01_service_goal.md
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/04_domain/04_ubiquitous_language.md
```

### Read If Applicable

```text
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if roles, permissions, sensitive data, compliance, audit, security, or privacy affect concept classification

/workflow/03_requirements/03_traceability_matrix.md
- if Stage 3 produced it

/workflow/04_domain/USER_DIRECTIVES.md
- if present

/workflow/04_domain/review_notes.md
- if revising a prior Stage 4 draft

/workflow/00_intake/00_existing_context_review.md
- if brownfield or migration constraints affect terminology or concept identity
```

### Do Not Read By Default

```text
implementation source code, except for brownfield domain extraction
final database schema
architecture/API/data design drafts
full historical agent logs
superseded or rejected artifacts
```

## 4. Missing Input Handling

Blocking:

- missing or unusable `04_ubiquitous_language.md`;
- missing requirements or acceptance criteria;
- missing role/stakeholder artifact when role semantics affect domain concepts;
- unresolved term conflicts that make concept classification unsafe.

Non-blocking with explicit assumptions:

- incomplete risk/privacy screening when not concept-shaping;
- missing brownfield context for a greenfield project;
- incomplete Stage 3 traceability matrix.

Record gaps under `## Modeling Uncertainties` in `/workflow/04_domain/04_domain_model.md`.

## 5. Execution Procedure

### Step 1. Confirm Scope

State:

```text
This sub-skill identifies domain concepts and classifies entities/value objects. It does not finalize aggregate boundaries, database tables, API contracts, architecture modules, or implementation classes.
```

### Step 2. Extract Concept Candidates

Use the ubiquitous language and approved requirements to identify:

- actors / roles;
- core domain concepts;
- lifecycle-bearing concepts;
- value-like concepts;
- identifiers;
- policies and rules;
- workflows / processes;
- external systems;
- sensitive or security-relevant concepts;
- unclear concepts.

Do not convert every noun into a domain concept. Prefer concepts that affect requirements, rules, workflows, permissions, lifecycle, audit, validation, or tests.

### Step 3. Classify Concept Types

Allowed concept types:

```text
actor / role
entity candidate
value object candidate
aggregate root candidate
domain service candidate
policy / rule candidate
workflow / process
state candidate
domain event candidate
external system
unclear concept
```

Use `candidate` when classification is not yet approved or final.

### Step 4. Distinguish Entities and Value Objects

Classify as entity candidate when:

- continuity of identity matters over time;
- the concept can change while remaining the same domain thing;
- requirements refer to tracking, ownership, state, assignment, approval, audit, or lifecycle of the same thing;
- equality is not merely structural value equality.

Classify as value object candidate when:

- equality is based on values, not identity;
- the concept is replaceable rather than mutable identity-bearing;
- it expresses measurement, range, amount, label, address-like value, score-like value, rule parameter, or descriptive value;
- validation belongs to its value semantics.

Do not classify something as an entity merely because it may be stored in a database.

Do not classify something as a value object merely because it has no obvious UI page.

### Step 5. Identify Domain Identifiers

For identity-bearing concepts, identify domain identity separately from technical IDs.

Examples of identity questions:

- What makes this the same thing over time?
- Is the identifier assigned by the business, system, external system, or human?
- Is the identifier meaningful to users or only technical?
- Can the identifier change?
- Does identity differ across bounded contexts?

Do not design primary keys or database IDs.

### Step 6. Identify Relationships Without Database Modeling

Record domain relationships, not tables or joins.

For each relationship, capture:

- source concept;
- target concept;
- domain meaning;
- cardinality if it is domain-relevant;
- lifecycle dependency;
- permission or ownership implication;
- whether it may imply an aggregate or context boundary later.

### Step 7. Identify Domain Services and Policies

Use domain service candidate only when:

- behavior belongs to the domain but not naturally to a single entity or value object;
- behavior coordinates multiple concepts;
- the requirement describes a domain operation, policy, eligibility check, scoring, assignment, routing, or evaluation.

Use policy/rule candidate when:

- a rule may vary by organization, role, state, risk level, plan, workflow, or governance rule;
- a decision is made from domain conditions.

Do not turn application orchestration, UI logic, or infrastructure calls into domain services.

### Step 8. Prepare Handoff to 04c

Identify candidates that require aggregate/rule/lifecycle analysis:

- entity candidates with lifecycle or ownership;
- concepts modified together under invariants;
- relationships that imply consistency boundaries;
- policies that imply business rules;
- state-like terms from 04a;
- concept conflicts that affect aggregate boundaries.

## 6. Output Artifact

Create or update:

```text
/workflow/04_domain/04_domain_model.md
```

Status must be `Draft` unless explicit human approval exists.

Required structure:

```markdown
# 04 Domain Model

## 1. Status
- Status: Draft | Needs Review | Approved
- Source artifacts:
- Last updated:

## 2. Domain Overview

## 3. Core Domain Concepts
| Concept ID | Name | Type | Definition | Linked Requirements | Source Terms | Notes |
|---|---|---|---|---|---|---|

## 4. Actors and Roles
| Actor ID | Name | Domain Meaning | Permissions / Responsibilities | Linked Requirements | Notes |
|---|---|---|---|---|---|

## 5. Entities
| Entity ID | Name | Identity | Lifecycle Summary | Linked Requirements | Notes |
|---|---|---|---|---|---|

## 6. Value Objects
| Value Object ID | Name | Value Equality / Validation | Linked Requirements | Notes |
|---|---|---|---|---|

## 7. Domain Services / Policies
| Service / Policy ID | Name | Responsibility | Inputs / Outputs | Linked Requirements | Notes |
|---|---|---|---|---|---|

## 8. Relationships
| Relationship ID | Source Concept | Target Concept | Domain Meaning | Cardinality / Lifecycle Notes | Linked Requirements |
|---|---|---|---|---|---|

## 9. External Domain Actors or Systems
| External ID | Name | Domain Role | Interaction Meaning | Linked Requirements | Notes |
|---|---|---|---|---|---|

## 10. Aggregate / Rule / Lifecycle Candidates for 04c

## 11. Modeling Uncertainties

## 12. Open Questions
```

## 7. ID Conventions

Use stable IDs:

```text
DC-001        Domain concepts
ACT-001       Actors / roles
ENT-001       Entities
VO-001        Value objects
DSP-001       Domain services / policies
REL-001       Relationships
EXT-001       External systems / actors
```

Preserve existing IDs when revising.

## 8. Decision / Assumption / Open Question Rules

Decision candidates:

- entity vs value object classification;
- concept naming;
- concept boundaries;
- domain service or policy candidates.

Working assumptions:

- inferred identity semantics;
- inferred lifecycle relevance;
- inferred relationship cardinality when not specified.

Open questions:

- ambiguous concept identity;
- conflicting role semantics;
- unclear lifecycle ownership;
- unclear external system boundary;
- concept exists but no linked requirement.

Rejected options:

- classifications explicitly rejected by the user;
- terms or concepts superseded by approved terminology.

## 9. Validation Checklist

Before finishing, verify:

```text
[ ] Every major domain concept is traceable to approved requirements, stakeholders, or ubiquitous language.
[ ] Entities are classified by identity, not database storage.
[ ] Value objects are classified by value equality and validation semantics.
[ ] Domain services are not application services or infrastructure wrappers.
[ ] Relationships express domain meaning, not database joins.
[ ] Role, permission, audit, privacy, and security-sensitive concepts are not ignored.
[ ] Classification uncertainty is explicit.
[ ] No aggregate, database, API, architecture, or implementation decision was finalized prematurely.
```

## 10. Context Handoff to Next Sub-Skill

At the end, report:

```markdown
## Handoff to 04c_aggregates_rules_lifecycle

### Entity Candidates Requiring Aggregate Analysis
- ...

### Concepts Modified Together
- ...

### Rule / Policy Candidates
- ...

### Lifecycle-Bearing Concepts
- ...

### Potential Invariants
- ...

### Open Questions 04c Must Preserve
- ...

### Do Not Do in 04c
- Do not treat aggregates as data containers.
- Do not choose transaction technology.
- Do not turn entity candidates into final database tables.
```

## 11. Human Approval Note

This sub-skill may request review of entity/value-object classifications, but Stage 4 is not ready for downstream approval until `04e_domain_modeling_finalizer` has run.
