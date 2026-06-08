---
name: 05b_system_module_boundaries
description: Define runtime, system, service, and module boundaries for Stage 5 architecture.
stage: 05 Architecture & Technical Contracts
parent_skill: /skills/05_architecture_contracts/SKILL.md
subskill_id: 05b
subskill_order: 2
previous_subskill: /skills/05_architecture_contracts/05a_architecture_drivers_options/SKILL.md
next_subskill: /skills/05_architecture_contracts/05c_technical_contracts/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/05_architecture/05_module_boundaries.md
requires_human_approval: true
external_visibility: internal
---

# 05b System & Module Boundaries

## 1. Purpose

Use this sub-skill to define architecture-level boundaries after architecture drivers and candidate direction have been drafted.

This sub-skill creates or updates:

```text
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_architecture_decisions.md
```

Its output remains draft until the Stage 5 finalizer consolidates all official artifacts and the human developer approves them.

## 2. When to Use

Use this sub-skill after `05a_architecture_drivers_options` has produced a draft architecture plan and architecture decision candidates.

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
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_architecture_decisions.md
```

### Read If Applicable

```text
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if roles, permissions, personal data, sensitive data, or compliance constraints affect module boundaries.

/workflow/00_intake/00_existing_context_review.md
- if this is brownfield, migration, or existing-system extension work.

/workflow/04_domain/04_domain_traceability_matrix.md
- if available and useful for mapping domain boundaries to architecture boundaries.
```

### Do Not Read By Default

```text
- implementation source code unless brownfield boundary analysis is explicitly required
- future Stage 6 data design artifacts
- future task/test/implementation artifacts
- raw prompt history
- unapproved internal sub-skill outputs from other stages
```

## 4. USER_DIRECTIVES.md Handling

If this file exists, read it before producing outputs:

```text
/workflow/05_architecture/USER_DIRECTIVES.md
```

Apply directives only after classifying them as approval, correction, preference, rejection, scope change, constraint, question, or new input.

## 5. Input Preflight Procedure

Verify:

```text
[ ] 05a output exists or the user explicitly instructed this sub-skill to run without it.
[ ] Architecture direction candidate is available or a missing-input issue is recorded.
[ ] Domain bounded contexts and business rules were checked.
[ ] Requirements and acceptance criteria were checked.
[ ] Conflicting approved decisions were reported.
[ ] Rejected module or architecture options are not reused.
```

## 6. Missing Input Handling

Blocking issues:

```text
- no usable requirements
- no usable domain model
- no architecture direction candidate and no user instruction to explore boundaries independently
- unresolved bounded context conflict that affects module boundaries
- unresolved role/permission model that affects protected module responsibilities
```

Non-blocking issues may be recorded as assumptions if boundaries can be drafted safely.

## 7. Execution Procedure

### Step 1. Restate Boundary Design Context

Summarize:

```text
- architecture direction candidate from 05a
- major domain boundaries
- major requirements shaping boundaries
- known constraints
- open questions affecting boundary decisions
```

### Step 2. Define Boundary Principles

Define project-specific boundary principles based on approved inputs, such as:

```text
- preserve bounded context language
- keep domain rules out of UI-only components
- separate external integration adapters from domain services
- isolate auth/security enforcement points
- avoid circular dependencies
- keep persistence details out of domain model when appropriate
```

Do not invent principles that contradict approved decisions.

### Step 3. Define Runtime / Container View

Describe the major runtime units at architecture level:

```text
- frontend application
- backend application or service layer
- database or storage boundary, conceptually only
- identity provider
- external services
- background workers
- queues/pub-sub if applicable
- admin/operator surfaces
```

Do not design physical database schema.

### Step 4. Define Module / Component Inventory

For each module, define:

```text
- module ID
- name
- responsibility
- owned domain concepts
- public interface
- internal responsibilities
- dependencies
- forbidden dependencies
- related requirements
- related domain concepts
- security/privacy notes
- testability notes
- data design implications
```

### Step 5. Define Dependency Rules

Specify:

```text
- allowed dependencies
- forbidden dependencies
- direction of dependency flow
- integration adapter rules
- domain logic placement rules
- validation responsibility boundaries
- error ownership boundaries
```

### Step 6. Identify Boundary Risks

Record risks such as:

```text
- unclear ownership of business rules
- over-coupled frontend/backend boundary
- integration leakage into domain model
- authorization enforcement ambiguity
- module with no traceable responsibility
- bounded context mismatch
```

### Step 7. Update Architecture Plan

Update `/workflow/05_architecture/05_architecture_plan.md` with:

```text
- runtime/container view
- frontend/backend/service boundary
- module boundary summary
- data flow implications
- cross-cutting policy implications discovered during boundary design
```

### Step 8. Update Decision Candidates

If boundary choices create architecture decision candidates, update:

```text
/workflow/05_architecture/05_architecture_decisions.md
```

Mark them as `Proposed` unless explicitly approved.

## 8. Output Artifacts

### Mandatory Outputs

```text
/workflow/05_architecture/05_module_boundaries.md
```

### Mandatory Updates

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_architecture_decisions.md
```

### Context Updates If Needed

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
```

## 9. Required Output Structure

### `05_module_boundaries.md`

Use this structure:

```markdown
# 05 Module Boundaries

## 1. Status
- Draft / Needs Review / Approved

## 2. Approved Inputs Used

## 3. Boundary Principles

## 4. Runtime / Container View

## 5. Module / Component Inventory

| Module ID | Name | Responsibility | Owned Domain Concepts | Public Interface | Dependencies | Forbidden Dependencies |
|---|---|---|---|---|---|---|

## 6. Module Details

### MOD-001 [[Name]]
#### Responsibility
#### Inputs
#### Outputs
#### Public Interface
#### Internal Responsibilities
#### Related Requirements
#### Related Domain Concepts
#### Security / Privacy Notes
#### Testability Notes
#### Data Design Implications

## 7. Dependency Rules

## 8. Boundary Risks

## 9. Open Questions

## 10. Handoff to 05c Technical Contracts

## 11. Human Approval Required
```

## 10. Traceability Rules

Every module must link to at least one of:

```text
- requirement
- acceptance criterion
- domain concept
- bounded context
- invariant
- domain event
- security/privacy risk
- operational constraint
```

Use stable IDs:

```text
MOD-001, MOD-002
```

If a module has no traceable source, mark it as a proposed addition requiring human approval.

## 11. Decision / Assumption / Open Question Rules

- Boundary recommendations are decision candidates.
- Unclear ownership is an open question, not a silent decision.
- If a rejected architecture or module option is encountered, record it in rejected/superseded options.
- Do not update `DECISIONS.md` without explicit human approval.

## 12. Validation Checklist

```text
[ ] 05a output was checked.
[ ] Requirements were linked to modules.
[ ] Domain concepts and bounded contexts were considered.
[ ] Module responsibilities are distinct.
[ ] Public interfaces are identified at architecture level.
[ ] Dependency rules are explicit.
[ ] Forbidden dependencies are listed where relevant.
[ ] Security/privacy notes are included where relevant.
[ ] Testability notes are included.
[ ] Data design implications are captured without designing schema.
[ ] Handoff to 05c is prepared.
```

## 13. Human Approval Gate

This sub-skill may request interim approval for:

```text
- module boundaries
- frontend/backend/service split
- dependency direction
- protected module responsibilities
- major boundary trade-offs
```

Full Stage 5 approval happens after finalizer execution.

## 14. Context Handoff to Next Sub-Skill

At the end of `05_module_boundaries.md`, include:

```markdown
## Handoff to 05c Technical Contracts

### Modules Requiring Public Contracts

### Internal Interfaces That Should Remain Private

### APIs Likely Needed

### External Integrations Likely Needed

### Events / Async Workflows Likely Needed

### Open Questions Affecting Contracts
```

## 15. Do Not Do

Do not:

- design detailed API fields prematurely
- create database tables
- implement code
- create task cards
- make modules depend on unapproved architecture decisions
- collapse all domain concepts into one generic service
- create modules with no traceable responsibility
- treat draft module boundaries as approved
