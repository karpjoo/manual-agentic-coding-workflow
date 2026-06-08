---
name: 07b_mvp_scope_classification
description: Classify approved requirements and capabilities into Must, Should, Could, Later, and Won't/Non-scope categories and draft the MVP scope artifact.
stage: 07 MVP Scope & Release Slicing
parent_skill: /skills/07_mvp_release_slicing/SKILL.md
subskill_id: 07b
subskill_order: 2
previous_subskill: /skills/07_mvp_release_slicing/07a_scope_input_review/SKILL.md
next_subskill: /skills/07_mvp_release_slicing/07c_release_slicing_dependency/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/07_mvp_release/07_mvp_scope.md
requires_human_approval: true
external_visibility: internal
---

# 07b MVP Scope Classification

## 1. Purpose

Classify requirements and capabilities into MVP and non-MVP categories. Draft `/workflow/07_mvp_release/07_mvp_scope.md` with clear rationale and traceability.

This sub-SKILL proposes MVP scope but does not make it approved. Human approval is required at the Stage 7 finalizer gate.

## 2. When to Use

Run after `07a_scope_input_review` has produced the scope inventory or when equivalent approved input inventory already exists.

## 3. Required Inputs

### Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/01_goal/01_service_goal.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/07_mvp_release/_internal/07a_scope_input_review.md
/workflow/07_mvp_release/_internal/07a_scope_inventory.md
```

### Read If Applicable

```text
/workflow/02_stakeholders_risk/02_stakeholders.md — if stakeholder priority affects MVP.
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md — if security/privacy constraints affect MVP minimums.
/workflow/04_domain/04_business_rules_invariants.md — if invariants define required behavior.
/workflow/05_architecture/05_architecture_plan.md — if architecture dependencies affect MVP feasibility.
/workflow/06_data/06_conceptual_data_model.md — if data entities affect MVP completeness.
/workflow/06_data/06_data_security_rules.md — if access rules are required for MVP safety.
/workflow/07_mvp_release/USER_DIRECTIVES.md — if present.
```

### Do Not Read By Default

```text
implementation code
later-stage task cards
test strategy drafts
unapproved scope brainstorming notes
```

## 4. USER_DIRECTIVES.md Handling

Apply stage-local directives before Agent assumptions. If directives attempt to override approved requirements or decisions, report a conflict instead of silently changing scope.

## 5. Input Preflight Procedure

```text
[ ] 07a outputs or equivalent inventory exist.
[ ] Approved requirements and acceptance criteria are available.
[ ] Rejected options were checked.
[ ] Scope-affecting open questions were identified.
[ ] Security/privacy/data constraints affecting MVP inclusion were checked.
```

## 6. Scope Classification Criteria

Use these categories:

```text
Must — required for MVP value, correctness, safety, legal/privacy/security compliance, or required dependency.
Should — important but not required to validate core MVP value.
Could — useful enhancement with low MVP necessity.
Later — valid future direction intentionally deferred.
Won't / Non-scope — explicitly excluded unless reopened by human approval.
```

Apply these decision criteria:

```text
- essential to primary service goal;
- essential to primary user value;
- necessary for meaningful validation;
- required for security, privacy, compliance, or data integrity;
- required dependency for another MVP item;
- can be manually simulated for MVP;
- can be deferred without invalidating the MVP;
- high complexity relative to MVP value;
- unresolved uncertainty requiring later discovery;
- explicitly rejected or marked non-scope.
```

## 7. Execution Procedure

1. Restate the MVP classification task.
2. Review service goal, requirements, acceptance criteria, and 07a inventory.
3. Define classification criteria used for this project.
4. Classify each requirement or capability into Must, Should, Could, Later, or Won't.
5. Separate user-visible MVP scope from supporting/enabling scope.
6. Identify MVP security, privacy, data, and operational minimums that must not be deferred.
7. Identify scope risks and uncertain classifications.
8. Draft `/workflow/07_mvp_release/07_mvp_scope.md`.
9. Record assumptions, open questions, decision candidates, and risks.
10. Prepare handoff notes for `07c_release_slicing_dependency`.

## 8. Output Artifacts

### Official Draft Artifact

```text
/workflow/07_mvp_release/07_mvp_scope.md
```

### Internal Working Artifact

```text
/workflow/07_mvp_release/_internal/07b_mvp_scope_classification_notes.md
```

## 9. Required Output Structure

`07_mvp_scope.md`:

```markdown
# 07 MVP Scope

## 1. Stage Status
- Status: Draft / Needs Review / Approved
- Source artifacts:
- Approval required:

## 2. MVP Definition Summary
- MVP purpose:
- Primary user value:
- Minimum success outcome:
- What the MVP proves:
- What the MVP intentionally does not prove:

## 3. Scope Classification Method
- Categories:
- Decision criteria:
- Constraints considered:

## 4. MVP Must-Have Scope
| Scope Item ID | Requirement IDs | Capability | User / Actor | Acceptance Criteria Links | Rationale | Dependency Notes |
|---|---|---|---|---|---|---|

## 5. MVP Supporting / Enabling Scope
| Scope Item ID | Requirement IDs | Enabling Capability | Why Needed for MVP | Architecture/Data Dependency | User-visible? |
|---|---|---|---|---|---|

## 6. Should-Have Candidates
| Scope Item ID | Requirement IDs | Capability | Why Not Must | Risk If Deferred | Reconsideration Trigger |
|---|---|---|---|---|---|

## 7. Could-Have Candidates
| Scope Item ID | Requirement IDs | Capability | Value | Deferral Rationale | Reconsideration Trigger |
|---|---|---|---|---|---|

## 8. Later Release Items
| Scope Item ID | Requirement IDs | Capability | Proposed Release | Deferral Rationale | Dependency Notes |
|---|---|---|---|---|---|

## 9. Won't / Non-Scope Items
| Scope Item ID | Requirement IDs | Capability / Idea | Reason Excluded | Reopen Only If |
|---|---|---|---|---|

## 10. Security / Privacy / Compliance Scope Notes
## 11. Operational / Deployment Scope Notes
## 12. Scope Risks
## 13. Decision Candidates
## 14. Working Assumptions
## 15. Open Questions
## 16. Human Approval Required
```

## 10. Traceability Rules

Use stable IDs: `SCOPE-001`, `SCOPE-002`. Link every scope item to requirement IDs and acceptance criteria where available. Record gaps instead of inventing missing links.

## 11. Validation Checklist

```text
[ ] Each requirement was considered.
[ ] MVP Must items are justified.
[ ] Supporting/enabling scope is separated from user-visible scope.
[ ] Deferred items are not treated as rejected.
[ ] Non-scope items require explicit rationale.
[ ] Security/privacy/compliance minimums were checked.
[ ] Draft status is clear.
```

## 12. Human Approval Gate

Mark MVP classifications as decision candidates. Do not claim approval. Final approval happens after `07e_mvp_release_finalizer`.

## 13. Context Packet Update Rules

Do not prepare Stage 8 context. Provide local handoff notes for `07c`. The finalizer updates `/workflow/context/context_packet.md`.

## 14. Do Not Do

- Do not create release slices beyond preliminary notes.
- Do not create detailed test plans.
- Do not create implementation tasks.
- Do not update DECISIONS.md.
- Do not call deferred items rejected unless explicitly approved as non-scope.
