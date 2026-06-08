---
name: 08_test_strategy_validation
description: Use this stage package to define the test strategy, acceptance tests, validation commands, manual test plan, and Stage 9 validation handoff before implementation begins.
stage: "08 Test Strategy & Validation Harness"
version: 1.0.0
status: draft
primary_output: /workflow/08_test_strategy/result.md
requires_human_approval: true
internal_split: true
subskills:
  - /skills/08_test_strategy_validation/08a_validation_scope_strategy/SKILL.md
  - /skills/08_test_strategy_validation/08b_acceptance_test_design/SKILL.md
  - /skills/08_test_strategy_validation/08c_validation_commands_harness/SKILL.md
  - /skills/08_test_strategy_validation/08d_manual_specialized_validation/SKILL.md
  - /skills/08_test_strategy_validation/08e_test_strategy_finalizer/SKILL.md
---

# 08 Test Strategy & Validation Harness — Stage Entrypoint

## 1. Purpose

This is the stage-level entrypoint for Stage 8 of the Manual Agentic Coding Workflow.

Stage 8 defines how the project will prove that approved requirements, acceptance criteria, architecture decisions, data rules, and MVP scope are satisfied before implementation work is decomposed into task cards.

This parent `SKILL.md` does not perform the whole Stage 8 analysis itself. It orchestrates the internal sub-skills and preserves the public stage boundary.

Core outcome:

```text
Approved requirements and MVP scope
→ validation strategy
→ acceptance tests
→ validation commands / placeholders
→ manual validation plan
→ traceability handoff for Stage 9 task breakdown
```

## 2. When to Use

Use this stage package when:

- Stage 3 requirements and acceptance criteria exist.
- Stage 5 architecture and technical contracts exist.
- Stage 6 data design exists if persistent data is used.
- Stage 7 MVP scope and release slicing exist.
- The next workflow step is Stage 9 Task Breakdown.
- Implementation should be TDD-ready or at least test-aware.

Do not use this package to:

- write application code;
- implement test files;
- run final QA after implementation;
- perform Stage 12 release readiness or security review;
- revise requirements, architecture, data design, or MVP scope without explicit human instruction.

## 3. Public Stage Contract

The internal sub-skill split is an implementation detail. Downstream stages must depend only on approved official Stage 8 artifacts, not on sub-skill names, prompt history, or intermediate notes.

Official Stage 8 artifacts are:

```text
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
/workflow/08_test_strategy/result.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/context_packet.md
```

Conditional Stage 8 artifacts may also be created by the relevant sub-skills when applicable:

```text
/workflow/08_test_strategy/08_test_data_fixtures.md
/workflow/08_test_strategy/08_ci_validation_plan.md
/workflow/08_test_strategy/08_security_privacy_tests.md
/workflow/08_test_strategy/08_performance_validation.md
/workflow/08_test_strategy/08_accessibility_validation.md
/workflow/08_test_strategy/08_regression_baseline.md
/workflow/08_test_strategy/08_model_or_data_evaluation_plan.md
/workflow/08_test_strategy/08_mobile_platform_validation.md
```

If a conditional artifact is not applicable, the finalizer must record an N/A rationale.

## 4. Internal Sub-Skill Sequence

Run the sub-skills in this order:

```text
08a_validation_scope_strategy
→ 08b_acceptance_test_design
→ 08c_validation_commands_harness
→ 08d_manual_specialized_validation
→ 08e_test_strategy_finalizer
```

### 08a — Validation Scope and Test Strategy

Defines MVP validation scope, risk-based priorities, test levels, and requirement-to-validation method mapping.

Primary output:

```text
/workflow/08_test_strategy/08_test_strategy.md
```

### 08b — Acceptance Test Design

Converts acceptance criteria into acceptance test specifications, including negative, edge, permission, data, integration, and manual-only acceptance tests.

Primary output:

```text
/workflow/08_test_strategy/08_acceptance_tests.md
```

### 08c — Validation Commands and Harness Planning

Defines validation command inventory, command placeholders, fixture/test data needs, CI suitability, and harness prerequisites.

Primary outputs:

```text
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_test_data_fixtures.md, if applicable
/workflow/08_test_strategy/08_ci_validation_plan.md, if applicable
```

### 08d — Manual and Specialized Validation Planning

Defines manual validation and specialized validation plans for security/privacy, performance, accessibility, brownfield regression, AI/data products, and mobile platforms when applicable.

Primary output:

```text
/workflow/08_test_strategy/08_manual_test_plan.md
```

### 08e — Test Strategy Finalizer

Consolidates Stage 8 artifacts, resolves inconsistencies, updates traceability, prepares `result.md`, prepares `context_packet.md` for Stage 9, and presents the human approval gate.

Primary outputs:

```text
/workflow/08_test_strategy/result.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/context_packet.md
```

## 5. Required Inputs

Each sub-skill defines its own precise input contract. At the stage level, Stage 8 normally depends on these approved inputs.

### Always Read

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
/workflow/07_mvp_release/07_mvp_scope.md
```

### Read If Applicable

```text
/workflow/00_intake/00_existing_context_review.md
- if this is a brownfield, migration, extension, or existing-codebase project.

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if roles, permissions, sensitive data, privacy, compliance, abuse, or operational risk affects validation.

/workflow/04_domain/04_business_rules_invariants.md
- if domain invariants, lifecycle rules, state transitions, or business rules require validation.

/workflow/04_domain/04_domain_events.md
- if domain events, async workflows, notifications, or event-driven behavior exist.

/workflow/05_architecture/05_api_contracts.md
- if APIs exist.

/workflow/05_architecture/05_integration_contracts.md
- if external systems, webhooks, queues, third-party services, or LLM/model APIs exist.

/workflow/05_architecture/05_module_boundaries.md
- if module-level tests, contract tests, or boundary tests are needed.

/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_physical_schema.md
- if persistent data exists.

/workflow/06_data/06_indexes.md
- if query performance, ordering, filtering, or pagination behavior must be validated.

/workflow/06_data/06_data_security_rules.md
- if data access control, tenant isolation, row/document-level security, or role-based data visibility exists.

/workflow/06_data/06_migration_plan.md
- if migration, seed data, compatibility, rollback, or data backfill validation is needed.

/workflow/07_mvp_release/07_release_slices.md
- if validation differs by release slice or phased rollout.

/workflow/07_mvp_release/07_out_of_scope.md
- if test scope must explicitly exclude non-MVP behavior.
```

## 6. USER_DIRECTIVES.md Handling

Before running any sub-skill, check whether this file exists:

```text
/workflow/08_test_strategy/USER_DIRECTIVES.md
```

If it exists:

1. Read it before producing outputs.
2. Classify directives as approval, correction, preference, rejection, scope change, constraint, question, or new input.
3. Apply it before agent assumptions.
4. Report conflicts with `DECISIONS.md`, `APPROVAL_LOG.md`, or approved artifacts.
5. Do not automatically treat every directive as a globally approved decision.
6. Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

## 7. Input Preflight Procedure

Every sub-skill must perform preflight before creating or updating artifacts:

```text
[ ] Read the current sub-skill SKILL.md.
[ ] Read artifact_manifest.yml if available.
[ ] Read context_packet.md if available.
[ ] Read DECISIONS.md and APPROVAL_LOG.md if available.
[ ] Check USER_DIRECTIVES.md.
[ ] Identify Always Read inputs.
[ ] Identify conditional inputs activated by project profile, context, directives, or approved decisions.
[ ] Verify that required inputs exist.
[ ] Verify that source artifacts are approved or clearly marked as draft.
[ ] Check for superseded or rejected artifacts.
[ ] Identify missing, ambiguous, or conflicting information.
[ ] Restate the sub-skill task before producing outputs.
```

If preflight reveals a blocking issue, produce a blocker report or partial result instead of pretending completion.

## 8. Execution Policy

- Execute the sub-skills in order.
- Use official project artifacts under `/workflow`, not chat history, as source of truth.
- Keep sub-skill outputs aligned with official Stage 8 artifact paths.
- Do not create implementation tasks in Stage 8.
- Do not implement tests or product code in Stage 8.
- Do not declare validation passed without execution evidence.
- Treat exact commands as confirmed only when source artifacts or user directives provide them.
- Use command placeholders when tooling is not yet confirmed.
- Preserve traceability from requirements and acceptance criteria to tests and validation methods.

## 9. Failure Handling

If Stage 8 cannot be completed safely, the active sub-skill or finalizer must produce a blocker report containing:

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
- ...

### Affected Artifacts or Stages
- ...

### Safe Partial Work Completed
- ...

### Human Decision Needed
- ...
```

Blocking issues normally include:

- missing approved requirements;
- missing acceptance criteria;
- missing approved MVP scope;
- architecture boundary missing where validation depends on it;
- missing data access or privacy rules for sensitive data;
- conflict between MVP scope and requirements;
- conflict between user directives and approved decisions.

## 10. Finalizer Requirement

Stage 8 is not ready for downstream use until `08e_test_strategy_finalizer` has run.

The finalizer must:

- read the outputs of all prior Stage 8 sub-skills;
- consolidate official artifacts;
- detect contradictions among validation scope, acceptance tests, commands, and manual tests;
- update or prepare `/workflow/context/TRACEABILITY_MATRIX.md`;
- create or update `/workflow/08_test_strategy/result.md`;
- update `/workflow/context/context_packet.md` for Stage 9;
- prepare the human approval gate;
- list artifacts ready for review;
- clearly state that artifacts are draft until approved.

## 11. Human Approval Gate

The final Stage 8 approval gate must ask the human developer to approve or resolve:

```text
- automated test scope for MVP;
- manual validation scope for MVP;
- required validation commands or command placeholders;
- CI validation expectations;
- security/privacy validation scope;
- performance/accessibility validation scope, if applicable;
- validation gaps accepted for Stage 9 task breakdown;
- test data and fixture assumptions;
- manual-only validation assumptions;
- unresolved open questions that affect task cards.
```

Do not update `DECISIONS.md` unless explicit human approval exists.

## 12. Downstream Handoff Rule

Stage 9 Task Breakdown may depend only on approved Stage 8 official artifacts:

```text
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/context_packet.md
```

Stage 9 must not depend on:

```text
- internal sub-skill folder names;
- prompt history;
- chat context;
- unapproved drafts;
- intermediate notes not promoted to official artifacts;
- command placeholders treated as confirmed commands.
```

## 13. Do Not Do

The agent must not:

- collapse all Stage 8 work into one uncontrolled task;
- skip the finalizer;
- implement product code;
- implement test code unless the human explicitly changes the stage boundary;
- claim tests passed without evidence;
- invent exact commands when tooling is unknown;
- treat command placeholders as approved commands;
- change requirements, acceptance criteria, architecture, data design, or MVP scope;
- include later-release or out-of-scope features in MVP validation unless explicitly requested;
- silently ignore security, privacy, authorization, or data-access validation needs;
- reduce all validation to E2E tests;
- leave manual tests without pass/fail criteria;
- update `DECISIONS.md` without explicit human approval;
- treat Stage 8 artifacts as approved until human approval is recorded.
