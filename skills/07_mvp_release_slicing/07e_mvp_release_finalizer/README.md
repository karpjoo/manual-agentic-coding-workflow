# 07e MVP Release Finalizer

## 1. What this SKILL is for

This reusable sub-SKILL is part of the Stage 7 MVP Release Slicing package.

Consolidate official Stage 7 artifacts, detect contradictions, update traceability and context handoff, and prepare the human approval gate.

It is an internal sub-SKILL. Downstream stages must not depend on this sub-SKILL directly; they must depend on approved official Stage 7 artifacts after finalization.

## 2. When to use it

Use this as sub-SKILL 5 in Stage 7.

Final sub-SKILL. It consolidates official Stage 7 artifacts and prepares the public handoff to Stage 8.

## 3. When not to use it

Do not use this sub-SKILL to:

- execute the whole Stage 7 package alone;
- create Stage 8 test strategy;
- create Stage 9 task cards;
- write implementation prompts or code;
- change approved upstream requirements, architecture, or data design.

Run the previous sub-SKILL first unless equivalent approved or draft input artifacts already exist.

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
/workflow/05_architecture/05_architecture_plan.md
/workflow/06_data/result.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md
```

If a required input is missing, report it as blocking or non-blocking before continuing.

## 5. Optional or conditional inputs

Conditional inputs include project profile, USER_DIRECTIVES.md, security/privacy artifacts, integration contracts, authorization models, data security rules, migration plans, and other Stage 7 draft artifacts when applicable.

Read conditional inputs only when activated by context, project profile, USER_DIRECTIVES.md, or dependency needs.

## 6. Outputs created when the SKILL is executed

Mandatory outputs:

- `/workflow/07_mvp_release/07_mvp_scope.md` — Defines MVP scope classification, supporting scope, risks, assumptions, and approval candidates.
- `/workflow/07_mvp_release/07_release_slices.md` — Defines coherent release slices, dependency-driven ordering, risks, and Stage 8 validation handoff.
- `/workflow/07_mvp_release/07_out_of_scope.md` — Records deferred items, explicit non-scope items, rejected options, and scope creep watchlist.
- `/workflow/07_mvp_release/07_scope_traceability_matrix.md` — Links goals, requirements, acceptance criteria, scope categories, release slices, and Stage 8 validation handoff.
- `/workflow/07_mvp_release/result.md` — Summarizes Stage 7 execution, outputs, decisions needed, assumptions, risks, traceability updates, and next step.

Conditional outputs:

- `/workflow/07_mvp_release/07_release_risk_register.md` — Release sequencing introduces significant business, technical, security, privacy, operational, migration, or delivery risks.
- `/workflow/07_mvp_release/07_dependency_map.md` — Release slices have non-trivial dependencies across requirements, bounded contexts, modules, APIs, integrations, data models, or migrations.
- `/workflow/07_mvp_release/07_scope_tradeoff_analysis.md` — Multiple plausible MVP boundaries require human comparison.
- `/workflow/07_mvp_release/07_specialization_scope_notes.md` — A project-type specialization adds scope concerns such as AI evaluation, mobile release constraints, regulated gates, or brownfield migration constraints.

## 7. Human approval requirements

This sub-SKILL prepares items requiring human approval. Approval is finalized by 07e and the human developer.

Agent output is not approval. Explicit human approval is required before Stage 8 relies on official Stage 7 artifacts.

## 8. How to run the SKILL in an Agentic Coding tool

Open or invoke:

```text
/skills/07_mvp_release_slicing/07e_mvp_release_finalizer/SKILL.md
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
/skills/07_mvp_release_slicing/07d_out_of_scope_deferral_risk/SKILL.md
```

Next sub-SKILL or stage:

```text
08 Test Strategy & Validation Harness, after finalizer completion and human approval.
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

After human approval, run Stage 8 Test Strategy & Validation Harness.
