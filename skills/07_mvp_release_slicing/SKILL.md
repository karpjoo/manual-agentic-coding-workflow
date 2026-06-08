---
name: 07_mvp_release_slicing
description: Stage entrypoint for MVP scope and release slicing. Use this when Stage 6 data design is complete or when the user explicitly asks to plan MVP/release scope from approved upstream artifacts.
stage: 07 MVP Scope & Release Slicing
version: 1.0.0
status: draft
primary_output: /workflow/07_mvp_release/result.md
requires_human_approval: true
internal_split: true
---

# 07 MVP Release Slicing Stage Entrypoint

## 1. Purpose

This parent SKILL orchestrates Stage 7 as a split stage package. It does not perform all analysis itself. It directs the Agent or human operator to run the Stage 7 sub-SKILLs in order, then requires finalizer consolidation and human approval before downstream stages rely on the results.

Stage 7 decides:

- what belongs in the MVP;
- what belongs in later releases;
- what is explicitly out of scope;
- what release order is coherent, testable, and safe;
- what Stage 8 Test Strategy & Validation Harness must validate next.

## 2. Public Stage Contract

Downstream stages must depend only on approved official Stage 7 artifacts, not on internal sub-SKILL outputs, prompt history, or chat context.

Official Stage 7 artifacts:

```text
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md
/workflow/07_mvp_release/07_scope_traceability_matrix.md
/workflow/07_mvp_release/result.md
/workflow/context/context_packet.md
```

Conditional Stage 7 artifacts:

```text
/workflow/07_mvp_release/07_release_risk_register.md
/workflow/07_mvp_release/07_dependency_map.md
/workflow/07_mvp_release/07_scope_tradeoff_analysis.md
/workflow/07_mvp_release/07_specialization_scope_notes.md
```

## 3. Internal Sub-SKILL Sequence

Run these sub-SKILLs in order:

```text
07a_scope_input_review
→ 07b_mvp_scope_classification
→ 07c_release_slicing_dependency
→ 07d_out_of_scope_deferral_risk
→ 07e_mvp_release_finalizer
```

Recommended paths:

```text
/skills/07_mvp_release_slicing/07a_scope_input_review/SKILL.md
/skills/07_mvp_release_slicing/07b_mvp_scope_classification/SKILL.md
/skills/07_mvp_release_slicing/07c_release_slicing_dependency/SKILL.md
/skills/07_mvp_release_slicing/07d_out_of_scope_deferral_risk/SKILL.md
/skills/07_mvp_release_slicing/07e_mvp_release_finalizer/SKILL.md
```

## 4. Required Inputs

The sub-SKILLs define detailed input contracts. At stage level, the expected upstream source artifacts are:

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

Read conditional inputs only when activated by context, project profile, USER_DIRECTIVES.md, or dependency needs.

## 5. Execution Policy

- Do not collapse all sub-SKILLs into one uncontrolled task.
- Do not treat intermediate outputs as approved Stage 7 artifacts.
- Do not create Stage 8 test strategy, Stage 9 task cards, implementation prompts, or code.
- Use approved upstream artifacts as source of truth.
- Mark draft, missing, conflicting, superseded, or unapproved inputs explicitly.
- Preserve stable requirement IDs and acceptance criteria IDs.
- Separate approved decisions, decision candidates, working assumptions, open questions, risks, rejected options, and recommendations.

## 6. Finalizer Requirement

Stage 7 is not ready for downstream use until `07e_mvp_release_finalizer` has run and official Stage 7 artifacts have been reviewed and approved by the human developer.

The finalizer must:

- consolidate official Stage 7 artifacts;
- detect contradictions across sub-SKILL outputs;
- update `07_scope_traceability_matrix.md`;
- create or update `result.md`;
- prepare `/workflow/context/context_packet.md` for Stage 8;
- present a human approval gate.

## 7. Human Approval Gate

The human developer must approve:

- MVP scope;
- MVP supporting/enabling scope;
- deferred items;
- explicit out-of-scope items;
- release order;
- scope trade-offs;
- security/privacy/compliance items that must not be deferred.

Do not proceed to Stage 8 as if Stage 7 is approved unless explicit approval exists.

## 8. Downstream Handoff Rule

Stage 8 may read Stage 7 outputs only after human approval. Stage 8 must validate approved MVP scope and release slices, not internal sub-SKILL notes.

## 9. Do Not Do

- Do not create or modify README.md or artifact_contract.yml unless explicitly instructed.
- Do not create implementation tasks.
- Do not write detailed tests.
- Do not redesign architecture or data models.
- Do not treat deferred items as rejected.
- Do not revive rejected options unless the human explicitly reopens them.
- Do not update DECISIONS.md without explicit human approval.
