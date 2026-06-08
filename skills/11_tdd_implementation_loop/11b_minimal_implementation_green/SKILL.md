---
name: 11b_minimal_implementation_green
description: Implements the smallest approved code change needed to satisfy the selected failing test and task acceptance criteria.
stage: 11 TDD Implementation Loop
parent_skill: /skills/11_tdd_implementation_loop/SKILL.md
subskill_id: 11b
subskill_order: 2
previous_subskill: /skills/11_tdd_implementation_loop/11a_task_preflight_and_red_test/SKILL.md
next_subskill: /skills/11_tdd_implementation_loop/11c_refactor_regression_evidence/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
requires_human_approval: true
external_visibility: internal
---

# 11b Minimal Implementation Green

## 1. Purpose

Implement the smallest code change required to make the selected failing test pass and satisfy the approved task acceptance criteria.

This sub-SKILL covers the Green step of the Stage 11 TDD loop.

It must preserve the approved scope and avoid broad refactoring.

---

## 2. Core Question

For the selected `TASK_ID`:

```text
Can the agent make the targeted validation pass with the smallest correct change while avoiding unauthorized scope, architecture, API, data, security, or privacy changes?
```

---

## 3. Required Inputs

### Always Read

```text
/skills/11_tdd_implementation_loop/SKILL.md
/skills/11_tdd_implementation_loop/11a_task_preflight_and_red_test/SKILL.md
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/09_tasks/09_task_cards.md
/workflow/10_prompts/10_implementation_prompts.md
/workflow/10_prompts/10_prompt_handoff_packets.md
/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
```

### Read If Applicable

```text
/workflow/03_requirements/03_acceptance_criteria.md
  if acceptance criteria details are needed.

/workflow/04_domain/04_business_rules_invariants.md
  if domain invariants or lifecycle rules are touched.

/workflow/05_architecture/05_module_boundaries.md
  if module ownership or dependency direction is touched.

/workflow/05_architecture/05_api_contracts.md
  if API behavior is touched.

/workflow/06_data/06_logical_schema.md
  if persistent data structures are touched.

/workflow/06_data/06_migration_plan.md
  if migration behavior is touched.

/workflow/06_data/06_data_security_rules.md
  if access control, privacy, or data visibility is touched.
```

### Required 11a Handoff

Confirm that 11a produced one of:

```text
- a confirmed failing automated test;
- a confirmed existing failing test;
- a documented test-aware validation plan.
```

If none exists, stop and return to 11a.

---

## 4. Pre-Implementation Checklist

Before editing code, verify:

```text
[ ] TASK_ID is selected.
[ ] Approved task card and implementation prompt are available.
[ ] Allowed change scope is clear.
[ ] Forbidden changes are clear.
[ ] Red step or test-aware plan exists.
[ ] Relevant code and tests were inspected.
[ ] There are no uncommitted human changes that may be overwritten.
[ ] No missing architecture/API/data/security/privacy decision blocks implementation.
[ ] No new dependency is required unless already approved.
```

If any check fails, produce a blocker report.

---

## 5. Minimal Implementation Procedure

### 5.1 Restate the Green Plan

Write a short plan:

```markdown
## Green Plan

### Target Test / Validation
- ...

### Minimal Code Change
- ...

### Files Expected to Change
- ...

### Files That Must Not Change
- ...

### Validation Command
- ...

### Stop Conditions
- ...
```

### 5.2 Implement Only the Minimal Change

Implement only what is needed to satisfy:

```text
- the confirmed failing test or test-aware validation plan;
- the approved task acceptance criteria;
- the task definition of done.
```

Prefer existing code patterns over new abstractions.

### 5.3 Forbidden Implementation Moves

Do not:

```text
- add unrelated feature behavior;
- broaden task scope;
- perform broad cleanup or rewrites;
- change public API contracts without approval;
- change data schema or migrations without approval;
- change auth, authorization, privacy, or security behavior without approval;
- add dependencies without approval;
- silently change test expectations to match incorrect implementation;
- weaken tests to pass;
- remove failing tests unless the task explicitly requires deleting obsolete behavior.
```

### 5.4 Run Targeted Validation

Run the smallest relevant command first.

Record:

```text
- command run;
- test names or suite names;
- result;
- output summary;
- if failed, whether failure is task-related, unrelated, environment-related, or unknown.
```

If the targeted test still fails, iterate only within the approved scope.

If passing requires unapproved changes, stop and produce a blocker report.

---

## 6. Update Task Result Draft

Create or update:

```text
/workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
```

At minimum, prepare these sections for the finalizer:

```markdown
# Task Result: {{TASK_ID}} — {{TASK_TITLE}}

## 1. Status
- Status: Draft
- Task ID:
- Implementation prompt ID:
- Date:
- Agent/tool:

## 2. Task Summary
- Approved goal:
- Linked requirements:
- Linked acceptance criteria:
- Linked test cases:
- Definition of done:

## 3. Inputs Used
- Approved task card:
- Approved implementation prompt:
- Context files:
- Code files inspected:
- Test files inspected:

## 4. Scope Control
- Allowed changes:
- Forbidden changes:
- Scope changes requested: None | List
- Scope conflicts: None | List

## 5. Files Changed
| File | Change Type | Reason | Linked Test/Evidence |
|---|---|---|---|

## 6. Tests Added or Modified
| Test File | Test Case | Purpose | Linked Requirement/Task |
|---|---|---|---|

## 7. Tests and Commands Run
| Command | Purpose | Result | Evidence Reference |
|---|---|---|---|

## 8. TDD Summary
- Red step completed: Yes | No | Not feasible
- Failure confirmed before implementation: Yes | No | Not feasible
- Green step completed: Yes | No
```

Do not mark the task as complete. Final status is set by the finalizer after regression and evidence review.

---

## 7. Update Test Evidence

Append Green step evidence to:

```text
/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
```

Required section:

```markdown
## 3. Green Step Evidence
- Implementation summary:
- Files changed:
- Command run:
- Result:
- Output summary:
- Remaining failures:
- Notes:
```

---

## 8. Handling Failures During Green Step

### Task-Related Failure

If the targeted test still fails for task-related reasons:

```text
- analyze the smallest local fix;
- continue only within approved scope;
- do not broaden implementation behavior beyond acceptance criteria.
```

### Unrelated Failure

If the failure appears unrelated:

```text
- record the failure;
- do not hide it;
- decide whether targeted validation can still prove the task;
- proceed only if safe and clearly recorded;
- otherwise stop for human decision.
```

### Environment Failure

If validation cannot run because of environment setup:

```text
- record the command attempted;
- record the environment failure;
- identify manual or alternative validation if safe;
- do not claim tests passed.
```

---

## 9. Blocker Report

Use this format when implementation cannot safely continue:

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

Blocking conditions include:

```text
- no valid 11a Red evidence or test-aware plan;
- implementation requires forbidden file changes;
- implementation requires unapproved architecture/API/data/security/privacy changes;
- targeted test cannot be made to pass without weakening the test;
- new dependency is needed but unapproved;
- human changes may be overwritten;
- repository state becomes unsafe or unclear.
```

---

## 10. Handoff to Next Sub-SKILL

Prepare a concise handoff for `11c_refactor_regression_evidence`:

```markdown
## 11b → 11c Handoff

### TASK_ID
- ...

### Green Status
- Targeted validation passed | Failed | Partial | Not runnable

### Files Changed
- ...

### Tests Added or Modified
- ...

### Targeted Commands Run
- ...

### Remaining Failures or Risks
- ...

### Refactor Candidates Within Scope
- ...

### Regression Commands to Run
- ...
```

---

## 11. Human Approval Gate

Stop for human approval before proceeding to 11c if:

```text
- a scope change is needed;
- validation passed only by changing test expectations;
- implementation reveals missing product, architecture, data, security, or privacy decisions;
- a new dependency appears necessary;
- task completion is uncertain.
```

Otherwise proceed to:

```text
/skills/11_tdd_implementation_loop/11c_refactor_regression_evidence/SKILL.md
```

---

## 12. Do Not Do

The agent must not:

```text
- skip the 11a Red/test-aware plan;
- implement unrelated behavior;
- broaden scope to make tests pass;
- silently alter acceptance criteria;
- weaken or delete tests to pass;
- perform broad refactors;
- alter approved architecture/API/data/security/privacy decisions;
- claim task completion before regression and finalization;
- update DECISIONS.md without explicit human approval.
```
