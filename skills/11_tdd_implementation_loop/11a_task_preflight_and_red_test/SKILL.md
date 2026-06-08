---
name: 11a_task_preflight_and_red_test
description: Validates one approved implementation task, inspects relevant code and tests, and writes or identifies the initial failing test.
stage: 11 TDD Implementation Loop
parent_skill: /skills/11_tdd_implementation_loop/SKILL.md
subskill_id: 11a
subskill_order: 1
previous_subskill: null
next_subskill: /skills/11_tdd_implementation_loop/11b_minimal_implementation_green/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
requires_human_approval: true
external_visibility: internal
---

# 11a Task Preflight and Red Test

## 1. Purpose

Prepare one approved implementation task for safe coding by validating inputs, inspecting relevant code, restating scope, and creating or identifying the first failing test.

This sub-SKILL covers the Red step of the Stage 11 TDD loop.

It must not implement the feature.

---

## 2. Core Question

For the selected `TASK_ID`:

```text
Can the agent verify that implementation is authorized, understand the bounded change scope, and create or identify a failing test that proves the current behavior gap?
```

---

## 3. When to Use

Use this sub-SKILL at the start of implementation for a single approved task.

Required conditions:

```text
- A TASK_ID is selected.
- Stage 9 task card exists for that TASK_ID.
- Stage 10 implementation prompt or handoff packet exists for that TASK_ID.
- The task has required tests or validation expectations.
- The relevant codebase can be inspected.
```

---

## 4. Required Inputs

### Always Read

```text
/skills/11_tdd_implementation_loop/SKILL.md
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_dependency_order.md
/workflow/10_prompts/10_implementation_prompts.md
/workflow/10_prompts/10_prompt_handoff_packets.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_validation_commands.md
```

### Read If Applicable

```text
/workflow/03_requirements/03_requirements.md
  if requirement details must be checked.

/workflow/03_requirements/03_acceptance_criteria.md
  if acceptance criteria are not fully included in the task card.

/workflow/04_domain/04_domain_model.md
  if domain objects, behaviors, or services are touched.

/workflow/04_domain/04_business_rules_invariants.md
  if domain invariants or lifecycle rules are touched.

/workflow/05_architecture/05_architecture_plan.md
  if module boundaries, layering, or deployment shape are touched.

/workflow/05_architecture/05_api_contracts.md
  if API behavior or request/response shapes are touched.

/workflow/06_data/06_data_security_rules.md
  if access control, privacy, data visibility, or security rules are touched.
```

### USER_DIRECTIVES.md

If present, read before executing:

```text
/workflow/11_implementation_results/USER_DIRECTIVES.md
```

Classify any directive as approval, correction, scope change, forbidden change, priority update, test requirement update, review comment, rollback instruction, or question.

---

## 5. Do Not Read By Default

Do not read these unless explicitly relevant:

```text
- full historical agent logs
- superseded artifacts
- rejected artifacts
- unrelated stage drafts
- unrelated source code directories
- unrelated tests
- secrets, private keys, credentials, production environment files
- generated build artifacts
- dependency lockfile diffs unless dependency changes are approved
```

---

## 6. Input Preflight Procedure

Perform this checklist before writing or running tests:

```text
[ ] Confirm selected TASK_ID.
[ ] Locate the approved task card for TASK_ID.
[ ] Locate the approved implementation prompt or handoff packet.
[ ] Verify approval or explicit authorization to execute the task.
[ ] Identify linked requirements and acceptance criteria.
[ ] Identify allowed change scope.
[ ] Identify forbidden changes.
[ ] Identify required tests and validation commands.
[ ] Identify expected evidence artifacts.
[ ] Identify rollback or recovery notes, if any.
[ ] Check artifact_manifest.yml for approved/superseded/rejected status.
[ ] Check DECISIONS.md and APPROVAL_LOG.md for relevant constraints.
[ ] Check TRACEABILITY_MATRIX.md for existing IDs and links.
[ ] Check USER_DIRECTIVES.md, if present.
[ ] Identify conditional inputs activated by this task.
[ ] Check for missing, conflicting, superseded, or unapproved inputs.
[ ] Inspect relevant code and tests before editing.
[ ] Check for existing local changes or files that may be overwritten.
```

If any blocking issue exists, stop and produce a blocker report.

---

## 7. Codebase Inspection Rules

Before editing any code or test, inspect:

```text
- files explicitly listed in the task card or prompt
- nearby implementation files in the same module
- nearby test files for the same behavior
- test helpers, fixtures, factories, mocks, and setup files
- package/build/test scripts
- relevant API route/controller/service files
- relevant schema/migration/access-control files
- existing patterns for error handling, logging, validation, and naming
```

Record inspected files in the task result draft or working notes for later finalization.

Do not scan or rewrite unrelated repository areas by default.

---

## 8. Restate the Task Before Test Work

Before writing or running tests, produce a short restatement:

```markdown
## Task Restatement

### TASK_ID
- ...

### Approved Goal
- ...

### Linked Requirements / Acceptance Criteria
- ...

### Allowed Change Scope
- ...

### Forbidden Changes
- ...

### Required Tests / Validation
- ...

### Expected Evidence
- ...

### Stop Conditions
- ...
```

Do not add new product behavior beyond the approved task.

---

## 9. Red Step Procedure

The agent must do exactly one of these:

```text
Option A: Write a new failing automated test that directly verifies the approved task.
Option B: Identify an existing failing test that directly verifies the approved task.
Option C: If strict test-first is not feasible, document why and create a test-aware validation plan before any implementation.
```

### Option A — Write a New Failing Test

1. Choose the smallest test level that validates the task.
2. Prefer unit or narrow integration tests unless the task requires E2E or manual validation.
3. Name the test after the behavior, not the implementation detail.
4. Link the test to `TASK_ID` and requirement/acceptance criterion IDs if available.
5. Run the targeted test.
6. Confirm the failure matches the intended behavior gap.

### Option B — Identify Existing Failing Test

1. Confirm the existing test directly maps to the task.
2. Run only the targeted test or the smallest relevant subset.
3. Confirm the failure is relevant to the intended behavior gap.
4. Do not proceed if the failure is unrelated or environmental without recording the issue.

### Option C — Test-Aware Plan

Use only when strict Red step is not feasible.

Record:

```text
- why no automated failing test can be written first;
- what validation will prove the behavior;
- exact commands or manual steps to run after implementation;
- risk created by not having a true Red step;
- whether human review is needed before coding.
```

---

## 10. Evidence to Record

Append or prepare the following sections in:

```text
/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
```

Required structure for this sub-SKILL:

```markdown
# Test Evidence: {{TASK_ID}} — {{TASK_TITLE}}

## 1. Evidence Summary
- Task ID:
- Test strategy reference:
- Validation command reference:
- Environment summary:

## 2. Red Step Evidence
- Test added or identified:
- Test file:
- Test case:
- Command run:
- Expected failure:
- Actual failure:
- Failure matched intended behavior gap: Yes | No
- Notes:

## 3. Test-Aware Plan If Strict Red Was Not Feasible
- Strict Red feasible: Yes | No
- Reason if not feasible:
- Planned validation:
- Risk:
- Human review needed before coding: Yes | No
```

Do not claim implementation progress in this file.

---

## 11. Blocking Conditions

Stop and produce a blocker report if:

```text
- TASK_ID is missing or ambiguous;
- task card is not approved or not explicitly authorized;
- implementation prompt is not approved or not explicitly authorized;
- allowed change scope is missing;
- required test strategy is missing and cannot be safely inferred;
- relevant codebase files cannot be inspected;
- human changes may be overwritten;
- selected test failure is unrelated or unreliable;
- implementation would require unapproved architecture/API/data/security/privacy/scope change;
- secrets or sensitive files would need to be exposed or modified.
```

Blocker report format:

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
- ...

### Affected Task / Artifact / Code Area
- ...

### Evidence Collected Before Stopping
- ...

### Safe Partial Work Completed
- ...

### Human Decision Needed
- ...

### Recommended Next Step
- ...
```

---

## 12. Handoff to Next Sub-SKILL

Prepare a concise handoff for `11b_minimal_implementation_green`:

```markdown
## 11a → 11b Handoff

### TASK_ID
- ...

### Test Selected
- ...

### Red Step Status
- Failing test confirmed | Existing failing test confirmed | Test-aware plan recorded | Blocked

### Failure Summary
- ...

### Files Inspected
- ...

### Files Allowed to Change
- ...

### Forbidden Changes
- ...

### Implementation Stop Conditions
- ...
```

This handoff may be placed in `11_test_evidence_{{TASK_ID}}.md`, a task-local working note, or the conversation summary. Do not treat it as an approved downstream artifact until the finalizer consolidates evidence.

---

## 13. Human Approval Gate

Human approval is required before proceeding to implementation if:

```text
- strict Red step is not feasible and risk is significant;
- task scope is ambiguous;
- required behavior conflicts with approved artifacts;
- test failure suggests design, architecture, data, security, or privacy decisions are missing;
- implementation would touch forbidden areas.
```

Otherwise, proceed to:

```text
/skills/11_tdd_implementation_loop/11b_minimal_implementation_green/SKILL.md
```

---

## 14. Do Not Do

The agent must not:

```text
- implement production code in this sub-SKILL;
- change broad test infrastructure unless approved;
- create a weak test that does not verify the approved behavior;
- continue when the failing test is unrelated;
- silently assume missing approved scope;
- read secrets or credentials;
- overwrite human changes;
- mark the task complete;
- update DECISIONS.md without explicit human approval.
```
