---
name: 05_architecture_contracts
description: Stage 5 entrypoint for architecture and technical contract design in the Manual Agentic Coding Workflow.
stage: 05 Architecture & Technical Contracts
version: 1.0.0
status: draft
primary_output: /workflow/05_architecture/result.md
requires_human_approval: true
internal_split: true
---

# 05 Architecture & Technical Contracts Stage Entrypoint

## 1. Purpose

Use this stage package to translate approved requirements and approved domain modeling outputs into architecture direction, module boundaries, technical contracts, authorization direction, security/privacy architecture, operational policies, and Stage 6 Data Design handoff.

This parent `SKILL.md` is an orchestrator. It does not perform the whole architecture design in one pass. Run the sub-skills in order and finish with the finalizer.

## 2. Public Stage Contract

The public contract of Stage 5 is the approved set of official artifacts under `/workflow/05_architecture` and the updated workflow context files.

Downstream stages must depend on approved official Stage 5 artifacts, not on:

- internal sub-skill folder names
- intermediate notes
- prompt history
- agent chat history
- unapproved drafts

The stage is not ready for downstream use until `05e_architecture_finalizer` has run and the human developer has reviewed the official artifacts.

## 3. Internal Sub-Skill Sequence

Run the sub-skills in this order:

```text
05a_architecture_drivers_options
→ 05b_system_module_boundaries
→ 05c_technical_contracts
→ 05d_auth_security_operations
→ 05e_architecture_finalizer
```

### 05a Architecture Drivers & Options

Path:

```text
/skills/05_architecture_contracts/05a_architecture_drivers_options/SKILL.md
```

Purpose:

- Read approved prior-stage context.
- Extract architecture drivers.
- define system context and architecture options.
- recommend architecture direction as a decision candidate.
- start `/workflow/05_architecture/05_architecture_plan.md`.
- start `/workflow/05_architecture/05_architecture_decisions.md`.

### 05b System & Module Boundaries

Path:

```text
/skills/05_architecture_contracts/05b_system_module_boundaries/SKILL.md
```

Purpose:

- Define runtime/system boundaries.
- Define frontend/backend/service/module boundaries.
- Create `/workflow/05_architecture/05_module_boundaries.md`.
- update architecture plan with boundary implications.

### 05c Technical Contracts

Path:

```text
/skills/05_architecture_contracts/05c_technical_contracts/SKILL.md
```

Purpose:

- Create API contracts if APIs exist.
- Create integration contracts if external integrations exist.
- Create event/async contracts if async workflows exist.
- Record N/A rationale for non-applicable contract artifacts.

### 05d Auth, Security & Operations

Path:

```text
/skills/05_architecture_contracts/05d_auth_security_operations/SKILL.md
```

Purpose:

- Create architecture-level authn/authz model if applicable.
- Create security/privacy architecture if applicable.
- Create operational architecture if applicable.
- Create brownfield compatibility plan if applicable.
- define cross-cutting technical policies.

### 05e Architecture Finalizer

Path:

```text
/skills/05_architecture_contracts/05e_architecture_finalizer/SKILL.md
```

Purpose:

- Consolidate official Stage 5 artifacts.
- resolve contradictions among sub-skill outputs.
- finalize architecture traceability.
- create/update `/workflow/05_architecture/result.md`.
- update `/workflow/context/context_packet.md` for Stage 6 Data Design.
- prepare the human approval gate.

## 4. Official Stage Artifacts

### Mandatory Official Artifacts

The final Stage 5 package must produce or update:

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/05_architecture/05_architecture_traceability_matrix.md
/workflow/05_architecture/result.md
/workflow/context/context_packet.md
```

### Conditional Official Artifacts

Create these only when applicable. If not applicable, record N/A rationale in `result.md`.

```text
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_authn_authz_model.md
/workflow/05_architecture/05_event_contracts.md
/workflow/05_architecture/05_security_privacy_architecture.md
/workflow/05_architecture/05_operational_architecture.md
/workflow/05_architecture/05_brownfield_compatibility_plan.md
```

## 5. Required Inputs

Each sub-skill must check the workflow context files and the stage-local `USER_DIRECTIVES.md` if present.

The Stage 5 package expects approved artifacts from:

```text
/workflow/01_goal/01_service_goal.md
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/03_requirements/03_traceability_matrix.md
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
```

If Stage 4 was internally split, read approved official Stage 4 artifacts only. Do not read Stage 4 sub-skill internals as source of truth.

## 6. Execution Policy

The agent must:

1. Run sub-skills in order unless the user explicitly instructs otherwise.
2. Treat each sub-skill output as draft until finalization and human review.
3. Preserve official artifact paths.
4. Keep Stage 5 architecture decisions separate from approved decisions.
5. Record assumptions and open questions instead of silently resolving them.
6. Preserve traceability from requirements and domain model to architecture artifacts.
7. Prepare Stage 6 Data Design handoff only after finalizer consolidation.

## 7. Finalizer Requirement

The finalizer is required.

Do not treat Stage 5 as complete until `05e_architecture_finalizer` has:

- read all Stage 5 official artifacts and conditional artifacts that were created
- checked consistency among architecture plan, module boundaries, contracts, auth/security/operations artifacts, and decisions
- created or updated `05_architecture_traceability_matrix.md`
- created or updated `result.md`
- updated `context_packet.md` for Stage 6 Data Design
- prepared the human approval gate

## 8. Human Approval Gate

The human developer must review and approve, reject, or revise:

- architecture direction
- major technical choices
- module boundaries
- API contracts, if applicable
- integration contracts, if applicable
- authentication and authorization model, if applicable
- event/async contracts, if applicable
- security/privacy architecture direction, if applicable
- operational architecture direction, if applicable
- Stage 6 Data Design handoff assumptions

The agent must not claim approval unless the human explicitly provides it.

## 9. Downstream Handoff Rule

Stage 6 Data Design may use only approved Stage 5 official artifacts and updated workflow context.

Stage 6 must not depend on:

```text
/skills/05_architecture_contracts/05a_architecture_drivers_options/SKILL.md
/skills/05_architecture_contracts/05b_system_module_boundaries/SKILL.md
/skills/05_architecture_contracts/05c_technical_contracts/SKILL.md
/skills/05_architecture_contracts/05d_auth_security_operations/SKILL.md
/skills/05_architecture_contracts/05e_architecture_finalizer/SKILL.md
```

Those are execution procedures, not project source-of-truth artifacts.

## 10. Do Not Do

Do not:

- collapse all sub-skills into one uncontrolled architecture task
- skip the finalizer
- create project artifacts outside `/workflow/05_architecture` and `/workflow/context`
- update `DECISIONS.md` without explicit human approval
- design detailed database schema
- implement code
- create task cards
- create implementation prompts
- treat architecture recommendations as approved decisions
- let downstream stages depend on sub-skill internals
