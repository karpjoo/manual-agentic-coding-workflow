---
name: 08e_test_strategy_finalizer
description: Consolidate Stage 8 validation artifacts, update traceability and context handoff, and prepare the human approval gate for Stage 9 Task Breakdown.
stage: "08 Test Strategy & Validation Harness"
parent_skill: /skills/08_test_strategy_validation/SKILL.md
subskill_id: 08e
subskill_order: 5
previous_subskill: /skills/08_test_strategy_validation/08d_manual_specialized_validation/SKILL.md
next_subskill: /skills/09_task_breakdown/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/08_test_strategy/result.md
requires_human_approval: true
external_visibility: internal
---

# 08e Test Strategy Finalizer

## 1. Purpose

Finalize Stage 8 by consolidating all test strategy and validation artifacts into a coherent, reviewable stage result.

This sub-skill prepares Stage 8 for human approval and Stage 9 handoff. It does not approve the artifacts itself.

Primary outputs:

```text
/workflow/08_test_strategy/result.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/context_packet.md
```

It also reviews and, if needed, aligns the official Stage 8 artifacts:

```text
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
```

## 2. When to Use

Use this finalizer after these sub-skills have run or their absence has been explicitly explained:

```text
08a_validation_scope_strategy
08b_acceptance_test_design
08c_validation_commands_harness
08d_manual_specialized_validation
```

Do not use this sub-skill to:

- perform Stage 8 from scratch;
- implement tests or code;
- create Stage 9 task cards;
- approve Stage 8 outputs without human approval;
- mark validation as passed.

## 3. Required Inputs

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
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
```

### Read If Applicable

```text
/workflow/00_intake/00_existing_context_review.md
- if brownfield, migration, extension, or existing-codebase context affects final validation readiness.

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if security/privacy/risk validation must be checked.

/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
- if domain rules, state transitions, or event behavior must be traceable to tests.

/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_module_boundaries.md
- if API, integration, or module validation coverage must be checked.

/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_indexes.md
/workflow/06_data/06_migration_plan.md
/workflow/06_data/06_data_security_rules.md
- if data, migration, performance, or data-security validation coverage must be checked.

/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md
- if release-slice or explicit non-scope validation consistency must be checked.

/workflow/08_test_strategy/08_test_data_fixtures.md
/workflow/08_test_strategy/08_ci_validation_plan.md
/workflow/08_test_strategy/08_security_privacy_tests.md
/workflow/08_test_strategy/08_performance_validation.md
/workflow/08_test_strategy/08_accessibility_validation.md
/workflow/08_test_strategy/08_regression_baseline.md
/workflow/08_test_strategy/08_model_or_data_evaluation_plan.md
/workflow/08_test_strategy/08_mobile_platform_validation.md
- if these conditional artifacts were created or should have been considered.
```

### Do Not Read By Default

```text
- internal chat history;
- raw agent logs;
- superseded/rejected artifacts;
- unapproved unrelated drafts;
- Stage 10 implementation prompts;
- Stage 11 implementation evidence;
- Stage 12 release review artifacts.
```

## 4. USER_DIRECTIVES.md Handling

Check:

```text
/workflow/08_test_strategy/USER_DIRECTIVES.md
```

If present, verify that final artifacts reflect applicable directives or report conflicts.

## 5. Input Preflight Procedure

Before finalizing Stage 8:

```text
[ ] Confirm official Stage 8 artifacts exist or report missing artifacts.
[ ] Confirm each artifact is marked Draft, Needs Review, or Approved.
[ ] Verify requirements, acceptance criteria, MVP scope, and validation artifacts are consistent.
[ ] Verify conditional artifacts were created or have N/A rationale.
[ ] Check for conflicting validation assumptions.
[ ] Check for command placeholders incorrectly treated as confirmed.
[ ] Check for manual tests lacking pass/fail criteria.
[ ] Check for MVP requirements without validation methods.
[ ] Check for acceptance criteria without acceptance tests or gaps.
[ ] Check USER_DIRECTIVES.md and approval log.
```

If a blocking issue remains, produce a blocker report and partial `result.md` instead of presenting Stage 8 as ready.

## 6. Execution Procedure

### Step 1. Consolidate Inputs Used

List all artifacts used, grouped as:

```text
Always-read source artifacts
Conditional source artifacts
Stage 8 artifacts
Context files
User directive files
Missing or unavailable files
```

### Step 2. Verify Official Artifact Completeness

Check required artifacts:

```text
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
```

For each, verify:

- status exists;
- required sections exist;
- it is not incorrectly marked Approved without human approval;
- open questions and assumptions are visible;
- it does not include out-of-scope behavior as MVP validation unless approved.

### Step 3. Verify Conditional Artifacts and N/A Records

For each conditional artifact, classify as:

```text
Created
Not applicable
Needed but missing
Deferred
Blocked by open question
```

N/A records must include:

```text
Artifact
Why not applicable
Revisit if
Related requirement or decision
```

### Step 4. Verify Coverage and Traceability

Check that Stage 8 creates or prepares these links:

```text
Requirement ID → Acceptance Criteria ID
Acceptance Criteria ID → Acceptance Test ID
Acceptance Test ID → Validation Method
Acceptance Test ID → Command ID or Manual Test ID
Validation Gap ID → Affected Requirement / Acceptance Criteria
```

If task IDs do not exist yet, mark:

```text
Task: TBD in Stage 9
```

Do not invent Stage 9 task IDs.

### Step 5. Update TRACEABILITY_MATRIX.md

Update or prepare:

```text
/workflow/context/TRACEABILITY_MATRIX.md
```

Use stable IDs:

```text
AT-001     Acceptance test
CMD-001    Validation command
MAN-001    Manual test
FX-001     Fixture/test data need
VG-001     Validation gap
```

Preserve existing IDs and links. If traceability cannot be completed, record traceability gaps.

### Step 6. Create or Update result.md

Create or update:

```text
/workflow/08_test_strategy/result.md
```

Required structure:

```markdown
# Result: 08 Test Strategy & Validation Harness

## 1. Task Summary

## 2. Inputs Used

## 3. Outputs Created or Updated

## 4. Validation Strategy Summary

## 5. Coverage Summary

## 6. Missing Information

## 7. Decision Candidates

## 8. Working Assumptions

## 9. Open Questions

## 10. Risks and Constraints

## 11. N/A Records

## 12. Traceability Updates

## 13. Human Approval Required

## 14. Recommended Next Step
```

### Step 7. Update Context Files

Update or prepare the following context files when applicable:

```text
/workflow/context/ASSUMPTIONS.md
- update if validation assumptions exist.

/workflow/context/OPEN_QUESTIONS.md
- update if unresolved validation questions exist.

/workflow/context/REJECTED_OPTIONS.md
- update if validation approaches were explicitly rejected or superseded.

/workflow/context/TRACEABILITY_MATRIX.md
- update if links were introduced or changed.
```

Do not update:

```text
/workflow/context/DECISIONS.md
```

unless explicit human approval exists.

### Step 8. Update context_packet.md for Stage 9

Update or prepare:

```text
/workflow/context/context_packet.md
```

Required structure:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 08 Test Strategy & Validation Harness
- Completed stages:
- Next recommended stage: 09 Task Breakdown

## 2. Approved Decisions
- Only human-approved validation decisions.

## 3. Working Assumptions
- Validation assumptions that Stage 9 must preserve or confirm.

## 4. Open Questions
- Questions that may affect task size, task order, required tests, or implementation prompts.

## 5. Rejected / Superseded Options
- Validation approaches that should not be revived unless reopened.

## 6. Constraints That Must Not Be Violated
- Test scope constraints
- Security/privacy constraints
- MVP scope constraints
- Tooling/environment constraints
- Manual validation constraints

## 7. Key Context for Next Stage
- Required tests per requirement
- Required commands or placeholders
- Test data/fixture needs
- Manual validation requirements
- Validation gaps

## 8. Required Inputs for Next Stage
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/07_mvp_release/07_mvp_scope.md
- /workflow/08_test_strategy/08_test_strategy.md
- /workflow/08_test_strategy/08_acceptance_tests.md
- /workflow/08_test_strategy/08_validation_commands.md
- /workflow/08_test_strategy/08_manual_test_plan.md
- /workflow/context/TRACEABILITY_MATRIX.md

## 9. Do Not Do
- Do not create implementation tasks without required tests.
- Do not treat command placeholders as confirmed commands.
- Do not include out-of-scope features in MVP task cards.
- Do not ignore validation gaps.
```

Keep `context_packet.md` concise. It is a navigation layer, not the sole source of truth.

### Step 9. Prepare Human Approval Gate

Present the final approval section exactly enough for human review.

## 7. Output Artifacts

Mandatory finalizer outputs:

```text
/workflow/08_test_strategy/result.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/context_packet.md
```

The finalizer may update these artifacts only to align inconsistencies or add final status/gap information:

```text
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
```

Conditional artifacts must be listed as created, N/A, deferred, or missing.

## 8. Traceability Rules

Required links:

```text
Requirement ID → Acceptance Criteria ID
Acceptance Criteria ID → Acceptance Test ID
Acceptance Test ID → Validation Method
Acceptance Test ID → Command ID or Manual Test ID
Command ID → Fixture ID, if applicable
Manual Test ID → Requirement ID
Validation Gap ID → Affected Requirement / Acceptance Criteria
```

Prohibited premature links:

```text
Acceptance Test ID → Implementation Task ID
Command ID → Implementation Evidence ID
Manual Test ID → Release Approval
```

Those are completed later by Stage 9, Stage 11, and Stage 12.

## 9. Decision / Assumption / Open Question Rules

Classify all final statements:

```text
Approved Decision
Decision Candidate
Working Assumption
Open Question
Rejected Option
Risk
Recommendation
```

Rules:

- Only explicit human approval can create an approved decision.
- Agent recommendations are decision candidates, not decisions.
- Working assumptions remain assumptions until confirmed.
- Open questions that affect Stage 9 must be in `context_packet.md`.
- Rejected validation approaches must not be revived unless reopened.

## 10. Human Approval Required

The final `result.md` must include this section:

```markdown
## Human Approval Required

### Decisions to Approve
- Automated test scope for MVP
- Manual validation scope for MVP
- Required validation commands or command placeholders
- CI validation expectations
- Security/privacy validation scope
- Performance/accessibility validation scope, if applicable
- Validation gaps accepted for task breakdown

### Assumptions to Confirm
- Test runner/tool assumptions
- Fixture/test data assumptions
- Environment assumptions
- Manual-only validation assumptions

### Open Questions to Resolve
- Questions blocking test design
- Questions blocking validation commands
- Questions affecting Stage 9 task cards

### Risks to Review
- Untestable or ambiguous requirements
- High-risk flows with weak validation
- Security/privacy-sensitive flows without automated coverage
- External dependency validation limitations

### Artifacts Ready for Review
- /workflow/08_test_strategy/08_test_strategy.md
- /workflow/08_test_strategy/08_acceptance_tests.md
- /workflow/08_test_strategy/08_validation_commands.md
- /workflow/08_test_strategy/08_manual_test_plan.md
- /workflow/08_test_strategy/result.md

### Recommended Next Step
- After human approval, run Stage 9 Task Breakdown using Stage 8 validation artifacts as official inputs.
```

## 11. Validation Checklist

Before finishing 08e, verify:

```text
[ ] Every MVP requirement has at least one validation method or recorded gap.
[ ] Every acceptance criterion has at least one acceptance test or recorded gap.
[ ] Acceptance tests have stable IDs.
[ ] Commands or placeholders are linked to automated/hybrid tests.
[ ] Command placeholders are not treated as confirmed commands.
[ ] Manual tests have pass/fail criteria and evidence expectations.
[ ] Security/privacy-sensitive behavior has coverage or a gap.
[ ] Role and permission behavior has coverage where applicable.
[ ] Data access, retention, deletion, and migration behavior has coverage where applicable.
[ ] External integrations have contract, mock, sandbox, or manual validation strategy where applicable.
[ ] Conditional artifacts are created or have N/A records.
[ ] TRACEABILITY_MATRIX.md is updated or traceability gaps are recorded.
[ ] context_packet.md prepares Stage 9 only with minimal needed context.
[ ] Decision candidates, assumptions, open questions, and risks are separated.
[ ] No Stage 8 artifact is marked Approved without explicit human approval.
[ ] Human approval gate is explicit.
```

## 12. Failure Handling

If finalization cannot be completed safely, produce a blocker report in `result.md`:

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

Common blockers:

```text
- missing requirements or acceptance criteria;
- missing MVP scope;
- Stage 8 artifacts contradict each other;
- high-risk validation gaps are hidden;
- command placeholders are treated as confirmed;
- security/privacy validation required but absent;
- manual tests lack pass/fail criteria;
- downstream Stage 9 would not know required tests.
```

## 13. Do Not Do

Do not:

- approve Stage 8 artifacts yourself;
- update DECISIONS.md without explicit human approval;
- create Stage 9 task cards;
- implement tests or code;
- claim tests passed;
- hide validation gaps;
- treat command placeholders as confirmed commands;
- include out-of-scope features in MVP validation;
- rely on internal sub-skill folders as downstream source of truth;
- copy entire artifacts into context_packet.md;
- skip the human approval gate.
