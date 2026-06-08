---
name: 11d_implementation_finalizer
description: Consolidates Stage 11 implementation artifacts, updates traceability and context handoff, and prepares human review for one completed task.
stage: 11 TDD Implementation Loop
parent_skill: /skills/11_tdd_implementation_loop/SKILL.md
subskill_id: 11d
subskill_order: 4
previous_subskill: /skills/11_tdd_implementation_loop/11c_refactor_regression_evidence/SKILL.md
next_subskill: /skills/12_review_release_handoff/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
requires_human_approval: true
external_visibility: internal
---

# 11d Implementation Finalizer

## 1. Purpose

Consolidate official Stage 11 artifacts for one implementation task, update traceability, prepare context handoff, and present a human approval gate.

This sub-SKILL does not approve the task. It prepares the task for human review.

---

## 2. Core Question

For the selected `TASK_ID`:

```text
Are the implementation result, test evidence, traceability links, remaining risks, and next handoff context complete enough for human review?
```

---

## 3. Required Inputs

### Always Read

```text
/skills/11_tdd_implementation_loop/SKILL.md
/skills/11_tdd_implementation_loop/11a_task_preflight_and_red_test/SKILL.md
/skills/11_tdd_implementation_loop/11b_minimal_implementation_green/SKILL.md
/skills/11_tdd_implementation_loop/11c_refactor_regression_evidence/SKILL.md
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/09_tasks/09_task_cards.md
/workflow/10_prompts/10_implementation_prompts.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
```

### Read If Applicable

Read conditional evidence artifacts if created:

```text
/workflow/11_implementation_results/11_manual_verification_{{TASK_ID}}.md
/workflow/11_implementation_results/11_migration_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_api_contract_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_security_privacy_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_ui_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_performance_evidence_{{TASK_ID}}.md
/workflow/11_implementation_results/11_rollback_notes_{{TASK_ID}}.md
```

Read the corresponding previous-stage artifact when conditional evidence touches architecture, API, data, security, or privacy.

---

## 4. Finalization Preflight

Before finalizing, verify:

```text
[ ] TASK_ID is selected.
[ ] 11a Red evidence or test-aware plan exists.
[ ] 11b Green evidence exists.
[ ] 11c regression evidence exists or skipped validation is justified.
[ ] Task result draft exists.
[ ] Files changed are listed.
[ ] Tests added or modified are listed.
[ ] Commands run and results are listed.
[ ] Conditional evidence artifacts exist or N/A records are prepared.
[ ] Remaining risks are listed.
[ ] Assumptions and open questions are separated.
[ ] Traceability updates can be made or gaps are recorded.
```

If finalization cannot be completed safely, produce a blocker report.

---

## 5. Consolidate Task Result Artifact

Create or update:

```text
/workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
```

Required final structure:

```markdown
# Task Result: {{TASK_ID}} — {{TASK_TITLE}}

## 1. Status
- Status: Draft | Needs Review | Blocked | Completed Pending Human Review
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

## 11. Assumptions Used
- ...

## 12. Open Questions
- ...

## 13. Risks and Follow-up Tasks
- ...

## 14. Traceability Updates
- Requirement → Acceptance Criteria → Test → Task → Evidence links updated:
- Traceability gaps:

## 15. Conditional Artifact N/A Record
| Artifact | Why Not Applicable | Revisit If |
|---|---|---|

## 16. Human Review Required
### Review Checklist
- [ ] Code change is within approved scope.
- [ ] Required tests were added or identified.
- [ ] Required validation passed or exceptions are justified.
- [ ] No unauthorized architecture/API/data/security changes were made.
- [ ] Evidence is sufficient for reviewer confidence.

### Reviewer Decision Needed
- Approve task completion | Request changes | Block task | Reopen scope/design decision
```

Set status as:

```text
Completed Pending Human Review
  if required evidence exists and no blocker remains.

Needs Review
  if implementation may be acceptable but skipped validation, risks, or assumptions require reviewer attention.

Blocked
  if implementation cannot be validated or requires human decision before completion.

Draft
  if the result is incomplete and not ready for review.
```

---

## 6. Consolidate Test Evidence Artifact

Verify that:

```text
/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
```

contains:

```text
- Evidence Summary
- Red Step Evidence
- Green Step Evidence
- Refactor Evidence
- Regression Evidence
- Manual Verification Evidence, if applicable
- Not-Run Tests or Skipped Validation
- Failure Log Summary
```

If evidence is missing, either complete it from available records or mark the task as `Needs Review` or `Blocked`.

---

## 7. Update Traceability

Update:

```text
/workflow/context/TRACEABILITY_MATRIX.md
```

Required link pattern:

```text
Goal ID
→ Requirement ID
→ Acceptance Criteria ID
→ Domain Concept / Invariant ID
→ Architecture / Module / API / Data Component ID
→ Task ID
→ Test Case ID
→ Changed File Path
→ Test Evidence Artifact
→ Task Result Artifact
```

Use existing IDs when available.

If new implementation evidence IDs are needed, use:

```text
IMPL-{{TASK_ID}}-001
TEST-EVID-{{TASK_ID}}-001
MANUAL-EVID-{{TASK_ID}}-001
TRACE-GAP-{{TASK_ID}}-001
```

Record a traceability gap when:

```text
- a task lacks a linked requirement;
- a test lacks a linked acceptance criterion;
- a changed file cannot be linked to the approved task;
- implementation evidence cannot be linked to a validation method;
- the task requires behavior not present in approved requirements.
```

---

## 8. Update Context Files

### 8.1 context_packet.md

Update:

```text
/workflow/context/context_packet.md
```

Use this structure:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 11_tdd_implementation_loop
- Completed implementation tasks:
- Current task status:
- Next recommended task or stage:

## 2. Approved Decisions
- Only human-approved decisions.

## 3. Working Assumptions
- Assumptions used during implementation that remain relevant.

## 4. Open Questions
- Questions that may affect later implementation, review, release, security, or operations.

## 5. Rejected / Superseded Options
- Options rejected or superseded during implementation.

## 6. Constraints That Must Not Be Violated
- Approved scope constraints:
- Architecture constraints:
- Data constraints:
- Security/privacy constraints:
- Testing constraints:

## 7. Key Context for Next Task or Stage
- Minimal notes needed by the next Agent.

## 8. Required Inputs for Next Task or Stage
- Next task card or Stage 12 review inputs.
- Task result artifacts.
- Test evidence artifacts.

## 9. Do Not Do
- Do not rely on unapproved implementation outputs as final decisions.
- Do not skip review of failed or skipped validation.
- Do not broaden implementation scope based on local code observations alone.
```

Do not copy full logs, full diffs, or prompt history into `context_packet.md`.

### 8.2 ASSUMPTIONS.md

Update only if implementation used assumptions that remain relevant.

Do not convert assumptions into decisions.

### 8.3 OPEN_QUESTIONS.md

Update if unresolved questions may affect later implementation, review, release, security, or operations.

### 8.4 REJECTED_OPTIONS.md

Update if options were explicitly rejected or superseded during implementation.

### 8.5 DECISIONS.md

Do not update unless the human explicitly approved a decision.

---

## 9. Stage-Level Result

Create or update:

```text
/workflow/11_implementation_results/result.md
```

Use this concise stage-level index:

```markdown
# Result: 11_tdd_implementation_loop

## 1. Stage Summary
- Current implementation status:
- Completed tasks:
- Tasks pending review:
- Blocked tasks:

## 2. Task Evidence Index
| Task ID | Status | Task Result | Test Evidence | Reviewer Action Needed |
|---|---|---|---|

## 3. Cross-Task Risks
- ...

## 4. Traceability Status
- Updated links:
- Gaps:

## 5. Human Approval Required
- ...

## 6. Recommended Next Step
- Continue next task | Move to Stage 12 review | Resolve blockers
```

Do not turn unapproved task results into approved stage decisions.

---

## 10. Human Approval Gate

End with:

```markdown
## Human Approval Required

### Task Completion to Approve
- TASK_ID:
- Task result artifact:
- Test evidence artifact:

### Scope Review
- Files changed:
- Scope deviations: None | List
- Forbidden changes avoided: Yes | No

### Validation Review
- Required tests passed: Yes | No | Partial
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

The task is not approved until the human explicitly approves it.

---

## 11. Blocking Conditions

Stop and produce a blocker report if:

```text
- required evidence is missing;
- task result and test evidence contradict each other;
- traceability cannot be updated and the gap affects review confidence;
- required validation failed and is not classified;
- skipped validation creates unacceptable release risk;
- implementation exceeded approved scope;
- conditional security/privacy/API/data evidence is missing;
- prior sub-SKILL output is incomplete or inconsistent.
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

## 12. Do Not Do

The agent must not:

```text
- approve its own implementation;
- hide incomplete or contradictory evidence;
- update DECISIONS.md without explicit human approval;
- use sub-SKILL handoff notes as downstream source of truth without consolidation;
- mark skipped validation as passed;
- omit traceability gaps;
- copy full logs or diffs into context_packet.md;
- proceed to Stage 12 as if human approval has been granted;
- make Stage 12 depend on internal sub-SKILL outputs.
```

---

## 13. Recommended Next Step

If the task is ready for review, ask the human reviewer to choose one:

```text
- Approve task completion.
- Request changes and rerun Stage 11 for the same TASK_ID.
- Block task and reopen Stage 9 or Stage 10.
- Reopen prior architecture, API, data, security, privacy, or requirements decision.
```

If all implementation tasks are completed and approved, proceed to:

```text
/skills/12_review_release_handoff/SKILL.md
```
