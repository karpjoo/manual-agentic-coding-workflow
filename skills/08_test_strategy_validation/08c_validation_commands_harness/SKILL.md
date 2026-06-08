---
name: 08c_validation_commands_harness
description: Define validation commands, command placeholders, test data fixture needs, CI applicability, and validation harness prerequisites for Stage 8.
stage: "08 Test Strategy & Validation Harness"
parent_skill: /skills/08_test_strategy_validation/SKILL.md
subskill_id: 08c
subskill_order: 3
previous_subskill: /skills/08_test_strategy_validation/08b_acceptance_test_design/SKILL.md
next_subskill: /skills/08_test_strategy_validation/08d_manual_specialized_validation/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/08_test_strategy/08_validation_commands.md
requires_human_approval: true
external_visibility: internal
---

# 08c Validation Commands and Harness Planning

## 1. Purpose

Define the command and harness plan that later implementation tasks can use to validate their work.

This sub-skill does not run commands and does not implement tests. It records known validation commands or safe placeholders, expected success signals, failure evidence, prerequisites, fixture needs, and CI suitability.

Primary output:

```text
/workflow/08_test_strategy/08_validation_commands.md
```

Conditional outputs:

```text
/workflow/08_test_strategy/08_test_data_fixtures.md
/workflow/08_test_strategy/08_ci_validation_plan.md
```

## 2. When to Use

Use this sub-skill after:

```text
08a_validation_scope_strategy
08b_acceptance_test_design
```

have created or updated:

```text
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
```

Do not use this sub-skill to:

- run a full validation suite;
- claim tests passed;
- create actual test files;
- choose new tooling as an approved decision without human approval;
- create Stage 9 implementation tasks.

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
```

### Read If Applicable

```text
Project package, build, or CI config files
- if this is a brownfield project or approved tooling already exists.

/workflow/00_intake/00_existing_context_review.md
- if existing codebase, test scripts, CI configuration, or compatibility constraints exist.

/workflow/05_architecture/05_api_contracts.md
- if API or contract validation commands are needed.

/workflow/05_architecture/05_integration_contracts.md
- if external service mocks, stubs, sandbox checks, or contract commands are needed.

/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_indexes.md
/workflow/06_data/06_migration_plan.md
/workflow/06_data/06_data_security_rules.md
- if database, migration, performance, or access-rule validation commands are needed.

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if security or privacy validation commands are needed.
```

### Do Not Read By Default

```text
- entire source code tree for greenfield projects;
- implementation prompts;
- implementation evidence;
- unrelated historical result files;
- superseded/rejected artifacts;
- unapproved draft tooling notes.
```

If exact commands cannot be confirmed, use placeholders marked `Needs Confirmation`.

## 4. USER_DIRECTIVES.md Handling

Check:

```text
/workflow/08_test_strategy/USER_DIRECTIVES.md
```

If the user fixed tooling or command conventions, treat that directive as higher priority than agent assumptions. If it conflicts with approved decisions, report the conflict.

## 5. Input Preflight Procedure

Before producing command artifacts:

```text
[ ] Confirm 08a and 08b outputs exist or report missing outputs.
[ ] Identify accepted test levels and AT IDs.
[ ] Identify which validation methods require commands.
[ ] Identify whether exact commands are available from existing project files or approved decisions.
[ ] Identify commands that must remain placeholders.
[ ] Identify fixture, seed data, mock, stub, or environment needs.
[ ] Identify CI-suitable and local-only validations.
[ ] Report missing tooling information as non-blocking unless it prevents useful planning.
```

Blocking issues may include:

```text
- no acceptance tests or validation methods exist;
- validation command assumptions conflict with approved technology stack;
- security/privacy validation command is required but data handling rules are missing.
```

## 6. Execution Procedure

### Step 1. Inventory Validation Needs

From `08_test_strategy.md` and `08_acceptance_tests.md`, list validation categories that need commands or harness support:

```text
unit
integration
contract
E2E
lint/type/static validation
security/privacy
migration/data
performance
accessibility
AI/data evaluation
mobile/device validation
manual-support commands
```

### Step 2. Create Command IDs

Use stable IDs:

```text
CMD-001, CMD-002, CMD-003
```

If the project already has command ID conventions, preserve them.

### Step 3. Record Known Commands or Placeholders

For each command or placeholder, record:

```text
Command ID
Command / Placeholder
Purpose
When to Run
Prerequisites
Expected Success Signal
Failure Evidence
CI Suitable
Related Test IDs
Status: Confirmed | Placeholder | Needs Confirmation | Deferred | N/A
```

Rules:

- Exact commands may be recorded only when known from approved project files, user directives, or existing configuration.
- If command names are unknown, create placeholders such as `[[CMD: unit test command to confirm]]`.
- Do not invent package manager, framework, test runner, CI provider, or shell command as approved fact.

### Step 4. Define Fixture and Test Data Needs

Create fixture/test data needs using stable IDs:

```text
FX-001, FX-002, FX-003
```

Record:

```text
Fixture ID
Related Test IDs
Data Shape or Persona
Valid/Invalid/Edge Case
Privacy Sensitivity
Seed/Reset Needs
Mock/Stub Needs
Cleanup Needs
Owner Stage
```

Use privacy-safe sample data. Do not include real personal data.

### Step 5. Define Harness and Environment Prerequisites

Record any needed harness setup:

- local test runner;
- test database or emulator;
- seeded test data;
- auth/role simulation;
- external service mock/stub/sandbox;
- browser or device runner;
- CI environment variables;
- secrets handling expectations;
- test reset/cleanup behavior.

### Step 6. Define CI Applicability

For each command, mark:

```text
CI Suitable: Yes | No | Conditional | Unknown
```

If conditional, explain prerequisites.

Create `08_ci_validation_plan.md` if CI expectations need a separate artifact.

### Step 7. Identify Command Gaps

Record:

```text
Command Gap ID
Affected Test IDs
Missing Information
Impact
Needed Human or Tooling Decision
Suggested Stage 9 / 10 Handling
```

Use stable IDs:

```text
VG-001, VG-002
```

## 7. Output Artifacts

### Mandatory Artifact

Create or update:

```text
/workflow/08_test_strategy/08_validation_commands.md
```

Required structure:

```markdown
# 08 Validation Commands

## 1. Status
- Draft / Needs Review / Approved

## 2. Command ID Convention

## 3. Command Inventory
| Command ID | Command / Placeholder | Purpose | When to Run | Prerequisites | Expected Success Signal | Failure Evidence | CI Suitable | Related Test IDs | Status |

## 4. Local Developer Validation

## 5. CI Validation

## 6. Environment-Specific Validation

## 7. Manual Command Setup Needed

## 8. Unknown or Deferred Commands
```

### Conditional Artifact: Test Data Fixtures

Create or update when fixture planning is non-trivial:

```text
/workflow/08_test_strategy/08_test_data_fixtures.md
```

Suggested structure:

```markdown
# 08 Test Data and Fixtures

## 1. Status

## 2. Fixture ID Convention

## 3. Fixture Inventory
| Fixture ID | Related Test IDs | Persona/Data Shape | Valid/Invalid/Edge | Privacy Sensitivity | Seed/Reset Needs | Mock/Stub Needs | Cleanup Needs | Notes |

## 4. Role and Permission Personas

## 5. External Service Mocks / Stubs

## 6. Data Reset and Cleanup Strategy

## 7. Fixture Gaps
```

### Conditional Artifact: CI Validation Plan

Create or update when CI expectations are in scope:

```text
/workflow/08_test_strategy/08_ci_validation_plan.md
```

Suggested structure:

```markdown
# 08 CI Validation Plan

## 1. Status

## 2. CI Scope

## 3. CI Command Candidates

## 4. Required Secrets / Environment Variables

## 5. CI Blockers and Unknowns

## 6. CI N/A Records
```

## 8. Traceability Rules

Create or prepare these links:

```text
Acceptance Test ID → Command ID or Manual Test ID TBD
Command ID → Validation Method
Command ID → Fixture ID, if applicable
Command Gap ID → Affected Test IDs
```

Do not create implementation evidence links. Stage 11 owns evidence links.

## 9. Decision / Assumption / Open Question Rules

Examples:

```text
Candidate: CI should run unit, integration, contract, and lint/type checks before merge.
Assumption: Exact E2E command will be confirmed when tooling is selected.
Open Question: Will external API validation use mocks, sandbox, or manual review for MVP?
```

Do not update `DECISIONS.md` without explicit approval.

## 10. Validation Checklist

Before finishing 08c, verify:

```text
[ ] Each automated or hybrid validation method has a command or placeholder.
[ ] Each command has expected success signal and failure evidence.
[ ] Unknown commands are marked as placeholders, not facts.
[ ] CI suitability is recorded.
[ ] Fixture/test data needs are identified where applicable.
[ ] External dependency mocks/stubs/sandbox needs are recorded where applicable.
[ ] Security/privacy or data validation commands are not silently omitted.
[ ] Command gaps are traceable to affected tests.
[ ] No command claims test success without execution evidence.
```

## 11. Context Handoff to 08d

Prepare handoff:

```text
Next sub-skill: 08d_manual_specialized_validation
Use these as primary inputs:
- /workflow/08_test_strategy/08_test_strategy.md
- /workflow/08_test_strategy/08_acceptance_tests.md
- /workflow/08_test_strategy/08_validation_commands.md
- /workflow/08_test_strategy/08_test_data_fixtures.md, if created
- /workflow/08_test_strategy/08_ci_validation_plan.md, if created

Preserve:
- command IDs;
- placeholders requiring confirmation;
- manual-only validation needs;
- fixture and environment assumptions;
- gaps that require manual or specialized validation.
```

## 12. Human Approval Gate

Final approval occurs in 08e. Interim review may be needed for:

```text
- command placeholders that block task breakdown;
- CI expectations;
- fixture strategy;
- security/privacy command gaps;
- external dependency validation approach.
```

## 13. Do Not Do

Do not:

- run commands and claim results;
- implement tests;
- choose tooling as approved without human approval;
- invent exact commands;
- include real secrets or real personal data;
- treat placeholders as confirmed;
- create task IDs;
- skip failure evidence expectations.
