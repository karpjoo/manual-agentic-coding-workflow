---
name: 07d_out_of_scope_deferral_risk
description: Separate deferred items, explicit non-scope items, rejected options, scope creep risks, and release deferral risks.
stage: 07 MVP Scope & Release Slicing
parent_skill: /skills/07_mvp_release_slicing/SKILL.md
subskill_id: 07d
subskill_order: 4
previous_subskill: /skills/07_mvp_release_slicing/07c_release_slicing_dependency/SKILL.md
next_subskill: /skills/07_mvp_release_slicing/07e_mvp_release_finalizer/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/07_mvp_release/07_out_of_scope.md
requires_human_approval: true
external_visibility: internal
---

# 07d Out-of-Scope, Deferral, and Risk Review

## 1. Purpose

Clarify what is deferred, what is explicitly out of scope, what has been rejected, and what scope risks may affect MVP/release execution.

This sub-SKILL prevents deferred items from being confused with rejected items and prevents scope creep from re-entering later stages silently.

## 2. When to Use

Run after `07c_release_slicing_dependency` drafts release slices.

## 3. Required Inputs

### Always Read

```text
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
```

### Read If Applicable

```text
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md — if deferral affects security/privacy/compliance.
/workflow/05_architecture/05_architecture_decisions.md — if deferral affects architecture trade-offs.
/workflow/06_data/06_data_security_rules.md — if deferral affects safe data access.
/workflow/06_data/06_migration_plan.md — if deferral affects migration or rollout.
/workflow/07_mvp_release/07_dependency_map.md — if created by 07c.
/workflow/07_mvp_release/USER_DIRECTIVES.md — if present.
```

### Do Not Read By Default

```text
implementation files
test strategy drafts
unapproved product brainstorming notes
later-stage task artifacts
```

## 4. USER_DIRECTIVES.md Handling

If user directives define non-scope, deferral, or rejection, distinguish explicit approved rejection from preference or tentative scope guidance. Report conflicts with DECISIONS.md or upstream artifacts.

## 5. Input Preflight Procedure

```text
[ ] 07_mvp_scope.md exists.
[ ] 07_release_slices.md exists.
[ ] REJECTED_OPTIONS.md was checked.
[ ] Deferred items and non-scope items are distinguishable.
[ ] Security/privacy/compliance deferral risks were checked.
```

## 6. Classification Rules

Use these distinctions:

```text
Deferred — valid requirement or capability intentionally moved to a later release.
Explicit Non-Scope — item the current product/release plan must not build unless reopened.
Rejected Option — explicitly rejected or superseded approach that must not reappear.
Scope Creep Watchlist — attractive item likely to reappear without approval.
Open Question — unresolved item that cannot yet be classified safely.
```

## 7. Execution Procedure

1. Restate the deferral and out-of-scope review task.
2. Extract all Should, Could, Later, and Won't items from `07_mvp_scope.md`.
3. Extract release deferrals from `07_release_slices.md`.
4. Compare with `REJECTED_OPTIONS.md` and approved decisions.
5. Separate deferred items from explicit non-scope items.
6. Identify scope creep watchlist items.
7. Identify deferral risks and mitigation.
8. Create `/workflow/07_mvp_release/07_out_of_scope.md`.
9. Create `/workflow/07_mvp_release/07_release_risk_register.md` if significant risks exist.
10. Create `/workflow/07_mvp_release/07_scope_tradeoff_analysis.md` if multiple plausible MVP boundaries require human comparison.
11. Record assumptions, open questions, risks, and decision candidates.
12. Prepare handoff notes for `07e_mvp_release_finalizer`.

## 8. Output Artifacts

### Official Draft Artifact

```text
/workflow/07_mvp_release/07_out_of_scope.md
```

### Conditional Artifacts

```text
/workflow/07_mvp_release/07_release_risk_register.md — create if significant release or deferral risks exist.
/workflow/07_mvp_release/07_scope_tradeoff_analysis.md — create if multiple plausible MVP boundaries require human comparison.
```

### Internal Working Artifact

```text
/workflow/07_mvp_release/_internal/07d_deferral_risk_notes.md
```

## 9. Required Output Structure

`07_out_of_scope.md`:

```markdown
# 07 Out of Scope

## 1. Purpose

## 2. Explicit Non-Scope Items
| Non-Scope ID | Item | Related Requirement / Idea | Reason | Reopen Only If | Notes |
|---|---|---|---|---|---|

## 3. Deferred but Not Rejected Items
| Deferred ID | Item | Deferred To | Reason | Reconsideration Trigger | Risk If Forgotten |
|---|---|---|---|---|---|

## 4. Rejected Options to Record
| Rejected Option | Source | Reason Rejected | Must Not Reappear Unless |
|---|---|---|---|

## 5. Scope Creep Watchlist
| Watch Item | Why It May Reappear | How To Handle |
|---|---|---|

## 6. Open Questions Affecting Scope

## 7. Human Approval Required
```

`07_release_risk_register.md`, if created:

```markdown
# 07 Release Risk Register

| Risk ID | Risk | Affected Scope / Release | Severity | Likelihood | Mitigation | Owner / Review Needed |
|---|---|---|---|---|---|---|
```

`07_scope_tradeoff_analysis.md`, if created:

```markdown
# 07 Scope Tradeoff Analysis

| Option ID | MVP Boundary Option | Pros | Cons | Risks | Recommended? | Human Decision Needed |
|---|---|---|---|---|---|---|
```

## 10. Traceability Rules

Use stable IDs: `NON-SCOPE-001`, `DEF-001`, `RISK-001`. Link each item to requirement IDs or source decisions where available.

## 11. Validation Checklist

```text
[ ] Deferred items are not mislabeled as rejected.
[ ] Explicit non-scope items include reopen conditions.
[ ] Rejected options align with REJECTED_OPTIONS.md or explicit user instruction.
[ ] Scope creep watchlist is present if relevant.
[ ] Deferral risks are recorded.
[ ] Security/privacy/compliance deferral risks were checked.
```

## 12. Human Approval Gate

Non-scope, rejection, and release-risk items require human review. The final approval gate is prepared by `07e_mvp_release_finalizer`.

## 13. Context Packet Update Rules

Do not prepare Stage 8 context yet. Provide local handoff notes for finalizer. The finalizer updates `/workflow/context/context_packet.md`.

## 14. Do Not Do

- Do not reject items without explicit basis.
- Do not erase deferred items.
- Do not change requirements.
- Do not write test strategy.
- Do not update DECISIONS.md without approval.
