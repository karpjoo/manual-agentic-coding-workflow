---
name: 11_tdd_implementation_loop
description: Orchestrates Stage 11 implementation as a bounded per-task TDD loop using approved task cards and implementation prompts.
stage: 11 TDD Implementation Loop
version: 1.0.0
status: draft
primary_output: /workflow/11_implementation_results/result.md
requires_human_approval: true
internal_split: true
subskills:
  - /skills/11_tdd_implementation_loop/11a_task_preflight_and_red_test/SKILL.md
  - /skills/11_tdd_implementation_loop/11b_minimal_implementation_green/SKILL.md
  - /skills/11_tdd_implementation_loop/11c_refactor_regression_evidence/SKILL.md
  - /skills/11_tdd_implementation_loop/11d_implementation_finalizer/SKILL.md
---

# 11 TDD Implementation Loop Stage Entrypoint

## 1. Purpose

This SKILL is the public stage-level entrypoint for Stage 11: `11_tdd_implementation_loop`.

Use it to coordinate implementation of approved task cards through a controlled test-first or test-aware loop.

Stage 11 is not a single large implementation request. It is a repeated loop over one approved task at a time:

```text
One approved task → one bounded code change → one evidence record → one human review point
```

This parent SKILL does not perform all implementation details itself. It routes execution through smaller internal sub-SKILLs so that each agent session can remain bounded and reviewable.

---

## 2. Public Stage Contract

Stage 11 exposes one public stage package:

```text
/skills/11_tdd_implementation_loop/
```

Internal sub-SKILLs are implementation details. Downstream Stage 12 must depend only on approved official Stage 11 artifacts under `/workflow/11_implementation_results/` and `/workflow/context/`, not on sub-SKILL names, prompt history, or temporary working notes.

Official Stage 11 artifacts include:

```text
/workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/result.md
/workflow/context/context_packet.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Conditional evidence artifacts may also be produced when applicable:

```text
/workflow/11_implementation_results/11_manual_verification_{{TASK_ID}}.md
/workflow/11_implementation_results/11_migration_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_api_contract_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_security_privacy_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_ui_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_performance_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_rollback_notes_{{TASK_ID}}.md
```

Do not create `README.md` or `artifact_contract.yml` from this SKILL. Those support files are maintained separately.

---

## 3. Internal Sub-SKILL Sequence

Run the sub-SKILLs in this order for each selected `TASK_ID`:

```text
11a_task_preflight_and_red_test
→ 11b_minimal_implementation_green
→ 11c_refactor_regression_evidence
→ 11d_implementation_finalizer
```

### 11a — Task Preflight and Red Test

Validates the selected task, reads approved inputs, inspects relevant code and tests, restates scope, and writes or identifies a failing test.

### 11b — Minimal Implementation Green

Implements the smallest code change required to make the targeted test pass while preserving approved scope and forbidden-change rules.

### 11c — Refactor, Regression, and Evidence

Performs only scope-safe refactoring, runs broader validation, records regression/manual/conditional evidence, and classifies failures.

### 11d — Implementation Finalizer

Consolidates official Stage 11 task result and evidence artifacts, updates traceability and context handoff, and prepares the human approval gate.

---

## 4. When to Use

Use this stage package when all conditions are true:

```text
- Stage 9 task cards exist and are approved or explicitly authorized.
- Stage 10 implementation prompts or handoff packets exist and are approved or explicitly authorized.
- The selected task has a stable TASK_ID.
- The task has allowed change scope, forbidden changes, required tests, and definition of done.
- The agent can inspect the relevant codebase and tests.
- The user wants implementation, not task breakdown, prompt writing, architecture redesign, or release review.
```

---

## 5. When Not to Use

Do not use this stage package when:

```text
- the selected TASK_ID is missing, ambiguous, or unapproved;
- the implementation prompt is missing or unapproved;
- the task lacks allowed change scope;
- the task requires an unapproved architecture, API, data, security, privacy, or release decision;
- the agent cannot inspect the relevant codebase;
- the agent cannot record validation evidence;
- the user is asking for Stage 12 review/release/handoff instead of implementation.
```

If any blocking issue is detected, produce a blocker report instead of continuing.

---

## 6. Required Inputs

Before any sub-SKILL runs, check these common workflow files when they exist:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Always read the task and implementation inputs needed for the selected task:

```text
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_dependency_order.md
/workflow/10_prompts/10_implementation_prompts.md
/workflow/10_prompts/10_prompt_handoff_packets.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_validation_commands.md
```

If the project uses different paths, preserve the same logical roles.

---

## 7. Conditional Inputs

Read these only when activated by the task card, implementation prompt, context packet, project profile, or USER_DIRECTIVES:

```text
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_migration_plan.md
/workflow/06_data/06_data_security_rules.md
/workflow/12_review_release_handoff/review_notes.md
```

---

## 8. USER_DIRECTIVES.md Handling

If this file exists, read it before implementation:

```text
/workflow/11_implementation_results/USER_DIRECTIVES.md
```

Classify each directive as one of:

```text
explicit approval
correction
scope change
forbidden change
task priority update
test requirement update
review comment
rollback instruction
question
```

If a directive conflicts with approved task scope, implementation prompt, architecture decision, data decision, security constraint, or privacy constraint, report the conflict. Stop if the conflict changes implementation scope or risk.

Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

---

## 9. Execution Policy

### Operate on One Task

Operate on exactly one `TASK_ID` at a time unless the user explicitly authorizes a small batch.

### Preserve Approved Scope

The agent may implement only the behavior described by the approved task card and implementation prompt.

The agent must not silently expand scope based on codebase observations.

### Use TDD When Feasible

Follow this sequence whenever feasible:

```text
inspect code and tests
→ write or identify failing test
→ run test and confirm relevant failure
→ implement minimal change
→ run targeted tests
→ refactor locally if needed
→ run broader validation
→ record evidence
→ prepare human review
```

If strict test-first implementation is not feasible, document why and create a test-aware validation plan before implementation.

### Do Not Self-Approve

Agent output is not human approval. Mark task completion as `Completed Pending Human Review` until the human explicitly approves it.

---

## 10. Output Artifacts

For each `TASK_ID`, the sub-SKILL sequence must prepare or update:

```text
/workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/context_packet.md
```

The finalizer must also update:

```text
/workflow/11_implementation_results/result.md
```

Conditional artifacts must include an N/A record in the task result when not produced.

---

## 11. Human Approval Gate

At the end of each task, present:

```markdown
## Human Approval Required

### Task Completion to Approve
- TASK_ID:
- Task result artifact:
- Test evidence artifact:

### Scope Review
- Files changed:
- Scope deviations:
- Forbidden changes avoided:

### Validation Review
- Required tests passed:
- Required tests not run:
- Manual verification required:

### Decisions to Approve
- ...

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Risks to Review
- ...

### Recommended Reviewer Action
- Approve task completion | Request changes | Block task | Reopen prior stage decision
```

---

## 12. Downstream Handoff Rule

Stage 12 may use only approved Stage 11 official artifacts as source of truth.

The Stage 11 finalizer must prepare `/workflow/context/context_packet.md` for Stage 12 when implementation tasks are complete, or for the next implementation task when tasks remain.

Do not put large diffs, full logs, or prompt history into `context_packet.md`. It is a concise navigation layer.

---

## 13. Failure Handling

If Stage 11 cannot continue safely, produce a blocker report:

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
- missing or ambiguous TASK_ID
- unapproved task card
- unapproved implementation prompt
- missing allowed change scope
- unavailable codebase inspection
- unknown or unreliable test baseline
- unrelated failing test blocking reliable validation
- unapproved architecture/API/data/security/privacy/scope change required
- human changes may be overwritten
- secrets or sensitive files would need to be exposed or modified
```

---

## 14. Do Not Do

The agent must not:

```text
- treat Stage 11 as a one-shot full implementation phase;
- implement before identifying or writing a validating test unless a test-aware validation plan is recorded first;
- claim tests passed without command evidence;
- hide skipped validation;
- broaden scope beyond the approved task;
- add unrelated features;
- perform broad refactors unrelated to the task;
- change API contracts without approval;
- change database schema or migrations without approval;
- change authentication, authorization, privacy, or security behavior without approval;
- add dependencies without approval;
- overwrite human changes;
- update DECISIONS.md unless explicit human approval exists;
- mark the task complete if required evidence is missing;
- make downstream stages depend on internal sub-SKILL outputs.
```

---

## 15. Recommended Next Step

To execute Stage 11 for a task, run:

```text
/skills/11_tdd_implementation_loop/11a_task_preflight_and_red_test/SKILL.md
```

Then proceed through `11b`, `11c`, and `11d` for the same `TASK_ID`.
