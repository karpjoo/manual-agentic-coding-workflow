---
name: 08b_acceptance_test_design
description: Convert approved acceptance criteria and Stage 8 validation strategy into acceptance test specifications.
stage: "08 Test Strategy & Validation Harness"
parent_skill: /skills/08_test_strategy_validation/SKILL.md
subskill_id: 08b
subskill_order: 2
previous_subskill: /skills/08_test_strategy_validation/08a_validation_scope_strategy/SKILL.md
next_subskill: /skills/08_test_strategy_validation/08c_validation_commands_harness/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/08_test_strategy/08_acceptance_tests.md
requires_human_approval: true
external_visibility: internal
---

# 08b Acceptance Test Design

## 1. Purpose

Create acceptance test specifications from approved requirements, acceptance criteria, MVP scope, and the Stage 8 validation strategy.

This sub-skill answers:

```text
For each MVP acceptance criterion, what concrete acceptance test or validation gap will prove whether it is satisfied?
```

Primary output:

```text
/workflow/08_test_strategy/08_acceptance_tests.md
```

## 2. When to Use

Use this sub-skill after `08a_validation_scope_strategy` has drafted or updated:

```text
/workflow/08_test_strategy/08_test_strategy.md
```

Do not use it to:

- design general test strategy from scratch;
- define exact shell commands;
- write test implementation code;
- create implementation tasks;
- change acceptance criteria.

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
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/08_test_strategy/08_test_strategy.md
```

### Read If Applicable

```text
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if roles, permissions, privacy, compliance, or abuse scenarios affect acceptance tests.

/workflow/04_domain/04_business_rules_invariants.md
- if invariants, lifecycle, or state transitions require scenario tests.

/workflow/04_domain/04_domain_events.md
- if async workflows, events, notifications, or event-driven behavior exist.

/workflow/05_architecture/05_api_contracts.md
- if acceptance tests must reference API behavior or contract expectations.

/workflow/05_architecture/05_integration_contracts.md
- if external dependency behavior must be accepted, mocked, stubbed, or manually verified.

/workflow/06_data/06_data_security_rules.md
- if role/data visibility must be represented in acceptance tests.

/workflow/07_mvp_release/07_release_slices.md
- if acceptance tests must be grouped by release slice.

/workflow/07_mvp_release/07_out_of_scope.md
- if acceptance tests must explicitly avoid non-MVP behavior.
```

### Do Not Read By Default

```text
- implementation prompt drafts;
- implementation evidence;
- source code tree unless brownfield baseline requires it;
- superseded or rejected artifacts;
- raw agent logs;
- unrelated prior-stage result files.
```

## 4. USER_DIRECTIVES.md Handling

Check this file before producing acceptance tests:

```text
/workflow/08_test_strategy/USER_DIRECTIVES.md
```

Apply directives according to precedence, but report conflicts rather than silently resolving them.

## 5. Input Preflight Procedure

Before creating or updating acceptance tests:

```text
[ ] Confirm 08a strategy artifact exists or identify it as missing.
[ ] Confirm requirements and acceptance criteria are available.
[ ] Confirm MVP scope boundary is available.
[ ] Check if any requirements are excluded from MVP.
[ ] Check if USER_DIRECTIVES.md adds acceptance-test constraints.
[ ] Identify missing, ambiguous, or conflicting acceptance criteria.
[ ] Record blocked criteria as validation gaps, not invented tests.
```

Blocking issues include:

```text
- acceptance criteria missing for MVP requirements;
- acceptance criteria contradict MVP scope;
- actor/role behavior required but roles are undefined;
- security/privacy-sensitive criteria lack enough information for safe test design.
```

## 6. Execution Procedure

### Step 1. Build Acceptance Coverage Inventory

For each MVP requirement and acceptance criterion:

- identify the requirement ID;
- identify the acceptance criterion ID;
- identify release slice or MVP status;
- determine whether the criterion should be automated, manual, hybrid, deferred, or recorded as a gap.

### Step 2. Define Acceptance Test IDs

Use stable IDs:

```text
AT-001, AT-002, AT-003
```

Preserve existing project ID conventions if already defined.

### Step 3. Write Acceptance Test Specifications

Each acceptance test must include:

```text
Test ID
Requirement ID
Acceptance Criteria ID
Release Slice
Actor/System
Preconditions
Scenario
Expected Result
Validation Method
Automation Level
Test Data
Pass/Fail Criteria
Notes
```

Do not write executable code. Describe test behavior precisely enough that Stage 9 can create task cards and Stage 10 can write implementation prompts.

### Step 4. Include Negative and Edge Case Tests

For applicable requirements, add tests for:

- invalid input;
- empty state;
- unauthorized access;
- permission boundary failure;
- unavailable external dependency;
- duplicate or conflicting action;
- boundary values;
- state transition errors;
- privacy or data exposure risks.

### Step 5. Include Role and Permission Tests

If roles or permissions exist, define tests for:

- allowed actions;
- denied actions;
- cross-role access attempts;
- tenant/account boundary violations;
- admin/operator actions;
- audit-visible events if applicable.

### Step 6. Include Data and Privacy Tests

If persistent, personal, or sensitive data exists, define tests for:

- create/read/update/delete behavior;
- data visibility rules;
- retention/deletion behavior if required;
- redaction or masking if required;
- data validation rules;
- migration/backfill behavior if in scope.

### Step 7. Include Integration Tests

If external systems exist, define acceptance tests for:

- success response;
- failure response;
- retry or fallback behavior;
- timeout behavior;
- sandbox/mock/stub assumptions;
- manual-only external checks if automation is not feasible.

### Step 8. Record Coverage Gaps

If a criterion cannot be converted into a test, record:

```text
Gap ID
Affected Requirement ID
Affected Acceptance Criteria ID
Reason
Impact
Needed Decision or Input
Suggested Next Stage Handling
```

Use stable IDs:

```text
VG-001, VG-002
```

## 7. Output Artifact

Create or update:

```text
/workflow/08_test_strategy/08_acceptance_tests.md
```

Required structure:

```markdown
# 08 Acceptance Tests

## 1. Status
- Draft / Needs Review / Approved

## 2. Acceptance Test ID Convention

## 3. Acceptance Test Inventory
| Test ID | Requirement ID | Acceptance Criteria ID | Release Slice | Actor/System | Preconditions | Scenario | Expected Result | Validation Method | Automation Level | Test Data | Pass/Fail Criteria | Notes |

## 4. Negative and Edge Case Tests

## 5. Role and Permission Tests

## 6. Data and Privacy Tests

## 7. Integration and External Dependency Tests

## 8. Manual-Only Acceptance Tests

## 9. Coverage Gaps
```

Mark the artifact as `Draft` unless explicit human approval exists.

## 8. Traceability Rules

Create or prepare these links:

```text
Requirement ID → Acceptance Criteria ID
Acceptance Criteria ID → Acceptance Test ID
Acceptance Test ID → Validation Method
Acceptance Test ID → Coverage Gap ID, if test cannot be defined
```

Do not create finalized links to implementation task IDs. Stage 9 owns task IDs.

## 9. Decision / Assumption / Open Question Rules

Examples:

```text
Candidate: Treat AT-004 as manual-only for MVP because external approval cannot be automated yet.
Assumption: Admin role exists as described in requirements unless later corrected.
Open Question: Should failed external API calls be accepted as retryable or terminal failures?
```

Do not silently rewrite requirements. If acceptance criteria are ambiguous, record a gap or open question.

## 10. Validation Checklist

Before finishing 08b, verify:

```text
[ ] Every MVP acceptance criterion has at least one AT ID or a coverage gap.
[ ] Each acceptance test has clear preconditions, scenario, expected result, and pass/fail criteria.
[ ] Manual-only tests are explicitly marked.
[ ] Role and permission tests are included where applicable.
[ ] Data and privacy tests are included where applicable.
[ ] Integration and external dependency tests are included where applicable.
[ ] Non-MVP behavior is not accidentally included in MVP acceptance tests.
[ ] Coverage gaps are explicit and traceable.
[ ] Test IDs are stable.
```

## 11. Context Handoff to 08c

Prepare the next sub-skill handoff:

```text
Next sub-skill: 08c_validation_commands_harness
Use these as primary inputs:
- /workflow/08_test_strategy/08_test_strategy.md
- /workflow/08_test_strategy/08_acceptance_tests.md

Preserve:
- AT IDs;
- automation level choices;
- manual-only classification;
- test data needs;
- coverage gaps;
- open questions affecting command or harness setup.
```

## 12. Human Approval Gate

Final approval occurs in 08e. Interim review may be requested for:

```text
- acceptance criteria that cannot be tested;
- manual-only acceptance tests for critical MVP flows;
- security/privacy-sensitive tests;
- high-risk coverage gaps.
```

## 13. Do Not Do

Do not:

- implement tests;
- invent missing acceptance criteria;
- change requirement IDs or acceptance criterion IDs without reason;
- create implementation task IDs;
- mark acceptance tests as approved without human approval;
- collapse detailed acceptance tests into vague checklist items;
- omit pass/fail criteria.
