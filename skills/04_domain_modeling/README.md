# 04 Domain Modeling / DDD Skill Package

## What this stage package is for

This reusable skill package runs Stage 04 Domain Modeling / DDD in a split Stage Facade Pattern. The parent `SKILL.md` is the public stage entrypoint; the five sub-skills perform the internal work in sequence and the finalizer consolidates the official Stage 4 artifacts.

The stage models domain meaning, language, rules, consistency boundaries, events, and bounded contexts before architecture, data design, API design, UI design, implementation, or test-command design.

## When to use it

Use this package after Stage 03 Requirements & Acceptance Criteria has produced approved or clearly reviewable requirements and acceptance criteria.

Use it when the project has domain terminology, roles, permissions, workflows, approvals, scoring, lifecycle states, policy rules, audit needs, data governance, external systems, or other business rules that later implementation must preserve.

## When not to use it

Do not use this package to design database tables, API endpoints, UI screens, architecture style, implementation tasks, test commands, or code. Do not use it to invent new requirements or approve product scope.

## Required inputs before running

Verify these exist and are approved or clearly marked as draft/reviewable before running sub-skills:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`
- `/workflow/01_goal/01_service_goal.md`
- `/workflow/02_stakeholders_risk/02_stakeholders.md`
- `/workflow/03_requirements/03_requirements.md`
- `/workflow/03_requirements/03_acceptance_criteria.md`

## Optional or conditional inputs

Read these when applicable:

- `/workflow/00_intake/00_project_intake.md`
- `/workflow/00_intake/00_existing_context_review.md`
- `/workflow/02_stakeholders_risk/02_risk_privacy_screening.md`
- `/workflow/03_requirements/03_traceability_matrix.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/04_domain/USER_DIRECTIVES.md`
- `/workflow/04_domain/review_notes.md`
- `/workflow_templates/specializations/*.md`

## Sub-skill execution order

Run the sub-skills in this order. Do not skip the finalizer.

1. `/skills/04_domain_modeling/04a_ubiquitous_language/SKILL.md`
2. `/skills/04_domain_modeling/04b_domain_concepts_entities_values/SKILL.md`
3. `/skills/04_domain_modeling/04c_aggregates_rules_lifecycle/SKILL.md`
4. `/skills/04_domain_modeling/04d_events_bounded_contexts/SKILL.md`
5. `/skills/04_domain_modeling/04e_domain_modeling_finalizer/SKILL.md`

## Official outputs created by the stage

Downstream stages may rely only on approved official Stage 4 artifacts, not on sub-skill folders or prompt history.

Mandatory official artifacts:

- `/workflow/04_domain/04_ubiquitous_language.md`
- `/workflow/04_domain/04_domain_model.md`
- `/workflow/04_domain/04_bounded_contexts.md`
- `/workflow/04_domain/04_business_rules_invariants.md`
- `/workflow/04_domain/04_domain_events.md`
- `/workflow/04_domain/04_domain_traceability_matrix.md`
- `/workflow/04_domain/result.md`
- `/workflow/context/context_packet.md`

Conditional artifacts:

- `/workflow/04_domain/04_state_lifecycle.md`
- `/workflow/04_domain/04_context_map.md`
- `/workflow/04_domain/04_domain_risk_notes.md`
- `/workflow/04_domain/04_domain_model_diagrams.md`
- `/workflow/04_domain/04_domain_open_questions.md`

Skipped conditional artifacts must be recorded with N/A rationale in `/workflow/04_domain/result.md`.

## Internal working artifacts

The internal sub-skills update official Stage 4 draft artifacts. However, Stage 4 is not ready for downstream use until `04e_domain_modeling_finalizer` has consolidated outputs and the human developer has reviewed and approved the official artifacts.

## Human approval requirements

Human approval is required for:

- preferred ubiquitous language terms;
- entity and value object classifications;
- aggregate roots and aggregate boundaries;
- business rules and invariants;
- state lifecycle model, if applicable;
- domain events;
- bounded contexts and context relationships;
- single-context rationale, if applicable;
- substantial unresolved domain assumptions.

The finalizer prepares the approval gate. It does not approve artifacts on behalf of the human developer.

## How to run this package in an Agentic Coding tool

1. Start from the parent `SKILL.md` to understand the public stage contract.
2. Run each sub-skill in the required order.
3. Use a clean or bounded context session between sub-skills if helpful, relying on saved artifacts rather than chat history.
4. After each sub-skill, review its handoff notes before running the next sub-skill.
5. Run the finalizer before requesting Stage 4 approval.

## Relationship to previous and next stages

Previous stage: `03_requirements_acceptance`.

Stage 4 reads approved Stage 1, Stage 2, and Stage 3 artifacts and converts them into a domain model. Stage 5 Architecture & Technical Contracts must read approved Stage 4 official artifacts after human approval, not internal sub-skill outputs.

## Status meanings

- `Draft`: Agent-generated or revised artifact that has not been approved.
- `Needs Review`: Artifact is ready for human review but has unresolved issues or approval needs.
- `Approved`: Human developer explicitly approved the artifact or decision.

## Common mistakes to avoid

- Treating sub-skill outputs as approved final artifacts.
- Skipping the finalizer.
- Designing database tables, API endpoints, or architecture modules during Stage 4.
- Converting every noun into an entity.
- Treating aggregates as data containers.
- Treating bounded contexts as microservices by default.
- Updating `DECISIONS.md` without explicit human approval.

## Troubleshooting / blocker cases

Stop or produce a blocker report if:

- requirements or acceptance criteria are missing or contradictory;
- stakeholder roles are missing but role semantics drive the domain;
- artifact approval status cannot be determined;
- privacy/security constraints conflict with domain operations;
- existing-system terminology conflicts with approved terminology;
- sub-skill outputs contradict each other and cannot be safely reconciled.

## Recommended next step after successful execution

After the finalizer runs, the human developer should review and approve or revise the Stage 4 official artifacts. Only then should Stage 5 Architecture & Technical Contracts use them as source of truth.
