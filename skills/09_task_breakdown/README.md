# 09 Task Breakdown SKILL Package

## 1. What this SKILL is for

This reusable SKILL package performs Stage 9 of the Manual Agentic Coding Workflow: converting approved requirements, MVP/release scope, architecture, data design, and validation strategy into small, ordered, traceable implementation tasks.

It is a split stage package. The parent `SKILL.md` acts as the public entrypoint and orchestrator. The sub-SKILLs perform the actual Stage 9 work in sequence.

## 2. When to use it

Use this package after Stage 8 Test Strategy & Validation Harness has produced approved or review-ready validation artifacts and the MVP/release scope is clear.

Use it when you need task cards that can later be transformed into Stage 10 implementation prompts.

## 3. When not to use it

Do not use this package to:

- implement code;
- write implementation prompts;
- invent new requirements;
- expand MVP scope;
- bypass validation planning;
- approve task cards without human review.

## 4. Required inputs before running

The package expects approved or clearly status-marked artifacts from:

- Stage 3 Requirements & Acceptance Criteria;
- Stage 5 Architecture & Technical Contracts;
- Stage 7 MVP Scope & Release Slicing;
- Stage 8 Test Strategy & Validation Harness;
- `/workflow/context` files, including decisions, assumptions, open questions, rejected options, traceability, and approval log.

## 5. Optional or conditional inputs

Read conditional artifacts when they apply:

- Stage 4 domain model, invariants, events, bounded contexts;
- Stage 5 API, integration, and architecture decision artifacts;
- Stage 6 data schema, migration, indexes, and data security rules;
- Stage 0 existing-context review for brownfield work;
- Stage 2 stakeholder/risk/privacy artifacts for security-sensitive work.

## 6. Sub-SKILL execution order

Run the sub-SKILLs in this order:

```text
09a_task_source_mapping
→ 09b_task_inventory_and_cards
→ 09c_dependency_ordering
→ 09d_traceability_and_quality_review
→ 09e_task_breakdown_finalizer
```

The stage is not ready for downstream use until the finalizer has run and the official Stage 9 artifacts have been reviewed.

## 7. Outputs created when executed

Official Stage 9 outputs:

```text
/workflow/09_tasks/09_task_inventory.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_dependency_order.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/09_tasks/result.md
/workflow/context/context_packet.md
```

Conditional outputs may include:

```text
/workflow/09_tasks/09_migration_tasks.md
/workflow/09_tasks/09_security_privacy_tasks.md
/workflow/09_tasks/09_integration_tasks.md
/workflow/09_tasks/09_frontend_backend_coordination.md
/workflow/09_tasks/09_risk_reduction_spikes.md
```

## 8. Human approval requirements

Human approval is required for:

- task inventory;
- task cards;
- task dependency order;
- task sizing and split decisions;
- enabling tasks;
- risk-reduction spikes;
- deferred tasks;
- definition of done;
- Stage 10 prompt writing order.

Agent output is not approval.

## 9. How to run in an Agentic Coding tool

1. Open the parent `SKILL.md` first.
2. Confirm the package structure and execution order.
3. Run each sub-SKILL in order.
4. Review each generated artifact before moving forward if you need intermediate control.
5. Run the finalizer.
6. Review the final human approval gate before Stage 10.

## 10. Relationship to previous and next stages

Previous stage:

```text
08_test_strategy_validation
```

Next stage:

```text
10_implementation_prompt_writing
```

Stage 10 must depend only on approved official Stage 9 artifacts, not internal sub-SKILL outputs or prompt history.

## 11. Status meanings

- `Draft`: Created by the Agent but not approved.
- `Needs Review`: Requires human review before downstream use.
- `Approved`: Explicitly approved by the human developer.

## 12. Common mistakes to avoid

- Running Stage 10 from draft task cards.
- Creating tasks for out-of-scope or rejected features.
- Creating broad tasks such as “build backend”.
- Omitting tests or validation commands from task cards.
- Skipping dependency ordering.
- Treating sub-SKILL internal outputs as downstream source of truth.

## 13. Troubleshooting / blocker cases

Stop and request human decision if:

- approved requirements are missing;
- acceptance criteria are not testable;
- MVP/release scope is missing;
- Stage 8 validation strategy is missing;
- architecture boundaries are too ambiguous for task boundaries;
- USER_DIRECTIVES.md conflicts with approved artifacts.

## 14. Recommended next step after successful execution

After human approval, proceed to:

```text
/skills/10_implementation_prompt_writing/SKILL.md
```

Use the approved Stage 9 task cards and dependency order as the primary input.

