# 08 Test Strategy & Validation Harness

## 1. What this SKILL package is for

This reusable Stage 8 SKILL package defines the project's validation structure before Stage 9 Task Breakdown and before implementation begins.

It converts approved requirements, acceptance criteria, architecture decisions, data/security constraints, and MVP scope into:

- a test strategy;
- acceptance test specifications;
- validation commands or command placeholders;
- manual and specialized validation plans;
- traceability handoff for implementation task planning.

This package uses a split Stage Facade Pattern. The parent `SKILL.md` is the stage entrypoint and orchestrator. The actual work is performed by ordered internal sub-SKILLs, followed by a finalizer.

## 2. When to use it

Use this package when:

- Stage 3 requirements and acceptance criteria are available;
- Stage 5 architecture direction is available;
- Stage 6 data design is available if persistent data exists;
- Stage 7 MVP scope and release slicing are available;
- the next stage is Stage 9 Task Breakdown;
- implementation should be test-first or at least test-aware.

## 3. When not to use it

Do not use this package to:

- implement product code;
- implement test files;
- run final QA after implementation;
- perform Stage 12 release readiness review;
- rewrite requirements, architecture, data design, or MVP scope;
- create Stage 9 task cards;
- treat command placeholders as confirmed commands.

## 4. Required inputs before running

The package normally requires these approved or review-ready inputs:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/03_requirements/03_requirements.md`
- `/workflow/03_requirements/03_acceptance_criteria.md`
- `/workflow/05_architecture/05_architecture_plan.md`
- `/workflow/07_mvp_release/07_mvp_scope.md`

If `USER_DIRECTIVES.md` exists at `/workflow/08_test_strategy/USER_DIRECTIVES.md`, it must be read before executing any sub-SKILL.

## 5. Optional or conditional inputs

Read these only when applicable:

- `/workflow/00_intake/00_existing_context_review.md` for brownfield or existing-system validation.
- `/workflow/02_stakeholders_risk/02_risk_privacy_screening.md` for roles, permissions, privacy, compliance, abuse, or operational risk.
- `/workflow/04_domain/04_business_rules_invariants.md` for domain invariants, state transitions, and lifecycle rules.
- `/workflow/04_domain/04_domain_events.md` for event-driven or async workflows.
- `/workflow/05_architecture/05_api_contracts.md` for API validation.
- `/workflow/05_architecture/05_integration_contracts.md` for external services, webhooks, queues, LLM/model APIs, or third-party integrations.
- `/workflow/05_architecture/05_module_boundaries.md` for module, contract, or boundary tests.
- `/workflow/06_data/*` for persistent data, access rules, migrations, indexes, query patterns, or data security.
- `/workflow/07_mvp_release/07_release_slices.md` when validation differs by release slice.
- `/workflow/07_mvp_release/07_out_of_scope.md` when validation scope must explicitly exclude non-MVP behavior.

## 6. Sub-SKILL execution order

Run the sub-SKILLs in this order:

```text
08a_validation_scope_strategy
→ 08b_acceptance_test_design
→ 08c_validation_commands_harness
→ 08d_manual_specialized_validation
→ 08e_test_strategy_finalizer
```

The finalizer is required. Stage 8 is not ready for downstream use until `08e_test_strategy_finalizer` has consolidated the official artifacts and prepared the human approval gate.

## 7. Outputs created when the package is executed

Mandatory official Stage 8 artifacts:

- `/workflow/08_test_strategy/08_test_strategy.md`
- `/workflow/08_test_strategy/08_acceptance_tests.md`
- `/workflow/08_test_strategy/08_validation_commands.md`
- `/workflow/08_test_strategy/08_manual_test_plan.md`
- `/workflow/08_test_strategy/result.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`
- `/workflow/context/context_packet.md`

Conditional artifacts may be created when applicable:

- `/workflow/08_test_strategy/08_test_data_fixtures.md`
- `/workflow/08_test_strategy/08_ci_validation_plan.md`
- `/workflow/08_test_strategy/08_security_privacy_tests.md`
- `/workflow/08_test_strategy/08_performance_validation.md`
- `/workflow/08_test_strategy/08_accessibility_validation.md`
- `/workflow/08_test_strategy/08_regression_baseline.md`
- `/workflow/08_test_strategy/08_model_or_data_evaluation_plan.md`
- `/workflow/08_test_strategy/08_mobile_platform_validation.md`

If a conditional artifact is not applicable, the finalizer must record an N/A rationale with the artifact name, why it is not applicable, and what change would make it applicable later.

## 8. Human approval requirements

Human approval is required before Stage 9 relies on Stage 8 outputs.

The approval gate must cover:

- automated MVP test scope;
- manual MVP validation scope;
- validation commands or command placeholders;
- CI validation expectations;
- security/privacy validation scope;
- performance/accessibility validation scope, if applicable;
- accepted validation gaps;
- test data and fixture assumptions;
- manual-only validation assumptions;
- unresolved open questions that affect task cards.

Do not record anything in `DECISIONS.md` unless explicit human approval exists.

## 9. How to run this package in an Agentic Coding tool

1. Start from `/skills/08_test_strategy_validation/SKILL.md` to understand the public stage contract and execution order.
2. Run `08a_validation_scope_strategy/SKILL.md` and review the draft strategy.
3. Run `08b_acceptance_test_design/SKILL.md` to create acceptance test specifications.
4. Run `08c_validation_commands_harness/SKILL.md` to define commands, fixtures, harness needs, and CI applicability.
5. Run `08d_manual_specialized_validation/SKILL.md` to define manual and specialized validation.
6. Run `08e_test_strategy_finalizer/SKILL.md` to consolidate outputs, update traceability and context, and prepare approval.
7. Human developer reviews and approves, requests revision, or records blockers.

A new agent session should be able to run any sub-SKILL from files alone. Do not rely on chat history as source of truth.

## 10. Relationship to previous and next stages

Previous stage: `07_mvp_release_slicing`

Stage 8 uses approved MVP and release slicing decisions to decide what must be validated now, what is deferred, and what is explicitly out of scope.

Next stage: `09_task_breakdown`

Stage 9 may depend only on approved official Stage 8 artifacts, not on internal sub-SKILL names, prompt history, or unapproved drafts.

## 11. How to interpret status values

- `Draft`: Agent-created or revised output that has not been approved.
- `Needs Review`: Output appears complete enough for human review but still requires approval.
- `Approved`: Human explicitly approved the artifact or decision.

An agent output is not approved simply because it exists.

## 12. Common mistakes to avoid

- Skipping the finalizer.
- Treating sub-SKILL outputs as approved stage artifacts.
- Making Stage 9 depend on internal sub-SKILL paths.
- Inventing exact test commands when tooling is unknown.
- Reducing all validation to E2E tests.
- Leaving manual tests without pass/fail criteria.
- Ignoring security, privacy, authorization, and data-access validation.
- Including later-release or out-of-scope features in MVP validation.
- Updating `DECISIONS.md` without explicit human approval.

## 13. Troubleshooting / blocker cases

Produce a blocker report if:

- approved requirements are missing;
- acceptance criteria are missing;
- approved MVP scope is missing;
- MVP scope conflicts with requirements;
- architecture boundaries are missing where validation depends on them;
- data access or privacy rules are missing for sensitive data;
- user directives conflict with approved decisions;
- Stage 8 artifacts disagree and cannot be reconciled safely.

A blocker report should include the blocking issue, why it matters, affected artifacts or stages, safe partial work completed, and the human decision needed.

## 14. Recommended next step after successful execution

After `08e_test_strategy_finalizer` completes and the human developer approves the official Stage 8 artifacts, proceed to:

```text
/skills/09_task_breakdown/SKILL.md
```

Stage 9 should use approved Stage 8 artifacts to attach required tests, validation commands, manual checks, and evidence expectations to implementation task cards.
