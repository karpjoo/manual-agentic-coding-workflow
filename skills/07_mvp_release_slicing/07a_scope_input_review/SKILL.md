---
name: 07a_scope_input_review
description: Review approved upstream artifacts and build the Stage 7 scope input inventory before MVP classification.
stage: 07 MVP Scope & Release Slicing
parent_skill: /skills/07_mvp_release_slicing/SKILL.md
subskill_id: 07a
subskill_order: 1
previous_subskill: null
next_subskill: /skills/07_mvp_release_slicing/07b_mvp_scope_classification/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/07_mvp_release/_internal/07a_scope_input_review.md
requires_human_approval: false
external_visibility: internal
---

# 07a Scope Input Review

## 1. Purpose

Prepare Stage 7 by reviewing approved upstream artifacts, checking approval status, identifying missing or conflicting inputs, and building an internal requirement/scope inventory for MVP classification.

This sub-SKILL does not decide MVP scope. It prepares the evidence base for `07b_mvp_scope_classification`.

## 2. When to Use

Use this as the first sub-SKILL in Stage 7 after Stage 6 Data Design is complete or when the human explicitly asks to start MVP/release slicing from the current approved artifacts.

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
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/result.md
```

### Read If Applicable

```text
/workflow/02_stakeholders_risk/02_stakeholders.md — if stakeholder or actor priority affects MVP scope.
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md — if security, privacy, compliance, personal data, sensitive data, external API, or LLM transfer concerns affect release order.
/workflow/04_domain/04_ubiquitous_language.md — if terms need normalization for scope items.
/workflow/04_domain/04_bounded_contexts.md — if release slices may cross bounded contexts.
/workflow/04_domain/04_domain_events.md — if workflows or events affect release order.
/workflow/05_architecture/05_api_contracts.md — if APIs exist.
/workflow/05_architecture/05_integration_contracts.md — if integrations exist.
/workflow/05_architecture/05_authz_model.md — if roles or permissions affect MVP scope.
/workflow/06_data/06_logical_schema.md — if persistent data exists.
/workflow/06_data/06_data_security_rules.md — if data access rules affect safe release scope.
/workflow/06_data/06_migration_plan.md — if migration affects release order.
/workflow/00_intake/00_existing_context_review.md — if brownfield or legacy context exists.
/workflow/07_mvp_release/USER_DIRECTIVES.md — if present.
```

### Do Not Read By Default

```text
full historical agent logs
superseded artifacts unless checking conflict history
unrelated draft artifacts
implementation source code unless brownfield context requires it
test plans, task cards, implementation prompts, or implementation results from later stages
```

## 4. USER_DIRECTIVES.md Handling

If `/workflow/07_mvp_release/USER_DIRECTIVES.md` exists, read it before analysis. Classify each directive as approval, correction, preference, rejection, scope change, constraint, question, or new input. Report conflicts with approved decisions. Do not modify USER_DIRECTIVES.md.

## 5. Input Preflight Procedure

Perform this checklist before producing outputs:

```text
[ ] Current stage is Stage 7.
[ ] artifact_manifest.yml was checked if available.
[ ] context_packet.md was read.
[ ] DECISIONS.md and APPROVAL_LOG.md were checked if available.
[ ] USER_DIRECTIVES.md was checked.
[ ] Required upstream artifacts exist or missing items are reported.
[ ] Approval status of source artifacts is known or uncertainty is reported.
[ ] Superseded or rejected artifacts are not used as current truth.
[ ] Open questions affecting scope are identified.
[ ] Security/privacy/data/architecture constraints affecting release order are identified.
```

## 6. Execution Procedure

1. Restate the Stage 7 task and this sub-SKILL boundary.
2. Build an input inventory with artifact path, status, approval state, and relevance.
3. Extract service goals and success criteria relevant to MVP value.
4. Extract all requirement IDs and acceptance criteria IDs.
5. Extract non-functional, security, privacy, operational, and data constraints.
6. Extract domain, architecture, API, integration, data, migration, and auth dependencies affecting release order.
7. Identify existing rejected options or non-scope statements.
8. Identify missing, ambiguous, conflicting, draft, or superseded inputs.
9. Create an internal Stage 7 scope inventory.
10. Record decision candidates, assumptions, open questions, and risks.
11. Prepare handoff notes for `07b_mvp_scope_classification`.

## 7. Output Artifacts

### Internal Working Artifacts

```text
/workflow/07_mvp_release/_internal/07a_scope_input_review.md
/workflow/07_mvp_release/_internal/07a_scope_inventory.md
```

These are internal working artifacts. Downstream stages must not depend on them directly.

## 8. Required Output Structure

`07a_scope_input_review.md`:

```markdown
# 07a Scope Input Review

## 1. Task Summary
## 2. Inputs Checked
## 3. Source Artifact Status
## 4. Missing / Draft / Superseded / Rejected Inputs
## 5. Conflicts Found
## 6. Scope-Relevant Goals
## 7. Scope-Relevant Constraints
## 8. Security / Privacy / Data Concerns
## 9. Decision Candidates
## 10. Working Assumptions
## 11. Open Questions
## 12. Risks
## 13. Handoff to 07b
```

`07a_scope_inventory.md`:

```markdown
# 07a Scope Inventory

| Requirement ID | Acceptance Criteria IDs | User / Actor | Value | Constraint / Dependency | Security / Privacy Note | Source Artifact | Notes |
|---|---|---|---|---|---|---|---|
```

## 9. Traceability Rules

Preserve existing IDs. Do not rename requirements or acceptance criteria. If a link is missing, record it as a traceability gap instead of inventing it.

## 10. Validation Checklist

```text
[ ] All required inputs were checked.
[ ] Artifact approval status was considered.
[ ] Scope inventory includes all known requirements.
[ ] Acceptance criteria links are preserved where available.
[ ] Rejected options were identified.
[ ] Blocking gaps are reported.
[ ] No MVP classification was finalized.
```

## 11. Human Approval Gate

This sub-SKILL normally does not require final human approval. It must escalate if required upstream artifacts are missing, unapproved, conflicting, or unsafe to use.

## 12. Context Packet Update Rules

Do not prepare Stage 8 context. Add only local handoff notes for `07b` in the internal output. The finalizer updates `/workflow/context/context_packet.md`.

## 13. Do Not Do

- Do not decide MVP scope.
- Do not create release slices.
- Do not create official Stage 7 artifacts except internal working notes.
- Do not update DECISIONS.md.
- Do not treat missing inputs as approved assumptions.
