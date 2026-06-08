# 07 MVP Release Slicing SKILL Package

## 1. What this SKILL package is for

This reusable SKILL package runs Stage 7 of the Manual Agentic Coding Workflow: MVP Scope & Release Slicing.

It helps an Agent and human developer decide what belongs in the MVP, what should be deferred, what is explicitly out of scope, and how approved requirements should be grouped into coherent release slices.

This package uses a split Stage Facade Pattern. The parent `SKILL.md` is the stage entrypoint. The sub-SKILLs perform the internal work. Downstream stages must depend only on approved official Stage 7 artifacts, not on internal sub-SKILL outputs.

## 2. When to use it

Use this package after Stage 6 Data Design is complete or when the human developer explicitly asks to plan MVP/release scope from approved upstream artifacts.

Use it when you need to:

- prevent uncontrolled MVP expansion;
- classify requirements into Must, Should, Could, Later, and Won't / Non-scope;
- define release slices that are coherent and testable;
- identify deferral and scope risks;
- prepare Stage 8 Test Strategy & Validation Harness.

## 3. When not to use it

Do not use this package to:

- rewrite service goals, requirements, architecture, or data design;
- create detailed test strategy or validation commands;
- create task cards or implementation prompts;
- implement code;
- treat unapproved Agent recommendations as approved MVP scope.

If upstream requirements, acceptance criteria, architecture, or data design are missing or unapproved, run or repair those stages first unless the human explicitly requests exploratory slicing.

## 4. Required inputs before running

At stage level, the package expects approved or clearly marked source artifacts such as:

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

## 5. Optional or conditional inputs

Read additional artifacts only when applicable:

```text
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_domain_events.md
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_authz_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_data_security_rules.md
/workflow/06_data/06_migration_plan.md
/workflow/00_intake/00_existing_context_review.md
/workflow/07_mvp_release/USER_DIRECTIVES.md
```

## 6. Sub-SKILL execution order

Run the sub-SKILLs in this order:

```text
07a_scope_input_review
→ 07b_mvp_scope_classification
→ 07c_release_slicing_dependency
→ 07d_out_of_scope_deferral_risk
→ 07e_mvp_release_finalizer
```

The stage is not ready for downstream use until the finalizer has run and the human developer has approved the official Stage 7 artifacts.

## 7. Outputs created when the SKILL package is executed

Official Stage 7 artifacts:

```text
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md
/workflow/07_mvp_release/07_scope_traceability_matrix.md
/workflow/07_mvp_release/result.md
/workflow/context/context_packet.md
```

Conditional artifacts:

```text
/workflow/07_mvp_release/07_release_risk_register.md
/workflow/07_mvp_release/07_dependency_map.md
/workflow/07_mvp_release/07_scope_tradeoff_analysis.md
/workflow/07_mvp_release/07_specialization_scope_notes.md
```

Internal working artifacts may be created under:

```text
/workflow/07_mvp_release/_internal/
```

Internal working artifacts are not downstream source of truth.

## 8. Human approval requirements

Human approval is required for:

- MVP scope;
- supporting/enabling MVP scope;
- deferred items;
- explicit out-of-scope items;
- release order;
- scope trade-offs;
- security, privacy, compliance, or operational items that must not be deferred.

Do not proceed to Stage 8 as if Stage 7 is approved until explicit approval exists.

## 9. How to run the SKILL in an Agentic Coding tool

Start with the parent skill:

```text
/skills/07_mvp_release_slicing/SKILL.md
```

Then run each sub-SKILL in order. Start a clean or bounded session for a sub-SKILL if context size becomes large. Each sub-SKILL should rely on files, not prior chat history.

Do not edit `SKILL.md` for project-specific information. Put project-specific corrections or instructions in:

```text
/workflow/07_mvp_release/USER_DIRECTIVES.md
```

## 10. Relationship to previous and next stages

Previous stage:

```text
06 Data Design
```

Stage 7 uses approved requirements, architecture, and data design to decide MVP and release scope. It does not redesign those artifacts.

Next stage:

```text
08 Test Strategy & Validation Harness
```

Stage 8 should validate the approved MVP scope and release slices. It should not validate deferred or out-of-scope items unless explicitly required as guards.

## 11. How to interpret Draft, Approved, and Needs Review

- `Draft`: Agent-created or updated artifact. Not yet a decision.
- `Needs Review`: Human review is required before downstream stages depend on it.
- `Approved`: Human developer explicitly approved the artifact or decision.

Agent output is not approval.

## 12. Common mistakes to avoid

- Treating every requirement as MVP.
- Treating deferred items as rejected.
- Creating release slices without requirement IDs.
- Ignoring architecture, data, security, privacy, or migration dependencies.
- Writing test strategy during Stage 7.
- Creating task cards during Stage 7.
- Using internal sub-SKILL outputs as downstream source of truth.
- Updating `DECISIONS.md` without explicit human approval.

## 13. Troubleshooting / blocker cases

Stop and produce a blocker report when:

- approved requirements are missing;
- acceptance criteria are missing;
- architecture or data design conflicts with MVP requirements;
- security or privacy constraints make scope unsafe;
- artifact approval status cannot be determined;
- USER_DIRECTIVES conflict with approved decisions.

Safe partial work may include an input inventory or list of conflicts, but not final MVP scope.

## 14. Recommended next step after successful execution

After `07e_mvp_release_finalizer` completes, the human developer should review and approve or revise Stage 7 artifacts. After approval, run Stage 8 Test Strategy & Validation Harness using the approved Stage 7 artifacts.
