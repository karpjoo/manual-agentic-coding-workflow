---
name: 11c_refactor_regression_evidence
description: Performs scope-safe refactoring, broader validation, manual or conditional evidence capture, and failure classification for one implementation task.
stage: 11 TDD Implementation Loop
parent_skill: /skills/11_tdd_implementation_loop/SKILL.md
subskill_id: 11c
subskill_order: 3
previous_subskill: /skills/11_tdd_implementation_loop/11b_minimal_implementation_green/SKILL.md
next_subskill: /skills/11_tdd_implementation_loop/11d_implementation_finalizer/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
requires_human_approval: true
external_visibility: internal
---

# 11c Refactor, Regression, and Evidence

## 1. Purpose

After the targeted test passes or a test-aware implementation has been completed, perform only approved-scope refactoring, run broader validation, and record sufficient evidence for human review.

This sub-SKILL covers the Refactor and Regression portions of the Stage 11 loop.

---

## 2. Core Question

For the selected `TASK_ID`:

```text
Does the implementation remain correct after safe local refactoring and broader regression validation, and is the evidence sufficient for human review?
```

---

## 3. Required Inputs

### Always Read

```text
/skills/11_tdd_implementation_loop/SKILL.md
/skills/11_tdd_implementation_loop/11a_task_preflight_and_red_test/SKILL.md
/skills/11_tdd_implementation_loop/11b_minimal_implementation_green/SKILL.md
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/09_tasks/09_task_cards.md
/workflow/10_prompts/10_implementation_prompts.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
```

### Read If Applicable

```text
/workflow/05_architecture/05_api_contracts.md
  if API behavior was touched.

/workflow/06_data/06_migration_plan.md
  if migration behavior was touched.

/workflow/06_data/06_data_security_rules.md
  if access control, privacy, or data visibility was touched.

/workflow/12_review_release_handoff/review_notes.md
  if the task addresses a review finding.
```

---

## 4. Pre-Regression Checklist

Before refactoring or broader validation, verify:

```text
[ ] TASK_ID is selected.
[ ] 11a Red evidence or test-aware plan exists.
[ ] 11b Green evidence exists.
[ ] Files changed are within allowed scope.
[ ] Targeted validation passed or any failure is clearly classified.
[ ] Required broader validation commands are identified.
[ ] Conditional evidence needs are identified.
[ ] No forbidden changes were introduced.
```

If targeted validation did not pass and there is no justified partial path, stop and produce a blocker report.

---

## 5. Refactor Procedure

Refactor only if useful and safe.

Allowed refactoring:

```text
- remove duplication introduced by this task;
- align with existing naming and structure;
- simplify local implementation while preserving behavior;
- improve local readability in changed files;
- update tests for clarity without weakening assertions.
```

Forbidden refactoring:

```text
- broad architectural reshaping;
- unrelated module cleanup;
- style-only churn across many files;
- dependency restructuring;
- public contract changes without approval;
- changes to authorization/security behavior without approval;
- migration/schema changes without approval.
```

After any refactor, rerun the targeted validation command and record the result.

---

## 6. Broader Regression Validation Procedure

Run broader validation defined by the task, implementation prompt, or Stage 8 validation commands.

Potential validation includes:

```text
- related unit test suite;
- related integration tests;
- E2E smoke tests;
- typecheck;
- lint;
- build;
- migration validation;
- API contract tests;
- security rule tests;
- performance or query validation;
- manual verification.
```

Use the smallest broader scope that gives confidence without doing unrelated work.

Record every command attempted. Do not claim a validation passed unless the command result supports it.

---

## 7. Conditional Evidence Procedure

Create conditional evidence artifacts when applicable.

### Manual Verification

Create:

```text
/workflow/11_implementation_results/11_manual_verification_{{TASK_ID}}.md
```

when UI, workflow, external integration, operational behavior, or manual-only behavior requires human-verifiable steps.

### Migration Evidence

Create:

```text
/workflow/11_implementation_results/11_migration_evidence_{{TASK_ID}}.md
```

when schema, migration, seed data, or data backfill behavior is implemented or changed.

### API Contract Evidence

Create:

```text
/workflow/11_implementation_results/11_api_contract_evidence_{{TASK_ID}}.md
```

when API request/response, status codes, error semantics, or integration behavior is changed.

### Security / Privacy Evidence

Create:

```text
/workflow/11_implementation_results/11_security_privacy_evidence_{{TASK_ID}}.md
```

when auth, authorization, personal data, sensitive data, audit logs, privacy, or external data transfer is touched.

### UI Evidence

Create:

```text
/workflow/11_implementation_results/11_ui_evidence_{{TASK_ID}}.md
```

when user-visible UI or navigation behavior changes.

### Performance Evidence

Create:

```text
/workflow/11_implementation_results/11_performance_evidence_{{TASK_ID}}.md
```

when performance, scalability, query efficiency, or resource usage is part of the task definition of done.

### Rollback Notes

Create:

```text
/workflow/11_implementation_results/11_rollback_notes_{{TASK_ID}}.md
```

when rollback or recovery procedures are needed.

If a conditional artifact is not applicable, record an N/A entry in the task result.

---

## 8. Required Evidence Updates

Update:

```text
/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
```

Required sections:

```markdown
## 4. Refactor Evidence
- Refactor performed: Yes | No
- Reason:
- Files touched:
- Tests rerun:
- Result:

## 5. Regression Evidence
| Command | Scope | Result | Notes |
|---|---|---|---|

## 6. Manual Verification Evidence
- Required: Yes | No
- Steps:
- Expected result:
- Observed result:
- Evidence location:

## 7. Not-Run Tests or Skipped Validation
| Validation | Reason Not Run | Risk | Recommended Follow-up |
|---|---|---|---|

## 8. Failure Log Summary
- Remaining failures:
- Failure classification: task-related | unrelated | environment | unknown
- Human action needed:
```

---

## 9. Update Task Result Draft

Update:

```text
/workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
```

Ensure these sections reflect current evidence:

```markdown
## 7. Tests and Commands Run
| Command | Purpose | Result | Evidence Reference |
|---|---|---|---|

## 8. TDD Summary
- Red step completed: Yes | No | Not feasible
- Failure confirmed before implementation: Yes | No | Not feasible
- Green step completed: Yes | No
- Refactor completed: Yes | No | Not needed
- Regression validation completed: Yes | No | Partial

## 9. Validation Result
- Overall result:
- Passing evidence:
- Failing evidence:
- Not-run validation:
- Manual verification:

## 10. Known Limitations
- ...

## 13. Risks and Follow-up Tasks
- ...

## 15. Conditional Artifact N/A Record
| Artifact | Why Not Applicable | Revisit If |
|---|---|---|
```

---

## 10. Failure Classification Rules

Classify failures as:

```text
task-related
  The implementation does not satisfy the selected task or acceptance criteria.

unrelated
  The failure appears outside the task scope and was not introduced by the task.

environment
  The validation command cannot run due to setup, dependency, sandbox, service, or permission issues.

unknown
  The cause cannot be confidently classified.
```

Unknown failures are not safe to ignore. Record them as risks and escalate if they affect reviewer confidence.

---

## 11. Blocker Report

Stop and report a blocker if:

```text
- regression failure appears task-related and cannot be fixed within scope;
- failure cause is unknown and blocks confidence;
- required validation cannot be run and no safe alternative exists;
- conditional evidence reveals security/privacy/data/API risk;
- refactor would require broad architecture or contract change;
- validation requires secrets or production credentials;
- human changes may be overwritten.
```

Use this format:

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

Prepare a concise handoff for `11d_implementation_finalizer`:

```markdown
## 11c → 11d Handoff

### TASK_ID
- ...

### Final Validation Status
- Pass | Partial | Fail | Blocked

### Commands Run
- ...

### Conditional Evidence Created
- ...

### Skipped Validation
- ...

### Remaining Risks
- ...

### Traceability Gaps
- ...

### Recommended Finalizer Status
- Completed Pending Human Review | Needs Review | Blocked
```

---

## 13. Human Approval Gate

Stop for human review before finalization if:

```text
- required validation failed;
- required validation was skipped and risk is high;
- security/privacy/API/data evidence is incomplete;
- a scope deviation occurred;
- the task appears completed but acceptance criteria are ambiguous.
```

Otherwise proceed to:

```text
/skills/11_tdd_implementation_loop/11d_implementation_finalizer/SKILL.md
```

---

## 14. Do Not Do

The agent must not:

```text
- perform broad cleanup unrelated to the task;
- hide failing regression tests;
- claim skipped validation as passed;
- treat unrelated failures as irrelevant without recording them;
- create conditional evidence only as vague summaries;
- edit secrets or production credentials;
- update DECISIONS.md without explicit human approval;
- mark the task approved;
- proceed to Stage 12 without finalizer consolidation.
```
