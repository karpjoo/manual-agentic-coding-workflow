# 06 Data Design Skill Template

> This is a **Stage-Specific Skill Template**, not an executable `SKILL.md`.
> Use this template together with the Core Skill Template to create a reusable `/skills/06_data_design/SKILL.md`.
>
> Target stage: **Stage 6 — Data Design**
> Previous stage: **Stage 5 — Architecture & Technical Contracts**
> Next stage: **Stage 7 — MVP Scope & Release Slicing**

---

## 0. Template Scope

This template defines the stage-specific extension for Stage 6 Data Design in the Manual Agentic Coding Workflow.

It defines:

- Stage purpose
- Core question
- Input contract
- Output artifact contract
- Required output structures
- Data design procedure
- Traceability requirements
- Security, privacy, and retention handling
- Human approval gate
- Next `context_packet.md` handoff rules

It does **not** replace the Core Skill Template.

The generated executable `SKILL.md` must still follow the core rules for:

- agent role and operating mode
- input precedence
- `USER_DIRECTIVES.md` handling
- artifact status checking
- decision / assumption / open-question separation
- human approval gate
- failure handling
- do-not-do rules

---

## 1. Stage Purpose

Stage 6 Data Design converts approved requirements, domain model, and architecture contracts into explicit data structures and data access rules.

The goal is to design data structures **after** domain and architecture decisions are clear, but **before** MVP slicing, test strategy, task breakdown, implementation prompts, and code changes.

This stage must produce a data design that is:

- aligned with approved requirements and acceptance criteria;
- consistent with approved domain concepts, aggregates, invariants, and bounded contexts;
- compatible with approved architecture, module boundaries, API contracts, and integration boundaries;
- explicit about data ownership, access control, retention, deletion, migration, and query patterns;
- traceable enough for later test strategy, task breakdown, and implementation.

This stage is not a code implementation stage.

---

## 2. Core Question

The core question for Stage 6 is:

```text
Given the approved requirements, domain model, and architecture contracts, what data structures, relationships, constraints, access rules, query patterns, indexes, migration approach, and retention/deletion policies are needed to support the system safely and verifiably?
```

Supporting questions:

```text
1. What persistent data does the system need?
2. Which domain concepts become stored data, references, documents, records, events, or derived views?
3. What data belongs to which bounded context, module, user, tenant, or external integration?
4. What data must be normalized, embedded, denormalized, cached, indexed, encrypted, retained, deleted, audited, or derived?
5. Which access rules are enforced at the database, service, API, or application layer?
6. What query patterns must be supported for the MVP and known later releases?
7. What migration or seed-data strategy is needed before implementation begins?
8. Which parts of the data design require human approval before downstream stages rely on them?
```

---

## 3. Stage Folder

Recommended project execution folder:

```text
/workflow/06_data
```

Recommended reusable skill folder:

```text
/skills/06_data_design
```

Recommended stage template path:

```text
/workflow_templates/stage_templates/06_data_design_skill_template.md
```

---

## 4. Always Read Inputs

The generated Stage 6 `SKILL.md` must define these as **Always Read** inputs.

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

Rationale:

```text
Stage 6 must not design data structures from vague feature ideas.
It must derive data design from approved goals, risks, requirements, domain model, architecture, and approved decisions.
```

---

## 5. Read If Applicable Inputs

The generated Stage 6 `SKILL.md` must activate the following conditional inputs based on project profile, `context_packet.md`, `artifact_manifest.yml`, `DECISIONS.md`, architecture artifacts, and `USER_DIRECTIVES.md`.

```text
/workflow/00_intake/00_existing_context_review.md
- if this is a brownfield, legacy, migration, extension, or integration project

/workflow/04_domain/04_bounded_contexts.md
- if bounded contexts, context map, or ownership boundaries exist

/workflow/04_domain/04_domain_events.md
- if the system stores, emits, consumes, replays, or derives data from events

/workflow/05_architecture/05_api_contracts.md
- if APIs expose, mutate, validate, paginate, filter, or aggregate persisted data

/workflow/05_architecture/05_integration_contracts.md
- if external systems provide, consume, sync, transform, or store project data

/workflow/05_architecture/05_authz_model.md
- if roles, permissions, tenants, row-level access, document-level access, or policy-based access exists

/workflow/05_architecture/05_event_contracts.md
- if asynchronous messaging, event sourcing, queues, or pub/sub are part of the architecture

/workflow/05_architecture/05_observability_policy.md
- if logs, metrics, traces, audit events, or operational telemetry store user or system data

/workflow/05_architecture/05_error_handling_policy.md
- if validation errors, retries, idempotency records, dead-letter records, or error logs must be persisted

/workflow/07_mvp_release/07_mvp_scope.md
- if Stage 7 already exists and the data design is being revised after MVP slicing

/workflow/08_test_strategy/08_test_strategy.md
- if Stage 6 is being revised after validation strategy has already been created
```

---

## 6. Do Not Read By Default

The generated Stage 6 `SKILL.md` must not read the following by default:

```text
- unrelated previous stage drafts
- superseded architecture or domain artifacts
- rejected schema designs
- full historical agent chat logs
- implementation files or source code, unless brownfield review requires them
- dependency lockfiles, generated code, build output, or raw logs
- previous prototype schemas unless explicitly marked current or useful for migration review
- downstream Stage 7/8/9 artifacts unless this is a revision pass and the user explicitly asks for alignment
```

Exception:

```text
For brownfield or migration projects, selected existing schema, migration, seed, fixture, or model files may be inspected if Stage 0 or USER_DIRECTIVES.md identifies them as relevant.
```

---

## 7. Missing Input Handling

The generated Stage 6 `SKILL.md` must handle missing inputs as follows.

### 7.1 Blocking Missing Inputs

Treat these as blocking unless the user explicitly requests exploratory draft work:

```text
- missing approved requirements
- missing approved architecture direction
- missing domain model or equivalent domain context
- missing data store / persistence architecture decision, when persistence is required
- missing security/privacy screening when personal or sensitive data exists
- missing authorization model when access control affects data visibility or mutation
```

When blocking:

```text
1. Stop before producing final data design artifacts.
2. Produce a Blocker Report.
3. Explain why the missing input affects data design safety or correctness.
4. List safe partial work, if any.
5. Request the specific human decision or missing artifact.
```

### 7.2 Non-Blocking Missing Inputs

Treat these as non-blocking only if a clearly labeled draft can safely proceed:

```text
- missing optional integration detail
- incomplete future-release query pattern
- incomplete analytics/reporting requirement
- unresolved performance target that does not affect MVP schema shape
- unclear seed data needs
```

When non-blocking:

```text
1. Record a working assumption.
2. State risk if the assumption is wrong.
3. Mark affected artifacts as Draft or Needs Review.
4. Add an open question.
5. Do not record the assumption as an approved decision.
```

---

## 8. Stage-Specific Execution Procedure

The generated executable `SKILL.md` should implement the following Stage 6 procedure in addition to the core runtime procedure.

### Step 1. Confirm Data Design Scope

Identify whether the project uses:

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

Record non-applicable categories in the N/A section.

### Step 2. Extract Data-Relevant Requirements

From requirements and acceptance criteria, identify:

```text
- entities or records that must be stored
- user-generated content
- system-generated data
- administrative data
- audit or operational data
- external integration data
- lifecycle states
- retention and deletion expectations
- access control conditions
- validation and consistency constraints
- reporting, filtering, sorting, search, or pagination needs
```

### Step 3. Map Domain Model to Conceptual Data Model

Create the conceptual model from domain concepts without prematurely committing to table, collection, or storage syntax.

For each conceptual data object, record:

```text
- conceptual ID
- domain term
- related requirement IDs
- related domain concept / aggregate / bounded context
- owner or actor
- purpose
- lifecycle
- key invariants
- privacy/sensitivity classification
- whether it is source-of-truth, derived, cached, external, temporary, or audit data
```

### Step 4. Define Data Ownership and Boundaries

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

Clarify which component is allowed to create, read, update, delete, archive, export, or purge each data object.

### Step 5. Design Logical Schema

Create a technology-neutral logical schema that includes:

```text
- records / entities / documents / value records
- fields and field types at a conceptual level
- identifiers and references
- relationships
- constraints
- uniqueness rules
- required vs optional fields
- lifecycle state fields
- timestamps and actor fields
- derived fields
- audit fields
- validation rules
```

The logical schema must state whether each field is:

```text
- required
- optional
- computed
- immutable after creation
- system-managed
- user-editable
- admin-editable
- sensitive
- indexed
- encrypted or protected
- retained or deletable
```

### Step 6. Design Physical Schema

If a storage technology is approved, translate the logical schema into a physical schema.

For relational storage, include:

```text
- tables
- columns
- primary keys
- foreign keys
- unique constraints
- check constraints
- join tables
- indexes
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

For key-value, object, event, search, vector, or analytics storage, include storage-specific structure only if applicable.

Do not invent a physical schema if the storage decision is not approved. Record it as a decision candidate or open question.

### Step 7. Identify Query Patterns

For each major use case, API operation, screen, background job, report, or integration flow, record:

```text
- query pattern ID
- actor or system
- linked requirement / acceptance criteria / API contract
- data objects accessed
- filter conditions
- sort order
- pagination needs
- authorization condition
- expected scale or frequency if known
- required indexes or performance notes
- stale data tolerance
- caching or denormalization needs
```

### Step 8. Design Index Strategy

Create index recommendations only from actual query patterns, uniqueness constraints, ordering needs, and security-rule constraints.

For each index, record:

```text
- index ID
- data object / table / collection
- fields
- sort direction if relevant
- linked query patterns
- linked requirement or API contract
- reason
- expected benefit
- trade-off or write cost
- whether required for MVP or later
```

Do not create speculative indexes without a linked query pattern or constraint.

### Step 9. Define Data Security Rules

Map data access control to approved roles, permissions, architecture, and privacy constraints.

For each data object, record:

```text
- who can create
- who can read
- who can update
- who can delete
- who can export
- who can restore
- who can access audit/history data
- enforcement layer: database, backend service, API gateway, application, or hybrid
- validation required before write
- sensitive fields that require masking, encryption, or exclusion
- audit log requirements
```

If database-level rules are used, describe rule intent without requiring implementation syntax unless the storage technology is already approved.

### Step 10. Define Retention, Deletion, and Archival Policy

For each relevant data category, define:

```text
- retention period or retention trigger
- deletion trigger
- soft delete vs hard delete
- archive behavior
- legal/privacy/compliance constraints
- user-requested deletion behavior
- admin purge behavior
- backup retention considerations
- audit retention considerations
- cascading delete or orphan handling
```

If unknown, record an open question rather than inventing a policy.

### Step 11. Define Migration and Seed Strategy

Create a migration plan if:

```text
- persistent schema is introduced
- existing data must be migrated
- seed data is required
- reference data must be loaded
- test fixtures depend on data shape
- indexes or security rules need staged rollout
```

The migration plan should include:

```text
- migration scope
- source data
- target data
- ordering
- rollback or recovery concept
- data validation checks
- backfill requirements
- seed/reference data requirements
- environment considerations
- risks and manual approval points
```

Do not write executable migration code in this stage.

### Step 12. Identify Data Design Trade-offs

Record trade-offs such as:

```text
- normalization vs denormalization
- consistency vs availability
- embedded vs referenced documents
- relational joins vs application-side joins
- synchronous validation vs eventual consistency
- storage cost vs query performance
- audit completeness vs privacy minimization
- soft delete convenience vs retention risk
```

Classify each as:

```text
- approved decision used
- decision candidate
- working assumption
- open question
- rejected option
```

### Step 13. Update Data Traceability

Update traceability links from:

```text
Requirement → Acceptance Criteria → Domain Concept / Aggregate → Architecture Module / API → Data Object → Query Pattern → Index / Security Rule / Migration Item
```

Record traceability gaps explicitly.

### Step 14. Prepare Stage 7 Handoff

Summarize only the data design context needed for MVP scope and release slicing:

```text
- data objects required for MVP
- data objects suitable for later release
- high-risk or high-cost data features
- migration dependencies
- security/privacy blockers
- query or index work that affects release slicing
- data features that should be excluded from MVP unless approved
```

---

## 9. Mandatory Artifacts

The generated Stage 6 `SKILL.md` must define the following mandatory artifacts.

```text
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_query_patterns.md
/workflow/06_data/06_data_design_traceability.md
/workflow/06_data/result.md
/workflow/context/context_packet.md
```

### 9.1 `/workflow/06_data/06_conceptual_data_model.md`

Required sections:

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

### 9.2 `/workflow/06_data/06_logical_schema.md`

Required sections:

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

### 9.3 `/workflow/06_data/06_query_patterns.md`

Required sections:

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

### 9.4 `/workflow/06_data/06_data_design_traceability.md`

Required sections:

```markdown
# 06 Data Design Traceability

## 1. Traceability Scope
## 2. Requirement to Data Object Links
## 3. Acceptance Criteria to Query Pattern Links
## 4. Domain Concept / Aggregate to Data Object Links
## 5. Architecture Module / API to Data Object Links
## 6. Data Object to Security Rule Links
## 7. Data Object to Migration Item Links
## 8. Traceability Gaps
## 9. Traceability Updates Needed in /workflow/context/TRACEABILITY_MATRIX.md
```

### 9.5 `/workflow/06_data/result.md`

Required sections:

```markdown
# Result: 06 Data Design

## 1. Task Summary
## 2. Inputs Used
## 3. Outputs Created or Updated
## 4. Approved Decisions Used
## 5. Key Data Design Findings
## 6. Decision Candidates
## 7. Working Assumptions
## 8. Open Questions
## 9. Risks and Constraints
## 10. Rejected or Superseded Options
## 11. N/A Items
## 12. Traceability Updates
## 13. Human Approval Required
## 14. Recommended Next Step
```

---

## 10. Conditional Artifacts

The generated Stage 6 `SKILL.md` must define the following conditional artifacts.

```text
/workflow/06_data/06_physical_schema.md
- if a concrete storage technology has been approved or must be compared as a decision candidate

/workflow/06_data/06_indexes.md
- if query patterns, uniqueness constraints, sorting, filtering, search, or database security rules require indexes

/workflow/06_data/06_data_security_rules.md
- if roles, permissions, ownership, tenants, personal data, sensitive data, or data-dependent access control exists

/workflow/06_data/06_retention_deletion_policy.md
- if personal data, user-generated content, audit logs, operational records, compliance constraints, or deletion needs exist

/workflow/06_data/06_migration_plan.md
- if persistent schema, existing data, seed/reference data, staged rollout, backfill, or migration risk exists

/workflow/06_data/06_data_dictionary.md
- if downstream implementation, analytics, API documentation, or team collaboration needs stable field definitions

/workflow/06_data/06_seed_fixture_strategy.md
- if test strategy or implementation will require seed data, fixtures, reference data, or sample records

/workflow/06_data/06_external_data_mapping.md
- if external integrations provide, transform, sync, or consume persisted data

/workflow/06_data/06_event_data_model.md
- if events, messages, event sourcing, audit events, or asynchronous workflows carry persistent or replayable data

/workflow/06_data/06_analytics_reporting_model.md
- if analytics, dashboards, exports, reporting, ML, or BI requirements exist

/workflow/06_data/06_blob_object_storage_model.md
- if files, media, documents, uploads, generated artifacts, or large objects must be stored
```

---

## 11. N/A Record Rules

If a conditional artifact is not produced, the generated `SKILL.md` must require an N/A record in `/workflow/06_data/result.md`.

Each N/A record must include:

```text
- artifact name
- why it is not applicable now
- which approved input supports this conclusion, if any
- what future change would make it applicable
- whether the conclusion requires human confirmation
```

Example format:

```markdown
## N/A Items

| Artifact | Why Not Applicable | Revisit If | Human Confirmation Needed |
|---|---|---|---|
| 06_migration_plan.md | No existing data or schema migration is in scope for the greenfield MVP draft. | Brownfield import, schema change, seed data, or production migration becomes required. | Yes |
```

---

## 12. Required Output Structure Details

### 12.1 Conceptual Data Object Format

Use this format in `06_conceptual_data_model.md`:

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

### 12.2 Logical Schema Object Format

Use this format in `06_logical_schema.md`:

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

### 12.3 Physical Schema Format

Use this format in `06_physical_schema.md` if applicable:

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

### 12.4 Query Pattern Format

Use this format in `06_query_patterns.md`:

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

### 12.5 Index Format

Use this format in `06_indexes.md` if applicable:

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

### 12.6 Data Security Rule Format

Use this format in `06_data_security_rules.md` if applicable:

```markdown
## DSR-001 — [[Data Rule Name]]

- Data object:
- Actor / role / system:
- Operation: create / read / update / delete / export / restore
- Condition:
- Enforcement layer:
- Related requirement:
- Related architecture authz rule:
- Sensitive fields affected:
- Audit required:
- Failure behavior:
- Test implication:
- Open questions:
```

### 12.7 Migration Item Format

Use this format in `06_migration_plan.md` if applicable:

```markdown
## MIG-001 — [[Migration Item Name]]

- Trigger:
- Source:
- Target:
- Data affected:
- Environment:
- Ordering:
- Validation check:
- Rollback / recovery concept:
- Manual approval point:
- Risks:
- Open questions:
```

---

## 13. Traceability Requirements

The generated Stage 6 `SKILL.md` must preserve or improve the project traceability matrix.

Required traceability links:

```text
Requirement → Acceptance Criteria → Domain Concept / Aggregate → Architecture Module / API → Data Object
Requirement → Query Pattern
Query Pattern → Index
Data Object → Data Security Rule
Data Object → Retention / Deletion Policy
Data Object → Migration Item, if applicable
Sensitive Data → Security Rule / Retention Rule / Audit Rule
External Integration → External Data Mapping, if applicable
Domain Event → Event Data Model, if applicable
```

Traceability rules:

```text
- Do not invent requirement IDs.
- Preserve existing requirement, acceptance criteria, domain, architecture, and API IDs.
- Introduce stable Stage 6 IDs only for data artifacts.
- Record traceability gaps explicitly.
- Do not create task IDs or test case IDs prematurely unless existing downstream artifacts already require them.
- Update /workflow/context/TRACEABILITY_MATRIX.md or record exact updates needed if the workflow requires manual matrix consolidation.
```

Recommended Stage 6 ID conventions:

```text
DATA-OBJ-001    conceptual data object
DSCH-001        logical schema object
PHY-001         physical schema object
QP-001          query pattern
IDX-001         index
DSR-001         data security rule
RET-001         retention/deletion rule
MIG-001         migration item
SEED-001        seed/fixture item
EXTDATA-001     external data mapping
EVENTDATA-001   event data model item
```

---

## 14. Stage-Specific Validation Checklist

The generated Stage 6 `SKILL.md` must include a checklist equivalent to the following.

```text
[ ] Data design is derived from approved requirements, domain model, and architecture artifacts.
[ ] The stage did not design database tables before understanding domain concepts and architecture boundaries.
[ ] Conceptual data model separates source-of-truth, derived, cached, temporary, audit, and external data.
[ ] Logical schema defines fields, relationships, constraints, lifecycle states, and validation rules.
[ ] Physical schema is created only when storage technology is approved or clearly marked as a decision candidate.
[ ] Query patterns are linked to requirements, APIs, screens, jobs, integrations, or acceptance criteria.
[ ] Indexes are justified by query patterns, uniqueness constraints, sorting/filtering needs, or security-rule needs.
[ ] Data ownership and bounded-context/module ownership are explicit.
[ ] Security rules are mapped to approved roles, permissions, and access-control decisions.
[ ] Sensitive, personal, or regulated data is identified and handled explicitly.
[ ] Retention, deletion, archival, and audit needs are addressed or recorded as open questions.
[ ] Migration, seed, fixture, or backfill needs are addressed or marked N/A with rationale.
[ ] All conditional artifacts have either been produced or recorded as N/A.
[ ] Decision candidates are not treated as approved decisions.
[ ] Working assumptions are recorded separately from requirements and decisions.
[ ] Open questions that affect MVP slicing or implementation are visible.
[ ] Traceability links from requirements/domain/architecture to data objects are preserved.
[ ] context_packet.md is prepared for Stage 7.
```

---

## 15. Stage-Specific Human Approval Gate

At the end of Stage 6, the generated `SKILL.md` must request human review and approval for at least the following.

### Decisions to Approve

```text
- conceptual data model
- logical schema
- physical schema, if applicable
- data ownership and source-of-truth boundaries
- access-control and data security rule direction
- retention/deletion policy direction
- migration and seed strategy, if applicable
- major normalization / denormalization trade-offs
- indexes required for MVP, if applicable
- conditional artifacts marked N/A
```

### Assumptions to Confirm

```text
- expected data volume and query frequency assumptions
- MVP vs later-release data needs
- unclear personal/sensitive data classification
- default retention/deletion behavior
- default audit logging behavior
- database-specific capabilities or limitations
- migration or seed data assumptions
```

### Open Questions to Resolve

```text
- unresolved schema choices affecting implementation
- unresolved access-control rules affecting security
- unresolved retention/deletion rules affecting compliance or privacy
- unresolved external data ownership or synchronization rules
- unresolved query patterns affecting indexes or release slicing
- unresolved migration risks affecting MVP feasibility
```

### Risks to Review

```text
- schema coupling across bounded contexts
- over-denormalization or premature optimization
- missing indexes for required query patterns
- data leakage through overly broad read access
- inconsistent authorization between API and database layers
- retention or deletion gaps
- migration risk
- audit log privacy risk
- unbounded data growth
```

### Artifacts Ready for Review

```text
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_query_patterns.md
/workflow/06_data/06_data_design_traceability.md
/workflow/06_data/result.md

Plus any applicable conditional artifacts.
```

### Recommended Next Step

```text
After human approval, proceed to Stage 7 MVP Scope & Release Slicing using approved Stage 6 official artifacts as source of truth.
```

---

## 16. Next `context_packet.md` Rules

The generated Stage 6 `SKILL.md` must update or prepare `/workflow/context/context_packet.md` for Stage 7.

The Stage 7 handoff must include only minimal operational context, not a full copy of Stage 6 artifacts.

Required Stage 7 handoff content:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 06_data_design completed or needs review
- Completed stages:
- Next recommended stage: 07_mvp_release_slicing

## 2. Approved Decisions
- Only human-approved data decisions.

## 3. Working Assumptions
- Data-related assumptions that affect MVP slicing or release order.

## 4. Open Questions
- Data questions that may affect MVP scope, release sequence, implementation risk, or test strategy.

## 5. Rejected / Superseded Options
- Rejected schema, storage, access-control, migration, or retention options.

## 6. Constraints That Must Not Be Violated
- Data ownership constraints
- Access-control constraints
- Privacy/security constraints
- Retention/deletion constraints
- Migration constraints
- Storage technology constraints

## 7. Key Context for Next Stage
- Data objects required for MVP
- Data objects that can be deferred
- high-risk data features
- expensive migrations or schema choices
- security/privacy-sensitive data features
- query/index work that may affect release slicing

## 8. Required Inputs for Next Stage
- /workflow/06_data/06_conceptual_data_model.md
- /workflow/06_data/06_logical_schema.md
- /workflow/06_data/06_query_patterns.md
- /workflow/06_data/06_data_design_traceability.md
- /workflow/06_data/result.md
- applicable conditional artifacts

## 9. Do Not Do
- Do not treat unapproved schema proposals as final.
- Do not include deferred data features in MVP unless explicitly approved.
- Do not ignore data security, retention, deletion, or migration blockers during MVP slicing.
```

---

## 17. Decision / Assumption / Open Question Rules for Stage 6

The generated Stage 6 `SKILL.md` must use the following classification rules.

### Approved Decision

Only use when explicit human approval exists.

Examples:

```text
Approved: The MVP will use Cloud Firestore as the primary database.
Approved: User profile data must be soft-deleted for 30 days before hard deletion.
Approved: Only Admin users may export audit records.
```

### Decision Candidate

Use for recommended data choices requiring approval.

Examples:

```text
Candidate: Store order line items as embedded records inside Order documents for the MVP.
Candidate: Add a composite index for projectId + status + createdAt because QP-003 requires filtered, sorted project lists.
```

### Working Assumption

Use when the agent must proceed with an unverified but safe temporary assumption.

Examples:

```text
Assumption: MVP query volume is low enough that the first release does not require a separate search index.
Assumption: Audit log retention is needed but the exact retention period is not yet approved.
```

### Open Question

Use when unresolved information can change schema, security, migration, retention, or MVP scope.

Examples:

```text
Open Question: Should deleted user-generated records remain visible to administrators?
Open Question: Is tenant-level isolation required at the database level or only at the service layer?
```

### Rejected Option

Use when a schema, storage, security, migration, or retention approach has been explicitly rejected or superseded.

Examples:

```text
Rejected: Do not store raw third-party API payloads unless the human explicitly reopens this option.
Rejected: Do not use a shared public collection for private user records.
```

---

## 18. Failure Handling

The generated Stage 6 `SKILL.md` must produce a blocker report instead of pretending completion when safe data design is impossible.

Stage-specific blocker examples:

```text
- requirements are missing or unapproved
- architecture does not identify persistence approach but persistent data is required
- domain model is missing or conflicts with architecture
- authorization model is missing but data visibility depends on role or ownership
- personal/sensitive data is present but privacy/security direction is missing
- external source-of-truth ownership is unresolved
- existing brownfield schema is unavailable for a migration project
- artifact_manifest.yml marks required inputs as superseded or rejected
```

Blocker report format:

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
- ...

### Affected Data Artifacts
- ...

### Affected Later Stages
- Stage 7 MVP Scope & Release Slicing
- Stage 8 Test Strategy & Validation Harness
- Stage 9 Task Breakdown
- Stage 10 Implementation Prompt Writing
- Stage 11 TDD Implementation Loop

### Safe Partial Work Completed
- ...

### Human Decision Needed
- ...
```

---

## 19. Specialization Hooks

Project-type specialization addenda may extend this template, but must not replace it.

### Web SaaS

May add:

```text
- tenant / organization data ownership
- account, membership, subscription, billing, and audit data
- RBAC / ABAC data implications
- admin dashboard query patterns
- soft deletion and account closure policy
```

### Internal Tool

May add:

```text
- operator workflow records
- approval records
- internal audit logs
- import/export data
- operational reporting needs
```

### Mobile App

May add:

```text
- offline cache model
- sync conflict strategy
- local device storage
- push notification token data
- platform permission-related data
```

### AI / Data Product

May add:

```text
- dataset schema
- data provenance
- labeling and annotation data
- model input/output records
- evaluation result data
- reproducibility metadata
- human review data
```

### Regulated / Security-Sensitive

May add:

```text
- stronger data classification
- encryption requirements
- audit log retention
- privacy impact notes
- access review records
- export and deletion controls
- compliance evidence artifacts
```

### Brownfield / Legacy

May add:

```text
- existing schema review
- compatibility constraints
- migration mapping
- data cleanup strategy
- backfill validation
- rollback plan
- parallel-run considerations
```

---

## 20. Tool Wrapper Hooks

Tool-specific wrappers may define:

```text
- where to save the generated executable SKILL.md
- file creation commands
- path conventions
- sandbox or permission rules
- review workflow conventions
- command invocation conventions
```

Tool wrappers must not change:

```text
- Stage 6 reasoning logic
- data design approval rules
- input/output artifact contract
- assumption handling
- traceability requirements
- stage boundaries
```

---

## 21. Do Not Do

The generated Stage 6 `SKILL.md` must include these Stage 6-specific anti-patterns.

```text
- Do not design database tables before reading approved domain and architecture artifacts.
- Do not treat the database schema as the domain model.
- Do not collapse conceptual, logical, and physical design into one vague schema summary.
- Do not create a physical schema if the storage technology is not approved, unless clearly marked as a decision candidate.
- Do not create speculative indexes without linked query patterns or constraints.
- Do not ignore data security rules because Stage 12 will do a final security review later.
- Do not treat application-layer authorization as sufficient without checking whether database-level access risks exist.
- Do not store personal or sensitive data without classification, access, retention, and deletion notes.
- Do not silently omit migration, seed, or fixture concerns.
- Do not use unapproved downstream MVP assumptions to remove required data objects.
- Do not create implementation code, migrations, ORM models, security-rule files, or tests in this stage.
- Do not update DECISIONS.md unless the human explicitly approves a decision.
- Do not use context_packet.md as the sole source of truth.
- Do not rely on previous chat history.
```

---

## 22. Acceptance Criteria for the Generated Executable SKILL

A reusable `/skills/06_data_design/SKILL.md` generated from this template is acceptable only if:

```text
[ ] It follows the Core Skill Template.
[ ] It clearly states that it is Stage 6 Data Design.
[ ] It defines Always Read, Read If Applicable, Do Not Read By Default, and Missing Input Handling.
[ ] It defines mandatory and conditional artifacts.
[ ] It requires N/A records for skipped conditional artifacts.
[ ] It provides a step-by-step data design procedure.
[ ] It separates conceptual, logical, and physical data design.
[ ] It includes query pattern and index design rules.
[ ] It includes data ownership and access-control rules.
[ ] It includes retention/deletion/migration handling.
[ ] It includes traceability from requirements/domain/architecture to data objects.
[ ] It includes a Stage 7 context handoff rule.
[ ] It separates approved decisions, decision candidates, assumptions, open questions, risks, and rejected options.
[ ] It includes a human approval gate.
[ ] It does not include project-specific product assumptions.
[ ] It does not include executable implementation instructions.
[ ] It can be executed in a fresh agent session using files only.
```

---

## 23. Recommended Prompt to Generate the Executable Stage 6 SKILL

Use this prompt after saving this template.

```text
You are creating an executable reusable SKILL.md for Stage 6 Data Design in a Manual Agentic Coding Workflow.

Use the following source documents:
- /workflow_templates/core/core_skill_template.md
- /workflow_templates/stage_templates/06_data_design_skill_template.md
- agentic-coding-workflow-concept-and-design.md
- skill-template-design-principles.md
- workflow_folder_structure_guide.md

Target output:
- /skills/06_data_design/SKILL.md

Create a reusable SKILL.md that an agent can actually execute.

Rules:
1. Follow the core skill template.
2. Implement the Stage 6 Data Design template.
3. Do not create project artifacts under /workflow.
4. Do not create project-specific schema, database tables, UI, tasks, tests, or implementation code.
5. Define required inputs and conditional inputs.
6. Define mandatory and conditional artifacts.
7. Include N/A record rules.
8. Define the execution procedure.
9. Define traceability rules.
10. Define decision / assumption / open question handling.
11. Define context_packet.md update rules for Stage 7.
12. Include a human approval gate.
13. Keep the SKILL reusable across projects.
```
