# 05 Architecture & Technical Contracts

## What this SKILL package is for

This reusable stage package guides Stage 5 of the Manual Agentic Coding Workflow. It translates approved goals, requirements, stakeholder/risk context, and domain modeling outputs into architecture direction, module boundaries, technical contracts, architecture-level security/privacy decisions, operational policies, and a handoff for Stage 6 Data Design.

This package uses a split Stage Facade Pattern. The parent `SKILL.md` is the stage entrypoint and orchestrator. The actual work is performed by ordered sub-skills, and the finalizer consolidates the official Stage 5 artifacts.

## When to use it

Use this package after Stage 4 Domain Modeling / DDD has produced approved or explicitly allowed source artifacts. It is appropriate when you need architecture direction before data design, test strategy, task breakdown, implementation prompt writing, or coding.

Use it for greenfield MVPs, prototypes, internal tools, web SaaS, mobile apps, AI/data products, regulated/security-sensitive systems, and brownfield work, with appropriate specialization addenda when available.

## When not to use it

Do not use this package to implement code, design detailed database schema, write migrations, create task cards, write implementation prompts, or perform final release/security review. Those belong to later workflow stages.

Do not use it when Stage 3 requirements or Stage 4 domain artifacts are missing or unapproved, unless the human developer explicitly requests exploratory architecture drafting.

## Required inputs before running

The Stage 5 package expects these approved inputs or explicit permission to use drafts:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/01_goal/01_service_goal.md`
- `/workflow/02_stakeholders_risk/02_stakeholders.md`
- `/workflow/02_stakeholders_risk/02_risk_privacy_screening.md`
- `/workflow/03_requirements/03_requirements.md`
- `/workflow/03_requirements/03_acceptance_criteria.md`
- `/workflow/03_requirements/03_traceability_matrix.md`
- `/workflow/04_domain/04_ubiquitous_language.md`
- `/workflow/04_domain/04_domain_model.md`
- `/workflow/04_domain/04_bounded_contexts.md`
- `/workflow/04_domain/04_business_rules_invariants.md`
- `/workflow/04_domain/04_domain_events.md`

## Optional or conditional inputs

Read these only when applicable:

- `/workflow/00_intake/00_project_intake.md` — if project profile, fixed stack, hosting, platform, or constraints are unclear.
- `/workflow/00_intake/00_existing_context_review.md` — if brownfield, legacy, migration, or existing-system extension work applies.
- `/workflow/04_domain/04_domain_traceability_matrix.md` — if Stage 4 created a separate traceability matrix.
- `/workflow/04_domain/result.md` — if Stage 4 contains architecture-relevant warnings, assumptions, or handoff notes.
- `/workflow/03_requirements/result.md` — if requirements contain unresolved architecture implications.
- `/workflow/02_stakeholders_risk/result.md` — if stakeholder/risk outputs contain unresolved security, privacy, compliance, or operational implications.
- Specialization addenda under `/workflow_templates/specializations/` — if the project profile requires one.

## Sub-skill execution order

Run the sub-skills in this order:

05a. `05a_architecture_drivers_options` — Architecture Drivers & Options
05b. `05b_system_module_boundaries` — System & Module Boundaries
05c. `05c_technical_contracts` — Technical Contracts
05d. `05d_auth_security_operations` — Auth, Security & Operations
05e. `05e_architecture_finalizer` — Architecture Finalizer

The stage is not ready for downstream use until `05e_architecture_finalizer` has run and the human developer has reviewed the official artifacts.

## Outputs created when the SKILL package is executed

### Mandatory official Stage 5 artifacts

- `/workflow/05_architecture/05_architecture_plan.md` — Overall architecture plan, drivers, context, options, recommended direction, cross-cutting policies, and data/test implications.
- `/workflow/05_architecture/05_module_boundaries.md` — Module/component boundaries, responsibilities, dependencies, public interfaces, and forbidden dependencies.
- `/workflow/05_architecture/05_architecture_decisions.md` — Architecture decision records and decision candidates.
- `/workflow/05_architecture/05_architecture_traceability_matrix.md` — Requirement/domain-to-architecture traceability and gaps.
- `/workflow/05_architecture/result.md` — Consolidated Stage 5 result, approval gate, assumptions, open questions, risks, and handoff.
- `/workflow/context/context_packet.md` — Minimal operational context for Stage 6 Data Design.

### Conditional official Stage 5 artifacts

- `/workflow/05_architecture/05_api_contracts.md` — if System exposes APIs, service operations, RPC, GraphQL, server actions, or programmatic interfaces.
- `/workflow/05_architecture/05_integration_contracts.md` — if System communicates with external systems, third-party APIs, identity providers, model services, webhooks, data providers, or external storage.
- `/workflow/05_architecture/05_authn_authz_model.md` — if User accounts, roles, permissions, administrators, protected resources, or protected operations exist.
- `/workflow/05_architecture/05_event_contracts.md` — if Domain events, async messaging, queues, pub/sub, background jobs, webhooks, notifications, or event-driven workflows exist.
- `/workflow/05_architecture/05_security_privacy_architecture.md` — if Personal data, sensitive data, external transfer, LLM/API exposure, compliance concerns, audit needs, or security-sensitive workflows exist.
- `/workflow/05_architecture/05_operational_architecture.md` — if Deployment, hosting, scaling, reliability, observability, environment management, secrets, or operations are significant architecture concerns.
- `/workflow/05_architecture/05_brownfield_compatibility_plan.md` — if Project modifies, extends, migrates, or integrates with an existing system.

If a conditional artifact is not applicable, the finalizer must record an N/A rationale in `/workflow/05_architecture/result.md`.

## Human approval requirements

Human approval is required before Stage 6 Data Design or later stages treat Stage 5 outputs as source of truth.

The human developer must review and approve, reject, or revise:

- architecture direction
- major technical choices
- frontend/backend/service boundary
- module boundaries
- API contracts, if applicable
- integration contracts, if applicable
- authentication and authorization model, if applicable
- event/async contracts, if applicable
- security/privacy architecture direction, if applicable
- operational architecture direction, if applicable
- Stage 6 Data Design handoff assumptions

## How to run this SKILL package in an Agentic Coding tool

Start from the parent `SKILL.md`:

```text
/skills/05_architecture_contracts/SKILL.md
```

Then run each sub-skill in order. Keep project artifacts under `/workflow/05_architecture` and workflow context updates under `/workflow/context`.

Recommended usage pattern:

```text
1. Read /skills/05_architecture_contracts/SKILL.md.
2. Run 05a_architecture_drivers_options.
3. Review the draft architecture drivers and options.
4. Run 05b_system_module_boundaries.
5. Run 05c_technical_contracts.
6. Run 05d_auth_security_operations.
7. Run 05e_architecture_finalizer.
8. Human reviews and approves or requests revision.
```

## Relationship to previous and next stages

Previous stage:

```text
04_domain_modeling
```

Stage 5 reads approved official Stage 4 artifacts, not Stage 4 internal sub-skill outputs.

Next stage:

```text
06_data_design
```

Stage 6 may depend only on approved official Stage 5 artifacts and the updated `/workflow/context/context_packet.md`.

## How to interpret status values

- `Draft`: Agent-created or revised content that has not been approved.
- `Needs Review`: Content is ready for human review, but approval is not yet granted.
- `Approved`: The human developer explicitly approved the artifact or decision.

Agent recommendations are not approved decisions.

## Common mistakes to avoid

- Skipping the finalizer.
- Treating sub-skill outputs as approved Stage 5 artifacts.
- Letting Stage 6 depend on internal sub-skill paths.
- Updating `DECISIONS.md` without explicit human approval.
- Creating detailed database schema during architecture design.
- Implementing code or creating task cards in Stage 5.
- Omitting N/A rationale for conditional artifacts.
- Reviving rejected architecture or technology options without explicit approval.

## Troubleshooting / blocker cases

Stop and produce a blocker report if:

- service goal, requirements, acceptance criteria, or domain model are missing or unapproved;
- role/permission direction is unresolved when authorization is required;
- personal/sensitive data handling direction is unresolved;
- approved decisions conflict on stack, hosting, architecture style, or data ownership;
- a required conditional artifact is missing with no N/A rationale;
- Stage 5 artifacts contradict each other and cannot be safely reconciled.

## Recommended next step after successful execution

After `05e_architecture_finalizer` runs, the human developer should review all official Stage 5 artifacts. After explicit approval, proceed to Stage 6 Data Design using the approved Stage 5 artifacts and `/workflow/context/context_packet.md`.
