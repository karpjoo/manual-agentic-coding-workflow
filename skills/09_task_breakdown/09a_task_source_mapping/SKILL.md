---
name: 09a_task_source_mapping
description: Map approved requirements, acceptance criteria, release scope, architecture, data design, and validation strategy into task source candidates for Stage 9 Task Breakdown.
stage: 09 Task Breakdown
parent_skill: /skills/09_task_breakdown/SKILL.md
subskill_id: 09a
subskill_order: 1
previous_subskill: null
next_subskill: /skills/09_task_breakdown/09b_task_inventory_and_cards/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/09_tasks/09_task_source_map.md
requires_human_approval: false
external_visibility: internal
---

# 09a 09A Task Source Mapping

## 1. Purpose

Create an internal source map that identifies where implementation tasks should come from. This sub-skill prepares a structured mapping from approved inputs to candidate task areas; it does not create final task cards.

## 2. When to Use

Use this as sub-skill 1 of Stage 9 Task Breakdown. It must be run within `/skills/09_task_breakdown/` and should not be treated as an independent public stage.

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
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
```

Also read prior Stage 9 artifacts required by this sub-skill according to the parent execution sequence.

### Read If Applicable

```text
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_indexes.md
/workflow/06_data/06_migration_plan.md
/workflow/06_data/06_data_security_rules.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/00_intake/00_existing_context_review.md
```

### Do Not Read By Default

```text
- raw agent chat history;
- superseded artifacts;
- rejected artifacts;
- unrelated previous stage drafts;
- source code files unless brownfield task decomposition requires codebase awareness;
- internal sub-skill outputs from other stages unless promoted to official artifacts.
```

## 4. USER_DIRECTIVES.md Handling

Check `/workflow/09_tasks/USER_DIRECTIVES.md` before execution. Classify directives as approval, correction, preference, rejection, scope change, task instruction, validation instruction, risk/security constraint, or question. Report conflicts with approved decisions.

## 5. Input Preflight Procedure

```text
[ ] Read artifact_manifest.yml if available.
[ ] Read context_packet.md.
[ ] Read DECISIONS.md and APPROVAL_LOG.md if available.
[ ] Read required Stage 9 and prior-stage inputs.
[ ] Check USER_DIRECTIVES.md.
[ ] Identify missing, draft, superseded, rejected, or conflicting inputs.
[ ] Restate the current sub-skill task.
```

## 6. Execution Procedure

1. Identify the active MVP or release slice.
2. Extract in-scope requirements and acceptance criteria.
3. Exclude out-of-scope, rejected, later-release, or superseded items.
4. Identify architecture, API, integration, data, migration, security, privacy, and domain inputs affecting task boundaries.
5. Map each in-scope requirement to possible implementation areas.
6. Identify enabling task needs and coverage gaps.
7. Produce 09_task_source_map.md with handoff notes for 09b.

## 7. Output Artifacts

```text
/workflow/09_tasks/09_task_source_map.md
```

## 8. Required Output Sections

- Source Inputs Used
- Active Scope Basis
- Requirement Source Map
- Architecture / Module Source Map
- Domain / Business Rule Source Map
- Data / Migration Source Map
- Validation Source Map
- Candidate Task Areas
- Coverage Gaps
- Blocking Questions
- Handoff Notes for 09b

## 9. Traceability Rules

Preserve or improve the following links where applicable:

```text
Requirement → Acceptance Criteria → Release Slice → Task
Requirement → Acceptance Criteria → Test / Validation Method → Task
Domain Rule / Invariant → Required Test → Task
Architecture Component / API Contract → Task
Data Artifact / Security Rule → Task
Task → Future Implementation Prompt Placeholder
Task → Future Implementation Evidence Placeholder
```

Do not create tasks that cannot be traced to approved scope unless clearly marked as enabling tasks, risk-reduction spikes, or invalid candidates.

## 10. Decision / Assumption / Open Question Rules

- Approved decisions require explicit human approval.
- Agent recommendations are decision candidates.
- Working assumptions remain assumptions until confirmed.
- Open questions must be recorded if they affect task scope, order, validation, security, or Stage 10 readiness.
- Do not update `/workflow/context/DECISIONS.md` unless explicit human approval exists.

## 11. Validation Checklist

```text
[ ] Required inputs were checked.
[ ] Missing or conflicting inputs were reported.
[ ] Out-of-scope items were not converted into tasks.
[ ] Rejected options were not revived.
[ ] Validation linkage was preserved.
[ ] Traceability gaps were recorded.
[ ] Handoff notes for the next sub-skill or Stage 10 were prepared.
```

## 12. Context Packet Update Rules

Only `09e_task_breakdown_finalizer` performs the final Stage 10 `context_packet.md` handoff. Earlier sub-skills should record local handoff notes in their own output artifact and update context files only when unresolved issues or assumptions may affect later work.

## 13. Do Not Do

Do not:

```text
- create final task cards
- assign final implementation order
- write implementation prompts
- implement code
- treat candidate task areas as approved tasks
- update DECISIONS.md without explicit human approval.
```

