---
name: 09_task_breakdown
description: Orchestrate Stage 9 Task Breakdown by running sub-skills that convert approved scope, architecture, data design, and validation strategy into small, ordered, traceable implementation tasks.
stage: 09 Task Breakdown
version: 1.0.0
status: draft
primary_output: /workflow/09_tasks/result.md
requires_human_approval: true
internal_split: true
---

# 09 Task Breakdown Stage Entrypoint

## 1. Purpose

This SKILL is the stage-level entrypoint for Stage 9 Task Breakdown. It orchestrates sub-skills that convert approved requirements, MVP/release scope, architecture, data design, and validation strategy into implementation-ready task artifacts for Stage 10 Implementation Prompt Writing.

This parent SKILL does not perform all task breakdown work directly. It preserves the public stage boundary and ensures downstream stages depend only on approved official Stage 9 artifacts.

## 2. Public Stage Contract

Official Stage 9 artifacts:

```text
/workflow/09_tasks/09_task_inventory.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_dependency_order.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/09_tasks/result.md
/workflow/context/context_packet.md
```

Conditional Stage 9 artifacts:

```text
/workflow/09_tasks/09_migration_tasks.md
/workflow/09_tasks/09_security_privacy_tasks.md
/workflow/09_tasks/09_integration_tasks.md
/workflow/09_tasks/09_frontend_backend_coordination.md
/workflow/09_tasks/09_risk_reduction_spikes.md
```

Stage 10 must depend only on approved official Stage 9 artifacts, not internal sub-skill paths, prompt history, or unfinalized drafts.

## 3. Internal Sub-Skill Sequence

Run the sub-skills in this order:

```text
09a_task_source_mapping
→ 09b_task_inventory_and_cards
→ 09c_dependency_ordering
→ 09d_traceability_and_quality_review
→ 09e_task_breakdown_finalizer
```

Sub-skill responsibilities:

```text
09a_task_source_mapping
- Map approved inputs to task source candidates.

09b_task_inventory_and_cards
- Create task inventory and detailed task cards.

09c_dependency_ordering
- Order tasks by dependency, risk, validation readiness, and release sequence.

09d_traceability_and_quality_review
- Review coverage, validation linkage, task sizing, and traceability.

09e_task_breakdown_finalizer
- Consolidate official artifacts, update context_packet.md for Stage 10, and present the human approval gate.
```

## 4. Required Inputs

Always read:

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
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
```

Read if applicable:

```text
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_indexes.md
/workflow/06_data/06_migration_plan.md
/workflow/06_data/06_data_security_rules.md
/workflow/00_intake/00_existing_context_review.md
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
```

## 5. USER_DIRECTIVES.md Handling

Check `/workflow/09_tasks/USER_DIRECTIVES.md` before executing sub-skills. Apply directives before agent assumptions, but do not silently override approved decisions. Report conflicts.

## 6. Execution Policy

1. Confirm Stage 9 should run.
2. Confirm the official Stage 9 artifact contract.
3. Run sub-skills in sequence.
4. Do not treat intermediate sub-skill outputs as approved stage artifacts.
5. Require `09e_task_breakdown_finalizer` before Stage 9 can be considered ready for review.
6. Require human approval before Stage 10 relies on Stage 9 outputs.

## 7. Missing Input Handling

If required approved input is missing, draft, superseded, rejected, or conflicting:

1. Report the issue.
2. Explain why it matters.
3. Mark it as blocking or non-blocking.
4. Continue only if safe with an explicitly labeled working assumption.
5. Stop if task decomposition would create unapproved scope or unsafe implementation tasks.

Normally blocking:

```text
- missing approved requirements;
- missing approved acceptance criteria;
- missing approved MVP or release scope;
- missing approved validation strategy;
- missing architecture boundary where task boundaries depend on architecture;
- conflict between out-of-scope items and requested task generation.
```

## 8. Human Approval Gate

Stage 9 requires human approval for:

```text
- task inventory;
- task card set;
- task sizing;
- dependency order;
- tasks marked as enabling tasks;
- tasks marked as risk-reduction spikes;
- deferred tasks;
- definition of done for each task;
- Stage 10 prompt-writing order.
```

## 9. Downstream Handoff Rule

Stage 10 may read:

```text
/workflow/09_tasks/09_task_inventory.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_dependency_order.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/09_tasks/result.md
/workflow/context/context_packet.md
```

Stage 10 must not depend on:

```text
- internal sub-skill folder names;
- sub-skill prompt history;
- unapproved task candidates;
- draft task cards not finalized by 09e;
- assumptions treated as decisions.
```

## 10. Do Not Do

Do not:

```text
- implement code;
- write Stage 10 implementation prompts;
- create tasks for out-of-scope items;
- create tasks for rejected options;
- treat draft task cards as approved;
- skip validation linkage;
- skip dependency ordering;
- skip the finalizer;
- update DECISIONS.md without explicit human approval;
- make downstream stages depend on sub-skill internals.
```

