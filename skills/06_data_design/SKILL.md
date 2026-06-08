---
name: 06_data_design
description: Stage 6 entrypoint for designing data structures, access rules, query patterns, indexes, retention/deletion policy, and migration strategy from approved requirements, domain model, and architecture contracts.
stage: 06 Data Design
version: 1.0.0
status: draft
primary_output: /workflow/06_data/result.md
requires_human_approval: true
internal_split: true
---

# 06 Data Design Stage Entrypoint

## 1. Purpose

This is the parent stage-level `SKILL.md` for Stage 6 Data Design in the Manual Agentic Coding Workflow.

Stage 6 converts approved requirements, domain model, and architecture contracts into explicit data structures and data access rules before MVP slicing, test strategy, task breakdown, implementation prompts, or code changes.

This parent skill is an orchestrator. It does not duplicate all sub-skill procedures. Run the sub-skills in order, then run the finalizer before asking the human developer to approve the stage.

## 2. Core Question

```text
Given the approved requirements, domain model, and architecture contracts, what data structures, relationships, constraints, access rules, query patterns, indexes, migration approach, and retention/deletion policies are needed to support the system safely and verifiably?
```

## 3. Public Stage Contract

Downstream stages must depend only on approved official Stage 6 artifacts under `/workflow/06_data` and the workflow context files under `/workflow/context`.

Downstream stages must not depend on:

```text
- internal sub-skill names
- prompt history
- agent chat history
- unapproved drafts
- sub-skill working notes unless promoted into official artifacts
```

The stage is not ready for downstream use until:

```text
1. all applicable sub-skills have run,
2. the finalizer has consolidated the official artifacts,
3. decision candidates, assumptions, open questions, risks, and N/A items are visible,
4. the human developer has reviewed and approved the Stage 6 artifacts or explicitly allowed downstream work to proceed with drafts.
```

## 4. Internal Sub-Skill Sequence

Run the sub-skills in this order.

```text
06a_data_scope_conceptual_model
→ 06b_logical_schema_query_patterns
→ 06c_physical_schema_indexes
→ 06d_security_retention_migration
→ 06e_data_design_finalizer
```

### 06a — Data Scope and Conceptual Model

Purpose:

```text
Identify data design scope, extract data-relevant requirements, classify persistent/non-persistent data, and create the conceptual data model.
```

Primary output:

```text
/workflow/06_data/06_conceptual_data_model.md
```

### 06b — Logical Schema and Query Patterns

Purpose:

```text
Translate conceptual data objects into a technology-neutral logical schema and identify query patterns from requirements, APIs, screens, jobs, reports, and integrations.
```

Primary outputs:

```text
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_query_patterns.md
```

### 06c — Physical Schema and Indexes

Purpose:

```text
Create physical schema and index recommendations only when storage technology, query patterns, constraints, or security rules justify them.
```

Conditional outputs:

```text
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_indexes.md
```

### 06d — Security, Retention, and Migration

Purpose:

```text
Define data security rules, retention/deletion policy, migration/seed strategy, and optional external/event/blob/analytics data models where applicable.
```

Conditional outputs:

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

### 06e — Data Design Finalizer

Purpose:

```text
Consolidate official Stage 6 artifacts, resolve contradictions, update traceability, record N/A items, prepare result.md, update context_packet.md for Stage 7, and present the human approval gate.
```

Primary outputs:

```text
/workflow/06_data/06_data_design_traceability.md
/workflow/06_data/result.md
/workflow/context/context_packet.md
```

## 5. Official Stage Artifacts

### Mandatory Artifacts

The completed stage must produce or update:

```text
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_query_patterns.md
/workflow/06_data/06_data_design_traceability.md
/workflow/06_data/result.md
/workflow/context/context_packet.md
```

### Conditional Artifacts

Produce these only when applicable. If not produced, the finalizer must record an N/A rationale in `/workflow/06_data/result.md`.

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

## 6. Required Inputs

Before running the stage, the agent must check the standard workflow context files when present:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
```

Stage 6 should normally be based on these approved prior-stage artifacts:

```text
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

Conditional inputs may include:

```text
/workflow/00_intake/00_existing_context_review.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_domain_events.md
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_authz_model.md
/workflow/05_architecture/05_event_contracts.md
/workflow/05_architecture/05_observability_policy.md
/workflow/05_architecture/05_error_handling_policy.md
/workflow/07_mvp_release/07_mvp_scope.md, only for a revision pass
/workflow/08_test_strategy/08_test_strategy.md, only for a revision pass
```

## 7. USER_DIRECTIVES.md Handling

If `/workflow/06_data/USER_DIRECTIVES.md` exists, read it before executing any sub-skill.

Classify each directive as one of:

```text
approval, correction, preference, rejection, scope change, constraint, question, or new input
```

Do not treat every directive as a globally approved decision. If a directive conflicts with approved decisions, report the conflict and stop if the conflict affects schema, security, privacy, access control, migration, or release feasibility.

## 8. Missing Input Handling

Blocking missing inputs include:

```text
- missing approved requirements
- missing approved architecture direction
- missing domain model or equivalent domain context
- missing data store / persistence architecture decision, when persistence is required
- missing security/privacy screening when personal or sensitive data exists
- missing authorization model when access control affects data visibility or mutation
```

If a blocking input is missing:

```text
1. stop before producing final data design artifacts,
2. produce a Blocker Report,
3. explain why the missing input affects data design safety or correctness,
4. list safe partial work, if any,
5. request the specific human decision or missing artifact.
```

Non-blocking gaps may be handled as working assumptions only when a draft can safely proceed. Record the assumption, its risk, and an open question.

## 9. Execution Policy

1. Do not run this parent skill as one large uncontrolled data design task.
2. Run each sub-skill in order.
3. Each sub-skill may update official artifacts as drafts.
4. The finalizer consolidates the official Stage 6 artifact set.
5. The finalizer prepares the human approval gate.
6. Do not treat any Stage 6 output as approved until the human developer explicitly approves it.

## 10. Traceability Rule

Preserve and improve links among:

```text
Requirement → Acceptance Criteria → Domain Concept / Aggregate → Architecture Module / API → Data Object → Query Pattern → Index / Security Rule / Migration Item
```

Use Stage 6 ID conventions:

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

Do not invent upstream requirement, acceptance criteria, domain, architecture, or API IDs.

## 11. Human Approval Gate

The stage finalizer must ask the human developer to approve or reject:

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

The finalizer must also list:

```text
- assumptions to confirm
- open questions to resolve
- risks to review
- artifacts ready for review
- recommended next stage
```

## 12. Downstream Handoff Rule

After human approval, Stage 7 MVP Scope & Release Slicing should read approved official Stage 6 artifacts, not internal sub-skill outputs.

The Stage 7 context handoff must highlight:

```text
- data objects required for MVP
- data objects that can be deferred
- high-risk or high-cost data features
- migration dependencies
- security/privacy blockers
- query/index work that affects release slicing
- data features that should be excluded from MVP unless approved
```

## 13. Do Not Do

The agent must not:

```text
- design database tables before reading approved domain and architecture artifacts
- treat the database schema as the domain model
- collapse conceptual, logical, and physical design into one vague schema summary
- create a physical schema if the storage technology is not approved, unless clearly marked as a decision candidate
- create speculative indexes without linked query patterns or constraints
- ignore data security rules because a later review stage exists
- treat application-layer authorization as sufficient without checking database-level access risks
- store personal or sensitive data without classification, access, retention, and deletion notes
- silently omit migration, seed, or fixture concerns
- use unapproved downstream MVP assumptions to remove required data objects
- create implementation code, migrations, ORM models, security-rule files, or tests in this stage
- update DECISIONS.md unless the human explicitly approves a decision
- use context_packet.md as the sole source of truth
- rely on previous chat history
- create README.md or artifact_contract.yml as part of this skill unless explicitly requested
```
