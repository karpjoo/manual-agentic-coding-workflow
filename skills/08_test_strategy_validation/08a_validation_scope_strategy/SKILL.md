---
name: 08a_validation_scope_strategy
description: Define MVP validation scope, risk-based test priorities, test levels, and requirement-to-validation strategy for Stage 8.
stage: "08 Test Strategy & Validation Harness"
parent_skill: /skills/08_test_strategy_validation/SKILL.md
subskill_id: 08a
subskill_order: 1
previous_subskill: null
next_subskill: /skills/08_test_strategy_validation/08b_acceptance_test_design/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/08_test_strategy/08_test_strategy.md
requires_human_approval: true
external_visibility: internal
---

# 08a Validation Scope and Test Strategy

## 1. Purpose

Define the Stage 8 validation strategy before detailed acceptance tests and validation commands are written.

This sub-skill converts approved requirements, acceptance criteria, architecture, and MVP scope into a clear validation scope:

```text
Requirement / Acceptance Criterion
→ validation method
→ test level
→ automation level
→ priority
→ risk notes
```

This sub-skill creates or updates the Stage 8 strategy artifact:

```text
/workflow/08_test_strategy/08_test_strategy.md
```

## 2. When to Use

Use this sub-skill first in Stage 8 when:

- approved requirements and acceptance criteria exist;
- approved MVP scope exists;
- architecture direction exists;
- the project is ready to define validation before task breakdown.

Do not use this sub-skill to:

- write individual test cases in detail;
- define exact test commands;
- implement tests or code;
- perform final release QA;
- change requirements, acceptance criteria, architecture, data design, or MVP scope.

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
/workflow/05_architecture/05_architecture_plan.md
/workflow/07_mvp_release/07_mvp_scope.md
```

### Read If Applicable

```text
/workflow/00_intake/00_existing_context_review.md
- if this is a brownfield, migration, extension, or existing-codebase project.

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if roles, permissions, sensitive data, privacy, compliance, abuse, or operational risk affects validation.

/workflow/04_domain/04_business_rules_invariants.md
- if domain invariants, lifecycle rules, state transitions, or business rules require validation.

/workflow/04_domain/04_domain_events.md
- if domain events, async workflows, notifications, or event-driven behavior exist.

/workflow/05_architecture/05_api_contracts.md
- if public or internal APIs exist.

/workflow/05_architecture/05_integration_contracts.md
- if external systems, queues, webhooks, third-party services, or LLM/model APIs exist.

/workflow/05_architecture/05_module_boundaries.md
- if module-level tests, contract tests, or boundary tests are needed.

/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_data_security_rules.md
- if persistent data or data access rules exist.

/workflow/07_mvp_release/07_release_slices.md
- if validation differs by release slice.

/workflow/07_mvp_release/07_out_of_scope.md
- if test scope must explicitly exclude non-MVP behavior.
```

### Do Not Read By Default

```text
- full historical agent logs;
- unrelated stage result files;
- superseded artifacts;
- rejected artifacts;
- unapproved drafts unless explicitly requested;
- implementation prompts from Stage 10;
- implementation evidence from Stage 11;
- final release review artifacts from Stage 12;
- the full source code tree unless this is an approved brownfield validation baseline task.
```

## 4. USER_DIRECTIVES.md Handling

Before executing, check:

```text
/workflow/08_test_strategy/USER_DIRECTIVES.md
```

If it exists, read it and classify each directive as:

```text
approval | correction | preference | rejection | scope change | constraint | question | new input
```

Do not treat every directive as an approved global decision. Report conflicts with `DECISIONS.md`, `APPROVAL_LOG.md`, or approved artifacts.

## 5. Input Preflight Procedure

Before creating or updating `08_test_strategy.md`:

```text
[ ] Confirm this is Stage 8 and sub-skill 08a.
[ ] Read required context files and source artifacts.
[ ] Check artifact approval status when manifest or approval log exists.
[ ] Check for USER_DIRECTIVES.md.
[ ] Identify activated conditional inputs.
[ ] Report missing, draft, superseded, rejected, or conflicting inputs.
[ ] Classify missing inputs as Blocking or Non-blocking.
[ ] Restate the current validation scope task.
```

Blocking inputs normally include:

```text
- missing approved requirements;
- missing acceptance criteria;
- missing approved MVP scope;
- unresolved conflict between MVP scope and requirements;
- missing architecture direction when validation depends on system boundaries;
- missing privacy or data access rules when sensitive data is involved.
```

If blocked, create a partial blocker report instead of a completed strategy.

## 6. Execution Procedure

### Step 1. Restate Stage Context

Summarize:

- project validation boundary;
- MVP scope relevant to validation;
- architecture/data constraints relevant to test strategy;
- known risks that influence validation;
- explicit non-scope or later-release items.

### Step 2. Establish Validation Scope

Classify every requirement or feature into one of these categories:

```text
MVP validation required
Later-release validation deferred
Explicitly out of validation scope
Blocked by open question
```

Do not include out-of-scope features in MVP validation except to confirm they remain excluded.

### Step 3. Select Test Levels

For each requirement and acceptance criterion, identify the most appropriate validation level:

```text
unit test
integration test
contract test
end-to-end test
security/privacy test
performance test
accessibility test
manual validation
exploratory validation
```

Do not default everything to E2E. Prefer the lowest reliable level that proves the behavior clearly.

### Step 4. Map Requirements to Validation Methods

Create a requirement-to-validation strategy table.

For each row, include:

```text
Requirement ID
Acceptance Criteria ID
Validation Method
Automation Level
Priority
Risk Notes
```

Automation level should be one of:

```text
Automated
Manual
Hybrid
Deferred
Gap
Needs Confirmation
```

### Step 5. Identify Risk-Based Test Priorities

Identify high-priority validation areas, especially:

- security-sensitive behavior;
- privacy-sensitive behavior;
- role and permission boundaries;
- data correctness and data access boundaries;
- external integration boundaries;
- domain invariants and state transitions;
- critical user journeys;
- release-blocking MVP flows.

### Step 6. Draft Fixture and Environment Strategy

At strategy level, identify whether validation needs:

- personas or roles;
- tenant/account separation data;
- seed data;
- invalid and edge case data;
- external service mocks or stubs;
- browser/device matrix;
- local vs CI environment assumptions.

Detailed fixture planning may be completed in 08c.

### Step 7. Record Validation Gaps

Record gaps such as:

- untestable requirements;
- ambiguous acceptance criteria;
- missing test environment decisions;
- missing fixture or role definitions;
- unknown tool commands;
- unresolved security/privacy validation questions.

## 7. Output Artifact

Create or update:

```text
/workflow/08_test_strategy/08_test_strategy.md
```

Required structure:

```markdown
# 08 Test Strategy

## 1. Status
- Draft / Needs Review / Approved

## 2. Purpose

## 3. Inputs Used

## 4. Validation Scope
### In Scope for MVP
### Deferred to Later Release
### Explicitly Out of Scope
### Blocked by Open Question

## 5. Test Levels
### Unit Tests
### Integration Tests
### Contract Tests
### End-to-End Tests
### Security and Privacy Tests
### Performance Tests
### Accessibility Tests
### Manual Validation
### Exploratory Validation

## 6. Requirement-to-Validation Strategy
| Requirement ID | Acceptance Criteria ID | Validation Method | Automation Level | Priority | Risk Notes |

## 7. Risk-Based Test Priorities

## 8. Test Data and Fixture Strategy

## 9. Environment and Dependency Strategy

## 10. Validation Commands Summary
- Leave detailed commands to 08c. Use high-level needs only here.

## 11. CI Applicability

## 12. Non-Automated Validation Rationale

## 13. Validation Gaps

## 14. Decision Candidates

## 15. Working Assumptions

## 16. Open Questions

## 17. Approval Required
```

The artifact must be marked `Draft` unless explicit human approval already exists.

## 8. Traceability Rules

This sub-skill must create or prepare these links:

```text
Requirement ID → Acceptance Criteria ID
Acceptance Criteria ID → Validation Method
Validation Gap ID → Affected Requirement / Acceptance Criteria
```

Use stable gap IDs such as:

```text
VG-001, VG-002
```

Do not create finalized task links in this sub-skill. Stage 9 creates task links.

## 9. Decision / Assumption / Open Question Rules

Classify outputs carefully:

- Approved decisions require explicit human approval.
- Decision candidates are recommendations awaiting approval.
- Working assumptions are temporary and must remain assumptions.
- Open questions may affect later validation, task cards, implementation prompts, or release.
- Rejected options must not be revived unless the human reopens them.

Examples:

```text
Candidate: Use contract tests for public API endpoints.
Assumption: Exact command names will be confirmed in 08c or Stage 10.
Open Question: Which roles require separate permission-boundary tests?
```

Do not update `DECISIONS.md` unless explicit human approval exists.

## 10. Validation Checklist

Before finishing 08a, verify:

```text
[ ] MVP validation scope is separated from later-release and out-of-scope items.
[ ] Every MVP requirement has at least one proposed validation method or a recorded gap.
[ ] Acceptance criteria are considered in the strategy.
[ ] Test levels are intentionally selected.
[ ] Security/privacy-sensitive behavior is identified or marked N/A with rationale.
[ ] Role and permission behavior is identified where applicable.
[ ] Data and integration validation needs are identified where applicable.
[ ] Risk-based priorities are recorded.
[ ] Validation gaps are explicit.
[ ] Decision candidates, assumptions, and open questions are separated.
```

## 11. Context Handoff to 08b

Prepare a short handoff section at the end of `08_test_strategy.md` or in the active context packet for the next sub-skill:

```text
Next sub-skill: 08b_acceptance_test_design
Use these as primary inputs:
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/07_mvp_release/07_mvp_scope.md
- /workflow/08_test_strategy/08_test_strategy.md

Preserve:
- validation scope boundaries;
- requirement-to-validation method mapping;
- validation gaps;
- assumptions about automation level;
- open questions affecting acceptance tests.
```

## 12. Human Approval Gate

08a may request interim review if strategy choices are high impact. Final approval occurs in 08e.

Interim decisions that may need review:

```text
- MVP automated validation scope;
- high-risk manual-only validation choices;
- test level choices for critical flows;
- validation gaps that may affect task breakdown.
```

## 13. Do Not Do

Do not:

- write implementation tasks;
- write actual test files;
- claim validation commands exist unless confirmed;
- mark placeholders as approved commands;
- change requirements, architecture, data design, or MVP scope;
- use unapproved drafts as source of truth;
- leave untestable requirements unreported;
- classify agent recommendations as approved decisions.
