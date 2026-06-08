---
template_name: 08_test_strategy_skill_template
template_type: stage_specific_skill_template
target_stage: "08_test_strategy_validation"
stage_title: "08 Test Strategy & Validation Harness"
version: 1.0.0
status: draft
intended_output_skill: "/skills/08_test_strategy_validation/SKILL.md"
primary_project_output: "/workflow/08_test_strategy/08_test_strategy.md"
requires_human_approval: true
---

# 08 Test Strategy & Validation Harness — Stage-Specific SKILL Template

> This is a **stage-specific SKILL template**, not an executable `SKILL.md` yet.  
> Use this template together with the Core Skill Template to create `/skills/08_test_strategy_validation/SKILL.md`.

---

## 1. Stage Purpose

Stage 8 defines the validation structure before implementation begins.

The purpose is to make requirements, acceptance criteria, architecture decisions, data rules, and MVP scope practically testable by defining:

- automated test strategy;
- acceptance test design;
- validation harness expectations;
- commands or command placeholders to run later;
- manual verification steps;
- pass/fail criteria;
- traceability from requirements to validation methods;
- validation context that Stage 9 Task Breakdown must use.

This stage does **not** implement tests or product code. It prepares the strategy, test cases, commands, and validation expectations that later stages will use.

---

## 2. Core Question

> Given the approved requirements, acceptance criteria, architecture, data design, and MVP scope, how will the team prove that each requirement is satisfied, safe, and ready for implementation and release?

Sub-questions:

1. Which requirements need unit, integration, contract, E2E, manual, security, privacy, performance, or accessibility validation?
2. Which acceptance criteria can be automated, and which must remain manual for now?
3. What fixtures, test data, mocks, stubs, environments, roles, and permissions are needed?
4. What validation commands should later implementation tasks run?
5. What pass/fail evidence must be produced by Stage 11 implementation tasks?
6. What validation gaps must be recorded before task breakdown begins?

---

## 3. When to Use This Template

Use this template to create a reusable Stage 8 `SKILL.md` when:

- Stage 3 requirements and acceptance criteria exist;
- Stage 5 architecture and technical contracts exist;
- Stage 6 data design exists if the project uses persistent data;
- Stage 7 MVP scope has been defined;
- the next workflow step is Stage 9 task breakdown;
- the project needs test-aware or TDD-ready implementation prompts.

Do not use this template to:

- write implementation code;
- create actual test files;
- modify product source files;
- run a complete QA cycle after implementation;
- perform final release review;
- replace Stage 12 security, privacy, release, or handoff review.

---

## 4. Stage Boundary

### This Stage Does

- Define test strategy and validation scope.
- Convert acceptance criteria into acceptance test specifications.
- Identify unit, integration, contract, E2E, security, privacy, performance, accessibility, and manual validation needs.
- Define validation commands or command placeholders.
- Define required test data and fixtures.
- Update traceability so Stage 9 can attach required tests to task cards.
- Prepare human approval gate for validation strategy.

### This Stage Does Not

- Implement tests.
- Implement application code.
- Change requirements, architecture, data model, or MVP scope.
- Declare that tests passed.
- Create implementation evidence.
- Approve release readiness.

---

## 5. Required Inputs

### 5.1 Always Read

The generated Stage 8 SKILL must require the agent to read these inputs:

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

### 5.2 Read If Applicable

Read these only when the project profile, artifact manifest, context packet, user directives, or approved decisions make them relevant:

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
- if APIs exist.

/workflow/05_architecture/05_integration_contracts.md
- if external systems, webhooks, queues, third-party services, or LLM/model APIs exist.

/workflow/05_architecture/05_module_boundaries.md
- if module-level tests, contract tests, or boundary tests are needed.

/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_physical_schema.md
- if persistent data exists.

/workflow/06_data/06_indexes.md
- if query performance, ordering, filtering, or pagination behavior must be validated.

/workflow/06_data/06_data_security_rules.md
- if data access control, row/document-level security, tenant isolation, or role-based data visibility exists.

/workflow/06_data/06_migration_plan.md
- if migration, seed data, compatibility, rollback, or data backfill validation is needed.

/workflow/07_mvp_release/07_release_slices.md
- if validation differs by release slice or phased rollout.

/workflow/07_mvp_release/07_out_of_scope.md
- if test scope must explicitly exclude non-MVP behavior.

Project test configuration files
- if this is a brownfield project or if existing test commands, CI configuration, package scripts, or tool choices are already fixed.
```

### 5.3 Do Not Read By Default

The generated Stage 8 SKILL must not read these by default:

```text
- full historical result files from unrelated stages;
- raw agent logs;
- superseded artifacts;
- rejected artifacts;
- unapproved draft artifacts unless explicitly requested;
- entire source code tree, unless this is a brownfield validation baseline task;
- implementation prompt drafts from Stage 10;
- implementation evidence from Stage 11, because Stage 8 happens before implementation;
- final release review artifacts from Stage 12.
```

---

## 6. Missing Input Handling

The generated SKILL must classify missing inputs as follows.

### Blocking Missing Inputs

These normally block a complete Stage 8 output:

- missing approved requirements;
- missing acceptance criteria;
- missing approved MVP scope;
- missing architecture direction when validation depends on system boundaries;
- missing data access or privacy rules when sensitive data is involved;
- unresolved conflict between MVP scope and requirements.

### Non-Blocking Missing Inputs

These may allow partial progress with explicit assumptions:

- missing exact test runner command;
- missing CI provider;
- missing final package script names;
- missing exact fixture format;
- missing browser/device matrix for non-critical UI validation;
- missing final deployment environment.

### Required Handling

If an input is missing:

1. Report it under `Missing Information`.
2. Explain why it matters for validation.
3. Mark it as `Blocking` or `Non-blocking`.
4. If non-blocking, continue with a clearly labeled working assumption.
5. If blocking, produce a partial `result.md` and request human decision.
6. Do not silently convert missing information into validation strategy.

---

## 7. Mandatory Output Artifacts

The generated Stage 8 SKILL must create or update these official project artifacts:

```text
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
/workflow/08_test_strategy/result.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/context_packet.md
```

The first four files are official Stage 8 artifacts. `result.md` records execution summary, assumptions, gaps, risks, and approval needs. Context files are updated for Stage 9 handoff.

---

## 8. Conditional Output Artifacts

The generated SKILL may create these artifacts when applicable:

```text
/workflow/08_test_strategy/08_test_data_fixtures.md
- if fixtures, seed data, mock data, factories, personas, tenants, or data privacy constraints require explicit planning.

/workflow/08_test_strategy/08_ci_validation_plan.md
- if CI/CD validation is in scope or required before implementation starts.

/workflow/08_test_strategy/08_security_privacy_tests.md
- if authentication, authorization, sensitive data, external transfer, audit logging, tenant isolation, or abuse prevention requires explicit validation.

/workflow/08_test_strategy/08_performance_validation.md
- if performance, scalability, latency, throughput, query efficiency, or load behavior is an approved requirement.

/workflow/08_test_strategy/08_accessibility_validation.md
- if user-facing UI accessibility is required or legally/operationally important.

/workflow/08_test_strategy/08_regression_baseline.md
- if this is a brownfield or existing-codebase project.

/workflow/08_test_strategy/08_model_or_data_evaluation_plan.md
- if this is an AI/data product, analytics system, ML workflow, recommendation feature, or LLM-assisted feature.

/workflow/08_test_strategy/08_mobile_platform_validation.md
- if this is a mobile app or device-dependent product.
```

---

## 9. N/A Record Rules

If a conditional artifact is not created, the generated SKILL must record an N/A entry in `result.md` or `08_test_strategy.md`.

Each N/A record must include:

```text
Artifact:
Why not applicable:
Revisit if:
Related requirement or decision:
```

Example categories:

- no external API exists;
- no persistent data exists;
- no role-based authorization exists;
- no browser UI exists;
- no AI/model output exists;
- no brownfield regression baseline exists.

---

## 10. Required Output Structure

### 10.1 `/workflow/08_test_strategy/08_test_strategy.md`

Required sections:

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

## 5. Test Levels
### Unit Tests
### Integration Tests
### Contract Tests
### End-to-End Tests
### Security and Privacy Tests
### Performance Tests
### Accessibility Tests
### Manual Validation

## 6. Requirement-to-Validation Strategy
| Requirement ID | Acceptance Criteria ID | Validation Method | Automation Level | Priority | Risk Notes |

## 7. Risk-Based Test Priorities

## 8. Test Data and Fixture Strategy

## 9. Environment and Dependency Strategy

## 10. Validation Commands Summary

## 11. CI Applicability

## 12. Non-Automated Validation Rationale

## 13. Validation Gaps

## 14. Decision Candidates

## 15. Working Assumptions

## 16. Open Questions

## 17. Approval Required
```

### 10.2 `/workflow/08_test_strategy/08_acceptance_tests.md`

Required sections:

```markdown
# 08 Acceptance Tests

## 1. Status

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

### 10.3 `/workflow/08_test_strategy/08_validation_commands.md`

Required sections:

```markdown
# 08 Validation Commands

## 1. Status

## 2. Command ID Convention

## 3. Command Inventory
| Command ID | Command / Placeholder | Purpose | When to Run | Prerequisites | Expected Success Signal | Failure Evidence | CI Suitable | Related Test IDs |

## 4. Local Developer Validation

## 5. CI Validation

## 6. Environment-Specific Validation

## 7. Manual Command Setup Needed

## 8. Unknown or Deferred Commands
```

Rules:

- If exact commands are known, record them exactly.
- If exact commands are not known, create command placeholders and mark them as `Needs Confirmation`.
- Do not invent tool-specific commands as approved facts.
- Include expected success signal and failure evidence for every command or placeholder.

### 10.4 `/workflow/08_test_strategy/08_manual_test_plan.md`

Required sections:

```markdown
# 08 Manual Test Plan

## 1. Status

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

### 10.5 `/workflow/08_test_strategy/result.md`

Required sections:

```markdown
# Result: 08 Test Strategy & Validation Harness

## 1. Task Summary

## 2. Inputs Used

## 3. Outputs Created or Updated

## 4. Validation Strategy Summary

## 5. Coverage Summary

## 6. Missing Information

## 7. Decision Candidates

## 8. Working Assumptions

## 9. Open Questions

## 10. Risks and Constraints

## 11. N/A Records

## 12. Traceability Updates

## 13. Human Approval Required

## 14. Recommended Next Step
```

---

## 11. Stage-Specific Execution Procedure

The generated Stage 8 SKILL must include this procedure.

### Step 1. Run Input Preflight

- Read required context and approved artifacts.
- Check artifact status in `artifact_manifest.yml` if available.
- Confirm whether source artifacts are approved, draft, superseded, or conflicting.
- Read `USER_DIRECTIVES.md` if present in `/workflow/08_test_strategy/`.
- Report missing, ambiguous, superseded, rejected, or conflicting inputs.

### Step 2. Restate Stage Task

Briefly restate:

- current project validation scope;
- MVP boundary;
- relevant architecture/data constraints;
- known risks;
- what this stage will and will not produce.

### Step 3. Establish Validation Scope

Classify features and requirements as:

```text
MVP validation required
Later-release validation deferred
Explicitly out of validation scope
Blocked by open question
```

Do not validate out-of-scope features except to confirm they remain excluded.

### Step 4. Map Requirements to Validation Methods

For each requirement and acceptance criterion:

- assign at least one validation method;
- identify automation level;
- identify required fixture or test data;
- identify risk priority;
- record missing testability information;
- mark gaps that Stage 9 must preserve.

### Step 5. Define Test Levels

Define what belongs at each level:

```text
Unit test
Integration test
Contract test
End-to-end test
Security/privacy test
Performance test
Accessibility test
Manual validation
Exploratory validation
```

Do not overuse E2E tests when unit, integration, or contract tests would provide clearer feedback.

### Step 6. Design Acceptance Tests

Create acceptance test specifications from acceptance criteria.

Each test must include:

- stable test ID;
- linked requirement ID;
- linked acceptance criteria ID;
- actor or system role;
- preconditions;
- scenario;
- expected result;
- pass/fail criteria;
- automation level;
- related data/fixture needs.

### Step 7. Define Fixture and Test Data Strategy

Identify:

- minimal valid data;
- invalid data;
- edge case data;
- role/permission personas;
- tenant/account separation data if applicable;
- external service mocks/stubs;
- privacy-safe sample data;
- seed/reset needs;
- data cleanup needs.

### Step 8. Define Validation Commands

Record known commands or placeholders for:

- unit tests;
- integration tests;
- contract tests;
- E2E tests;
- lint/type checks if treated as validation;
- security/privacy checks if applicable;
- migration/data validation if applicable;
- CI checks if applicable.

For each command or placeholder, include prerequisites, expected success signal, failure evidence, and related tests.

### Step 9. Define Manual Test Plan

Identify manual verification that is necessary because:

- automation is not feasible yet;
- human judgment is required;
- visual or UX behavior matters;
- external services cannot be reliably automated;
- exploratory validation is useful for high-risk flows.

Manual tests must still have pass/fail criteria.

### Step 10. Identify Validation Gaps and Risks

Record:

- untestable requirements;
- ambiguous acceptance criteria;
- missing architecture/test environment decisions;
- missing fixtures;
- unconfirmed commands;
- risks that Stage 9 or Stage 10 must preserve.

### Step 11. Update Traceability

Update or prepare `/workflow/context/TRACEABILITY_MATRIX.md` with links from:

```text
Requirement → Acceptance Criteria → Acceptance Test → Validation Method → Validation Command / Manual Test
```

If task IDs do not exist yet, mark the task link as:

```text
Task: TBD in Stage 9
```

Do not invent implementation task IDs in Stage 8 unless a stable task ID system already exists.

### Step 12. Prepare Context for Stage 9

Update `/workflow/context/context_packet.md` so Stage 9 can create task cards with required tests and validation commands.

### Step 13. Prepare Human Approval Gate

List validation decisions requiring approval before Stage 9 depends on Stage 8 outputs.

---

## 12. Traceability Requirements

### 12.1 ID Conventions

The generated SKILL should use stable IDs such as:

```text
TEST-001     General test strategy item
AT-001       Acceptance test
CMD-001      Validation command
MAN-001      Manual test
FX-001       Fixture or test data need
VG-001       Validation gap
```

If the project already has an ID convention, preserve it.

### 12.2 Required Links

Stage 8 must create or update these links:

```text
Requirement ID → Acceptance Criteria ID
Acceptance Criteria ID → Acceptance Test ID
Acceptance Test ID → Validation Method
Acceptance Test ID → Command ID or Manual Test ID
Validation Gap ID → Affected Requirement / Acceptance Criteria
```

### 12.3 Links to Avoid Creating Prematurely

Stage 8 must not prematurely create these as finalized links unless they already exist:

```text
Acceptance Test ID → Implementation Task ID
Command ID → Implementation Evidence ID
Manual Test ID → Release Approval
```

Those links should be completed later by Stage 9, Stage 11, and Stage 12.

---

## 13. Decision / Assumption / Open Question Rules

The generated SKILL must classify validation statements carefully.

### Approved Decision

Only explicit human approval can create an approved validation decision.

Examples:

```text
Approved: MVP release requires automated acceptance tests for checkout flow.
Approved: Browser compatibility validation is limited to Chrome and Safari for MVP.
```

### Decision Candidate

Use for agent recommendations awaiting human approval.

Examples:

```text
Candidate: Use contract tests for all public API endpoints.
Candidate: Treat manual exploratory testing as required for admin workflows in MVP.
```

### Working Assumption

Use for temporary validation assumptions.

Examples:

```text
Assumption: Exact test runner commands will be confirmed during Stage 10 or Stage 11.
Assumption: E2E testing will use the same seeded data as integration tests unless changed.
```

### Open Question

Use when unresolved information may affect validation.

Examples:

```text
Open Question: Which CI provider will run validation commands?
Open Question: Which roles require separate permission boundary tests?
```

### Rejected Option

Use only when a validation approach was explicitly rejected or superseded.

Example:

```text
Rejected: Do not require cross-browser E2E testing for non-MVP admin-only screens unless reopened.
```

---

## 14. Stage-Specific Validation Checklist

Before Stage 8 output is considered ready for human review, verify:

```text
[ ] Every MVP requirement has at least one validation method.
[ ] Every acceptance criterion is linked to at least one acceptance test or documented validation gap.
[ ] Test levels are intentionally selected rather than defaulting everything to E2E.
[ ] Security/privacy-sensitive behavior has validation coverage or a recorded gap.
[ ] Role and permission behavior has validation coverage where applicable.
[ ] Data access, retention, deletion, and migration behavior has validation coverage where applicable.
[ ] External integrations have contract, mock, sandbox, or manual validation strategy where applicable.
[ ] Test data and fixture needs are identified.
[ ] Manual tests have pass/fail criteria.
[ ] Validation commands have expected success signals and failure evidence.
[ ] Unknown commands are marked as placeholders, not facts.
[ ] CI applicability is recorded.
[ ] Out-of-scope and later-release items are not mixed into MVP validation.
[ ] Traceability matrix is updated or traceability gaps are recorded.
[ ] Decision candidates, assumptions, open questions, and risks are separated.
[ ] Human approval gate is explicit.
```

---

## 15. Stage-Specific Human Approval Gate

The generated SKILL must end with a human approval section.

Required approval categories:

```markdown
## Human Approval Required

### Decisions to Approve
- Automated test scope for MVP
- Manual validation scope for MVP
- Required validation commands or command placeholders
- CI validation expectations
- Security/privacy validation scope
- Performance/accessibility validation scope, if applicable
- Validation gaps accepted for task breakdown

### Assumptions to Confirm
- Test runner/tool assumptions
- Fixture/test data assumptions
- Environment assumptions
- Manual-only validation assumptions

### Open Questions to Resolve
- Questions blocking test design
- Questions blocking validation commands
- Questions affecting Stage 9 task cards

### Risks to Review
- Untestable or ambiguous requirements
- High-risk flows with weak validation
- Security/privacy-sensitive flows without automated coverage
- External dependency validation limitations

### Artifacts Ready for Review
- /workflow/08_test_strategy/08_test_strategy.md
- /workflow/08_test_strategy/08_acceptance_tests.md
- /workflow/08_test_strategy/08_validation_commands.md
- /workflow/08_test_strategy/08_manual_test_plan.md
- /workflow/08_test_strategy/result.md

### Recommended Next Step
- After human approval, run Stage 9 Task Breakdown using Stage 8 validation artifacts as official inputs.
```

---

## 16. Next `context_packet.md` Rules

The generated SKILL must update `/workflow/context/context_packet.md` for Stage 9 Task Breakdown.

Required content:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 08 Test Strategy & Validation Harness
- Completed stages:
- Next recommended stage: 09 Task Breakdown

## 2. Approved Decisions
- Only human-approved validation decisions.

## 3. Working Assumptions
- Validation assumptions that Stage 9 must preserve or confirm.

## 4. Open Questions
- Questions that may affect task size, task order, required tests, or implementation prompts.

## 5. Rejected / Superseded Options
- Validation approaches that should not be revived unless reopened.

## 6. Constraints That Must Not Be Violated
- Test scope constraints
- Security/privacy constraints
- MVP scope constraints
- Tooling/environment constraints
- Manual validation constraints

## 7. Key Context for Next Stage
- Required tests per requirement
- Required commands or placeholders
- Test data/fixture needs
- Manual validation requirements
- Validation gaps

## 8. Required Inputs for Next Stage
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/07_mvp_release/07_mvp_scope.md
- /workflow/08_test_strategy/08_test_strategy.md
- /workflow/08_test_strategy/08_acceptance_tests.md
- /workflow/08_test_strategy/08_validation_commands.md
- /workflow/08_test_strategy/08_manual_test_plan.md
- /workflow/context/TRACEABILITY_MATRIX.md

## 9. Do Not Do
- Do not create implementation tasks without required tests.
- Do not treat command placeholders as confirmed commands.
- Do not include out-of-scope features in MVP task cards.
- Do not ignore validation gaps.
```

---

## 17. Specialization Hooks

The generated SKILL should allow specialization addenda to extend Stage 8.

### Web SaaS

May add:

- browser validation matrix;
- API contract tests;
- authentication/authorization tests;
- multi-tenant or account-boundary tests;
- deployment preview validation.

### Internal Tool

May add:

- operator workflow validation;
- admin permission checks;
- audit trail validation;
- manual approval workflow checks.

### Mobile App

May add:

- device/OS matrix;
- offline/sync validation;
- permission validation;
- app store release validation;
- push notification validation.

### AI/Data Product

May add:

- dataset split validation;
- data provenance validation;
- model evaluation metrics;
- benchmark or baseline comparison;
- human review checks;
- reproducibility checks;
- bias/error analysis.

### Regulated / Security-Sensitive

May add:

- threat-model-linked tests;
- audit log validation;
- privacy impact validation;
- data retention/deletion validation;
- security release blockers;
- compliance evidence requirements.

### Brownfield / Legacy

May add:

- regression baseline;
- compatibility validation;
- migration validation;
- existing test command inventory;
- change-impact validation.

Specialization must not replace the Stage 8 template or weaken approval, traceability, or assumption-handling rules.

---

## 18. Tool Wrapper Hooks

Tool-specific wrappers may add:

- where to save artifacts;
- how to invoke the skill;
- how to run available read-only test discovery commands;
- sandbox permission rules;
- review UI conventions;
- command execution conventions.

Tool wrappers must not define:

- validation scope;
- test strategy decisions;
- acceptance criteria;
- requirement priority;
- security or privacy approval decisions.

---

## 19. Do Not Do

The generated Stage 8 SKILL must prohibit the agent from doing the following:

```text
- Do not implement product code.
- Do not implement test code unless the user explicitly changes this stage boundary.
- Do not claim tests passed without execution evidence.
- Do not invent exact commands when tooling is unknown.
- Do not treat command placeholders as approved commands.
- Do not change requirements, acceptance criteria, architecture, data design, or MVP scope.
- Do not include later-release or out-of-scope features in MVP validation unless explicitly requested.
- Do not use unapproved draft artifacts as source of truth.
- Do not silently ignore security, privacy, authorization, or data-access validation needs.
- Do not collapse all validation into E2E tests.
- Do not leave manual tests without pass/fail criteria.
- Do not update DECISIONS.md without explicit human approval.
- Do not treat Stage 8 artifacts as approved until human approval is recorded.
```

---

## 20. Template Quality Checklist

Before using this template to generate `/skills/08_test_strategy_validation/SKILL.md`, verify:

```text
[ ] The template defines Stage 8 purpose and boundary.
[ ] It does not repeat the full core skill template.
[ ] Always Read inputs are defined.
[ ] Conditional inputs are defined.
[ ] Do Not Read By Default is defined.
[ ] Missing input handling is defined.
[ ] Mandatory artifacts are defined.
[ ] Conditional artifacts and N/A rules are defined.
[ ] Required artifact structures are defined.
[ ] Traceability requirements are defined.
[ ] Human approval gate is defined.
[ ] Next context_packet.md rules are defined.
[ ] Specialization hooks are included.
[ ] Tool wrapper hooks are separated from validation logic.
[ ] No project-specific content is included.
[ ] No implementation work is requested.
```

---

## 21. Recommended Prompt to Generate the Executable SKILL

Use this prompt after saving this template:

```text
You are creating an executable reusable SKILL.md for a Manual Agentic Coding Workflow.

Use the following source documents:
- /workflow_templates/core/core_skill_template.md
- /workflow_templates/stage_templates/08_test_strategy_skill_template.md
- skill-template-design-principles.md
- agentic-coding-workflow-concept-and-design.md

Target output:
- /skills/08_test_strategy_validation/SKILL.md

Create a reusable SKILL.md that an agent can execute for Stage 8 Test Strategy & Validation Harness.

Rules:
1. Follow the core skill template.
2. Implement the Stage 8 template.
3. Define required and conditional inputs.
4. Define official output artifacts and required sections.
5. Define the execution procedure.
6. Define traceability rules from requirements to validation methods.
7. Define decision, assumption, open question, and risk handling.
8. Define context_packet.md update rules for Stage 9 Task Breakdown.
9. Include a human approval gate.
10. Avoid project-specific details.
11. Do not implement tests or code.
12. Mark assumptions explicitly.
13. Do not treat agent proposals as approved decisions.
```
