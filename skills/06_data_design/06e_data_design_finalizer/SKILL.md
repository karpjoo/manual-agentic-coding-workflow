---
name: 06e_data_design_finalizer
description: Consolidate Stage 6 Data Design artifacts, resolve contradictions, update traceability, record N/A items, prepare result.md, update context_packet.md for Stage 7, and present the human approval gate.
stage: 06 Data Design
parent_skill: /skills/06_data_design/SKILL.md
subskill_id: 06e
subskill_order: 5
previous_subskill: /skills/06_data_design/06d_security_retention_migration/SKILL.md
next_subskill: /skills/07_mvp_release_slicing/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/06_data/result.md
requires_human_approval: true
external_visibility: internal
---

# 06e Data Design Finalizer

## 1. Purpose

This sub-skill finalizes Stage 6 Data Design. It consolidates outputs from prior Stage 6 sub-skills, detects contradictions, updates traceability, records N/A items, prepares `/workflow/06_data/result.md`, updates `/workflow/context/context_packet.md` for Stage 7, and presents the human approval gate.

The finalizer does not make agent proposals automatically approved decisions.

## 2. Core Question

```text
Are the Stage 6 data design artifacts complete, consistent, traceable, and safe enough for human review and downstream MVP slicing?
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
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_query_patterns.md
```

### Read If Applicable

Read every Stage 6 conditional artifact that exists:

```text
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_indexes.md
/workflow/06_data/06_data_security_rules.md
/workflow/06_data/06_retention_deletion_policy.md
/workflow/06_data/06_migration_plan.md
/workflow/06_data/06_data_dictionary.md
/workflow/06_data/06_seed_fixture_strategy.md
/workflow/06_data/06_external_data_mapping.md
/workflow/06_data/06_event_data_model.md
/workflow/06_data/06_analytics_reporting_model.md
/workflow/06_data/06_blob_object_storage_model.md
```

Also read applicable Stage 5 artifacts if needed to verify consistency:

```text
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_authz_model.md
/workflow/05_architecture/05_event_contracts.md
/workflow/05_architecture/05_observability_policy.md
/workflow/05_architecture/05_error_handling_policy.md
```

### Do Not Read By Default

```text
- implementation source files
- tests
- generated database files
- downstream task or implementation prompts
- historical chat logs
- rejected artifacts except REJECTED_OPTIONS.md or explicitly relevant supersession notes
```

## 4. Preflight Procedure

```text
[ ] Confirm prior Stage 6 mandatory artifacts exist.
[ ] Identify all existing conditional artifacts.
[ ] Identify expected conditional artifacts that are missing and need N/A records.
[ ] Verify that Stage 6 outputs are based on approved upstream artifacts or clearly marked draft assumptions.
[ ] Check contradictions among conceptual model, logical schema, query patterns, physical schema, indexes, security rules, retention policy, and migration plan.
[ ] Check whether any blocker prevents Stage 6 approval.
```

## 5. Missing Input Handling

Blocking gaps:

```text
- conceptual data model missing
- logical schema missing
- query patterns missing
- required security or retention artifact missing while personal/sensitive data exists
- migration plan missing while existing data migration or seed/reference data is in scope
- unresolved contradiction between architecture and data design
```

If blocking, produce a Blocker Report in `result.md` and do not mark the stage ready for approval.

## 6. Execution Procedure

### Step 1. Consolidate Official Artifacts

Review the mandatory and conditional Stage 6 artifacts. Ensure they use stable IDs and do not contradict each other.

Mandatory artifacts:

```text
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_query_patterns.md
/workflow/06_data/06_data_design_traceability.md
/workflow/06_data/result.md
/workflow/context/context_packet.md
```

Conditional artifacts:

```text
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_indexes.md
/workflow/06_data/06_data_security_rules.md
/workflow/06_data/06_retention_deletion_policy.md
/workflow/06_data/06_migration_plan.md
/workflow/06_data/06_data_dictionary.md
/workflow/06_data/06_seed_fixture_strategy.md
/workflow/06_data/06_external_data_mapping.md
/workflow/06_data/06_event_data_model.md
/workflow/06_data/06_analytics_reporting_model.md
/workflow/06_data/06_blob_object_storage_model.md
```

### Step 2. Check Consistency

Check consistency across:

```text
- conceptual data objects and logical schema objects
- logical schema and query patterns
- query patterns and indexes
- ownership boundaries and security rules
- sensitivity classification and retention/deletion policy
- physical schema and approved architecture decisions
- migration plan and existing/brownfield constraints
- external/event/blob/analytics data models and architecture contracts
```

Record contradictions as blockers, risks, or open questions depending on severity.

### Step 3. Record N/A Items

For every conditional artifact not produced, record an N/A item in `/workflow/06_data/result.md` with:

```text
- artifact name
- why it is not applicable now
- which approved input supports this conclusion, if any
- what future change would make it applicable
- whether human confirmation is needed
```

Use this format:

```markdown
| Artifact | Why Not Applicable | Revisit If | Human Confirmation Needed |
|---|---|---|---|
| 06_migration_plan.md | ... | ... | Yes/No |
```

### Step 4. Create Data Design Traceability

Create or update:

```text
/workflow/06_data/06_data_design_traceability.md
```

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

### Step 5. Update Workflow Traceability Context

Update `/workflow/context/TRACEABILITY_MATRIX.md` if the workflow permits direct update in this stage.

If direct update is not appropriate, record exact updates needed in:

```text
/workflow/06_data/06_data_design_traceability.md
```

Do not break existing upstream IDs.

### Step 6. Prepare Result Artifact

Create or update:

```text
/workflow/06_data/result.md
```

Required structure:

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

### Step 7. Update Context Files

Update or prepare these files as appropriate:

```text
/workflow/context/context_packet.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Do not update `/workflow/context/DECISIONS.md` unless the human has explicitly approved the decision.

### Step 8. Prepare Stage 7 Handoff

The Stage 7 handoff in `context_packet.md` must include only minimal operational context:

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
- High-risk data features
- Expensive migrations or schema choices
- Security/privacy-sensitive data features
- Query/index work that may affect release slicing

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

## 7. Classification Rules

### Approved Decision

Use only when explicit human approval exists.

### Decision Candidate

Use for recommended choices that require approval.

### Working Assumption

Use for temporary assumptions needed for progress.

### Open Question

Use for unresolved issues that may affect schema, security, migration, retention, MVP slicing, tests, tasks, or implementation.

### Rejected Option

Use for explicitly rejected or superseded schema, storage, security, migration, or retention options.

### Recommendation

Use for non-binding suggestions. Do not treat recommendations as decisions.

## 8. Validation Checklist

```text
[ ] Data design is derived from approved requirements, domain model, and architecture artifacts.
[ ] Conceptual, logical, and physical design levels are separated.
[ ] Mandatory artifacts exist or blockers are reported.
[ ] Conditional artifacts exist or N/A rationale is recorded.
[ ] Source-of-truth, derived, cached, temporary, audit, and external data are distinguished.
[ ] Logical schema defines fields, relationships, constraints, lifecycle states, and validation rules.
[ ] Physical schema is only final if storage technology is approved.
[ ] Query patterns link to requirements, APIs, screens, jobs, reports, or integrations.
[ ] Indexes are justified by query patterns, constraints, sorting/filtering, pagination, or security-rule needs.
[ ] Ownership and bounded-context/module ownership are explicit.
[ ] Security rules map to approved roles, permissions, and access-control decisions.
[ ] Sensitive, personal, or regulated data is identified and handled explicitly.
[ ] Retention, deletion, archival, audit, backup, migration, seed, and fixture needs are addressed or recorded as open questions/N/A.
[ ] Traceability links from requirements/domain/architecture to data objects are preserved.
[ ] Decision candidates are not treated as approved decisions.
[ ] Working assumptions are recorded separately from requirements and decisions.
[ ] Open questions affecting Stage 7 are visible.
[ ] context_packet.md is prepared for Stage 7.
```

## 9. Human Approval Gate

End with this section in `/workflow/06_data/result.md`.

```markdown
## Human Approval Required

### Decisions to Approve
- Conceptual data model
- Logical schema
- Physical schema, if applicable
- Data ownership and source-of-truth boundaries
- Access-control and data security rule direction
- Retention/deletion policy direction
- Migration and seed strategy, if applicable
- Major normalization / denormalization trade-offs
- Indexes required for MVP, if applicable
- Conditional artifacts marked N/A

### Assumptions to Confirm
- Expected data volume and query frequency assumptions
- MVP vs later-release data needs
- Personal/sensitive data classifications
- Default retention/deletion behavior
- Default audit logging behavior
- Database-specific capabilities or limitations
- Migration or seed data assumptions

### Open Questions to Resolve
- Unresolved schema choices affecting implementation
- Unresolved access-control rules affecting security
- Unresolved retention/deletion rules affecting compliance or privacy
- Unresolved external data ownership or synchronization rules
- Unresolved query patterns affecting indexes or release slicing
- Unresolved migration risks affecting MVP feasibility

### Risks to Review
- Schema coupling across bounded contexts
- Over-denormalization or premature optimization
- Missing indexes for required query patterns
- Data leakage through overly broad read access
- Inconsistent authorization between API and database layers
- Retention or deletion gaps
- Migration risk
- Audit log privacy risk
- Unbounded data growth

### Artifacts Ready for Review
- /workflow/06_data/06_conceptual_data_model.md
- /workflow/06_data/06_logical_schema.md
- /workflow/06_data/06_query_patterns.md
- /workflow/06_data/06_data_design_traceability.md
- /workflow/06_data/result.md
- Applicable conditional artifacts

### Recommended Next Step
- After human approval, proceed to Stage 7 MVP Scope & Release Slicing using approved Stage 6 official artifacts as source of truth.
```

## 10. Failure Handling

If the stage cannot be finalized safely, create this section in `result.md`:

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

## 11. Do Not Do

Do not:

```text
- approve the stage on behalf of the human developer
- update DECISIONS.md without explicit human approval
- hide contradictions among data artifacts
- mark conditional artifacts N/A without rationale
- let downstream stages depend on internal sub-skill outputs
- copy entire Stage 6 artifacts into context_packet.md
- treat context_packet.md as the sole source of truth
- create implementation code, database migrations, tests, ORM models, or security-rule files
- ignore personal/sensitive data, retention, deletion, access-control, or migration blockers
```
