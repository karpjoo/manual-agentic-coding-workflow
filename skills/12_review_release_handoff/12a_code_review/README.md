# 12a Code Review

## What this sub-SKILL is for

This reusable sub-SKILL is part of Stage 12 `12_review_release_handoff`.

Review implemented release candidate against approved requirements, acceptance criteria, task evidence, code quality, architecture boundaries, and scope control.

Core question:

```text
Does the implemented release candidate satisfy the approved scope with sufficient evidence and without code-quality, architecture, or scope-control issues that should block or warn against release?
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

- `/workflow/12_review_release_handoff/12_code_review.md` — Requirement satisfaction, evidence, code quality, architecture drift, scope control, blockers, warnings, and suggestions.

Conditional outputs:

- No conditional project artifacts. Use the mandatory artifact and handoff sections.

## Human approval requirements

This sub-SKILL prepares findings and decision candidates. It does not approve release, deployment, risk acceptance, accepted limitations, operations ownership, or handoff.

Items commonly requiring review:

- Code review blockers
- Accepted limitation candidates
- Scope drift or architecture drift findings
- Warnings that may affect release

## How to run this sub-SKILL in an Agentic Coding tool

1. Confirm the parent stage is `/skills/12_review_release_handoff/`.
2. Read this sub-SKILL's `SKILL.md`.
3. Run only this sub-SKILL's procedure.
4. Create or update only the outputs listed above.
5. Prepare the handoff section for the next sub-SKILL.

Previous sub-SKILL: `/skills/12_review_release_handoff/SKILL.md`  
Next sub-SKILL: `/skills/12_review_release_handoff/12b_security_privacy_review/SKILL.md`

## Relationship to previous and next stages

This is an internal Stage 12 sub-SKILL. Downstream Stage 13 must rely on finalized official Stage 12 artifacts, not this sub-SKILL folder.

## Draft / Approved / Needs Review

- `Draft`: Created by the agent and not yet reviewed.
- `Needs Review`: Contains unresolved blockers, warnings, assumptions, or open questions.
- `Approved`: Explicitly approved by the human developer.

## Common mistakes to avoid

- Do not implement, refactor, or deploy.
- Do not mark requirements satisfied without evidence.
- Do not approve release.
- Do not treat this sub-SKILL output as final Stage 12 approval.
- Do not bypass `12e_review_release_finalizer`.

## Troubleshooting / blocker cases

If required evidence or approved source artifacts are missing, produce a blocker report with safe partial work completed and the human decision needed.

## Recommended next step after successful execution

Run the next sub-SKILL in the Stage 12 sequence: `/skills/12_review_release_handoff/12b_security_privacy_review/SKILL.md`.
