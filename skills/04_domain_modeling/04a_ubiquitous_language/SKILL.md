---
name: 04a_ubiquitous_language
description: Extract, normalize, define, and stabilize ubiquitous language terms from approved goals, stakeholders, requirements, and acceptance criteria.
stage: 04 Domain Modeling / DDD
parent_skill: /skills/04_domain_modeling/SKILL.md
subskill_id: 04a
subskill_order: 1
previous_subskill: null
next_subskill: /skills/04_domain_modeling/04b_domain_concepts_entities_values/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/04_domain/04_ubiquitous_language.md
requires_human_approval: true
external_visibility: internal
---

# 04a Ubiquitous Language SKILL

## 1. Purpose

Create or update the Stage 4 ubiquitous language artifact.

This sub-skill extracts domain vocabulary from approved project artifacts and normalizes it into a consistent language that later artifacts, code, APIs, UI, and tests should preserve.

This sub-skill does not classify all concepts, design aggregates, define bounded contexts, design database schema, design APIs, or implement code.

## 2. Core Question

Which domain terms must be used consistently so that later requirements, domain model, architecture, data design, tests, UI, and code do not drift apart?

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
```

### Read If Applicable

```text
/workflow/00_intake/00_project_intake.md
- if project type, fixed constraints, or non-changeable areas affect terminology

/workflow/00_intake/00_existing_context_review.md
- if brownfield terminology or compatibility constraints exist

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if roles, permissions, sensitive data, compliance, audit, security, or privacy affect terminology

/workflow/03_requirements/03_traceability_matrix.md
- if Stage 3 produced it

/workflow/context/APPROVAL_LOG.md
- if approval status is ambiguous

/workflow/04_domain/USER_DIRECTIVES.md
- if present

/workflow/04_domain/review_notes.md
- if revising a prior Stage 4 draft
```

### Do Not Read By Default

```text
implementation source code
final database schemas
downstream architecture/API/data design drafts
full historical agent logs
superseded or rejected artifacts
```

## 4. Missing Input Handling

Blocking:

- missing or unapproved service goal;
- missing or unapproved requirements;
- missing or unapproved acceptance criteria;
- missing stakeholder roles when role names carry domain meaning;
- missing artifact status when source-of-truth cannot be identified.

Non-blocking with explicit assumptions:

- missing risk/privacy screening when terminology is not affected;
- missing Stage 3 traceability matrix;
- missing brownfield context for a greenfield project.

Record missing inputs in `/workflow/04_domain/result.md` if result already exists, otherwise include a `## Missing Information` section in `/workflow/04_domain/04_ubiquitous_language.md`.

Use this table:

```markdown
| Missing Input | Blocking? | Why It Matters | Safe Assumption | Human Decision Needed |
|---|---:|---|---|---|
```

## 5. Execution Procedure

### Step 1. Confirm Scope

State:

```text
This sub-skill defines ubiquitous language only. It does not classify the full domain model, define aggregates, design database tables, create APIs, or implement code.
```

### Step 2. Extract Candidate Terms

Extract candidate terms from:

- service goal;
- stakeholder roles;
- functional requirements;
- non-functional requirements when they contain domain concepts;
- acceptance criteria;
- risk/privacy/audit notes when they affect domain language;
- explicit user directives.

Include terms that affect:

- user roles or permissions;
- workflows;
- approvals;
- evaluations or scoring;
- lifecycle states;
- business policies;
- data governance;
- audit or compliance;
- future tests;
- concepts repeatedly referenced across requirements.

Do not include generic UI labels unless they carry domain meaning.

### Step 3. Normalize Preferred Terms

For each candidate term:

- choose a preferred term;
- define it in domain language;
- identify source requirement, acceptance criterion, stakeholder, or decision;
- list synonyms;
- list deprecated or rejected terms;
- flag ambiguity or conflict;
- identify whether the term must be preserved in APIs, UI, tests, code, documentation, or audit logs.

Prefer terminology from approved artifacts. If a user directive conflicts with approved terminology, report the conflict rather than silently replacing it.

### Step 4. Identify Term Types

Classify terms lightly for handoff to `04b`:

```text
role / actor
core concept
workflow / process
state
policy / rule
event candidate
external system
sensitive or security-relevant term
ambiguous
```

Do not force entity/value-object/aggregate classification in this sub-skill. That belongs to `04b` and `04c`.

### Step 5. Detect Language Problems

Explicitly record:

- synonyms that may cause confusion;
- overloaded terms with multiple meanings;
- terms used differently by different stakeholders;
- terms that conflict with approved decisions;
- implementation terms that should not become domain terms;
- domain terms that should replace technical or UI-driven names.

### Step 6. Prepare Handoff to 04b

Create a short section listing terms that are likely to become:

- entities;
- value objects;
- policies;
- events;
- states;
- bounded context split signals;
- open questions for concept classification.

## 6. Output Artifact

Create or update:

```text
/workflow/04_domain/04_ubiquitous_language.md
```

Status must be `Draft` unless explicit human approval is already present.

Required sections:

```markdown
# 04 Ubiquitous Language

## 1. Status
- Status: Draft | Needs Review | Approved
- Source artifacts:
- Last updated:

## 2. Language Scope

## 3. Preferred Domain Terms
| Term ID | Preferred Term | Definition | Term Type | Source Requirement / Stakeholder | Preserve In | Notes |
|---|---|---|---|---|---|---|

## 4. Synonyms and Deprecated Terms
| Term ID | Preferred Term | Synonyms | Deprecated / Rejected Terms | Reason |
|---|---|---|---|---|

## 5. Ambiguous or Conflicting Terms
| Term ID | Term | Conflict / Ambiguity | Sources | Impact | Human Decision Needed |
|---|---|---|---|---|---|

## 6. Terms to Preserve in Later Stages
| Term ID | Preferred Term | Later Stage Impact | Notes |
|---|---|---|---|

## 7. Handoff Notes for 04b

## 8. Missing Information

## 9. Open Questions
```

## 7. ID Conventions

Use stable IDs:

```text
TERM-001, TERM-002, ...
```

Preserve existing IDs if revising the artifact.

Do not reuse a deleted ID for a different concept.

## 8. Decision / Assumption / Open Question Rules

Decision candidates:

- preferred term selections;
- deprecated term recommendations;
- terms that should replace ambiguous or implementation-driven names.

Working assumptions:

- inferred term meanings when source artifacts imply but do not explicitly define them.

Open questions:

- conflicting term meanings;
- role names that affect permissions;
- terms that may represent multiple concepts;
- terms requiring domain expert confirmation.

Rejected options:

- terms explicitly rejected by the user or superseded by approved terminology.

Do not record any term as an approved decision unless explicit human approval exists.

## 9. Validation Checklist

Before finishing, verify:

```text
[ ] Source artifacts are approved or clearly labeled as draft.
[ ] Preferred terms are traceable to requirements, stakeholders, or approved decisions.
[ ] Generic UI labels are not promoted without domain meaning.
[ ] Implementation names are not treated as domain language unless justified.
[ ] Synonyms and deprecated terms are recorded.
[ ] Ambiguous or conflicting terms are flagged.
[ ] Role, permission, privacy, security, and audit-related terms are not ignored.
[ ] Terms likely to affect later concepts, rules, events, or contexts are handed off to 04b.
[ ] No database, API, architecture, or implementation design was created.
```

## 10. Context Handoff to Next Sub-Skill

At the end, report:

```markdown
## Handoff to 04b_domain_concepts_entities_values

### Terms Most Likely to Become Domain Concepts
- ...

### Terms Likely to Be Roles / Actors
- ...

### Terms Likely to Be States / Events / Policies
- ...

### Ambiguities 04b Must Preserve
- ...

### Do Not Do in 04b
- Do not silently resolve term conflicts.
- Do not convert every term into an entity.
- Do not use rejected terms unless reopened by the human developer.
```

## 11. Human Approval Note

This sub-skill may request review of preferred terminology, but Stage 4 is not ready for downstream approval until `04e_domain_modeling_finalizer` has run.
