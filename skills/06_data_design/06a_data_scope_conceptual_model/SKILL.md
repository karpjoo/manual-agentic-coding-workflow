---
name: 06a_data_scope_conceptual_model
description: Identify Stage 6 data scope, extract data-relevant requirements, classify data categories, and draft the conceptual data model.
stage: 06 Data Design
parent_skill: /skills/06_data_design/SKILL.md
subskill_id: 06a
subskill_order: 1
previous_subskill: null
next_subskill: /skills/06_data_design/06b_logical_schema_query_patterns/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/06_data/06_conceptual_data_model.md
requires_human_approval: true
external_visibility: internal
---

# 06a Data Scope and Conceptual Model

## 1. Purpose

This sub-skill starts Stage 6 Data Design. It identifies the data design scope, extracts data-relevant requirements, and creates the conceptual data model without prematurely designing database tables, collections, ORM models, or implementation code.

## 2. Core Question

```text
What data does the system need to know about, own, derive, cache, audit, retain, delete, or receive from external systems, before choosing concrete schema structures?
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
/workflow/01_goal/01_service_goal.md
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
```

### Read If Applicable

```text
/workflow/00_intake/00_existing_context_review.md
- if the project is brownfield, legacy, migration, extension, or integration-oriented

/workflow/04_domain/04_bounded_contexts.md
- if bounded contexts, context map, ownership boundaries, or aggregate boundaries exist

/workflow/04_domain/04_domain_events.md
- if events produce, consume, store, or derive persistent data

/workflow/05_architecture/05_api_contracts.md
- if APIs expose, mutate, filter, paginate, or aggregate data

/workflow/05_architecture/05_integration_contracts.md
- if external systems provide, consume, sync, or transform data

/workflow/05_architecture/05_authz_model.md
- if roles, permissions, tenants, or ownership affect data visibility or mutation
```

### Do Not Read By Default

```text
- implementation source files unless brownfield context explicitly requires them
- rejected schema proposals
- downstream MVP, test, task, or implementation artifacts unless this is a revision pass
- historical agent chat logs
- generated build outputs, raw logs, dependency lockfiles
```

## 4. USER_DIRECTIVES.md Handling

If `/workflow/06_data/USER_DIRECTIVES.md` exists, read it before performing analysis. Classify directives as approval, correction, preference, rejection, scope change, constraint, question, or new input.

Do not convert a directive into an approved decision unless explicit approval is present.

## 5. Preflight Procedure

Before producing the conceptual model:

```text
[ ] Confirm that Stage 6 is the current intended stage.
[ ] Check artifact_manifest.yml for missing, draft, rejected, or superseded inputs.
[ ] Verify that requirements, domain model, and architecture direction exist.
[ ] Identify whether persistence is required, optional, or absent.
[ ] Identify whether personal, sensitive, regulated, tenant, external, or audit data exists.
[ ] Report missing or conflicting inputs before drafting.
```

## 6. Missing Input Handling

Blocking gaps:

```text
- approved requirements are missing
- approved architecture direction is missing
- domain model or equivalent domain context is missing
- privacy/security screening is missing while personal or sensitive data exists
```

If blocking, produce a Blocker Report and do not pretend the conceptual model is complete.

Non-blocking gaps may be handled as working assumptions only if the affected section is clearly marked Draft or Needs Review.

## 7. Execution Procedure

### Step 1. Confirm Data Design Scope

Classify the project data scope:

```text
- no persistent data
- local-only data
- relational database
- document database
- key-value store
- search index
- object/blob storage
- event store
- analytics warehouse
- vector store
- external system as source of record
- hybrid persistence model
```

Record categories that are not applicable and why.

### Step 2. Extract Data-Relevant Requirements

From requirements and acceptance criteria, identify:

```text
- data that must be stored
- user-generated content
- system-generated data
- administrative data
- audit or operational data
- external integration data
- lifecycle states
- retention and deletion expectations
- access-control conditions
- validation and consistency constraints
- reporting, filtering, sorting, search, or pagination needs
```

### Step 3. Map Domain Model to Conceptual Data Objects

For each conceptual data object, define:

```text
- conceptual ID
- domain term
- related requirement IDs
- related acceptance criteria IDs
- related domain concept, aggregate, or bounded context
- owner or actor
- purpose
- lifecycle
- key invariants
- privacy/sensitivity classification
- source-of-truth / derived / cached / external / temporary / audit classification
```

### Step 4. Define Ownership and Boundaries

Identify ownership by:

```text
- bounded context
- module
- aggregate
- user role
- tenant or organization
- external system
- operational responsibility
```

Clarify which component or actor may create, read, update, delete, archive, export, or purge each conceptual data object at a high level. Do not write detailed security rules here; that belongs to `06d_security_retention_migration`.

### Step 5. Classify Sensitivity and Lifecycle

For each data object, classify:

```text
- personal data
- sensitive data
- regulated data
- public/internal/private/confidential data
- temporary data
- audit data
- derived data
- external source-of-truth data
```

Record lifecycle states, retention hints, and deletion concerns as draft notes for later sub-skills.

### Step 6. Identify Early Trade-Offs

Record candidate trade-offs without deciding them:

```text
- normalize vs denormalize later
- source-of-truth vs derived copy
- audit completeness vs privacy minimization
- local cache vs server source of truth
- external data snapshot vs live integration lookup
```

## 8. Output Artifact

Create or update:

```text
/workflow/06_data/06_conceptual_data_model.md
```

Required structure:

```markdown
# 06 Conceptual Data Model

## 1. Purpose
## 2. Inputs Used
## 3. Data Scope
## 4. Conceptual Data Objects
## 5. Data Ownership and Boundaries
## 6. Source-of-Truth Classification
## 7. Derived / Cached / Temporary Data
## 8. Sensitive / Personal / Regulated Data Classification
## 9. Lifecycle and State Notes
## 10. Conceptual Model Diagram or Textual Map
## 11. Decision Candidates
## 12. Working Assumptions
## 13. Open Questions
```

Use this format for each conceptual data object:

```markdown
## DATA-OBJ-001 — [[Name]]

- Domain term:
- Description:
- Related requirement IDs:
- Related acceptance criteria IDs:
- Related domain concept / aggregate:
- Related bounded context:
- Owner:
- Source of truth:
- Lifecycle:
- Sensitivity classification:
- Access summary:
- Retention/deletion notes:
- Open questions:
```

## 9. Traceability Rules

Create initial Stage 6 links:

```text
Requirement → Acceptance Criteria → Domain Concept / Aggregate → Conceptual Data Object
Stakeholder / Role → Conceptual Data Object, when ownership or access is relevant
Risk / Privacy Concern → Conceptual Data Object, when personal or sensitive data exists
Architecture Module → Conceptual Data Object, when ownership is clear
```

Do not invent upstream IDs. Record gaps explicitly.

## 10. Decision / Assumption / Open Question Rules

Classify findings as:

```text
Approved Decision — only explicit human-approved input
Decision Candidate — recommended data scope or ownership choice needing approval
Working Assumption — temporary assumption needed to continue
Open Question — unresolved issue that may affect schema, security, migration, or MVP slicing
Rejected Option — explicitly rejected or superseded data direction
```

Do not update `DECISIONS.md` unless explicit approval exists.

## 11. Validation Checklist

```text
[ ] Conceptual data objects are derived from approved requirements, domain model, and architecture context.
[ ] The output does not contain concrete database table, collection, or ORM design unless clearly marked as a future consideration.
[ ] Source-of-truth, derived, cached, temporary, external, and audit data are distinguished.
[ ] Ownership and boundary notes are explicit enough for logical schema work.
[ ] Sensitive, personal, or regulated data is identified.
[ ] Lifecycle, retention, and deletion concerns are visible for later sub-skills.
[ ] Decision candidates and assumptions are separated from approved decisions.
[ ] Open questions that affect downstream schema/security work are recorded.
```

## 12. Handoff to Next Sub-Skill

Prepare a short handoff note inside `06_conceptual_data_model.md` or the stage result draft for `06b_logical_schema_query_patterns`:

```text
- conceptual data objects ready to translate into logical schema
- ownership boundaries that must be preserved
- open questions affecting fields, identifiers, relationships, or query patterns
- sensitive data classifications that must influence logical schema
- data categories that appear N/A so far
```

## 13. Human Approval Gate

This sub-skill may request focused review of the conceptual model, but full Stage 6 approval happens after `06e_data_design_finalizer`.

Ask the human to review:

```text
- conceptual data objects
- source-of-truth classifications
- ownership boundaries
- sensitive/personal data classification
- major open questions that block logical schema work
```

## 14. Do Not Do

Do not:

```text
- design database tables, collections, ORM models, migrations, indexes, or security-rule syntax
- treat domain entities as automatically equal to database tables
- remove a required data object based on unapproved MVP assumptions
- treat an unverified data classification as approved
- silently ignore personal, sensitive, audit, or external data
- create project implementation code
```
