---
name: 06d_security_retention_migration
description: Define data access rules, sensitive-data handling, retention/deletion policy, migration/seed strategy, and applicable external/event/blob/analytics data models.
stage: 06 Data Design
parent_skill: /skills/06_data_design/SKILL.md
subskill_id: 06d
subskill_order: 4
previous_subskill: /skills/06_data_design/06c_physical_schema_indexes/SKILL.md
next_subskill: /skills/06_data_design/06e_data_design_finalizer/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/06_data/06_data_security_rules.md
requires_human_approval: true
external_visibility: internal
---

# 06d Security, Retention, and Migration

## 1. Purpose

This sub-skill defines data security rules, retention/deletion policy, migration/seed strategy, and specialized data models for external, event, analytics, blob/object, or fixture data when applicable.

It expresses rule intent and design decisions. It does not write implementation code, database rule files, migration scripts, ORM models, or tests.

## 2. Core Question

```text
How must each data object be protected, retained, deleted, migrated, seeded, synced, audited, exported, or purged so that the data design is safe, traceable, and ready for MVP slicing?
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
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_query_patterns.md
```

### Read If Applicable

```text
/workflow/05_architecture/05_authz_model.md
- if roles, permissions, tenants, ownership, row/document-level access, or policy-based access exists

/workflow/05_architecture/05_api_contracts.md
- if APIs create, read, update, delete, export, or validate stored data

/workflow/05_architecture/05_integration_contracts.md
- if external data is synced, transformed, imported, exported, or used as source of truth

/workflow/05_architecture/05_event_contracts.md
- if event data is stored, replayed, audited, or consumed asynchronously

/workflow/05_architecture/05_observability_policy.md
- if audit logs, metrics, traces, or operational telemetry store user or system data

/workflow/05_architecture/05_error_handling_policy.md
- if validation errors, retries, dead-letter records, or idempotency records are persisted

/workflow/06_data/06_physical_schema.md
- if physical schema exists

/workflow/06_data/06_indexes.md
- if index design affects security-rule evaluation or migration rollout

/workflow/00_intake/00_existing_context_review.md
- if brownfield migration, import, cleanup, or compatibility constraints exist
```

### Do Not Read By Default

```text
- source code or rule implementation files
- production data dumps
- raw personal data samples
- unrelated operational logs
- superseded security or migration proposals
```

## 4. Preflight Procedure

```text
[ ] Confirm data objects and logical schema exist.
[ ] Identify all personal, sensitive, regulated, audit, and external data.
[ ] Confirm whether an authorization model exists if data visibility depends on roles or ownership.
[ ] Identify missing privacy, deletion, or retention requirements.
[ ] Confirm whether migration, seed, fixture, external mapping, event model, analytics model, or blob storage model is applicable.
```

## 5. Missing Input Handling

Blocking gaps:

```text
- personal/sensitive data exists but privacy/security direction is missing
- role/ownership-based access exists but authorization model is missing
- brownfield migration is in scope but existing schema/source data context is unavailable
- external source-of-truth ownership is unresolved
- legal/compliance retention requirement is referenced but undefined
```

Do not produce final security, retention, or migration artifacts when these blockers exist. Produce a Blocker Report.

Non-blocking gaps may be recorded as assumptions or open questions when a draft policy can safely proceed.

## 6. Execution Procedure

### Step 1. Define Data Security Rules

For each data object, define who can:

```text
- create
- read
- update
- delete
- export
- restore
- access audit/history data
```

Record:

```text
- actor / role / system
- condition
- enforcement layer: database, backend service, API gateway, application, or hybrid
- validation before write
- sensitive fields requiring masking, encryption, or exclusion
- audit log requirements
- failure behavior
- test implication
```

### Step 2. Identify Field-Level Protection Needs

For sensitive fields, record:

```text
- whether field must be masked
- whether field must be encrypted or otherwise protected
- whether field is excluded from normal reads
- whether field is exportable
- whether field appears in logs, metrics, traces, or audit events
- whether field participates in search or indexing
```

### Step 3. Define Retention, Deletion, and Archival Policy

For each relevant data category, define:

```text
- retention period or trigger
- deletion trigger
- soft delete vs hard delete
- archive behavior
- user-requested deletion behavior
- admin purge behavior
- backup retention considerations
- audit retention considerations
- cascade or orphan handling
```

If unknown, record an open question rather than inventing a policy.

### Step 4. Define Migration and Seed Strategy

Create migration or seed strategy if:

```text
- persistent schema is introduced
- existing data must be migrated
- seed/reference data is required
- test fixtures depend on data shape
- indexes or security rules need staged rollout
- backfill or cleanup is required
```

Record:

```text
- migration scope
- source data
- target data
- ordering
- validation checks
- rollback or recovery concept
- environment considerations
- manual approval points
- risks
```

### Step 5. Define Specialized Data Models If Applicable

Create specialized artifacts only if needed:

```text
- external data mapping
- event data model
- analytics/reporting model
- blob/object storage model
- data dictionary
- seed/fixture strategy
```

If not applicable, prepare N/A rationale for the finalizer.

### Step 6. Record Security and Migration Trade-Offs

Classify each trade-off as approved decision used, decision candidate, working assumption, open question, or rejected option.

Examples:

```text
- database-level vs service-layer enforcement
- audit completeness vs privacy minimization
- soft deletion convenience vs retention risk
- raw external payload storage vs normalized mapped records
- fixture realism vs privacy risk
- migration safety vs rollout speed
```

## 7. Output Artifacts

Create or update when applicable:

```text
/workflow/06_data/06_data_security_rules.md
/workflow/06_data/06_retention_deletion_policy.md
/workflow/06_data/06_migration_plan.md
/workflow/06_data/06_seed_fixture_strategy.md
/workflow/06_data/06_external_data_mapping.md
/workflow/06_data/06_event_data_model.md
/workflow/06_data/06_analytics_reporting_model.md
/workflow/06_data/06_blob_object_storage_model.md
/workflow/06_data/06_data_dictionary.md
```

If an artifact is not applicable, prepare an N/A item for `/workflow/06_data/result.md`.

### Data Security Rule Format

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

### Retention / Deletion Rule Format

```markdown
## RET-001 — [[Retention / Deletion Rule Name]]

- Data category:
- Data objects:
- Retention trigger or period:
- Deletion trigger:
- Soft delete / hard delete / archive:
- User-requested deletion behavior:
- Admin purge behavior:
- Audit/backups consideration:
- Cascade/orphan handling:
- Related requirement / risk:
- Open questions:
```

### Migration Item Format

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

### Seed / Fixture Item Format

```markdown
## SEED-001 — [[Seed / Fixture Item Name]]

- Purpose:
- Environment:
- Data objects:
- Source:
- Privacy / sensitivity concerns:
- Required for tests or manual validation:
- Refresh/reset behavior:
- Open questions:
```

## 8. Traceability Rules

Create links:

```text
Data Object → Data Security Rule
Sensitive Data → Security Rule / Retention Rule / Audit Rule
Data Object → Retention / Deletion Policy
Data Object → Migration Item, if applicable
External Integration → External Data Mapping, if applicable
Domain Event → Event Data Model, if applicable
Query Pattern → Security Rule, if authorization affects query shape
```

## 9. Validation Checklist

```text
[ ] Data security rules map to approved roles, permissions, ownership, and architecture decisions.
[ ] Sensitive/personal/regulated fields are identified and protected.
[ ] Enforcement layers are explicit.
[ ] Retention, deletion, archival, backup, and audit considerations are addressed or recorded as open questions.
[ ] Migration, seed, fixture, import/export, and backfill needs are addressed or marked N/A.
[ ] External/event/blob/analytics data models are created only when applicable.
[ ] Security and migration trade-offs are classified correctly.
[ ] No implementation code, rule files, migrations, or tests are created.
```

## 10. Handoff to Finalizer

Prepare notes for `06e_data_design_finalizer`:

```text
- security rules ready for consolidation
- retention/deletion decisions, candidates, and open questions
- migration/seed/external/event/blob/analytics artifacts created or N/A
- blockers affecting Stage 7 MVP slicing
- risks that require human review
- traceability updates to include in the final Stage 6 traceability artifact
```

## 11. Human Approval Gate

Focused review may be requested for:

```text
- access-control rule direction
- enforcement layer choices
- retention/deletion policy direction
- migration/seed strategy
- external data ownership
- audit logging and privacy risk
```

Full Stage 6 approval happens after the finalizer.

## 12. Do Not Do

Do not:

```text
- write executable security rules, migrations, seed scripts, tests, or implementation code
- assume security can be deferred to final release review
- store or expose personal/sensitive data without classification and access rules
- invent retention policy when the requirement is unresolved
- treat application-layer authorization as sufficient without recording database-level risk
- create raw sample personal data or production-like sensitive fixtures
- silently omit migration or seed concerns
```
