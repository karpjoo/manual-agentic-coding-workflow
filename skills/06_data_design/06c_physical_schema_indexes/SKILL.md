---
name: 06c_physical_schema_indexes
description: Translate logical schema into physical schema when storage technology is approved, and define justified index recommendations from query patterns, constraints, and security-rule needs.
stage: 06 Data Design
parent_skill: /skills/06_data_design/SKILL.md
subskill_id: 06c
subskill_order: 3
previous_subskill: /skills/06_data_design/06b_logical_schema_query_patterns/SKILL.md
next_subskill: /skills/06_data_design/06d_security_retention_migration/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/06_data/06_physical_schema.md
requires_human_approval: true
external_visibility: internal
---

# 06c Physical Schema and Indexes

## 1. Purpose

This sub-skill creates physical schema and index recommendations only when the storage technology, query patterns, uniqueness constraints, ordering/filtering needs, or security-rule constraints justify them.

If storage technology is not approved, do not invent a final physical schema. Instead, record decision candidates and open questions.

## 2. Core Question

```text
Given the logical schema and query patterns, what concrete storage structures and indexes are justified by approved architecture decisions and actual access patterns?
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
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_query_patterns.md
```

### Read If Applicable

```text
/workflow/05_architecture/05_api_contracts.md
- if API filtering, sorting, pagination, validation, or mutation affects physical design

/workflow/05_architecture/05_authz_model.md
- if row/document-level security or tenant isolation affects indexes or physical layout

/workflow/05_architecture/05_integration_contracts.md
- if integration sync, idempotency, external IDs, or import/export affects physical design

/workflow/05_architecture/05_event_contracts.md
- if persistent event, queue, or message data exists

/workflow/05_architecture/05_observability_policy.md
- if audit, logs, metrics, or traces require storage structures

/workflow/00_intake/00_existing_context_review.md
- if brownfield schema compatibility or migration constraints exist
```

### Do Not Read By Default

```text
- implementation code
- ORM models
- database migrations
- generated database artifacts
- rejected physical schema proposals
- unrelated operational logs
```

Exception: for brownfield or migration projects, inspect selected existing schema/migration/model files only when Stage 0 or USER_DIRECTIVES.md identifies them as relevant.

## 4. Preflight Procedure

```text
[ ] Confirm that logical schema and query patterns exist.
[ ] Confirm whether storage technology is approved.
[ ] Confirm whether physical schema is needed now or should be deferred.
[ ] Identify query patterns that require indexes.
[ ] Identify uniqueness, sorting, filtering, security, or migration constraints.
[ ] Check rejected options before recommending physical structures.
```

## 5. Missing Input Handling

Blocking gaps:

```text
- logical schema is missing
- query patterns are missing when index design is requested
- storage technology is not approved but a final physical schema is expected
- architecture decision conflicts with proposed physical storage
```

If blocking, produce a Blocker Report or mark physical schema as a decision candidate instead of a final design.

Non-blocking gaps:

```text
- unknown data volume
- unclear future reporting workload
- unresolved later-release search or analytics needs
```

Record non-blocking gaps as assumptions or open questions.

## 6. Execution Procedure

### Step 1. Confirm Storage Model

Identify the approved or candidate storage model:

```text
- relational
- document
- key-value
- object/blob
- event store
- search index
- vector store
- analytics warehouse
- external system as source of record
- hybrid
```

If no persistent storage is applicable, record N/A rationale for physical schema and indexes.

### Step 2. Translate Logical Schema to Physical Schema

For relational storage, include:

```text
- tables
- columns
- primary keys
- foreign keys
- unique constraints
- check constraints
- join tables
- transaction boundaries
```

For document storage, include:

```text
- collections
- document shapes
- nested objects
- references vs embedded documents
- denormalized fields
- consistency trade-offs
- document size risks
- collection group query implications
```

For key-value, object/blob, event, search, vector, or analytics storage, include only relevant storage-specific structures.

### Step 3. Identify Physical Consistency and Transaction Boundaries

Map physical boundaries to:

```text
- aggregates
- bounded contexts
- modules
- source-of-truth ownership
- transaction boundaries
- eventual consistency points
- idempotency or retry records
```

### Step 4. Design Index Strategy

Create index recommendations only from:

```text
- actual query patterns
- uniqueness constraints
- required sorting/filtering
- pagination needs
- search needs
- data security rule needs
- foreign key or reference access patterns
```

Do not create speculative indexes without linked query patterns or constraints.

### Step 5. Record Physical Design Trade-Offs

Record trade-offs such as:

```text
- normalization vs denormalization
- embedded vs referenced documents
- relational joins vs application-side joins
- consistency vs availability
- storage cost vs query performance
- write cost vs read performance
- document size vs read simplicity
- index cost vs query latency
```

Classify each trade-off as approved decision used, decision candidate, working assumption, open question, or rejected option.

## 7. Output Artifacts

Create or update when applicable:

```text
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_indexes.md
```

If either artifact is not applicable, do not create a fake artifact. Record the N/A item for the finalizer.

### Required Structure: `06_physical_schema.md`

```markdown
# 06 Physical Schema

## 1. Purpose
## 2. Inputs Used
## 3. Storage Technology Decision Status
## 4. Physical Schema Overview
## 5. Physical Tables / Collections / Stores
## 6. Physical Relationships and References
## 7. Constraints
## 8. Transaction / Consistency Boundaries
## 9. Denormalization / Embedding Decisions
## 10. Storage-Specific Risks
## 11. Decision Candidates
## 12. Working Assumptions
## 13. Open Questions
```

Use this format for each physical object:

```markdown
## PHY-001 — [[Table / Collection / Store Name]]

- Storage technology:
- Logical schema mapping:
- Purpose:
- Source of truth:
- Partition / tenant / namespace strategy:
- Primary key / document ID / object key:
- Foreign keys / references:
- Denormalized fields:
- Constraints:
- Transaction or consistency boundary:
- Security enforcement notes:
- Migration notes:
- Risks:
```

### Required Structure: `06_indexes.md`

```markdown
# 06 Indexes

## 1. Purpose
## 2. Inputs Used
## 3. Index Strategy Summary
## 4. Required MVP Indexes
## 5. Later-Release / Candidate Indexes
## 6. Uniqueness and Constraint Indexes
## 7. Query Pattern to Index Mapping
## 8. Write Cost and Trade-Off Notes
## 9. Index Risks
## 10. Decision Candidates
## 11. Working Assumptions
## 12. Open Questions
```

Use this format for each index:

```markdown
## IDX-001 — [[Index Name]]

- Data object / table / collection:
- Fields:
- Sort direction:
- Unique:
- Partial / composite / covering / full-text / vector / geospatial:
- Linked query patterns:
- Linked constraints:
- MVP required:
- Reason:
- Write cost / trade-off:
- Open questions:
```

## 8. Traceability Rules

Create links:

```text
DSCH → PHY
QP → IDX
REQ / AC / API → QP → IDX
Domain Aggregate → Transaction Boundary / Physical Object
Security-sensitive Query → Required Index or Security Constraint, if applicable
```

Record gaps where a required query pattern lacks physical support.

## 9. Validation Checklist

```text
[ ] Physical schema is only final if storage technology is approved.
[ ] Physical objects map back to logical schema objects.
[ ] Physical schema does not contradict architecture decisions.
[ ] Indexes are justified by query patterns, constraints, sorting/filtering, pagination, or security-rule needs.
[ ] Speculative indexes are avoided or clearly marked as later-release candidates.
[ ] Transaction and consistency boundaries are explicit.
[ ] Denormalization or embedding choices are recorded as decisions, candidates, or assumptions.
[ ] N/A rationale is prepared if physical schema or indexes are not applicable.
```

## 10. Handoff to Next Sub-Skill

Prepare notes for `06d_security_retention_migration`:

```text
- physical schema objects that need access rules
- fields requiring masking, protection, or encryption consideration
- indexes or structures required by security-sensitive queries
- deletion behaviors implied by physical relationships
- migration concerns implied by physical design
- open questions that affect security, retention, or migration
```

## 11. Human Approval Gate

Focused review may be requested for:

```text
- physical schema decision candidates
- database-specific trade-offs
- MVP-required indexes
- rejected or deferred physical alternatives
- storage technology conflicts or open questions
```

Full Stage 6 approval happens after the finalizer.

## 12. Do Not Do

Do not:

```text
- produce final physical schema without approved storage technology
- create speculative indexes without linked query patterns or constraints
- optimize for unknown future workloads without marking the decision as speculative
- create executable migration files, ORM models, database code, or security-rule syntax
- ignore rejected storage or schema options
- treat a candidate physical schema as approved
```
