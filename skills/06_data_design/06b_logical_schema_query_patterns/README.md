# 06b Logical Schema and Query Patterns

## 1. What this SKILL is for

Convert conceptual data objects into a technology-neutral logical schema and derive query patterns.

This is a reusable skill support guide. It is not a project artifact and it does not replace the executable `SKILL.md`.

## 2. When to use it

Use this sub-skill as part of Stage 6 after the previous required Stage 6 context is available. It answers: What logical records, fields, identifiers, relationships, constraints, lifecycle state fields, and query patterns are needed to support the approved system behavior?

## 3. When not to use it

Do not use it as a standalone replacement for the full Stage 6 package. Do not use it to implement code, migrations, security-rule files, ORM models, or tests.

## 4. Required inputs before running

- `/skills/06_data_design/06a_data_scope_conceptual_model/SKILL.md` — Read the previous sub-skill procedure or use it to understand expected upstream Stage 6 draft artifacts.
- `/workflow/01_goal/01_service_goal.md` — Understand service purpose and success criteria.
- `/workflow/02_stakeholders_risk/02_stakeholders.md` — Understand roles, actors, operators, and affected stakeholders.
- `/workflow/02_stakeholders_risk/02_risk_privacy_screening.md` — Identify personal/sensitive data, security, privacy, and compliance constraints.
- `/workflow/03_requirements/03_requirements.md` — Extract functional and non-functional data needs.
- `/workflow/03_requirements/03_acceptance_criteria.md` — Link data behavior to verifiable acceptance conditions.
- `/workflow/04_domain/04_ubiquitous_language.md` — Use approved domain terms consistently.
- `/workflow/04_domain/04_domain_model.md` — Map data objects to domain concepts, entities, value objects, and aggregates.
- `/workflow/04_domain/04_business_rules_invariants.md` — Preserve invariants, lifecycle rules, and consistency constraints.
- `/workflow/05_architecture/05_architecture_plan.md` — Align data design with architecture direction.
- `/workflow/05_architecture/05_module_boundaries.md` — Identify data ownership and module boundaries.
- `/workflow/05_architecture/05_architecture_decisions.md` — Use approved technical and storage-related decisions.

## 5. Optional or conditional inputs

- `/workflow/00_intake/00_existing_context_review.md` — If this is a brownfield or migration project. Capture existing data stores, constraints, compatibility, and migration risks.
- `/workflow/04_domain/04_bounded_contexts.md` — If bounded contexts exist. Align data ownership with bounded contexts.
- `/workflow/04_domain/04_domain_events.md` — If events, workflows, or async behavior exist. Identify event data, audit trails, and derived projections.
- `/workflow/05_architecture/05_api_contracts.md` — If APIs exist. Derive read/write/query patterns and data contract needs.
- `/workflow/05_architecture/05_integration_contracts.md` — If external systems exist. Map imported, exported, synchronized, and externally owned data.
- `/workflow/05_architecture/05_authz_model.md` — If roles or permissions affect data visibility or mutation. Design data security rules and authorization-aware query constraints.
- `/workflow/05_architecture/05_event_contracts.md` — If async messaging or domain events exist. Define event payload persistence and event-related data models.
- `/workflow/05_architecture/05_observability_policy.md` — If audit, logging, monitoring, or observability data exists. Classify operational data and retention requirements.
- `/workflow/05_architecture/05_error_handling_policy.md` — If error state must be persisted or audited. Design error, retry, dead-letter, or recovery data behavior.

## 6. Outputs created when the SKILL is executed

- `/workflow/06_data/06_logical_schema.md` — Technology-neutral logical schema.
- `/workflow/06_data/06_query_patterns.md` — Query and access patterns derived from requirements and architecture.

These outputs remain drafts until human approval is explicit.

## 7. Human approval requirements

The human developer must review and approve or reject:

- logical schema structure
- constraints and validation rules
- query pattern coverage
- authorization-aware query notes
- denormalization or caching candidates

Do not record approval in `DECISIONS.md` unless the human developer explicitly approves the decision.

## 8. How to run the SKILL in an Agentic Coding tool

1. Start from a clean or clearly bounded session when possible.
2. Open and follow the relevant `SKILL.md`.
3. Read standard workflow context files first.
4. Read `USER_DIRECTIVES.md` in `/workflow/06_data` if it exists.
5. Read only the required and applicable inputs.
6. Produce or update only the artifacts listed by the SKILL.
7. Record decision candidates, assumptions, open questions, risks, and N/A items separately.
8. Stop for human review where the SKILL requires approval.


## 9. Relationship to previous and next stages

- Previous stage or sub-skill: `/skills/06_data_design/06a_data_scope_conceptual_model/SKILL.md`
- Next stage or sub-skill: `06c Physical Schema and Indexes`

Downstream work must rely on approved official artifacts, not prompt history or internal notes.

## 10. How to interpret Draft, Approved, and Needs Review

- `Draft`: Agent-produced or revised artifact that has not been explicitly approved.
- `Approved`: Human-approved artifact or decision that downstream stages may treat as source of truth.
- `Needs Review`: Artifact has known gaps, conflicts, assumptions, or decision candidates requiring human review.

## 11. Common mistakes to avoid

- Treating an agent proposal as an approved schema decision.
- Using `context_packet.md` as the only source of truth.
- Reading all historical files instead of the required inputs.
- Silently converting missing information into assumptions.
- Creating implementation code, migrations, security-rule files, ORM models, or tests during Stage 6 design.
- Letting downstream stages depend on sub-skill folders or prompt history.

## 12. Troubleshooting / blocker cases

Stop and produce a blocker report if:

- approved requirements are missing;
- approved architecture direction is missing;
- domain model or equivalent domain context is missing;
- persistence is required but storage direction is unknown;
- personal or sensitive data exists but privacy/security screening is missing;
- authorization affects data access but the authz model is missing;
- source artifacts conflict in ways that affect schema, access control, privacy, migration, or release feasibility.

A blocker report should identify the blocking issue, why it matters, affected artifacts or stages, safe partial work completed, and the human decision needed.

## 13. Recommended next step after successful execution

After successful execution, review the created or updated artifacts and resolve approval items before the next sub-skill or downstream stage depends on them.
