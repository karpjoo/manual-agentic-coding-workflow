# 07a Scope Input Review

## 1. What this SKILL is for

This reusable sub-SKILL is part of the Stage 7 MVP Release Slicing package.

Prepare the evidence base for MVP classification by checking source artifacts, approvals, missing inputs, conflicts, and scope-relevant constraints.

It is an internal sub-SKILL. Downstream stages must not depend on this sub-SKILL directly; they must depend on approved official Stage 7 artifacts after finalization.

## 2. When to use it

Use this as sub-SKILL 1 in Stage 7.

This is the first internal sub-SKILL. It prepares evidence for 07b and does not produce approved Stage 7 scope.

## 3. When not to use it

Do not use this sub-SKILL to:

- execute the whole Stage 7 package alone;
- create Stage 8 test strategy;
- create Stage 9 task cards;
- write implementation prompts or code;
- change approved upstream requirements, architecture, or data design.



## 4. Required inputs before running

This sub-SKILL reads the files specified in its `SKILL.md`. Key inputs include:

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

If a required input is missing, report it as blocking or non-blocking before continuing.

## 5. Optional or conditional inputs

Conditional inputs include project profile, USER_DIRECTIVES.md, security/privacy artifacts, integration contracts, authorization models, data security rules, migration plans, and other Stage 7 draft artifacts when applicable.

Read conditional inputs only when activated by context, project profile, USER_DIRECTIVES.md, or dependency needs.

## 6. Outputs created when the SKILL is executed

Mandatory outputs:

- `/workflow/07_mvp_release/_internal/07a_scope_input_review.md` — Records input review, source status, missing/conflicting inputs, constraints, assumptions, open questions, and handoff to 07b.
- `/workflow/07_mvp_release/_internal/07a_scope_inventory.md` — Records scope-relevant requirement inventory, acceptance criteria, dependencies, constraints, and preliminary classification signals.

Conditional outputs:

- None specific to this sub-SKILL unless activated by project profile or USER_DIRECTIVES.md.

## 7. Human approval requirements

This sub-SKILL does not normally require human approval by itself, but blockers and conflicts should be reviewed before continuing.

Agent output is not approval. Explicit human approval is required before Stage 8 relies on official Stage 7 artifacts.

## 8. How to run the SKILL in an Agentic Coding tool

Open or invoke:

```text
/skills/07_mvp_release_slicing/07a_scope_input_review/SKILL.md
```

Run it from a clean or bounded session if possible. Do not rely on prior chat history. Project-specific corrections or instructions should go in:

```text
/workflow/07_mvp_release/USER_DIRECTIVES.md
```

## 9. Relationship to previous and next stages

Parent stage package:

```text
/skills/07_mvp_release_slicing/SKILL.md
```

Previous sub-SKILL:

```text
None. This is the first sub-SKILL in Stage 7.
```

Next sub-SKILL or stage:

```text
/skills/07_mvp_release_slicing/07b_mvp_scope_classification/SKILL.md
```

## 10. How to interpret Draft, Approved, and Needs Review

- `Draft`: Agent-created or updated artifact. Not yet a decision.
- `Needs Review`: Human review is required before downstream use.
- `Approved`: Human developer explicitly approved the artifact or decision.

Internal working artifacts are not public Stage 7 source of truth.

## 11. Common mistakes to avoid

- Treating this sub-SKILL output as approved Stage 7 result.
- Skipping the finalizer.
- Reading all historical files by default.
- Silently assuming missing source artifacts.
- Updating `DECISIONS.md` without explicit human approval.
- Creating tests, task cards, implementation prompts, or code.

## 12. Troubleshooting / blocker cases

Produce a blocker report when:

- required inputs are missing;
- source artifacts are draft, superseded, rejected, or conflicting;
- USER_DIRECTIVES conflict with approved decisions;
- security, privacy, data, or architecture constraints make scope decisions unsafe;
- the sub-SKILL cannot complete its handoff safely.

## 13. Recommended next step after successful execution

Run 07b_mvp_scope_classification after reviewing the internal input inventory.
