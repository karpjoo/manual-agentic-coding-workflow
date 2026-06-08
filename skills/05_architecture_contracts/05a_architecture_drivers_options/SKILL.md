---
name: 05a_architecture_drivers_options
description: Extract architecture drivers, system context, options, and recommended architecture direction for Stage 5.
stage: 05 Architecture & Technical Contracts
parent_skill: /skills/05_architecture_contracts/SKILL.md
subskill_id: 05a
subskill_order: 1
previous_subskill: /skills/04_domain_modeling/SKILL.md
next_subskill: /skills/05_architecture_contracts/05b_system_module_boundaries/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/05_architecture/05_architecture_plan.md
requires_human_approval: true
external_visibility: internal
---

# 05a Architecture Drivers & Options

## 1. Purpose

Use this sub-skill to start Stage 5 by extracting architecture drivers from approved prior-stage artifacts, defining system context, comparing viable architecture options, and recommending an architecture direction as a decision candidate.

This sub-skill creates or updates:

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_architecture_decisions.md
```

Its output remains draft until the Stage 5 finalizer consolidates all official artifacts and the human developer approves them.

## 2. When to Use

Use this sub-skill first in the Stage 5 sequence.

Run it after Stage 4 Domain Modeling artifacts are approved or explicitly allowed as draft inputs by the human developer.

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

### Read If Applicable

```text
/workflow/00_intake/00_project_intake.md
- if project profile, fixed stack, hosting, platform, or constraints are not clear from context_packet.md.

/workflow/00_intake/00_existing_context_review.md
- if this is brownfield, legacy, migration, or existing-system extension work.

/workflow/04_domain/04_domain_traceability_matrix.md
- if Stage 4 produced a separate domain traceability matrix.

/workflow/04_domain/result.md
- if Stage 4 contains architecture-relevant warnings, assumptions, or handoff notes.

/workflow/03_requirements/result.md
- if requirements contain unresolved architecture implications not reflected in official requirement artifacts.

/workflow/02_stakeholders_risk/result.md
- if risk/privacy outputs contain architecture-relevant unresolved issues.
```

### Do Not Read By Default

```text
- raw chat history
- raw agent logs
- unapproved Stage 4 sub-skill outputs
- implementation source code, unless brownfield review is explicitly required
- future-stage data design, task, test, or implementation artifacts
```

## 4. USER_DIRECTIVES.md Handling

If this file exists, read it before producing outputs:

```text
/workflow/05_architecture/USER_DIRECTIVES.md
```

Classify each directive as one of:

```text
approval, correction, preference, rejection, scope change, constraint, question, new input
```

If a directive conflicts with approved decisions, report the conflict. Do not silently resolve it.

## 5. Input Preflight Procedure

Before architecture analysis, verify:

```text
[ ] artifact_manifest.yml was checked if available.
[ ] context_packet.md was checked.
[ ] DECISIONS.md and APPROVAL_LOG.md were checked if available.
[ ] USER_DIRECTIVES.md was checked if present.
[ ] Required Stage 1, 2, 3, and 4 artifacts exist.
[ ] Source artifacts are approved or explicitly allowed as draft inputs.
[ ] Superseded or rejected artifacts are not used as current truth.
[ ] Missing or conflicting inputs are reported.
[ ] Blocking issues are identified before proceeding.
```

## 6. Missing Input Handling

Treat these as blocking unless the user explicitly requests exploratory architecture drafting:

```text
- missing or unapproved service goal
- missing or unapproved requirements
- missing or unapproved acceptance criteria
- missing or unapproved domain model
- unresolved role/permission direction when authorization architecture is required
- unresolved personal/sensitive data handling direction when personal/sensitive data exists
- conflicting approved decisions about technology stack, architecture style, hosting, or data ownership
```

If blocked, write a partial `result.md` section or blocker note with:

```markdown
## Blocker Report

### Blocking Issue
### Why It Matters
### Affected Architecture Areas
### Affected Downstream Stages
### Safe Partial Work Completed
### Human Decision Needed
```

## 7. Execution Procedure

### Step 1. Restate the Stage Context

Summarize:

```text
- current stage and sub-skill
- previous approved artifacts used
- project profile if known
- project-type specialization hooks that may apply
- next sub-skill
```

### Step 2. Extract Architecture Drivers

Extract and classify architecture drivers:

```text
- business goal drivers
- functional requirement drivers
- non-functional drivers
- security/privacy drivers
- stakeholder/role drivers
- domain model drivers
- invariant/consistency drivers
- integration drivers
- operational drivers
- data design implications
- testability implications
```

For each driver, link to source artifact and source ID when available.

### Step 3. Define System Context

Identify:

```text
- system under design
- primary users and actors
- administrators/operators
- external systems
- identity providers
- third-party APIs
- LLM/model services if applicable
- data providers
- out-of-scope systems
```

Use a textual diagram if useful.

### Step 4. Identify Architecture Constraints

Record:

```text
- approved technology constraints
- hosting/deployment constraints
- privacy/security constraints
- regulatory/compliance constraints
- integration constraints
- performance/scalability constraints
- organizational constraints
- brownfield compatibility constraints, if applicable
```

### Step 5. Generate Architecture Options

Generate 2–4 viable options when meaningful. If approved constraints make only one option realistic, explain why.

For each option, include:

```text
- summary
- architecture style
- major components
- fit with requirements
- fit with domain model
- security/privacy implications
- operational complexity
- implementation complexity
- testability
- scalability/performance implications
- major risks
- reasons to select
- reasons to reject
```

### Step 6. Recommend Architecture Direction

Recommend one direction as a `Decision Candidate`, not an approved decision.

Include:

```text
- recommended architecture style
- runtime component direction
- frontend/backend/service boundary direction
- module organization direction
- authn/authz approach direction
- contract boundary direction
- integration approach direction
- data design implications
- test strategy implications
- known risks
```

### Step 7. Start Architecture Decision Records

Create initial ADR entries in:

```text
/workflow/05_architecture/05_architecture_decisions.md
```

Each ADR must include:

```text
Decision ID
Title
Status: Proposed / Approved / Rejected / Superseded
Context
Options Considered
Recommendation
Consequences
Risks
Related Requirements
Related Domain Concepts
Human Approval Needed
```

Only mark as `Approved` when explicit human approval exists.

## 8. Output Artifacts

### Mandatory Outputs

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_architecture_decisions.md
```

### Optional Updates

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
```

Update these only if new assumptions, unresolved questions, or explicitly rejected/superseded options are identified.

## 9. Required Output Structure

### 9.1 `05_architecture_plan.md`

Create or update at least these sections:

```markdown
# 05 Architecture Plan

## 1. Status
- Draft / Needs Review / Approved

## 2. Approved Inputs Used

## 3. Architecture Drivers
### 3.1 Business Goal Drivers
### 3.2 Functional Drivers
### 3.3 Non-Functional Drivers
### 3.4 Security / Privacy Drivers
### 3.5 Domain Drivers
### 3.6 Operational Drivers

## 4. System Context
### 4.1 Actors
### 4.2 External Systems
### 4.3 System Boundary
### 4.4 Out-of-Scope Systems

## 5. Constraints

## 6. Architecture Options Considered

## 7. Recommended Architecture Direction
- Mark as Decision Candidate unless explicitly approved.

## 8. Data Design Implications for Stage 6

## 9. Test Strategy Implications for Stage 8

## 10. Risks and Trade-Offs

## 11. Open Questions

## 12. Handoff to 05b System & Module Boundaries
```

### 9.2 `05_architecture_decisions.md`

Create or update:

```markdown
# 05 Architecture Decisions

## 1. Status

## 2. Decision Table

| Decision ID | Title | Status | Recommendation | Requires Approval | Related Requirements |
|---|---|---|---|---|---|

## 3. Decision Records

### ADR-001 [[Decision Title]]
#### Status
#### Context
#### Options Considered
#### Recommendation
#### Consequences
#### Risks
#### Related Requirements
#### Related Domain Concepts
#### Human Approval Needed
```

## 10. Traceability Rules

Link architecture drivers and ADRs to source requirements, acceptance criteria, domain concepts, invariants, risks, or approved decisions.

Use stable IDs:

```text
ADR-001, ADR-002
ARISK-001, ARISK-002
AQ-001, AQ-002
```

If a recommendation has no traceable source, mark it as a proposed addition and require human approval.

## 11. Decision / Assumption / Open Question Rules

- Architecture recommendations are decision candidates.
- Working assumptions must remain assumptions until confirmed.
- Open questions that affect module boundaries, contracts, data design, security, or operations must be recorded.
- Rejected architecture options must be recorded and not revived unless explicitly reopened.
- Do not update `DECISIONS.md` without explicit human approval.

## 12. Validation Checklist

```text
[ ] Required source artifacts were checked.
[ ] USER_DIRECTIVES.md was checked if present.
[ ] Architecture drivers were extracted from approved sources.
[ ] System context was defined.
[ ] Options were considered or a single-option rationale was recorded.
[ ] Recommended architecture direction is marked as a decision candidate.
[ ] Initial ADRs were created or updated.
[ ] Risks and trade-offs were recorded.
[ ] Data design implications were identified without creating detailed schema.
[ ] Handoff to 05b was prepared.
```

## 13. Human Approval Gate

This sub-skill may request interim review, but full Stage 5 approval happens after the finalizer.

Interim approval may be requested for:

```text
- architecture option direction
- rejected architecture options
- fixed technology choices
- blocking architecture assumptions
```

## 14. Context Handoff to Next Sub-Skill

At the end of `05_architecture_plan.md`, include:

```markdown
## Handoff to 05b System & Module Boundaries

### Architecture Direction Candidate

### Drivers That Shape Module Boundaries

### Domain Boundaries to Preserve

### Constraints for Module Design

### Open Questions Affecting Module Boundaries
```

Do not prepare Stage 6 handoff here. Stage 6 handoff is the finalizer's responsibility.

## 15. Do Not Do

Do not:

- implement code
- design database schema
- create API details before module and boundary implications are clear
- mark recommendations as approved
- ignore rejected options
- use unapproved Stage 4 sub-skill outputs as source of truth
- create downstream handoff as if Stage 5 were complete
