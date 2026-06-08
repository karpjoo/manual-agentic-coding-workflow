# 10 Implementation Prompt Writing SKILL

## 1. What this SKILL is for

This reusable SKILL converts approved Stage 9 task cards into bounded, test-aware, evidence-producing implementation prompts for Stage 11 coding agents.

It prepares two kinds of Stage 11 handoff material:

- implementation prompts that define what to change, what not to change, what to inspect first, which tests to run, and what evidence to report;
- prompt handoff packets that allow a fresh coding-agent session to execute one approved task safely.

This SKILL does **not** implement code. It prepares implementation prompts and handoff artifacts only.

## 2. When to use it

Use this SKILL after Stage 9 Task Breakdown has produced task inventory, task cards, dependency order, and task-level traceability.

Use it when:

- task cards are approved or explicitly allowed for draft prompt writing;
- Stage 11 implementation should be performed task by task;
- implementation must stay within approved requirements, architecture, data design, scope, and validation constraints;
- a coding agent needs self-contained prompts that can run in a fresh context window;
- the project needs traceability from requirement to task, prompt, validation, and implementation evidence.

## 3. When not to use it

Do not use this SKILL when:

- the user wants direct code implementation;
- Stage 9 task cards are missing, too broad, or not approved enough to constrain implementation;
- architecture, data design, security, privacy, or validation rules are unresolved in a way that affects implementation scope;
- the current work is review, release, deployment, retrospective, or workflow improvement;
- the goal is to create a project-specific feature, UI, database schema, test suite, or code change directly.

Use a Stage 11 TDD Implementation Loop SKILL for actual implementation.

## 4. Required inputs before running

Before running this SKILL, the agent should check the following workflow context files when available:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`

The main Stage 9 inputs are:

- `/workflow/09_tasks/09_task_inventory.md`
- `/workflow/09_tasks/09_task_cards.md`
- `/workflow/09_tasks/09_dependency_order.md`
- `/workflow/09_tasks/09_traceability_matrix.md`

The SKILL also relies on approved upstream artifacts from requirements, architecture, MVP scope, and test strategy:

- `/workflow/03_requirements/03_requirements.md`
- `/workflow/03_requirements/03_acceptance_criteria.md`
- `/workflow/05_architecture/05_architecture_plan.md`
- `/workflow/05_architecture/05_module_boundaries.md`
- `/workflow/07_mvp_release/07_mvp_scope.md`
- `/workflow/08_test_strategy/08_test_strategy.md`
- `/workflow/08_test_strategy/08_validation_commands.md`

Only approved artifacts should be used as source of truth unless the user explicitly requests exploratory or draft prompt writing.

## 5. Optional or conditional inputs

Read these only when the project profile, task card, current context, or user directive makes them relevant:

- `/workflow/00_intake/00_existing_context_review.md` — for brownfield or existing-codebase projects.
- `/workflow/04_domain/04_ubiquitous_language.md` — when domain terms affect prompt wording.
- `/workflow/04_domain/04_domain_model.md` — when tasks touch entities, value objects, aggregates, or workflows.
- `/workflow/04_domain/04_business_rules_invariants.md` — when tasks touch invariants, validation rules, lifecycle, or state transitions.
- `/workflow/04_domain/04_domain_events.md` — when tasks touch domain events, async workflows, or notifications.
- `/workflow/05_architecture/05_api_contracts.md` — when tasks touch APIs.
- `/workflow/05_architecture/05_integration_contracts.md` — when tasks touch external services, queues, webhooks, or third-party APIs.
- `/workflow/05_architecture/05_architecture_decisions.md` — when prompts must preserve approved trade-offs.
- `/workflow/06_data/06_conceptual_data_model.md` — when tasks touch persistent data concepts.
- `/workflow/06_data/06_logical_schema.md` — when tasks touch data shape, relations, constraints, or ownership.
- `/workflow/06_data/06_physical_schema.md` — when tasks touch implementation-level schema.
- `/workflow/06_data/06_indexes.md` — when tasks touch query patterns or performance-sensitive reads.
- `/workflow/06_data/06_migration_plan.md` — when tasks require migration, seed, backfill, rollback, or compatibility work.
- `/workflow/06_data/06_data_security_rules.md` — when tasks touch authorization, access control, or privacy-sensitive data.
- `/workflow/08_test_strategy/08_acceptance_tests.md` — when acceptance tests are defined separately.
- `/workflow/08_test_strategy/08_manual_test_plan.md` — when manual validation is required.
- `/workflow/09_tasks/09_task_risk_notes.md` — when task-specific risk notes exist.
- `/workflow/10_prompts/USER_DIRECTIVES.md` — when stage-local human instructions exist.

## 6. Outputs created when the SKILL is executed

Mandatory project artifacts created or updated by Stage 10 execution:

- `/workflow/10_prompts/10_implementation_prompts.md`
- `/workflow/10_prompts/10_prompt_handoff_packets.md`
- `/workflow/10_prompts/result.md`
- `/workflow/context/context_packet.md`

Conditional artifacts may also be created when applicable:

- `/workflow/10_prompts/10_prompt_readiness_issues.md`
- `/workflow/10_prompts/10_prompt_execution_order.md`
- `/workflow/10_prompts/10_prompt_traceability_matrix.md`
- `/workflow/10_prompts/10_tool_wrapper_notes.md`
- `/workflow/10_prompts/10_security_privacy_prompt_notes.md`
- `/workflow/10_prompts/10_migration_prompt_notes.md`

If a conditional artifact is not applicable, the execution result should include an N/A record explaining why and when to revisit it.

## 7. Human approval requirements

Human approval is required before Stage 11 may rely on Stage 10 outputs.

The human developer should review and approve:

- implementation prompt set;
- prompt execution order;
- task splitting or prompt grouping;
- allowed change scope and forbidden changes for each prompt;
- security/privacy-sensitive implementation constraints;
- assumptions used to write prompts;
- unresolved validation command gaps or tool-specific execution assumptions.

Prompts marked `Draft`, `Needs Review`, or `Blocked` must not be treated as executable unless the user explicitly allows draft execution.

## 8. How to run the SKILL in an Agentic Coding tool

Recommended manual procedure:

1. Place the reusable SKILL at `/skills/10_implementation_prompt_writing/SKILL.md`.
2. Confirm that Stage 9 official artifacts exist and are approved or explicitly allowed for draft prompt writing.
3. Add any human instructions to `/workflow/10_prompts/USER_DIRECTIVES.md` if needed.
4. Start a clean or clearly bounded agent session.
5. Ask the agent to run `/skills/10_implementation_prompt_writing/SKILL.md`.
6. Require the agent to perform preflight before writing prompts.
7. Review the generated Stage 10 artifacts.
8. Approve, reject, or revise the prompts before Stage 11 implementation.

Do not ask the agent to implement code while running this SKILL.

## 9. Relationship to previous and next stages

Previous stage: `09_task_breakdown`

- Provides task inventory, task cards, dependency order, and task-level traceability.
- Stage 10 should not silently change task order or scope.
- If task cards are too broad or ambiguous, Stage 10 should record readiness issues instead of writing weak prompts.

Current stage: `10_implementation_prompt_writing`

- Converts approved task cards into bounded implementation prompts and handoff packets.
- Prepares the context needed for Stage 11.

Next stage: `11_tdd_implementation_loop`

- Executes approved prompts task by task.
- Must depend only on approved Stage 10 artifacts, not prompt-writing chat history or unapproved drafts.

## 10. How to interpret `Draft`, `Approved`, and `Needs Review`

`Draft` means the artifact or prompt has been generated but has not been approved for downstream execution.

`Needs Review` means the artifact or prompt may be usable, but there are unresolved questions, assumptions, scope issues, missing tests, missing validation commands, or risk items that require human review.

`Approved` means the human developer has explicitly approved the artifact or prompt for the next workflow step.

`Blocked` may be used for a prompt that cannot be safely written or executed until a missing input, conflict, or risk is resolved.

## 11. Common mistakes to avoid

Avoid these mistakes:

- treating implementation prompt writing as code implementation;
- writing one giant prompt for many unrelated tasks;
- omitting forbidden changes;
- omitting required tests or validation commands;
- failing to define expected evidence;
- using unapproved task cards as executable scope;
- changing task order without recording a decision candidate;
- reviving rejected implementation approaches;
- relying only on `context_packet.md` instead of approved source artifacts;
- allowing Stage 11 to depend on prompt-writing chat history;
- marking prompts as approved without explicit human approval.

## 12. Troubleshooting / blocker cases

Create a blocker report when:

- Stage 9 task cards are missing;
- task cards are not approved and draft prompt writing was not explicitly allowed;
- tasks are too broad or ambiguous;
- required tests or validation commands are missing;
- source artifacts conflict with task cards;
- architecture, data, security, or privacy constraints are unresolved;
- source artifacts are superseded or rejected;
- prompt execution order cannot be determined safely.

A blocker report should state the blocking issue, why it matters, affected tasks or artifacts, safe partial work completed, and the human decision needed.

## 13. Recommended next step after successful execution

After the Stage 10 artifacts are reviewed and approved, run Stage 11 TDD Implementation Loop using only approved prompts and handoff packets.

Recommended Stage 11 inputs:

- `/workflow/10_prompts/10_implementation_prompts.md`
- `/workflow/10_prompts/10_prompt_handoff_packets.md`
- `/workflow/10_prompts/result.md`
- `/workflow/context/context_packet.md`
- approved source artifacts referenced by each handoff packet

## 14. File distinction

This `README.md`, `/skills/10_implementation_prompt_writing/SKILL.md`, and `/skills/10_implementation_prompt_writing/artifact_contract.yml` are reusable SKILL support files.

They are not project execution artifacts.

Project artifacts are created only when the SKILL is executed under `/workflow/10_prompts/` and `/workflow/context/`.
