---
name: 04_domain_modeling
description: Stage-level entrypoint for split Stage 04 Domain Modeling / DDD. Use this to run the Stage 4 sub-skills in order and preserve the public artifact contract for Stage 5.
stage: 04 Domain Modeling / DDD
version: 1.0.0
status: draft
primary_output: /workflow/04_domain/result.md
requires_human_approval: true
internal_split: true
---

# 04 Domain Modeling / DDD Stage Entrypoint

## 1. Purpose

This parent SKILL is the stage-level entrypoint for Stage 04 Domain Modeling / DDD.

It does not perform all domain modeling work directly. It orchestrates the following internal sub-skills:

```text
04a_ubiquitous_language
→ 04b_domain_concepts_entities_values
→ 04c_aggregates_rules_lifecycle
→ 04d_events_bounded_contexts
→ 04e_domain_modeling_finalizer
```

The purpose of Stage 4 is to model domain meaning before architecture, data design, API design, UI design, implementation, or test command design.

DDD in this workflow means:

```text
ubiquitous language
→ domain concepts
→ entities / value objects
→ aggregates and consistency boundaries
→ business rules and invariants
→ state transitions
→ domain events
→ bounded contexts
→ traceability and architecture handoff
```

It does not mean database table extraction.

## 2. Public Stage Contract

Stage 4 exposes one public stage package:

```text
/skills/04_domain_modeling/
```

The internal sub-skills are implementation details. Downstream stages must depend only on approved official Stage 4 artifacts under `/workflow/04_domain` and approved context files under `/workflow/context`.

Downstream stages must not depend on:

```text
/skills/04_domain_modeling/04a_ubiquitous_language/
/skills/04_domain_modeling/04b_domain_concepts_entities_values/
/skills/04_domain_modeling/04c_aggregates_rules_lifecycle/
/skills/04_domain_modeling/04d_events_bounded_contexts/
/skills/04_domain_modeling/04e_domain_modeling_finalizer/
prompt history
agent chat history
internal working notes unless explicitly promoted and approved
unapproved draft artifacts
```

## 3. Official Stage Artifacts

The official Stage 4 artifacts are:

```text
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_domain_traceability_matrix.md
/workflow/04_domain/result.md
/workflow/context/context_packet.md
```

Conditional official artifacts:

```text
/workflow/04_domain/04_state_lifecycle.md
- if lifecycle-bearing concepts or meaningful state transitions exist

/workflow/04_domain/04_context_map.md
- if multiple contexts, external contexts, or brownfield context relationships exist

/workflow/04_domain/04_domain_risk_notes.md
- if security, privacy, compliance, audit, sensitive data, or model risk affects domain rules

/workflow/04_domain/04_domain_model_diagrams.md
- if diagrams clarify aggregates, contexts, or state transitions

/workflow/04_domain/04_domain_open_questions.md
- if domain open questions are substantial enough to need a stage-local file
```

Conditional artifacts that are not created must be recorded with N/A rationale in `/workflow/04_domain/result.md` by the finalizer.

## 4. Required Inputs

Before running any sub-skill, verify that the following inputs exist and are approved or clearly marked as draft.

Always read or verify:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/01_goal/01_service_goal.md
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
```

Read if applicable:

```text
/workflow/00_intake/00_project_intake.md
/workflow/00_intake/00_existing_context_review.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/03_requirements/03_traceability_matrix.md
/workflow/context/APPROVAL_LOG.md
/workflow/04_domain/USER_DIRECTIVES.md
/workflow/04_domain/review_notes.md
/workflow_templates/specializations/*.md
```

## 5. Execution Policy

Run the sub-skills in order.

Do not skip the finalizer.

```text
1. Run /skills/04_domain_modeling/04a_ubiquitous_language/SKILL.md
2. Run /skills/04_domain_modeling/04b_domain_concepts_entities_values/SKILL.md
3. Run /skills/04_domain_modeling/04c_aggregates_rules_lifecycle/SKILL.md
4. Run /skills/04_domain_modeling/04d_events_bounded_contexts/SKILL.md
5. Run /skills/04_domain_modeling/04e_domain_modeling_finalizer/SKILL.md
```

Each sub-skill may produce draft official artifacts. Draft artifacts are not approved stage output.

Only after the finalizer runs and the human developer approves the Stage 4 artifacts may Stage 5 treat Stage 4 outputs as source of truth.

## 6. Input Precedence

When inputs conflict, use this precedence order:

```text
1. Current explicit user instruction
2. /workflow/04_domain/USER_DIRECTIVES.md
3. /workflow/context/APPROVAL_LOG.md and /workflow/context/DECISIONS.md
4. /workflow/context/artifact_manifest.yml
5. /workflow/context/context_packet.md
6. Approved stage artifacts
7. Working assumptions
8. Agent inference
```

Do not silently resolve conflicts. Report the conflict and stop if it affects scope, role semantics, security, privacy, domain boundaries, architecture handoff, or approval status.

## 7. Stage-Level Do Not Do

Do not:

- collapse all sub-skills into one uncontrolled task;
- design database tables;
- design API endpoints;
- choose architecture style;
- design UI screens;
- create implementation tasks;
- write test commands;
- implement code;
- invent requirements;
- treat agent-generated domain proposals as approved decisions;
- update `/workflow/context/DECISIONS.md` without explicit human approval;
- allow Stage 5 to rely on draft or internal sub-skill output.

## 8. Finalizer Requirement

The finalizer is mandatory.

`04e_domain_modeling_finalizer` must:

- read outputs from `04a` through `04d`;
- detect contradictions across terminology, concepts, rules, events, and contexts;
- consolidate official Stage 4 artifacts;
- update `/workflow/04_domain/04_domain_traceability_matrix.md`;
- update `/workflow/04_domain/result.md`;
- prepare `/workflow/context/context_packet.md` for Stage 5;
- update ASSUMPTIONS, OPEN_QUESTIONS, REJECTED_OPTIONS, and TRACEABILITY_MATRIX as applicable;
- present a human approval gate.

## 9. Human Approval Gate

Stage 4 requires human approval for:

- preferred ubiquitous language terms;
- entity and value object classifications;
- aggregate roots and aggregate boundaries;
- business rules and invariants;
- state lifecycle model, if applicable;
- domain events;
- bounded contexts and context relationships;
- single-context rationale, if applicable;
- substantial unresolved domain assumptions.

The finalizer must present the approval gate. This parent SKILL only defines the stage-level approval requirement.

## 10. Downstream Handoff Rule

Stage 5 Architecture & Technical Contracts may read Stage 4 only after Stage 4 outputs are approved.

Stage 5 should read:

```text
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_domain_traceability_matrix.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Stage 5 must not treat sub-skill folders, prompt history, or unapproved drafts as source of truth.
