---
name: 07c_release_slicing_dependency
description: Convert draft MVP scope into coherent release slices and identify architecture, data, security, privacy, integration, and migration dependencies.
stage: 07 MVP Scope & Release Slicing
parent_skill: /skills/07_mvp_release_slicing/SKILL.md
subskill_id: 07c
subskill_order: 3
previous_subskill: /skills/07_mvp_release_slicing/07b_mvp_scope_classification/SKILL.md
next_subskill: /skills/07_mvp_release_slicing/07d_out_of_scope_deferral_risk/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/07_mvp_release/07_release_slices.md
requires_human_approval: true
external_visibility: internal
---

# 07c Release Slicing and Dependency Ordering

## 1. Purpose

Create coherent, testable release slices from the draft MVP scope and upstream architecture/data constraints. Identify dependencies that affect release order.

This sub-SKILL drafts release order. It does not approve release order.

## 2. When to Use

Run after `07b_mvp_scope_classification` has drafted `/workflow/07_mvp_release/07_mvp_scope.md`.

## 3. Required Inputs

### Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/result.md
/workflow/07_mvp_release/07_mvp_scope.md
```

### Read If Applicable

```text
/workflow/04_domain/04_bounded_contexts.md — if release slices cross domain boundaries.
/workflow/04_domain/04_domain_events.md — if workflows/events affect sequencing.
/workflow/05_architecture/05_api_contracts.md — if APIs affect slice boundaries.
/workflow/05_architecture/05_integration_contracts.md — if integrations affect release sequencing.
/workflow/05_architecture/05_authz_model.md — if authorization affects release sequencing.
/workflow/05_architecture/05_event_contracts.md — if async workflows exist.
/workflow/06_data/06_logical_schema.md — if persistent data exists.
/workflow/06_data/06_physical_schema.md — if storage choices affect sequencing.
/workflow/06_data/06_indexes.md — if performance/query constraints affect release readiness.
/workflow/06_data/06_migration_plan.md — if migration affects release order.
/workflow/06_data/06_data_security_rules.md — if data access rules affect safe release.
/workflow/07_mvp_release/USER_DIRECTIVES.md — if present.
```

### Do Not Read By Default

```text
implementation prompts
later-stage task cards
test implementation files
superseded architecture/data drafts
```

## 4. USER_DIRECTIVES.md Handling

Apply release sequencing directives if they do not conflict with approved decisions. Report conflicts involving architecture, data, privacy, security, or release commitments.

## 5. Input Preflight Procedure

```text
[ ] 07_mvp_scope.md exists and is marked Draft or Needs Review.
[ ] Architecture and data constraints were checked.
[ ] Security/privacy/access-control dependencies were checked.
[ ] Integration and migration dependencies were checked if applicable.
[ ] Rejected options were not revived.
```

## 6. Release Slicing Principles

Create release slices that are:

```text
coherent
value-oriented
traceable to requirements
small enough for later task breakdown
testable by Stage 8
safe with respect to data/security/privacy constraints
consistent with architecture and data dependencies
```

Preferred release pattern:

```text
R0 Foundation / Setup, if needed
R1 MVP
R2 Post-MVP Enhancements
R3 Advanced / Scale / Optimization, if needed
```

Do not create many releases unless the dependency structure requires it.

## 7. Execution Procedure

1. Restate the release slicing task.
2. Review draft MVP scope and supporting/enabling scope.
3. Identify dependency chains across requirements, modules, APIs, integrations, auth, data, migration, and security rules.
4. Define release slices and release goals.
5. Assign scope items and requirements to release slices.
6. Identify validation focus for each release without designing detailed tests.
7. Create a dependency-driven ordering table.
8. Create `/workflow/07_mvp_release/07_dependency_map.md` if dependencies are non-trivial.
9. Create `/workflow/07_mvp_release/07_release_slices.md`.
10. Record risks, assumptions, open questions, and decision candidates.
11. Prepare handoff notes for `07d_out_of_scope_deferral_risk`.

## 8. Output Artifacts

### Official Draft Artifact

```text
/workflow/07_mvp_release/07_release_slices.md
```

### Conditional Artifact

```text
/workflow/07_mvp_release/07_dependency_map.md — create if release dependencies are non-trivial.
```

### Internal Working Artifact

```text
/workflow/07_mvp_release/_internal/07c_release_slicing_notes.md
```

## 9. Required Output Structure

`07_release_slices.md`:

```markdown
# 07 Release Slices

## 1. Release Strategy Summary
- Release strategy:
- Release slicing principle:
- Smallest coherent vertical slice:
- Validation dependency:

## 2. Release Slice Overview
| Release ID | Release Name | Goal | Scope Summary | Primary Users | Validation Focus | Status |
|---|---|---|---|---|---|---|

## 3. Release Slice Details
### Release R0 / Foundation, if applicable
### Release R1 / MVP
### Release R2 / Post-MVP
### Release R3 / Later, if needed

For each release include:
- Purpose
- Included scope items
- Linked requirements
- Acceptance criteria included
- Architecture dependencies
- Data dependencies
- Security/privacy dependencies
- Validation implications
- Exit criteria
- Not included

## 4. Dependency-Driven Ordering
| Dependency | Source | Affected Release | Why It Affects Order | Alternative |
|---|---|---|---|---|

## 5. Deferred Requirement Impact
| Requirement ID | Deferred To | Impact | Risk | Mitigation |
|---|---|---|---|---|

## 6. Release Risks
| Risk ID | Release | Risk | Severity | Mitigation | Approval Needed |
|---|---|---|---|---|---|

## 7. Stage 8 Validation Handoff
## 8. Human Approval Required
```

`07_dependency_map.md`, if created:

```markdown
# 07 Dependency Map

| Dependency ID | Depends On | Required By | Type | Source Artifact | Release Impact | Notes |
|---|---|---|---|---|---|---|
```

## 10. Traceability Rules

Use stable IDs: `REL-001`, `DEP-001`. Link releases to scope item IDs, requirement IDs, acceptance criteria IDs, and architecture/data dependencies where applicable.

## 11. Validation Checklist

```text
[ ] Release slices are value-oriented.
[ ] Release slices are testable by Stage 8.
[ ] MVP release includes all Must items or explicitly explains exclusions.
[ ] Architecture dependencies are respected.
[ ] Data/security/privacy dependencies are respected.
[ ] Integration and migration dependencies are reflected if applicable.
[ ] Release order is marked as candidate, not approved.
```

## 12. Human Approval Gate

Release slices and release order are decision candidates until human approval. Final approval happens after `07e_mvp_release_finalizer`.

## 13. Context Packet Update Rules

Do not update Stage 8 context yet. Provide local handoff notes for `07d`. The finalizer updates `/workflow/context/context_packet.md`.

## 14. Do Not Do

- Do not create task cards.
- Do not write detailed validation commands.
- Do not change architecture or data decisions.
- Do not treat release order as approved.
