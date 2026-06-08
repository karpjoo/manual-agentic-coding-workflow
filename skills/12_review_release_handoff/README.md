# 12 Review / Security / Release / Handoff

## What this SKILL package is for

This reusable Stage 12 SKILL package is the final review, release readiness, deployment planning, operations preparation, and documentation handoff stage for the Manual Agentic Coding Workflow.

It is internally split into sub-SKILLs so that review work remains inspectable and stable. The parent `SKILL.md` is the stage entrypoint/orchestrator. The sub-SKILL folders are internal execution units.

## When to use it

Use this package after Stage 11 implementation work has produced task results and test/validation evidence. It is appropriate when a human developer needs a release decision package for an MVP, internal demo, staging release, production release, migration, or handoff.

## When not to use it

Do not use this stage to invent requirements, redesign architecture, write missing features, create test strategy from scratch, or perform retrospective analysis. Use earlier workflow stages for requirements/design/testing and Stage 13 for retrospective and skill improvement.

## Required inputs before running

The stage expects approved or clearly labeled source artifacts, especially:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/01_goal/01_service_goal.md`
- `/workflow/03_requirements/03_requirements.md`
- `/workflow/03_requirements/03_acceptance_criteria.md`
- `/workflow/07_mvp_release/07_mvp_scope.md`
- `/workflow/07_mvp_release/07_release_slices.md`
- `/workflow/08_test_strategy/08_test_strategy.md`
- `/workflow/08_test_strategy/08_validation_commands.md`
- `/workflow/09_tasks/09_task_cards.md`
- `/workflow/09_tasks/09_traceability_matrix.md`
- `/workflow/11_implementation_results/`

## Optional or conditional inputs

Read these only when the project context activates them:

- `/workflow/00_intake/00_existing_context_review.md` — if Project is brownfield, extension, migration, or compatibility-sensitive.
- `/workflow/02_stakeholders_risk/02_risk_privacy_screening.md` — if Roles, personal data, sensitive data, regulatory concerns, external transfer, or abuse risks exist.
- `/workflow/04_domain/04_business_rules_invariants.md` — if Domain invariants, lifecycle rules, or state transitions affect correctness or release risk.
- `/workflow/05_architecture/05_architecture_plan.md` — if Architecture affects deployment, runtime, integration, security, or rollback.
- `/workflow/05_architecture/05_api_contracts.md` — if APIs exist.
- `/workflow/05_architecture/05_integration_contracts.md` — if External integrations exist.
- `/workflow/06_data/06_logical_schema.md` — if Persistent data exists.
- `/workflow/06_data/06_migration_plan.md` — if Schema or data migration is part of release.
- `/workflow/06_data/06_data_security_rules.md` — if Data access rules are security-relevant.

## Sub-SKILL execution order

Run the sub-SKILLs in this order:

1. `12a_code_review/SKILL.md` — Code Review
2. `12b_security_privacy_review/SKILL.md` — Security / Privacy Review
3. `12c_release_deployment_readiness/SKILL.md` — Release / Deployment Readiness
4. `12d_operations_documentation_handoff/SKILL.md` — Operations / Documentation Handoff
5. `12e_review_release_finalizer/SKILL.md` — Review / Release Finalizer

The stage is not ready for downstream use until `12e_review_release_finalizer` has run and the official Stage 12 artifacts have been prepared for human review.

## Outputs created when the SKILL is executed

Mandatory official artifacts:

- `/workflow/12_review_release_handoff/12_code_review.md` — Official code review artifact.
- `/workflow/12_review_release_handoff/12_security_privacy_review.md` — Official security and privacy review artifact.
- `/workflow/12_review_release_handoff/12_release_readiness.md` — Official release readiness artifact.
- `/workflow/12_review_release_handoff/12_documentation_handoff.md` — Official documentation handoff artifact.
- `/workflow/12_review_release_handoff/result.md` — Consolidated Stage 12 result and approval gate.
- `/workflow/context/context_packet.md` — Context handoff prepared for Stage 13.

Conditional official artifacts:

- `/workflow/12_review_release_handoff/12_deployment_plan.md` — if Deployment, hosting, environment promotion, or release execution is in scope.
- `/workflow/12_review_release_handoff/12_operations_runbook.md` — if Operation, monitoring, support, maintenance, or handoff is in scope.
- `/workflow/12_review_release_handoff/12_release_notes.md` — if A versioned release, client handoff, internal MVP release, or production handoff is planned.
- `/workflow/12_review_release_handoff/12_migration_readiness.md` — if Data, schema, identity, storage, or external-system migration is required.
- `/workflow/12_review_release_handoff/12_incident_rollback_plan.md` — if Rollback, recovery, or incident response requires separate detail.
- `/workflow/12_review_release_handoff/12_compliance_review.md` — if Regulated, audit-sensitive, privacy-sensitive, or compliance-sensitive constraints require separate treatment.

If a conditional artifact is not applicable, the finalizer records an N/A rationale in `result.md`.

## Human approval requirements

The agent may recommend release, deployment, risk acceptance, limitation acceptance, operations ownership, or documentation handoff decisions. It must not approve them.

Human approval is required before downstream stages treat Stage 12 outputs as approved release/handoff decisions.

## How to run this SKILL in an Agentic Coding tool

1. Place this package at `/skills/12_review_release_handoff/`.
2. Start from `/skills/12_review_release_handoff/SKILL.md`.
3. Confirm the release candidate or implemented task set under review.
4. Run the sub-SKILLs in the documented order.
5. Review the finalizer output and approve, reject, or defer release decisions.

Do not collapse all sub-SKILLs into one uncontrolled review task.

## Relationship to previous and next stages

Previous stage: `11_tdd_implementation_loop`. Stage 12 depends on implementation results and validation evidence from Stage 11.

Next stage: `13_workflow_retrospective_skill_improvement`. Stage 13 may use only approved or clearly labeled Stage 12 artifacts and the updated `context_packet.md`.

## Draft / Approved / Needs Review

- `Draft`: Created by the agent and not yet approved.
- `Needs Review`: Requires human review because blockers, warnings, assumptions, or open questions remain.
- `Approved`: Explicitly approved by the human developer or recorded in the approval log.

## Common mistakes to avoid

- Treating the agent's release recommendation as approval.
- Deploying without explicit human approval.
- Treating missing validation evidence as passing evidence.
- Exposing secret values while reviewing configuration.
- Skipping the finalizer.
- Letting downstream stages depend on internal sub-SKILL outputs.
- Mixing blockers, warnings, and suggestions into one undifferentiated list.

## Troubleshooting / blocker cases

If approved release scope, implementation evidence, validation evidence, or security/privacy inputs are missing, produce a blocker report instead of pretending release readiness is complete.

If deployment is requested but environment, rollback, migration, or ownership information is missing, classify the gap as a blocker or warning and request human decision.

## Recommended next step after successful execution

After the finalizer has prepared `result.md` and `context_packet.md`, the human developer should review the approval gate. After explicit release/handoff decisions are recorded, proceed to Stage 13 Workflow Retrospective & Skill Improvement.
