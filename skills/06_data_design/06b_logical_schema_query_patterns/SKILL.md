---
name: 06b_logical_schema_query_patterns
description: Convert conceptual data objects into a technology-neutral logical schema and derive query patterns from requirements, APIs, screens, jobs, reports, and integrations.
stage: 06 Data Design
parent_skill: /skills/06_data_design/SKILL.md
subskill_id: 06b
subskill_order: 2
previous_subskill: /skills/06_data_design/06a_data_scope_conceptual_model/SKILL.md
next_subskill: /skills/06_data_design/06c_physical_schema_indexes/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/06_data/06_logical_schema.md
requires_human_approval: true
external_visibility: internal
---

# 06b Logical Schema and Query Patterns

## 1. Purpose

This sub-skill translates the conceptual data model into a technology-neutral logical schema and identifies query patterns needed by approved requirements, acceptance criteria, architecture modules, APIs, screens, jobs, reports, and integrations.

It must not prematurely commit to database-specific syntax unless a technology choice has already been approved and the output is clearly kept at logical design level.

## 2. Core Question

```text
What logical records, fields, identifiers, relationships, constraints, lifecycle state fields, and query patterns are needed to support the approved system behavior?
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
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/06_data/06_conceptual_data_model.md
```

### Read If Applicable

```text
/workflow/04_domain/04_bounded_contexts.md
- if ownership, boundaries, or context mapping affects logical schema

/workflow/04_domain/04_domain_events.md
- if event data is persisted or used to derive stored views

/workflow/05_architecture/05_api_contracts.md
- if APIs imply field structure, filtering, pagination, mutation, or validation needs

/workflow/05_architecture/05_integration_contracts.md
- if external systems imply mapping, sync, source-of-truth, or data transformation needs

/workflow/05_architecture/05_authz_model.md
- if data visibility or mutation depends on role, ownership, tenant, or policy

/workflow/05_architecture/05_error_handling_policy.md
- if validation errors, idempotency, retries, or dead-letter records must be stored
```

### Do Not Read By Default

```text
- implementation source files
- ORM model files
- generated schemas
- rejected or superseded schema proposals
- downstream task or test artifacts unless this is a revision pass
```

## 4. Preflight Procedure

```text
[ ] Confirm that 06_conceptual_data_model.md exists or report a blocker.
[ ] Verify conceptual objects have stable IDs.
[ ] Check whether architecture or API artifacts imply query patterns.
[ ] Identify missing authorization, integration, or domain-event inputs.
[ ] Report any conceptual-model contradictions before deriving schema.
```

## 5. Missing Input Handling

Blocking gaps:

```text
- conceptual data model is missing
- approved requirements or acceptance criteria are missing
- architecture module boundaries are missing where ownership affects data structure
- authorization model is missing while role/ownership affects query or field visibility
```

Non-blocking gaps:

```text
- incomplete future-release query pattern
- unclear analytics/reporting need
- unresolved performance target that does not affect logical schema shape
```

Record non-blocking gaps as assumptions or open questions.

## 6. Execution Procedure

### Step 1. Translate Conceptual Objects to Logical Records

For each conceptual data object, decide whether it becomes:

```text
- logical entity / record
- value record
- document-like structure
- relationship / association record
- event record
- audit record
- external reference
- derived view
- cache record
- temporary/session record
```

Do not assume one conceptual object always equals one table or collection.

### Step 2. Define Field Semantics

For each logical record, define fields and classify each field as:

```text
- required
- optional
- computed
- immutable after creation
- system-managed
- user-editable
- admin-editable
- sensitive
- indexed candidate
- encrypted or protected candidate
- retained or deletable
```

Include timestamps, actor fields, lifecycle status fields, versioning fields, and audit metadata where justified by requirements or architecture.

### Step 3. Define Identifiers and References

Specify:

```text
- stable identifiers
- natural vs surrogate identifier considerations
- external IDs
- tenant/organization/project/user ownership IDs
- references between logical records
- relationship cardinality
- delete behavior implications
```

### Step 4. Define Constraints and Validation Rules

Map approved invariants and acceptance criteria into logical constraints:

```text
- uniqueness rules
- required relationship rules
- lifecycle state transition constraints
- value range constraints
- cross-field consistency rules
- authorization-dependent validation
- external system consistency notes
```

### Step 5. Identify Query Patterns

For each major use case, API operation, screen, background job, report, or integration flow, record:

```text
- query pattern ID
- actor or system
- linked requirement / acceptance criteria / API contract
- data objects accessed
- filters
- sort order
- pagination
- authorization condition
- expected scale/frequency if known
- stale data tolerance
- caching or denormalization implications
```

### Step 6. Identify Logical Schema Risks

Record risks such as:

```text
- missing identifiers
- ambiguous ownership
- unclear delete behavior
- query pattern unsupported by logical structure
- field-level privacy ambiguity
- lifecycle state mismatch with domain rules
- hidden many-to-many relationships
- external source-of-truth conflicts
```

## 7. Output Artifacts

Create or update:

```text
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_query_patterns.md
```

### Required Structure: `06_logical_schema.md`

```markdown
# 06 Logical Schema

## 1. Purpose
## 2. Inputs Used
## 3. Schema Overview
## 4. Logical Records / Entities / Documents
## 5. Fields and Field Semantics
## 6. Identifiers and References
## 7. Relationships
## 8. Constraints and Validation Rules
## 9. Lifecycle State Fields
## 10. Audit and Metadata Fields
## 11. Sensitive Fields
## 12. Derived Fields
## 13. Schema Risks
## 14. Decision Candidates
## 15. Working Assumptions
## 16. Open Questions
```

Use this format for each logical schema object:

```markdown
## DSCH-001 — [[Logical Record / Entity / Document Name]]

- Purpose:
- Related conceptual object:
- Related requirements:
- Related domain concepts:
- Storage intent: source-of-truth / derived / cache / audit / external / temporary
- Ownership:
- Lifecycle:

### Fields

| Field | Meaning | Type | Required | Editable By | Sensitive | Constraint / Validation | Notes |
|---|---|---|---|---|---|---|---|

### Relationships

| Relationship | Target | Cardinality | Required | Delete Behavior | Notes |
|---|---|---|---|---|---|

### Constraints

- ...

### Security Notes

- ...

### Traceability

- Requirements:
- Acceptance criteria:
- Domain concepts:
- Architecture modules / APIs:
```

### Required Structure: `06_query_patterns.md`

```markdown
# 06 Query Patterns

## 1. Purpose
## 2. Query Pattern Summary
## 3. Query Patterns by Requirement / API / Screen / Job
## 4. Filtering, Sorting, Pagination, and Search Needs
## 5. Authorization-Aware Query Notes
## 6. Scale / Frequency Assumptions
## 7. Performance Risks
## 8. Index Implications
## 9. Caching or Denormalization Candidates
## 10. Open Questions
```

Use this format for each query pattern:

```markdown
## QP-001 — [[Query Pattern Name]]

- Actor / system:
- Use case:
- Related requirement IDs:
- Related acceptance criteria IDs:
- Related API / module / screen / job:
- Data objects accessed:
- Filters:
- Sort order:
- Pagination:
- Authorization condition:
- Expected frequency / scale:
- Freshness requirement:
- Required indexes:
- Caching / denormalization notes:
- Risks:
```

## 8. Traceability Rules

Create links:

```text
DATA-OBJ → DSCH
REQ / AC → DSCH
Domain Concept / Aggregate → DSCH
Architecture Module / API → DSCH
REQ / AC / API / Screen / Job → QP
QP → DSCH
```

Record gaps if a required behavior lacks a logical schema or query pattern.

## 9. Validation Checklist

```text
[ ] Logical schema is derived from conceptual data objects and approved inputs.
[ ] Fields include meaning, editability, sensitivity, and validation notes.
[ ] Identifiers and references are explicit.
[ ] Relationships include cardinality and delete behavior implications.
[ ] Constraints reflect requirements, acceptance criteria, and domain invariants.
[ ] Query patterns are linked to real requirements, APIs, screens, jobs, reports, or integrations.
[ ] Authorization-sensitive query notes are visible.
[ ] Logical schema remains technology-neutral.
[ ] Decision candidates, assumptions, and open questions are separated.
```

## 10. Handoff to Next Sub-Skill

Prepare notes for `06c_physical_schema_indexes`:

```text
- storage technology decisions already approved or still open
- logical schema objects that need physical mapping
- query patterns that imply indexes, ordering, search, pagination, or denormalization
- constraints that require database-level support
- authorization conditions that may affect physical schema or indexes
- unresolved questions that block physical schema or index design
```

## 11. Human Approval Gate

Focused review may be requested for:

```text
- logical record boundaries
- field semantics
- identifiers and references
- required constraints
- query pattern completeness
- risks that affect physical design
```

Full Stage 6 approval happens after the finalizer.

## 12. Do Not Do

Do not:

```text
- create physical schema syntax unless the next sub-skill is explicitly being run
- create speculative fields unrelated to approved requirements or domain rules
- create query patterns without linked behavior
- treat query performance assumptions as facts
- hide authorization conditions inside vague notes
- create code, migrations, tests, ORM classes, or database rules
```
