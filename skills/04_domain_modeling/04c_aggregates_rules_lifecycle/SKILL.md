---
name: 04c_aggregates_rules_lifecycle
description: Define aggregate candidates, consistency boundaries, business rules, invariants, and lifecycle/state transition models from the draft domain model.
stage: 04 Domain Modeling / DDD
parent_skill: /skills/04_domain_modeling/SKILL.md
subskill_id: 04c
subskill_order: 3
previous_subskill: /skills/04_domain_modeling/04b_domain_concepts_entities_values/SKILL.md
next_subskill: /skills/04_domain_modeling/04d_events_bounded_contexts/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/04_domain/04_business_rules_invariants.md
requires_human_approval: true
external_visibility: internal
---

# 04c Aggregates, Rules, and Lifecycle SKILL

## 1. Purpose

Define consistency boundaries, business rules, invariants, and lifecycle/state transitions from the draft domain model.

This sub-skill updates:

```text
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_business_rules_invariants.md
```

It may create:

```text
/workflow/04_domain/04_state_lifecycle.md
```

only when lifecycle-bearing concepts or meaningful state transitions exist.

This sub-skill does not design transactions, database tables, microservices, APIs, infrastructure, or implementation classes.

## 2. Core Question

Which domain rules must always hold, and which concepts form consistency boundaries that later architecture, data design, and tests must preserve?

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
```

### Read If Applicable

```text
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if privacy, security, permission, compliance, or audit rules affect invariants

/workflow/03_requirements/03_traceability_matrix.md
- if Stage 3 produced it

/workflow/04_domain/USER_DIRECTIVES.md
- if present

/workflow/04_domain/review_notes.md
- if revising a prior Stage 4 draft

/workflow/00_intake/00_existing_context_review.md
- if brownfield lifecycle or consistency constraints exist
```

### Do Not Read By Default

```text
database schemas, except brownfield supporting evidence
API contracts
architecture designs
implementation code
full historical agent logs
superseded or rejected artifacts
```

## 4. Missing Input Handling

Blocking:

- missing `04_domain_model.md`;
- missing requirements or acceptance criteria;
- concept classification conflicts that make aggregate boundaries unsafe;
- missing role or permission semantics when they define rules;
- privacy/security constraints conflict with domain operations.

Non-blocking with explicit assumptions:

- incomplete cardinality details;
- missing brownfield implementation details for greenfield projects;
- lifecycle states implied but not fully specified.

Record all rule gaps in `/workflow/04_domain/04_business_rules_invariants.md` under `## Rule Conflicts or Gaps`.

## 5. Execution Procedure

### Step 1. Confirm Scope

State:

```text
This sub-skill defines aggregates, consistency boundaries, business rules, invariants, and lifecycle/state transitions. It does not design database transactions, ORM models, microservices, API endpoints, or architecture components.
```

### Step 2. Identify Rule Sources

Extract rule candidates from:

- requirements;
- acceptance criteria;
- role/permission descriptions;
- lifecycle wording;
- business policies;
- risk/privacy/audit constraints;
- domain model relationships;
- terms such as must, only, cannot, before, after, requires, valid, invalid, approved, submitted, assigned, reviewed, expired, revoked.

Classify rules as:

```text
business rule
invariant
validation rule
permission rule
policy rule
workflow rule
state transition rule
audit / compliance rule
unclear rule
```

### Step 3. Define Aggregates as Consistency Boundaries

For each aggregate candidate:

- identify the aggregate root;
- identify member concepts only if they are protected by the same consistency boundary;
- list protected invariants;
- identify commands or domain operations that modify it;
- identify what must be immediately consistent;
- identify what may be eventually consistent;
- identify cross-aggregate references by identity only when appropriate;
- record unresolved boundary questions.

Do not group concepts into aggregates because they appear on the same screen, are stored together, or have database relationships.

Aggregates are consistency boundaries, not data containers.

### Step 4. Define Business Rules

For each business rule:

- assign stable ID;
- state the rule in domain language;
- link it to requirements and acceptance criteria;
- identify applicable concepts;
- classify enforcement notes as domain-level, application-level candidate, authorization candidate, audit candidate, or unresolved;
- identify invalid behavior prevented;
- identify future test implication.

Do not define implementation code or test commands.

### Step 5. Define Invariants

For each invariant:

- state what must always be true;
- identify which aggregate or concept protects it;
- identify invalid state prevented;
- link to requirement or acceptance criterion;
- identify future unit or scenario test target;
- record enforcement ambiguity if the invariant crosses aggregate candidates.

A rule is not automatically an invariant. Use invariant only when the condition must always hold within a consistency boundary.

### Step 6. Define Lifecycle and State Transitions

For lifecycle-bearing concepts:

- list states;
- define allowed transitions;
- define transition trigger;
- define guard/precondition;
- define invalid transitions;
- link to acceptance criteria;
- identify future scenario test target.

Create `/workflow/04_domain/04_state_lifecycle.md` only if lifecycle modeling is substantial enough to need a separate artifact. Otherwise include state transition rules in `04_business_rules_invariants.md`.

### Step 7. Identify Rule Conflicts and Gaps

Record:

- conflicting rules;
- rules with no linked requirement;
- requirements with missing rule implications;
- acceptance criteria too vague to infer rules;
- rules that require human approval;
- rule conflicts caused by role, privacy, security, or audit constraints.

### Step 8. Prepare Handoff to 04d

Identify:

- rules that imply domain events;
- state transitions that emit business-significant events;
- aggregates that may define event sources;
- rule clusters that may suggest bounded context boundaries;
- policies that may belong in separate contexts;
- cross-aggregate or external-system interactions.

## 6. Output Artifacts

Create or update:

```text
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_model.md
```

Create if applicable:

```text
/workflow/04_domain/04_state_lifecycle.md
```

### Required Structure: `04_business_rules_invariants.md`

```markdown
# 04 Business Rules and Invariants

## 1. Status
- Status: Draft | Needs Review | Approved
- Source artifacts:
- Last updated:

## 2. Business Rules
| Rule ID | Rule | Rule Type | Applies To | Linked Requirement | Acceptance Criteria | Enforcement Notes |
|---|---|---|---|---|---|---|

## 3. Invariants
| Invariant ID | Invariant | Protected By | Invalid State Prevented | Linked Requirement | Future Test Target | Notes |
|---|---|---|---|---|---|---|

## 4. State Transition Rules
| Transition ID | Concept | From State | To State | Trigger | Guard / Precondition | Invalid Transitions | Linked Acceptance Criteria |
|---|---|---|---|---|---|---|---|

## 5. Rule Conflicts or Gaps
| Gap ID | Type | Description | Affected Requirement / Concept | Impact | Human Decision Needed |
|---|---|---|---|---|---|

## 6. Handoff Notes for 04d
```

### Required Updates in `04_domain_model.md`

Update the aggregate-related sections:

```markdown
## Aggregates
| Aggregate ID | Root | Members | Protected Invariants | Consistency Boundary | Linked Requirements | Notes |
|---|---|---|---|---|---|---|
```

### Optional Structure: `04_state_lifecycle.md`

```markdown
# 04 State and Lifecycle Model

## 1. Status

## 2. Lifecycle-Bearing Concepts
| Concept ID | Concept | Why Lifecycle Matters | Linked Requirements |
|---|---|---|---|

## 3. State Models
| State ID | Concept | State | Meaning | Entry Condition | Exit Condition |
|---|---|---|---|---|---|

## 4. State Transitions
| Transition ID | Concept | From | To | Trigger | Guard | Invalid Transitions | Future Scenario Test Target |
|---|---|---|---|---|---|---|---|

## 5. Lifecycle Open Questions
```

## 7. ID Conventions

Use stable IDs:

```text
AGG-001       Aggregates
BR-001        Business rules
INV-001       Invariants
ST-001        State transitions
RG-001        Rule gaps
STATE-001     States, if separate lifecycle artifact exists
```

Preserve existing Stage 3 requirement and acceptance-criteria IDs.

## 8. Decision / Assumption / Open Question Rules

Decision candidates:

- aggregate root and boundary recommendations;
- invariant definitions;
- state lifecycle model;
- rule classification when it affects architecture or tests.

Working assumptions:

- inferred immediate consistency requirement;
- inferred lifecycle state;
- inferred invalid transition.

Open questions:

- unclear consistency boundary;
- conflicting acceptance criteria;
- rule dependent on missing policy;
- permission or privacy rule unclear;
- invariant crosses multiple aggregate candidates.

Rejected options:

- rejected aggregate boundaries;
- rejected rule interpretations;
- superseded lifecycle models.

## 9. Validation Checklist

Before finishing, verify:

```text
[ ] Aggregates are consistency boundaries, not data containers.
[ ] Aggregate members are included only when protected by shared invariants.
[ ] Each invariant links to a requirement, acceptance criterion, or explicit open question.
[ ] Rules are stated in domain language.
[ ] Permission, privacy, audit, and security-related domain rules are not ignored.
[ ] State transitions exist where lifecycle matters.
[ ] Invalid transitions are recorded where known.
[ ] Future test targets are identified without writing test commands.
[ ] Database/API/architecture/implementation decisions were not made.
[ ] Rule conflicts and traceability gaps are explicit.
```

## 10. Context Handoff to Next Sub-Skill

At the end, report:

```markdown
## Handoff to 04d_events_bounded_contexts

### Aggregates That May Emit Domain Events
- ...

### State Transitions That May Produce Events
- ...

### Rule Clusters That May Indicate Context Boundaries
- ...

### Cross-Aggregate or External Interactions
- ...

### Open Questions 04d Must Preserve
- ...

### Do Not Do in 04d
- Do not turn domain events into message broker topics.
- Do not equate bounded contexts with microservices.
- Do not resolve rule conflicts silently.
```

## 11. Human Approval Note

This sub-skill may request review of aggregate boundaries, rules, invariants, and lifecycle models, but Stage 4 is not ready for downstream approval until `04e_domain_modeling_finalizer` has run.
