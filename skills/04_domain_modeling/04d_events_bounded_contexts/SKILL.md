---
name: 04d_events_bounded_contexts
description: Define domain events, workflow implications, bounded contexts, context relationships, and optional context map candidates from Stage 4 draft artifacts.
stage: 04 Domain Modeling / DDD
parent_skill: /skills/04_domain_modeling/SKILL.md
subskill_id: 04d
subskill_order: 4
previous_subskill: /skills/04_domain_modeling/04c_aggregates_rules_lifecycle/SKILL.md
next_subskill: /skills/04_domain_modeling/04e_domain_modeling_finalizer/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/04_domain/04_domain_events.md
requires_human_approval: true
external_visibility: internal
---

# 04d Domain Events and Bounded Contexts SKILL

## 1. Purpose

Define business-significant domain events, workflow implications, bounded contexts, and context relationships.

This sub-skill creates or updates:

```text
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_bounded_contexts.md
```

It may create:

```text
/workflow/04_domain/04_context_map.md
/workflow/04_domain/04_domain_risk_notes.md
/workflow/04_domain/04_domain_model_diagrams.md
```

when applicable.

It does not design message brokers, event topics, microservices, deployment units, API contracts, database schema, or implementation tasks.

## 2. Core Question

Which business events, workflows, language boundaries, and context relationships must later architecture and data design preserve?

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
```

### Read If Applicable

```text
/workflow/04_domain/04_state_lifecycle.md
- if created by 04c or lifecycle states exist

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if audit, privacy, permission, compliance, or sensitive data affects events or contexts

/workflow/00_intake/00_existing_context_review.md
- if brownfield contexts, external systems, or compatibility constraints exist

/workflow/03_requirements/03_traceability_matrix.md
- if Stage 3 produced it

/workflow/04_domain/USER_DIRECTIVES.md
- if present

/workflow/04_domain/review_notes.md
- if revising a prior Stage 4 draft
```

### Do Not Read By Default

```text
message broker configuration
API contracts
deployment diagrams
implementation source code
final database schema
architecture drafts
full historical agent logs
superseded or rejected artifacts
```

## 4. Missing Input Handling

Blocking:

- missing `04_domain_model.md`;
- missing `04_business_rules_invariants.md` when event/context boundaries depend on rules;
- unresolved aggregate or rule conflicts that make event/context modeling unsafe;
- missing role or external-system semantics when context boundaries depend on them.

Non-blocking with explicit assumptions:

- no lifecycle artifact when lifecycle is simple;
- no brownfield context for greenfield projects;
- incomplete risk screening when no risk-sensitive events are present.

Record gaps in `04_domain_events.md`, `04_bounded_contexts.md`, or `04_domain_risk_notes.md` as appropriate.

## 5. Execution Procedure

### Step 1. Confirm Scope

State:

```text
This sub-skill defines domain events and bounded contexts. It does not design message topics, microservices, API endpoints, database tables, deployment units, or implementation tasks.
```

### Step 2. Identify Domain Event Candidates

Extract event candidates from:

- completed state transitions;
- approved/rejected/submitted/reviewed/assigned/expired/revoked lifecycle actions;
- aggregate changes that matter to other actors or contexts;
- audit-relevant business facts;
- integration-relevant business facts;
- workflow milestones;
- acceptance criteria that describe observable domain outcomes.

Use past-tense business event names when appropriate.

Examples of naming style:

```text
ReviewSubmitted
EvaluationApproved
AccessGrantRevoked
CaseAssigned
ConsentWithdrawn
```

Do not create events for:

- button clicks;
- page views;
- UI-only notifications;
- database row changes;
- message queue topics;
- implementation callbacks;
- technical logs unless they represent business-significant audit facts.

### Step 3. Define Domain Events

For each event:

- assign stable ID;
- name the event in past tense;
- identify source concept or aggregate;
- define trigger;
- define why it matters;
- identify interested actors, contexts, audit logs, integrations, or future tests;
- link to requirement or acceptance criterion;
- record event ordering or causality notes if domain-relevant.

### Step 4. Reject Technical or UI Events Explicitly

If a candidate is not a domain event, record it under rejected technical/UI events with a reason.

This prevents later agents from reviving it as a domain event.

### Step 5. Identify Bounded Context Candidates

Look for boundaries in:

- language differences;
- rule differences;
- lifecycle ownership;
- different actors or teams;
- external systems;
- privacy/security/compliance boundaries;
- policy ownership;
- different meanings for the same term;
- different consistency needs;
- different model purposes.

Do not equate bounded contexts with microservices, modules, repositories, screens, or deployment units.

### Step 6. Define Bounded Contexts

For each bounded context:

- define purpose;
- define owned language;
- define owned concepts;
- define owned rules or policies;
- identify inbound and outbound relationships;
- identify translation or contract needs;
- link to requirements;
- record approval-needed context split candidates.

If a single context is sufficient, record a single-context rationale.

### Step 7. Define Context Relationships

Use neutral relationship labels unless a specific DDD relationship is justified.

Possible labels:

```text
upstream/downstream candidate
shared kernel candidate
customer/supplier candidate
anti-corruption layer candidate
external integration candidate
policy dependency
language translation needed
unclear relationship
```

Do not finalize architecture integration patterns.

### Step 8. Create Domain Risk Notes If Applicable

Create `/workflow/04_domain/04_domain_risk_notes.md` if domain rules are shaped by:

- personal data;
- sensitive data;
- auditability;
- consent;
- retention;
- access control;
- compliance evidence;
- external model or LLM output;
- human override;
- regulated review.

### Step 9. Prepare Handoff to Finalizer

List:

- official artifacts updated;
- event/context decisions needing approval;
- unresolved context split questions;
- artifacts that were not applicable;
- traceability gaps.

## 6. Output Artifacts

Create or update:

```text
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_bounded_contexts.md
```

Create if applicable:

```text
/workflow/04_domain/04_context_map.md
/workflow/04_domain/04_domain_risk_notes.md
/workflow/04_domain/04_domain_model_diagrams.md
```

### Required Structure: `04_domain_events.md`

```markdown
# 04 Domain Events

## 1. Status
- Status: Draft | Needs Review | Approved
- Source artifacts:
- Last updated:

## 2. Domain Events
| Event ID | Event Name | Source Concept / Aggregate | Trigger | Why It Matters | Interested Contexts / Actors | Linked Requirement |
|---|---|---|---|---|---|---|

## 3. Event Ordering or Causality Notes
| Note ID | Event(s) | Ordering / Causality Rule | Linked Requirement | Notes |
|---|---|---|---|---|

## 4. Events Rejected as Technical or UI Events
| Candidate | Rejection Reason | Revisit If |
|---|---|---|

## 5. Event Open Questions
```

### Required Structure: `04_bounded_contexts.md`

```markdown
# 04 Bounded Contexts

## 1. Status
- Status: Draft | Needs Review | Approved
- Source artifacts:
- Last updated:

## 2. Context Strategy Summary

## 3. Bounded Contexts
| Context ID | Name | Purpose | Owned Language | Owned Concepts | Owned Rules / Policies | Linked Requirements |
|---|---|---|---|---|---|---|

## 4. Context Relationships
| Relationship ID | Upstream Context | Downstream Context | Relationship Type | Translation / Contract Need | Notes |
|---|---|---|---|---|---|

## 5. Single-Context Rationale, if Applicable

## 6. Context Split Candidates Requiring Approval
| Candidate ID | Proposed Split | Reason | Impact | Human Decision Needed |
|---|---|---|---|---|

## 7. Context Open Questions
```

### Optional Structure: `04_context_map.md`

```markdown
# 04 Context Map

## 1. Status

## 2. Context Relationship Summary

## 3. Context Map Table
| Relationship ID | Source Context | Target Context | Relationship Type | Translation Need | Architecture Implication Candidate |
|---|---|---|---|---|---|

## 4. Context Map Notes
```

### Optional Structure: `04_domain_risk_notes.md`

```markdown
# 04 Domain Risk Notes

## 1. Status

## 2. Risk-Sensitive Domain Rules
| Risk Note ID | Domain Concept / Rule | Risk Type | Constraint | Linked Requirement | Handoff Note |
|---|---|---|---|---|---|

## 3. Privacy / Security / Audit Language to Preserve

## 4. Open Risk Questions
```

## 7. ID Conventions

Use stable IDs:

```text
EVT-001       Domain events
EC-001        Event causality notes
BC-001        Bounded contexts
BCR-001       Bounded context relationships
BCS-001       Context split candidates
DRN-001       Domain risk notes
```

## 8. Decision / Assumption / Open Question Rules

Decision candidates:

- event names and event inclusion;
- rejected event candidates;
- bounded context boundaries;
- context relationship types;
- single-context rationale.

Working assumptions:

- inferred event significance;
- inferred context ownership;
- inferred translation need;
- inferred audit relevance.

Open questions:

- ambiguous event trigger;
- unclear interested context;
- unclear context ownership;
- unclear single-context vs split-context decision;
- external system boundary unclear.

Rejected options:

- UI-only or technical event candidates;
- rejected context split candidates;
- superseded context names.

## 9. Validation Checklist

Before finishing, verify:

```text
[ ] Domain events are business-significant, not technical messages.
[ ] Event names are past-tense business facts where appropriate.
[ ] Events link to requirements, rules, state transitions, audit, integration, or tests.
[ ] UI-only or technical candidates are rejected explicitly.
[ ] Bounded contexts are based on language, rules, ownership, lifecycle, or policy boundaries.
[ ] Bounded contexts are not equated with microservices or deployment units.
[ ] Single-context rationale is recorded if no split is needed.
[ ] Context relationships do not finalize architecture integration patterns.
[ ] Privacy/security/audit context boundaries are not ignored.
[ ] No API, database, message broker, or deployment design was created.
```

## 10. Context Handoff to Finalizer

At the end, report:

```markdown
## Handoff to 04e_domain_modeling_finalizer

### Official Artifacts Updated
- ...

### Event Decisions Needing Review
- ...

### Context Decisions Needing Review
- ...

### Conditional Artifacts Created
- ...

### Conditional Artifacts Not Applicable
- ...

### Traceability Gaps
- ...

### Do Not Do in 04e
- Do not approve Stage 4 artifacts on behalf of the human developer.
- Do not change official artifact paths.
- Do not let Stage 5 depend on internal sub-skill outputs.
```

## 11. Human Approval Note

This sub-skill may request review of events and bounded context candidates, but Stage 4 is not ready for downstream approval until `04e_domain_modeling_finalizer` has run.
