# 12c Release / Deployment Readiness

## What this sub-SKILL is for

This reusable sub-SKILL is part of Stage 12 `12_review_release_handoff`.

Review release readiness, deployment prerequisites, environment configuration, migration readiness, rollback/recovery, smoke tests, and release notes.

Core question:

```text
Can the release candidate be safely released or deployed with current evidence, known limitations, environment readiness, rollback readiness, and human approval?
```

## When to use it

Use this sub-SKILL when running Stage 12 in the documented sequence. It should be run after its previous sub-SKILL has completed or after the parent stage entrypoint if it is the first sub-SKILL.

## When not to use it

Do not use this sub-SKILL as a standalone public stage contract for downstream stages. Do not use it to implement features, approve release, or change approved requirements/scope.

## Required inputs before running

Always check standard workflow context files and the specific inputs listed in this sub-SKILL's `SKILL.md`. Only approved artifacts may be treated as source of truth unless exploratory review is explicitly requested.

## Optional or conditional inputs

Use conditional inputs from the sub-SKILL only when project profile, context, or `USER_DIRECTIVES.md` activates them.

## Outputs created when the sub-SKILL is executed

Mandatory outputs:

- `/workflow/12_review_release_handoff/12_release_readiness.md` — Release readiness status, evidence summary, blockers, warnings, limitations, and recommended release decision.

Conditional outputs:

- `/workflow/12_review_release_handoff/12_deployment_plan.md` — if Deployment, hosting, environment promotion, or release execution is in scope.
- `/workflow/12_review_release_handoff/12_migration_readiness.md` — if Data, schema, identity, storage, or external-system migration is required.
- `/workflow/12_review_release_handoff/12_incident_rollback_plan.md` — if Rollback, recovery, or incident response requires more detail than the deployment plan.
- `/workflow/12_review_release_handoff/12_release_notes.md` — if A versioned release, client handoff, internal MVP release, or production handoff is planned.

## Human approval requirements

This sub-SKILL prepares findings and decision candidates. It does not approve release, deployment, risk acceptance, accepted limitations, operations ownership, or handoff.

Items commonly requiring review:

- Release decision candidates
- Deployment decision candidates
- Migration and rollback decisions
- Accepted limitation candidates

## How to run this sub-SKILL in an Agentic Coding tool

1. Confirm the parent stage is `/skills/12_review_release_handoff/`.
2. Read this sub-SKILL's `SKILL.md`.
3. Run only this sub-SKILL's procedure.
4. Create or update only the outputs listed above.
5. Prepare the handoff section for the next sub-SKILL.

Previous sub-SKILL: `/skills/12_review_release_handoff/12b_security_privacy_review/SKILL.md`  
Next sub-SKILL: `/skills/12_review_release_handoff/12d_operations_documentation_handoff/SKILL.md`

## Relationship to previous and next stages

This is an internal Stage 12 sub-SKILL. Downstream Stage 13 must rely on finalized official Stage 12 artifacts, not this sub-SKILL folder.

## Draft / Approved / Needs Review

- `Draft`: Created by the agent and not yet reviewed.
- `Needs Review`: Contains unresolved blockers, warnings, assumptions, or open questions.
- `Approved`: Explicitly approved by the human developer.

## Common mistakes to avoid

- Do not deploy without explicit human approval.
- Do not treat warnings as resolved without evidence.
- Do not expose secret values.
- Do not treat this sub-SKILL output as final Stage 12 approval.
- Do not bypass `12e_review_release_finalizer`.

## Troubleshooting / blocker cases

If required evidence or approved source artifacts are missing, produce a blocker report with safe partial work completed and the human decision needed.

## Recommended next step after successful execution

Run the next sub-SKILL in the Stage 12 sequence: `/skills/12_review_release_handoff/12d_operations_documentation_handoff/SKILL.md`.
