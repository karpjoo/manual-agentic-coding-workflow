---
name: 08d_manual_specialized_validation
description: Define manual validation plans and specialized validation artifacts for security/privacy, performance, accessibility, brownfield, AI/data, or mobile concerns.
stage: "08 Test Strategy & Validation Harness"
parent_skill: /skills/08_test_strategy_validation/SKILL.md
subskill_id: 08d
subskill_order: 4
previous_subskill: /skills/08_test_strategy_validation/08c_validation_commands_harness/SKILL.md
next_subskill: /skills/08_test_strategy_validation/08e_test_strategy_finalizer/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/08_test_strategy/08_manual_test_plan.md
requires_human_approval: true
external_visibility: internal
---

# 08d Manual and Specialized Validation Planning

## 1. Purpose

Define manual validation and specialized validation plans for behavior that cannot or should not be fully automated before implementation.

This sub-skill creates or updates:

```text
/workflow/08_test_strategy/08_manual_test_plan.md
```

It may also create conditional validation artifacts when applicable:

```text
/workflow/08_test_strategy/08_security_privacy_tests.md
/workflow/08_test_strategy/08_performance_validation.md
/workflow/08_test_strategy/08_accessibility_validation.md
/workflow/08_test_strategy/08_regression_baseline.md
/workflow/08_test_strategy/08_model_or_data_evaluation_plan.md
/workflow/08_test_strategy/08_mobile_platform_validation.md
```

## 2. When to Use

Use this sub-skill after:

```text
08a_validation_scope_strategy
08b_acceptance_test_design
08c_validation_commands_harness
```

Do not use it to:

- perform final release review;
- execute manual tests;
- claim manual tests passed;
- add out-of-scope features to MVP validation;
- replace Stage 12 security/privacy/release review.

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
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
```

### Read If Applicable

```text
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if security, privacy, compliance, abuse, sensitive data, or operational risk exists.

/workflow/04_domain/04_business_rules_invariants.md
- if manual scenario checks need domain rules or lifecycle states.

/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
- if API or external dependency behavior needs manual or specialized validation.

/workflow/06_data/06_data_security_rules.md
- if data access, role visibility, tenant isolation, retention, deletion, or audit behavior needs validation.

/workflow/00_intake/00_existing_context_review.md
- if this is a brownfield, migration, or existing-system project.

/workflow/08_test_strategy/08_test_data_fixtures.md
- if created by 08c.

/workflow/08_test_strategy/08_ci_validation_plan.md
- if created by 08c.
```

### Do Not Read By Default

```text
- implementation evidence;
- release readiness reports;
- full source code tree unless brownfield baseline is explicitly needed;
- raw logs;
- superseded/rejected artifacts;
- unrelated draft artifacts.
```

## 4. USER_DIRECTIVES.md Handling

Check:

```text
/workflow/08_test_strategy/USER_DIRECTIVES.md
```

Pay special attention to directives about:

- required manual review;
- supported browsers/devices;
- security or privacy validation scope;
- regulatory constraints;
- accessibility requirements;
- performance targets;
- brownfield regression requirements;
- AI/data evaluation requirements.

## 5. Input Preflight Procedure

Before producing manual or specialized validation artifacts:

```text
[ ] Confirm strategy, acceptance tests, and command inventory exist.
[ ] Identify manual-only tests from 08b.
[ ] Identify command gaps from 08c that require manual checks.
[ ] Identify project profile: web, internal tool, mobile, AI/data, regulated/security-sensitive, brownfield.
[ ] Identify activated specialized validation artifacts.
[ ] Identify missing risk, data, security, performance, accessibility, or platform inputs.
[ ] Record N/A rationale for specialized validations that do not apply.
```

## 6. Execution Procedure

### Step 1. Define Manual Test Scope

Classify manual validation into:

```text
Required for MVP
Recommended but non-blocking
Deferred to later release
Not applicable
Blocked by open question
```

Manual validation is appropriate when:

- human judgment is required;
- visual/UX quality matters;
- automation is not feasible before implementation;
- external systems cannot be reliably automated;
- exploratory validation is useful for high-risk flows;
- regulated or sensitive workflows require human review.

### Step 2. Create Manual Test IDs

Use stable IDs:

```text
MAN-001, MAN-002, MAN-003
```

### Step 3. Write Manual Test Cases

Each manual test must include:

```text
Manual Test ID
Requirement ID
Role
Preconditions
Steps
Expected Result
Evidence to Capture
Pass/Fail Criteria
Notes
```

Manual tests must not be vague. They need pass/fail criteria and evidence expectations.

### Step 4. Cover Critical Journeys

Include manual validation for:

- critical user journeys;
- admin/operator journeys;
- error, empty, and edge states;
- onboarding or setup flows if relevant;
- external dependency fallbacks if relevant.

### Step 5. Plan Security and Privacy Validation, If Applicable

Create `08_security_privacy_tests.md` if authentication, authorization, sensitive data, personal data, external transfer, audit logging, tenant isolation, abuse prevention, or compliance concerns exist.

Suggested structure:

```markdown
# 08 Security and Privacy Tests

## 1. Status

## 2. Scope

## 3. Security / Privacy Test Inventory
| Test ID | Requirement/Risk ID | Role/Data Boundary | Scenario | Expected Result | Method | Automation Level | Evidence | Notes |

## 4. Access Control and Permission Tests

## 5. Data Exposure / Privacy Tests

## 6. Audit / Logging Tests

## 7. Security / Privacy Gaps
```

### Step 6. Plan Performance Validation, If Applicable

Create `08_performance_validation.md` if performance, scalability, latency, throughput, query efficiency, load behavior, or resource usage is an approved requirement or risk.

Record targets only if approved. Otherwise mark as `Needs Confirmation`.

### Step 7. Plan Accessibility Validation, If Applicable

Create `08_accessibility_validation.md` if user-facing UI accessibility is required or operationally important.

Record:

- scope;
- user journeys;
- assistive technology expectations if known;
- manual checks;
- automated checks if known;
- gaps.

### Step 8. Plan Brownfield Regression Baseline, If Applicable

Create `08_regression_baseline.md` if the project modifies or extends an existing system.

Record:

- existing test commands;
- critical existing behavior to preserve;
- compatibility checks;
- migration checks;
- smoke tests;
- high-risk regression areas.

### Step 9. Plan AI/Data Evaluation, If Applicable

Create `08_model_or_data_evaluation_plan.md` if the system includes AI/data product behavior, analytics, ML workflow, recommendation features, LLM-assisted features, dataset processing, or model outputs.

Record:

- evaluation purpose;
- dataset split or sample strategy;
- metrics if approved;
- benchmark/baseline expectations;
- human review checks;
- reproducibility expectations;
- bias/error analysis if applicable.

### Step 10. Plan Mobile Platform Validation, If Applicable

Create `08_mobile_platform_validation.md` if mobile app or device-dependent behavior exists.

Record:

- device/OS matrix if known;
- offline/sync checks;
- permission checks;
- push notification checks;
- app store release validation notes if applicable.

## 7. Output Artifacts

### Mandatory Artifact

Create or update:

```text
/workflow/08_test_strategy/08_manual_test_plan.md
```

Required structure:

```markdown
# 08 Manual Test Plan

## 1. Status
- Draft / Needs Review / Approved

## 2. Manual Test Scope

## 3. Manual Test Case Inventory
| Manual Test ID | Requirement ID | Role | Preconditions | Steps | Expected Result | Evidence to Capture | Pass/Fail Criteria | Notes |

## 4. Critical User Journeys

## 5. Admin / Operator Journeys

## 6. Error, Empty, and Edge States

## 7. Security / Privacy Manual Checks

## 8. Cross-Browser / Device / Environment Checks

## 9. Manual Tests Deferred or Not Applicable
```

### Conditional Artifacts

Create only if applicable:

```text
/workflow/08_test_strategy/08_security_privacy_tests.md
/workflow/08_test_strategy/08_performance_validation.md
/workflow/08_test_strategy/08_accessibility_validation.md
/workflow/08_test_strategy/08_regression_baseline.md
/workflow/08_test_strategy/08_model_or_data_evaluation_plan.md
/workflow/08_test_strategy/08_mobile_platform_validation.md
```

If not applicable, prepare N/A entries for the finalizer.

## 8. Traceability Rules

Create or prepare these links:

```text
Acceptance Test ID → Manual Test ID, if manual or hybrid
Manual Test ID → Requirement ID
Specialized Test ID → Requirement / Risk / Data Rule / Architecture Contract
Specialized Gap ID → Affected Requirement / Risk / Rule
```

Do not create release approval links. Stage 12 owns release approval.

## 9. Decision / Assumption / Open Question Rules

Examples:

```text
Candidate: Require manual exploratory validation for admin workflows in MVP.
Assumption: Accessibility validation will use manual checklist plus automated check placeholder unless tooling is confirmed.
Open Question: Which browser/device matrix is required for MVP?
```

## 10. Validation Checklist

Before finishing 08d, verify:

```text
[ ] Manual tests have concrete steps, evidence, and pass/fail criteria.
[ ] Critical user/admin/operator journeys are covered or marked as gaps.
[ ] Manual-only rationale is recorded.
[ ] Security/privacy validation is created or marked N/A with rationale.
[ ] Performance validation is created or marked N/A with rationale.
[ ] Accessibility validation is created or marked N/A with rationale.
[ ] Brownfield regression baseline is created or marked N/A with rationale.
[ ] AI/data evaluation plan is created or marked N/A with rationale.
[ ] Mobile platform validation is created or marked N/A with rationale.
[ ] Specialized validation gaps are explicit.
```

## 11. Context Handoff to 08e

Prepare handoff:

```text
Next sub-skill: 08e_test_strategy_finalizer
Use these as primary inputs:
- /workflow/08_test_strategy/08_test_strategy.md
- /workflow/08_test_strategy/08_acceptance_tests.md
- /workflow/08_test_strategy/08_validation_commands.md
- /workflow/08_test_strategy/08_manual_test_plan.md
- all conditional Stage 8 artifacts created by 08c or 08d

Preserve:
- manual test IDs;
- specialized test IDs;
- N/A rationales;
- validation gaps;
- open questions;
- assumptions requiring human confirmation.
```

## 12. Human Approval Gate

Final approval occurs in 08e. Interim review may be needed for:

```text
- manual-only validation of critical flows;
- security/privacy coverage gaps;
- performance/accessibility scope;
- brownfield regression scope;
- AI/data evaluation expectations;
- mobile device/platform matrix.
```

## 13. Do Not Do

Do not:

- execute manual tests;
- claim manual tests passed;
- omit pass/fail criteria;
- create final release approval;
- replace Stage 12 security/release review;
- include real personal data in examples;
- invent regulatory requirements;
- silently skip specialized validation when project profile requires it.
