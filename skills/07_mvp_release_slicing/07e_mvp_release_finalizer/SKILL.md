---
name: 07e_mvp_release_finalizer
description: Consolidate Stage 7 MVP scope and release slicing artifacts, update traceability, prepare Stage 8 context handoff, and present the human approval gate.
stage: 07 MVP Scope & Release Slicing
parent_skill: /skills/07_mvp_release_slicing/SKILL.md
subskill_id: 07e
subskill_order: 5
previous_subskill: /skills/07_mvp_release_slicing/07d_out_of_scope_deferral_risk/SKILL.md
next_stage: 08 Test Strategy & Validation Harness
version: 1.0.0
status: draft
primary_output: /workflow/07_mvp_release/result.md
requires_human_approval: true
external_visibility: internal
---

# 07e MVP Release Finalizer

## 1. Purpose

Finalize Stage 7 by consolidating MVP scope, release slices, out-of-scope records, traceability, context handoff, and human approval gate.

This sub-SKILL prepares official Stage 7 artifacts for review. It does not make Agent proposals approved decisions.

## 2. When to Use

Run after `07a`, `07b`, `07c`, and `07d` have completed, or when equivalent Stage 7 draft artifacts already exist.

## 3. Required Inputs

### Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/01_goal/01_service_goal.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/03_requirements/03_traceability_matrix.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/06_data/result.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md
```

### Read If Applicable

```text
/workflow/07_mvp_release/07_dependency_map.md — if created.
/workflow/07_mvp_release/07_release_risk_register.md — if created.
/workflow/07_mvp_release/07_scope_tradeoff_analysis.md — if created.
/workflow/07_mvp_release/07_specialization_scope_notes.md — if created.
/workflow/07_mvp_release/_internal/07a_scope_input_review.md — if available.
/workflow/07_mvp_release/_internal/07a_scope_inventory.md — if available.
/workflow/07_mvp_release/_internal/07b_mvp_scope_classification_notes.md — if available.
/workflow/07_mvp_release/_internal/07c_release_slicing_notes.md — if available.
/workflow/07_mvp_release/_internal/07d_deferral_risk_notes.md — if available.
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md — if security/privacy constraints affect approval.
/workflow/06_data/06_data_security_rules.md — if data access affects MVP safety.
/workflow/07_mvp_release/USER_DIRECTIVES.md — if present.
```

### Do Not Read By Default

```text
implementation code
test strategy drafts
task cards
implementation prompts
raw chat history
superseded artifacts unless needed to resolve conflict
```

## 4. USER_DIRECTIVES.md Handling

Read USER_DIRECTIVES.md before finalization. Classify directives carefully. If a directive changes MVP scope, release order, non-scope, or approval status, report whether it is an explicit approval, correction, preference, or conflict.

## 5. Input Preflight Procedure

```text
[ ] 07_mvp_scope.md exists.
[ ] 07_release_slices.md exists.
[ ] 07_out_of_scope.md exists.
[ ] Required upstream requirements and acceptance criteria are available.
[ ] Draft artifacts are clearly marked.
[ ] Conflicts among Stage 7 artifacts were checked.
[ ] Rejected options were checked.
[ ] Conditional artifacts have been created or N/A rationale is recorded.
```

## 6. Execution Procedure

1. Restate the finalization task and Stage 7 boundary.
2. Review `07_mvp_scope.md`, `07_release_slices.md`, and `07_out_of_scope.md` for consistency.
3. Detect contradictions:
   - item marked Must but excluded from MVP;
   - item deferred but also marked non-scope;
   - rejected option reintroduced;
   - release order conflicts with architecture/data/security dependencies;
   - Stage 8 handoff includes out-of-scope items.
4. Resolve non-blocking inconsistencies by marking draft corrections; escalate blocking conflicts.
5. Create or update `/workflow/07_mvp_release/07_scope_traceability_matrix.md`.
6. Record N/A rationale for conditional artifacts not created.
7. Create or update `/workflow/07_mvp_release/result.md`.
8. Update `/workflow/context/context_packet.md` for Stage 8.
9. Update `/workflow/context/ASSUMPTIONS.md` if working assumptions exist.
10. Update `/workflow/context/OPEN_QUESTIONS.md` if unresolved questions exist.
11. Update `/workflow/context/REJECTED_OPTIONS.md` only for explicitly rejected or superseded options.
12. Do not update `/workflow/context/DECISIONS.md` unless explicit human approval exists.
13. Present the human approval gate.

## 7. Output Artifacts

### Official Stage Artifacts

```text
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md
/workflow/07_mvp_release/07_scope_traceability_matrix.md
/workflow/07_mvp_release/result.md
/workflow/context/context_packet.md
```

### Conditional Artifacts

```text
/workflow/07_mvp_release/07_dependency_map.md
/workflow/07_mvp_release/07_release_risk_register.md
/workflow/07_mvp_release/07_scope_tradeoff_analysis.md
/workflow/07_mvp_release/07_specialization_scope_notes.md
```

### Context Files to Update If Applicable

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

## 8. Required Output Structure

`07_scope_traceability_matrix.md`:

```markdown
# 07 Scope Traceability Matrix

| Goal ID | Requirement ID | Acceptance Criteria ID | Domain Concept | Architecture / Module | Data Artifact | Scope Category | Release Slice | Validation Handoff |
|---|---|---|---|---|---|---|---|---|

## Traceability Gaps
| Gap ID | Missing Link | Why Missing | Risk | Required Action |
|---|---|---|---|---|
```

`result.md`:

```markdown
# Result: 07 MVP Scope & Release Slicing

## 1. Task Summary
## 2. Inputs Used
## 3. Outputs Created or Updated
## 4. MVP Scope Summary
## 5. Release Slice Summary
## 6. Out-of-Scope Summary
## 7. Decision Candidates
## 8. Working Assumptions
## 9. Open Questions
## 10. Risks and Constraints
## 11. Rejected or Superseded Options
## 12. Traceability Updates
## 13. N/A Items
## 14. Stage 8 Handoff Notes
## 15. Human Approval Required
## 16. Recommended Next Step
```

`context_packet.md` Stage 8 update must include:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 07 MVP Scope & Release Slicing
- Completed stages:
- Next recommended stage: 08 Test Strategy & Validation Harness
- Stage 7 status: Draft / Needs Review / Approved

## 2. Approved Decisions
- Only human-approved decisions.
- If Stage 7 is not approved, state that scope is pending approval.

## 3. Working Assumptions
## 4. Open Questions
## 5. Rejected / Superseded Options
## 6. Constraints That Must Not Be Violated
## 7. Key Context for Next Stage
- MVP scope summary.
- Release slice summary.
- Non-scope items.
- Validation-sensitive risks.
- Requirements to prioritize in Stage 8.

## 8. Required Inputs for Next Stage
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/06_data/result.md
- /workflow/07_mvp_release/07_mvp_scope.md
- /workflow/07_mvp_release/07_release_slices.md
- /workflow/07_mvp_release/07_out_of_scope.md
- /workflow/07_mvp_release/07_scope_traceability_matrix.md

## 9. Do Not Do
- Do not validate out-of-scope items as MVP requirements.
- Do not create tests for deferred items unless explicitly needed as regression guards.
- Do not treat unapproved Stage 7 scope as final.
- Do not revive rejected scope items unless reopened by the human developer.
```

## 9. Traceability Rules

Required links:

```text
Service Goal → Requirement
Requirement → Acceptance Criteria
Requirement → Scope Category
Requirement → Release Slice
Release Slice → Stage 8 Validation Handoff
```

Where applicable:

```text
Requirement → Domain Invariant
Requirement → Module / API / Integration
Requirement → Data Model / Security Rule / Migration
Requirement → Release Dependency
```

Use stable IDs. Do not rename upstream IDs.

## 10. Validation Checklist

```text
[ ] Official Stage 7 artifacts exist or missing artifacts are reported.
[ ] MVP scope, release slices, and out-of-scope artifacts agree.
[ ] Deferred items are not treated as rejected.
[ ] Non-scope items include reopen conditions.
[ ] Security/privacy/compliance minimums are not silently deferred.
[ ] Release order respects architecture and data dependencies.
[ ] Stage 8 validation handoff is clear.
[ ] Traceability matrix is updated.
[ ] Conditional artifacts are created or N/A rationale is recorded.
[ ] context_packet.md is prepared for Stage 8.
[ ] Human approval gate is explicit.
```

## 11. Failure Handling

If finalization cannot safely complete, create this in `result.md`:

```markdown
## Blocker Report

### Blocking Issue
### Why It Matters
### Affected Artifacts or Stages
### Safe Partial Work Completed
### Human Decision Needed
### Recommended Recovery Step
```

Blocking examples:

```text
requirements not approved
acceptance criteria missing
MVP scope contradicts architecture/data/security constraints
rejected option reintroduced
release order unsafe
approval status cannot be determined
```

## 12. Human Approval Gate

End with:

```markdown
## Human Approval Required

### Decisions to Approve
- MVP scope items.
- Supporting/enabling scope items.
- Deferred requirements.
- Explicit out-of-scope items.
- Release slice order.
- Scope trade-offs.
- Security/privacy/compliance items that must be included in MVP.

### Assumptions to Confirm
- MVP target user and usage context.
- Acceptable manual workarounds.
- Acceptable deferrals.
- Release timeline assumptions, if any.
- Operational assumptions.

### Open Questions to Resolve
- Questions that may change MVP scope.
- Questions that may block Stage 8 validation planning.
- Questions that may affect security, privacy, data, or compliance.

### Risks to Review
- Deferral risks.
- Scope creep risks.
- Architecture/data dependency risks.
- Security/privacy risks.
- Operational readiness risks.
- Validation risks.

### Artifacts Ready for Review
- /workflow/07_mvp_release/07_mvp_scope.md
- /workflow/07_mvp_release/07_release_slices.md
- /workflow/07_mvp_release/07_out_of_scope.md
- /workflow/07_mvp_release/07_scope_traceability_matrix.md
- /workflow/07_mvp_release/result.md
- Conditional artifacts, if created.

### Recommended Next Step
- Human reviews and approves or revises MVP scope and release order.
- After approval, run Stage 8 Test Strategy & Validation Harness.
```

## 13. Do Not Do

- Do not approve Stage 7 yourself.
- Do not update DECISIONS.md without explicit approval.
- Do not create Stage 8 test strategy.
- Do not create Stage 9 task cards.
- Do not make downstream stages depend on internal sub-SKILL outputs.
- Do not use context_packet.md as the only source of truth.
