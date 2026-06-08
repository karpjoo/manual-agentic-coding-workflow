# 11 TDD Implementation Loop

## 1. What this stage package is for

This reusable stage package coordinates Stage 11 of the Manual Agentic Coding Workflow: implementing approved tasks through a bounded TDD or test-aware loop.

It is a split stage package. The parent `SKILL.md` acts as the public entrypoint and orchestrator. The internal sub-SKILLs perform task preflight, Red test creation, minimal implementation, regression evidence capture, and finalization.

This package is not a one-shot “build the feature” prompt. It should be run one approved `TASK_ID` at a time.

## 2. When to use it

Use this package when:

- Stage 9 task cards are available and approved or explicitly authorized.
- Stage 10 implementation prompts or handoff packets are available and approved or explicitly authorized.
- A stable `TASK_ID` has been selected.
- The selected task defines allowed scope, forbidden changes, required tests, and definition of done.
- The agent can inspect the relevant codebase and tests.
- The expected output is implementation evidence, not new requirements, architecture, or release approval.

## 3. When not to use it

Do not use this package when:

- The task is missing, ambiguous, or unapproved.
- The implementation prompt is missing or unapproved.
- Required scope, test, architecture, data, security, or privacy decisions are unresolved.
- The agent cannot inspect code or tests.
- The user wants Stage 12 review, release, deployment, or handoff instead of implementation.
- The request would require broad redesign beyond the approved task.

## 4. Required inputs before running

Check these context files when they exist:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`

Read these Stage 8–10 artifacts for the selected task:

- `/workflow/08_test_strategy/08_test_strategy.md`
- `/workflow/08_test_strategy/08_validation_commands.md`
- `/workflow/09_tasks/09_task_cards.md`
- `/workflow/09_tasks/09_dependency_order.md`
- `/workflow/10_prompts/10_implementation_prompts.md`
- `/workflow/10_prompts/10_prompt_handoff_packets.md`

If the project uses different paths, preserve the same logical roles.

## 5. Optional or conditional inputs

Read these only when activated by the task card, implementation prompt, context packet, project profile, or `USER_DIRECTIVES.md`:

- `/workflow/03_requirements/03_requirements.md`
- `/workflow/03_requirements/03_acceptance_criteria.md`
- `/workflow/04_domain/04_domain_model.md`
- `/workflow/04_domain/04_business_rules_invariants.md`
- `/workflow/05_architecture/05_architecture_plan.md`
- `/workflow/05_architecture/05_module_boundaries.md`
- `/workflow/05_architecture/05_api_contracts.md`
- `/workflow/05_architecture/05_integration_contracts.md`
- `/workflow/06_data/06_logical_schema.md`
- `/workflow/06_data/06_physical_schema.md`
- `/workflow/06_data/06_migration_plan.md`
- `/workflow/06_data/06_data_security_rules.md`
- `/workflow/12_review_release_handoff/review_notes.md`

Also check `/workflow/11_implementation_results/USER_DIRECTIVES.md` if it exists.

## 6. Sub-SKILL execution order

Run the sub-SKILLs in this order for each selected `TASK_ID`:

1. `11a_task_preflight_and_red_test` — validate the task, inspect code/tests, and write or identify a failing test.
2. `11b_minimal_implementation_green` — make the smallest approved implementation change needed to pass targeted validation.
3. `11c_refactor_regression_evidence` — perform scope-safe refactoring and broader validation, then record evidence.
4. `11d_implementation_finalizer` — consolidate task result, test evidence, traceability, and context handoff for human review.

The finalizer is required before the task output is ready for downstream use.

## 7. Outputs created when the SKILL is executed

Official Stage 11 artifacts include:

- `/workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md`
- `/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md`
- `/workflow/11_implementation_results/result.md`
- `/workflow/context/context_packet.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`

Conditional evidence artifacts may be produced when applicable:

- `/workflow/11_implementation_results/11_manual_verification_{{TASK_ID}}.md`
- `/workflow/11_implementation_results/11_migration_evidence_{{TASK_ID}}.md`
- `/workflow/11_implementation_results/11_api_contract_evidence_{{TASK_ID}}.md`
- `/workflow/11_implementation_results/11_security_privacy_evidence_{{TASK_ID}}.md`
- `/workflow/11_implementation_results/11_ui_evidence_{{TASK_ID}}.md`
- `/workflow/11_implementation_results/11_performance_evidence_{{TASK_ID}}.md`
- `/workflow/11_implementation_results/11_rollback_notes_{{TASK_ID}}.md`

These are project execution artifacts. The files in `/skills/11_tdd_implementation_loop/` are reusable skill files and support contracts.

## 8. Human approval requirements

Human approval is required before Stage 12 or downstream work treats the implementation result as accepted.

At minimum, the human developer should review:

- code change scope;
- test and validation evidence;
- requirement and acceptance-criteria satisfaction;
- security, privacy, data, and API impact;
- known limitations and follow-up tasks;
- any skipped, partial, or failed validation.

Agent output is not approval.

## 9. How to run the SKILL in an Agentic Coding tool

1. Start from the parent skill: `/skills/11_tdd_implementation_loop/SKILL.md`.
2. Select exactly one `TASK_ID` unless explicitly authorizing a small batch.
3. Run the sub-SKILLs in order from 11a to 11d.
4. Review each sub-SKILL result before moving to the next one when the task is high-risk.
5. Do not skip 11d; it prepares the official handoff and approval gate.

## 10. Relationship to previous and next stages

Previous stage: `10_implementation_prompt_writing`.

Stage 11 consumes approved task cards, implementation prompts, validation commands, and relevant project context. It produces implementation result and evidence artifacts.

Next stage: `12_review_release_handoff`.

Stage 12 should depend only on approved official Stage 11 artifacts under `/workflow/11_implementation_results/` and `/workflow/context/`, not on internal sub-SKILL names or prompt history.

## 11. How to interpret status values

- `Draft`: Created by the agent but not yet reviewed or approved.
- `Needs Review`: Ready for human inspection; may still contain risks, assumptions, or open questions.
- `Approved`: Explicitly approved by the human developer.
- `Blocked`: Cannot proceed safely until a blocking issue is resolved.
- `Completed Pending Human Review`: Implementation and evidence appear complete, but approval has not been granted.

## 12. Common mistakes to avoid

- Running implementation before identifying or writing the verification test.
- Combining unrelated tasks into one implementation pass.
- Treating an unapproved implementation prompt as source of truth.
- Making broad architecture, schema, API, or security changes inside a task-level implementation loop.
- Claiming tests passed without command output or evidence.
- Updating `DECISIONS.md` from agent output without explicit human approval.
- Letting Stage 12 depend on internal sub-SKILL outputs instead of official artifacts.

## 13. Troubleshooting / blocker cases

Produce a blocker report when:

- required approved inputs are missing;
- task scope conflicts with user directives or approved decisions;
- a required failing test cannot be identified and no test-aware plan is safe;
- relevant code cannot be inspected;
- validation cannot be run or evidence cannot be captured;
- implementation requires an unapproved architecture, API, data, security, privacy, or dependency decision.

A blocker report should include the blocking issue, why it matters, affected artifacts or stages, safe partial work completed, and the human decision needed.

## 14. Recommended next step after successful execution

After all four sub-SKILLs have run for the selected `TASK_ID`, review:

- `11_task_result_{{TASK_ID}}.md`
- `11_test_evidence_{{TASK_ID}}.md`
- any conditional evidence artifacts
- updated traceability and context handoff

Then either approve the task result for Stage 12 review or request targeted corrections by adding review comments or `USER_DIRECTIVES.md` updates.
