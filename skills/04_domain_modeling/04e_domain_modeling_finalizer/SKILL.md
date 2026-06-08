---
name: 04e_domain_modeling_finalizer
description: Consolidate all Stage 4 domain modeling artifacts, update traceability and context handoff, record N/A decisions, and prepare the human approval gate for Stage 5.
stage: 04 Domain Modeling / DDD
parent_skill: /skills/04_domain_modeling/SKILL.md
subskill_id: 04e
subskill_order: 5
previous_subskill: /skills/04_domain_modeling/04d_events_bounded_contexts/SKILL.md
next_stage: 05_architecture_contracts
version: 1.0.0
status: draft
primary_output: /workflow/04_domain/result.md
requires_human_approval: true
external_visibility: internal
---

# 04e Domain Modeling Finalizer SKILL

## 1. Purpose

Finalize Stage 4 by consolidating official artifacts, checking consistency, updating traceability, preparing the Stage 5 context handoff, and presenting the human approval gate.

This sub-skill does not create new domain modeling from scratch unless necessary to repair gaps. It reviews and consolidates the outputs from:

```text
04a_ubiquitous_language
04b_domain_concepts_entities_values
04c_aggregates_rules_lifecycle
04d_events_bounded_contexts
```

The finalizer prepares Stage 4 for human approval. It does not approve artifacts on behalf of the human developer.

## 2. Core Question

Are the Stage 4 domain artifacts internally consistent, traceable to approved requirements, ready for human review, and sufficient to guide Stage 5 Architecture & Technical Contracts?

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
/workflow/01_goal/01_service_goal.md
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_bounded_contexts.md
```

### Read If Applicable

```text
/workflow/03_requirements/03_traceability_matrix.md
- if Stage 3 produced it

/workflow/04_domain/04_state_lifecycle.md
- if created or if lifecycle concepts exist

/workflow/04_domain/04_context_map.md
- if created or if multiple contexts/external contexts exist

/workflow/04_domain/04_domain_risk_notes.md
- if created or if security/privacy/audit/compliance affects domain rules

/workflow/04_domain/04_domain_model_diagrams.md
- if created

/workflow/04_domain/04_domain_open_questions.md
- if created

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if risk/privacy constraints affect final handoff

/workflow/context/APPROVAL_LOG.md
- if approval status is ambiguous

/workflow/04_domain/USER_DIRECTIVES.md
- if present

/workflow/04_domain/review_notes.md
- if revising a prior Stage 4 draft
```

### Do Not Read By Default

```text
implementation source code, except brownfield evidence explicitly needed
downstream architecture/API/data drafts
message broker configuration
final database schema
full historical agent logs
superseded or rejected artifacts
```

## 4. Missing Input Handling

Blocking:

- any mandatory Stage 4 artifact missing after its sub-skill should have produced it;
- source-of-truth ambiguity for requirements or acceptance criteria;
- major contradiction between terminology, concepts, rules, events, or contexts;
- requirement lacks any domain representation and cannot be safely marked as a gap;
- privacy/security constraints conflict with domain model behavior.

Non-blocking with explicit gap record:

- optional artifact not applicable;
- minor term ambiguity that does not block architecture;
- incomplete traceability that can be listed as a traceability gap;
- unresolved context split that Stage 5 can avoid until approved.

If blocked, create or update `/workflow/04_domain/result.md` with a Blocker Report.

## 5. Execution Procedure

### Step 1. Confirm Scope

State:

```text
This finalizer consolidates Stage 4 domain artifacts and prepares human approval. It does not approve decisions, design architecture, design database schema, design APIs, create tasks, or implement code.
```

### Step 2. Verify Official Artifact Set

Check mandatory artifacts:

```text
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
```

Check whether each conditional artifact exists or needs N/A rationale:

```text
/workflow/04_domain/04_state_lifecycle.md
/workflow/04_domain/04_context_map.md
/workflow/04_domain/04_domain_risk_notes.md
/workflow/04_domain/04_domain_model_diagrams.md
/workflow/04_domain/04_domain_open_questions.md
```

Do not create conditional artifacts merely to fill a checklist. If not applicable, record why.

### Step 3. Check Cross-Artifact Consistency

Verify that:

- preferred terms appear consistently in domain model, rules, events, and contexts;
- entity/value object names align with ubiquitous language;
- aggregate roots are valid entity candidates;
- invariants are protected by appropriate aggregate or concept candidates;
- state transitions align with lifecycle-bearing concepts;
- domain events have source concepts or aggregates;
- bounded contexts own language and concepts consistently;
- rejected terms, event candidates, or context boundaries were not revived;
- assumptions remain assumptions;
- agent recommendations are not recorded as approved decisions.

Record contradictions in `result.md`.

### Step 4. Update Domain Traceability Matrix

Create or update:

```text
/workflow/04_domain/04_domain_traceability_matrix.md
```

Required links:

```text
Goal → Requirement → Acceptance Criteria → Domain Term
Requirement → Domain Concept
Requirement → Business Rule / Invariant
Acceptance Criteria → State Transition / Rule / Event
Domain Concept → Bounded Context
Aggregate → Invariant
Invariant → Future Unit or Scenario Test Target
State Transition → Future Scenario Test Target
Domain Event → Future Integration or Audit Test Target
Bounded Context → Future Module / Architecture Boundary Candidate
Aggregate → Future Transaction Boundary Candidate
```

Prohibited premature links:

```text
Domain Concept → final Database Table
Aggregate → final Microservice
Domain Event → final Message Broker Topic
Bounded Context → final Deployment Unit
Entity → final ORM Model
```

### Step 5. Update Global Traceability Matrix If Applicable

Update `/workflow/context/TRACEABILITY_MATRIX.md` only to add or preserve Stage 4 links.

Do not break existing IDs.

If global traceability cannot be updated safely, record this as a traceability gap in `result.md`.

### Step 6. Consolidate Decision Candidates, Assumptions, Open Questions, Risks, and Rejections

Prepare sections in `result.md`:

- decision candidates;
- working assumptions;
- open questions;
- risks and constraints;
- rejected or superseded options;
- traceability gaps;
- conditional artifacts not created.

Update these files when applicable:

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Do not update `/workflow/context/DECISIONS.md` without explicit human approval.

### Step 7. Prepare Stage 5 Handoff

Update `/workflow/context/context_packet.md` for Stage 5.

Include only minimal operational context.

Stage 5 handoff must include:

- bounded contexts that may influence module boundaries;
- aggregates that may influence transaction boundaries;
- invariants that need enforcement points;
- domain events that may influence integration design;
- role/permission concepts that affect authorization;
- terms that should be preserved in APIs, UI, tests, and code;
- unresolved issues that block architecture decisions;
- required Stage 5 inputs.

Do not copy entire Stage 4 artifacts into `context_packet.md`.

### Step 8. Prepare Human Approval Gate

List exactly what the human developer must approve or revise before Stage 5.

Stage 5 must not treat Stage 4 artifacts as source of truth until the human approves them.

## 6. Output Artifacts

Create or update:

```text
/workflow/04_domain/04_domain_traceability_matrix.md
/workflow/04_domain/result.md
/workflow/context/context_packet.md
```

Update when applicable:

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Do not update:

```text
/workflow/context/DECISIONS.md
```

unless explicit human approval exists.

## 7. Required Structure: `04_domain_traceability_matrix.md`

```markdown
# 04 Domain Traceability Matrix

## 1. Status
- Status: Draft | Needs Review | Approved
- Source artifacts:
- Last updated:

## 2. Requirement to Domain Links
| Requirement ID | Acceptance Criteria IDs | Domain Terms | Concepts | Rules / Invariants | Events | Bounded Contexts | Gaps |
|---|---|---|---|---|---|---|---|

## 3. Domain to Future Stage Links
| Domain Item ID | Type | Architecture Implication | Data Design Implication | Test Implication | Notes |
|---|---|---|---|---|---|

## 4. Traceability Gaps
| Gap ID | Gap Type | Affected Requirement / Domain Item | Description | Impact | Follow-up Needed |
|---|---|---|---|---|---|
```

## 8. Required Structure: `result.md`

```markdown
# Result: 04_domain_modeling

## 1. Task Summary

## 2. Inputs Used

## 3. Outputs Created or Updated

## 4. Domain Modeling Summary

## 5. Key Domain Findings

## 6. Decision Candidates

## 7. Working Assumptions

## 8. Open Questions

## 9. Risks and Constraints

## 10. Rejected or Superseded Options

## 11. Traceability Updates

## 12. Conditional Artifacts Not Created
| Artifact | Why Not Applicable | Revisit If |
|---|---|---|

## 13. Consistency Review

## 14. Human Approval Required

## 15. Recommended Next Step
```

If blocked, include:

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
- ...

### Affected Artifacts or Stages
- ...

### Safe Partial Work Completed
- ...

### Human Decision Needed
- ...
```

## 9. Required Structure: `context_packet.md` for Stage 5

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 04 Domain Modeling / DDD
- Completed stages:
- Next recommended stage: 05 Architecture & Technical Contracts

## 2. Approved Decisions
- Only human-approved decisions.

## 3. Working Assumptions
- Temporary assumptions not yet confirmed.

## 4. Open Questions
- Questions that may affect Stage 5 or later stages.

## 5. Rejected / Superseded Options
- Options that should not be reused unless reopened.

## 6. Constraints That Must Not Be Violated
- Technology:
- Security:
- Privacy:
- Scope:
- Schedule:
- Operational:

## 7. Key Context for Next Stage
- Bounded contexts that may influence module boundaries:
- Aggregates that may influence transaction boundaries:
- Invariants that need enforcement points:
- Domain events that may influence integration design:
- Role/permission concepts that affect authorization:
- Terms to preserve in APIs, UI, tests, and code:
- Architecture-blocking open questions:

## 8. Required Inputs for Next Stage
- /workflow/04_domain/04_ubiquitous_language.md
- /workflow/04_domain/04_domain_model.md
- /workflow/04_domain/04_bounded_contexts.md
- /workflow/04_domain/04_business_rules_invariants.md
- /workflow/04_domain/04_domain_events.md
- /workflow/04_domain/04_domain_traceability_matrix.md
- /workflow/context/DECISIONS.md
- /workflow/context/ASSUMPTIONS.md
- /workflow/context/OPEN_QUESTIONS.md
- /workflow/context/TRACEABILITY_MATRIX.md

## 9. Do Not Do
- Do not design architecture from unapproved Stage 4 artifacts.
- Do not treat bounded contexts as microservices by default.
- Do not treat aggregates as database tables or services.
- Do not treat domain events as message broker topics.
```

## 10. ID Conventions

Use stable IDs:

```text
TG-001        Traceability gaps
A-001         Assumptions, if updating ASSUMPTIONS.md
Q-001         Open questions, if updating OPEN_QUESTIONS.md
R-001         Risks, if updating result.md or risk notes
```

Preserve all Stage 3 and Stage 4 IDs.

## 11. Validation Checklist

Before finishing, verify:

```text
[ ] All mandatory Stage 4 artifacts exist or blocker is reported.
[ ] Conditional artifacts either exist or have N/A rationale.
[ ] Terms are consistent across artifacts.
[ ] Entities, value objects, aggregates, rules, events, and contexts are aligned.
[ ] Requirements link to domain terms, concepts, rules, events, or contexts.
[ ] Traceability gaps are explicit.
[ ] Architecture implications are stated without making architecture decisions.
[ ] Data design implications are stated without creating schema.
[ ] Test implications are stated without writing test commands.
[ ] Decision candidates, assumptions, open questions, risks, and rejected options are separated.
[ ] DECISIONS.md was not updated without explicit human approval.
[ ] context_packet.md is concise and points to source artifacts.
[ ] Human approval gate is present.
```

## 12. Human Approval Required

End with this section:

```markdown
## Human Approval Required

### Decisions to Approve
- Preferred ubiquitous language terms
- Entity and value object classifications
- Aggregate roots and aggregate boundaries
- Business rules and invariants
- State lifecycle model, if applicable
- Domain events
- Bounded contexts and context relationships
- Single-context rationale, if applicable

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Risks to Review
- ...

### Artifacts Ready for Review
- /workflow/04_domain/04_ubiquitous_language.md
- /workflow/04_domain/04_domain_model.md
- /workflow/04_domain/04_bounded_contexts.md
- /workflow/04_domain/04_business_rules_invariants.md
- /workflow/04_domain/04_domain_events.md
- /workflow/04_domain/04_domain_traceability_matrix.md
- /workflow/04_domain/result.md

### Recommended Next Step
- Review and approve or revise Stage 4 artifacts before running Stage 5 Architecture & Technical Contracts.
```

## 13. Do Not Do

Do not:

- approve Stage 4 artifacts on behalf of the human developer;
- update `/workflow/context/DECISIONS.md` without explicit human approval;
- hide contradictions across sub-skill outputs;
- treat draft sub-skill outputs as approved official artifacts;
- change official Stage 4 artifact paths;
- design database schema;
- design API contracts;
- choose architecture style;
- create implementation tasks;
- write test commands;
- allow Stage 5 to depend on internal sub-skill folders or prompt history.
