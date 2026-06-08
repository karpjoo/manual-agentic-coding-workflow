---
name: 12_review_release_handoff
description: Stage 12 entrypoint for final review, security/privacy review, release readiness, deployment planning, operations preparation, and documentation handoff.
stage: 12 Review / Security / Release / Handoff
version: 1.0.0
status: draft
primary_output: /workflow/12_review_release_handoff/result.md
requires_human_approval: true
internal_split: true
---

# 12 Review / Security / Release / Handoff Stage Entrypoint

## 1. Purpose

This parent `SKILL.md` is the stage-level entrypoint for Stage 12 of the Manual Agentic Coding Workflow.

Stage 12 determines whether an implemented release candidate is ready for human-approved release, deployment, operation, and handoff.

This stage is the final verification gate. It is not the first place to invent requirements, create tests, redesign architecture, or implement missing features.

The agent must review the release candidate against:

- approved requirements;
- approved acceptance criteria;
- approved MVP or release scope;
- implementation task results;
- test and validation evidence;
- security and privacy constraints;
- architecture and data decisions where applicable;
- deployment readiness;
- rollback and recovery readiness;
- operations readiness;
- documentation freshness.

## 2. Public Stage Contract

This stage exposes one public stage package:

```text
/skills/12_review_release_handoff/
```

This package is internally split into sub-SKILLs. The split is an implementation detail.

Downstream stages must depend only on approved official Stage 12 artifacts under:

```text
/workflow/12_review_release_handoff/
/workflow/context/
```

Downstream stages must not depend on:

```text
/skills/12_review_release_handoff/12a_code_review/
/skills/12_review_release_handoff/12b_security_privacy_review/
/skills/12_review_release_handoff/12c_release_deployment_readiness/
/skills/12_review_release_handoff/12d_operations_documentation_handoff/
/skills/12_review_release_handoff/12e_review_release_finalizer/
prompt history
agent scratchpads
unapproved draft outputs
```

## 3. Internal Sub-SKILL Sequence

Run the sub-SKILLs in this order:

```text
12a_code_review
→ 12b_security_privacy_review
→ 12c_release_deployment_readiness
→ 12d_operations_documentation_handoff
→ 12e_review_release_finalizer
```

### 12a_code_review

Reviews requirement satisfaction, acceptance criteria coverage, implementation evidence, code quality, architectural drift, and scope expansion.

Primary output:

```text
/workflow/12_review_release_handoff/12_code_review.md
```

### 12b_security_privacy_review

Reviews authentication, authorization, data access, personal/sensitive data handling, external transfer, secrets, logs, and security/privacy release blockers.

Primary output:

```text
/workflow/12_review_release_handoff/12_security_privacy_review.md
```

### 12c_release_deployment_readiness

Reviews release readiness, deployment plan, migration readiness, rollback/recovery, release notes, and environment readiness.

Primary outputs:

```text
/workflow/12_review_release_handoff/12_release_readiness.md
/workflow/12_review_release_handoff/12_deployment_plan.md
```

### 12d_operations_documentation_handoff

Prepares operations runbook and documentation handoff review.

Primary outputs:

```text
/workflow/12_review_release_handoff/12_operations_runbook.md
/workflow/12_review_release_handoff/12_documentation_handoff.md
```

### 12e_review_release_finalizer

Consolidates all Stage 12 outputs, classifies blockers/warnings/suggestions, updates traceability and context, and prepares the human approval gate.

Primary outputs:

```text
/workflow/12_review_release_handoff/result.md
/workflow/context/context_packet.md
```

## 4. Official Stage Artifacts

The official Stage 12 artifacts are:

```text
/workflow/12_review_release_handoff/12_code_review.md
/workflow/12_review_release_handoff/12_security_privacy_review.md
/workflow/12_review_release_handoff/12_release_readiness.md
/workflow/12_review_release_handoff/12_documentation_handoff.md
/workflow/12_review_release_handoff/result.md
/workflow/context/context_packet.md
```

Conditional official artifacts:

```text
/workflow/12_review_release_handoff/12_deployment_plan.md
/workflow/12_review_release_handoff/12_operations_runbook.md
/workflow/12_review_release_handoff/12_release_notes.md
/workflow/12_review_release_handoff/12_migration_readiness.md
/workflow/12_review_release_handoff/12_incident_rollback_plan.md
/workflow/12_review_release_handoff/12_compliance_review.md
```

If a conditional artifact is not applicable, the finalizer must record an N/A rationale in `result.md`.

## 5. Required Inputs

Every sub-SKILL must check the standard context files when available:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
```

The Stage 12 package expects these approved source artifacts when available:

```text
/workflow/01_goal/01_service_goal.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/11_implementation_results/
```

Read conditional artifacts only when project context activates them.

## 6. Execution Policy

The parent SKILL is an orchestrator.

It must not collapse the whole stage into one uncontrolled task. Run sub-SKILLs in sequence and let each sub-SKILL produce its own artifact.

The agent must:

1. Start from the parent SKILL.
2. Confirm the release review boundary.
3. Run `12a_code_review`.
4. Run `12b_security_privacy_review`.
5. Run `12c_release_deployment_readiness`.
6. Run `12d_operations_documentation_handoff`.
7. Run `12e_review_release_finalizer`.
8. Present the final human approval gate.

## 7. Finalizer Requirement

Stage 12 is not ready for downstream use until:

```text
12e_review_release_finalizer has run.
Official Stage 12 artifacts have been consolidated.
Blockers, warnings, suggestions, assumptions, and open questions have been separated.
context_packet.md has been prepared for Stage 13.
The human approval gate has been presented.
```

Sub-SKILL outputs are not final Stage 12 approval by themselves.

## 8. Human Approval Gate

The human developer must explicitly approve or reject:

```text
release readiness status
release decision
deployment decision
migration decision, if applicable
rollback/recovery readiness
accepted limitations
security/privacy risk acceptance
operations ownership
documentation handoff
```

The agent must not claim release approval without explicit human approval.

## 9. Downstream Handoff Rule

Stage 13 Workflow Retrospective & Skill Improvement may use only approved or clearly labeled Stage 12 artifacts and the updated context packet.

The finalizer must prepare:

```text
/workflow/context/context_packet.md
```

for Stage 13 with:

```text
release readiness outcome
blockers/warnings summary
evidence quality notes
agent failure patterns observed during review
human decision points
skill/template improvement candidates
required inputs for Stage 13
do-not-do instructions for Stage 13
```

## 10. Do Not Do

The agent must not:

- approve the release on behalf of the human developer;
- deploy without explicit human approval;
- perform implementation or refactoring unless explicitly instructed;
- create Stage 13 retrospective artifacts;
- modify approved requirements, release scope, or architecture decisions;
- treat missing evidence as passing evidence;
- claim tests passed without evidence;
- expose or copy secret values;
- silently accept unresolved security or privacy issues;
- treat warnings as resolved without evidence;
- collapse blockers, warnings, and suggestions into one list;
- use `context_packet.md` as the only source of truth;
- depend on internal sub-SKILL outputs as downstream public contract;
- create `README.md` or `artifact_contract.yml` as part of this SKILL generation task unless explicitly requested.
