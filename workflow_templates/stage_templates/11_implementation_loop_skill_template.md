---
name: 11_tdd_implementation_loop_skill_template
description: Template for creating a reusable Stage 11 SKILL that executes approved implementation tasks through a controlled TDD loop with traceable test evidence.
stage: 11 TDD Implementation Loop
template_type: stage_specific_skill_template
version: 1.0.0
status: draft
extends: /workflow_templates/core/core_skill_template.md
primary_output: /workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
requires_human_approval: true
---

# 11 TDD Implementation Loop SKILL Template

> Use this template to create a reusable `SKILL.md` for Stage 11: `11_tdd_implementation_loop`.
> This is a stage-specific implementation template. It defines how an Agent should implement one approved task at a time using a TDD or test-aware loop.

---

## 0. Template Scope

This template is for creating a reusable Stage 11 implementation SKILL.

The generated SKILL must help an Agent:

1. Select one approved implementation task.
2. Read only the approved and relevant context.
3. Inspect the existing code before editing.
4. Restate the task, allowed scope, and forbidden changes.
5. Write or identify a failing test before implementation whenever feasible.
6. Confirm the test failure.
7. Implement the smallest change needed.
8. Run targeted and broader validation commands.
9. Refactor only within the approved scope.
10. Record implementation and test evidence.
11. Update result and context artifacts.
12. Prepare the task for human review.

This template must not be used to:

- generate requirements;
- redesign architecture;
- change task scope;
- rewrite implementation prompts;
- perform final release review;
- approve its own implementation work.

---

## 1. Purpose

Create a Stage 11 SKILL that implements approved task cards through a disciplined TDD implementation loop.

The generated SKILL must treat implementation as a repeated per-task cycle, not as one large coding phase.

The SKILL must preserve this principle:

```text
One approved task → one bounded code change → one evidence record → one human review point
```

---

## 2. Core Question

For the selected approved task:

```text
Can the Agent implement the smallest correct change, verify it with tests or validation evidence, and record enough traceable evidence for human review?
```

---

## 3. When to Use

Use the generated SKILL when all of the following are true:

- Stage 9 task cards have been created and approved.
- Stage 10 implementation prompts or handoff packets have been created and approved.
- The task has a stable `TASK_ID`.
- The task has defined acceptance criteria, required tests, and a definition of done.
- The Agent is allowed to modify the codebase within a specified scope.
- The user wants a test-first or test-aware implementation loop.

---

## 4. When Not to Use

Do not use the generated SKILL when:

- the task card is missing or unapproved;
- the implementation prompt is missing or unapproved;
- the requested change affects architecture, API contract, data schema, security, privacy, or release scope without approval;
- the user is asking for task breakdown, prompt writing, or release review instead of implementation;
- the Agent cannot inspect the relevant codebase;
- the Agent cannot record validation evidence;
- the current task requires a human product/design/security decision before code changes can safely proceed.

---

## 5. Required Inputs

The generated SKILL must define the following input contract.

### 5.1 Always Read

The Agent must read these files before editing code:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_dependency_order.md
/workflow/10_prompts/10_implementation_prompts.md
/workflow/10_prompts/10_prompt_handoff_packets.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_validation_commands.md
```

If the project uses a different path convention, the generated SKILL must preserve the same logical input roles.

### 5.2 Task-Specific Required Inputs

For the selected `TASK_ID`, the Agent must identify:

```text
- approved task card
- approved implementation prompt or handoff packet
- linked requirements
- linked acceptance criteria
- linked domain concepts or invariants, if any
- linked architecture/module/API/data components, if any
- allowed change scope
- forbidden changes
- required tests
- commands to run
- expected evidence
- definition of done
- rollback or recovery notes, if any
```

### 5.3 Read If Applicable

Read these only when activated by the task card, implementation prompt, project profile, or context packet:

```text
/workflow/03_requirements/03_requirements.md
  if requirement details or acceptance criteria must be verified

/workflow/03_requirements/03_acceptance_criteria.md
  if acceptance criteria are referenced but not fully visible in the task card

/workflow/04_domain/04_business_rules_invariants.md
  if the task touches domain rules, state transitions, lifecycle, or invariants

/workflow/04_domain/04_domain_model.md
  if the task changes domain objects, use cases, entities, value objects, or services

/workflow/05_architecture/05_architecture_plan.md
  if the task touches module boundaries, layering, deployment shape, or cross-cutting architecture

/workflow/05_architecture/05_module_boundaries.md
  if the task touches module ownership or dependency direction

/workflow/05_architecture/05_api_contracts.md
  if the task changes or consumes API behavior

/workflow/05_architecture/05_integration_contracts.md
  if the task touches external systems, queues, webhooks, or third-party services

/workflow/06_data/06_logical_schema.md
  if the task touches persistent data structures

/workflow/06_data/06_physical_schema.md
  if the task touches database implementation details

/workflow/06_data/06_migration_plan.md
  if the task includes schema or data migration

/workflow/06_data/06_data_security_rules.md
  if the task affects access control, row/document security, privacy, or data visibility

/workflow/12_review_release_handoff/review_notes.md
  if this task is a follow-up from review findings
```

### 5.4 Codebase Files to Inspect First

The generated SKILL must require the Agent to inspect existing code before editing.

The Agent should inspect:

```text
- files explicitly listed in the task card or implementation prompt
- nearby tests for the same module or behavior
- test configuration and test helper files
- package/build/test scripts
- API route/controller/service files relevant to the task
- schema/migration files relevant to the task
- security/access-control files relevant to the task
- existing patterns for error handling, logging, validation, and naming
```

The Agent must not scan or rewrite unrelated parts of the repository by default.

### 5.5 Do Not Read By Default

The generated SKILL must tell the Agent not to read these by default:

```text
- full historical agent logs
- superseded artifacts
- rejected artifacts
- unrelated stage drafts
- unrelated source code directories
- unrelated tests
- secrets, private keys, credentials, production environment files
- generated build artifacts unless needed for debugging
- dependency lockfile diffs unless dependency changes are explicitly allowed
```

### 5.6 Missing Input Handling

If a required input is missing, the generated SKILL must require the Agent to classify it:

```text
Blocking:
- no approved task card
- no approved implementation prompt
- no allowed change scope
- no definition of done
- required codebase files cannot be inspected
- security/privacy-impacting change lacks approval
- schema/API/architecture change lacks approval

Non-blocking with explicit assumption:
- minor test command ambiguity when a safe local command can be inferred
- missing optional manual verification detail
- missing non-critical linked artifact when the task card contains enough approved detail
```

If progress continues with assumptions, the generated SKILL must record them in the task result and `ASSUMPTIONS.md` as appropriate.

---

## 6. USER_DIRECTIVES.md Handling

The generated SKILL must check:

```text
/workflow/11_implementation_results/USER_DIRECTIVES.md
```

If present, it must be read before implementation.

The Agent must classify directives as:

```text
- explicit approval
- correction
- scope change
- forbidden change
- task priority update
- test requirement update
- review comment
- rollback instruction
- question
```

If `USER_DIRECTIVES.md` conflicts with an approved task, implementation prompt, architecture decision, data decision, or security constraint, the Agent must report the conflict and stop if the conflict changes implementation scope or risk.

---

## 7. Input Preflight Procedure

The generated SKILL must include this preflight procedure.

```text
1. Confirm the selected TASK_ID.
2. Read artifact_manifest.yml, context_packet.md, DECISIONS.md, APPROVAL_LOG.md, and TRACEABILITY_MATRIX.md.
3. Read Stage 9 task card and Stage 10 implementation prompt for TASK_ID.
4. Verify that the task and prompt are approved or explicitly authorized for execution.
5. Identify allowed change scope and forbidden changes.
6. Identify required tests and validation commands.
7. Identify expected evidence artifacts.
8. Identify conditional inputs activated by this task.
9. Inspect relevant existing code and tests before editing.
10. Check for missing, conflicting, superseded, or unapproved inputs.
11. Check for existing local changes or files that may be overwritten.
12. Restate the task, scope, test plan, and stop conditions before editing.
```

If the repository has uncommitted human changes or unexpected modifications, the generated SKILL must require the Agent to avoid overwriting them and report the risk.

---

## 8. Execution Procedure

The generated SKILL must implement this per-task loop.

### 8.1 Select One Task

Operate on exactly one approved `TASK_ID` unless the user explicitly authorizes a small batch.

Record:

```text
Task ID:
Task title:
Linked implementation prompt:
Linked requirements:
Allowed scope:
Forbidden changes:
Required tests:
Commands to run:
Definition of done:
```

### 8.2 Inspect Before Editing

Before making changes, inspect:

```text
- existing implementation patterns
- relevant tests
- test helpers and fixtures
- current behavior
- module boundaries
- error-handling conventions
- security/access rules if relevant
```

Record files inspected in the result artifact.

### 8.3 Restate the Implementation Plan

The Agent must write a short plan before editing:

```text
- test to add or identify
- expected failing behavior
- minimal implementation change
- validation commands
- evidence to record
- risks or stop conditions
```

The plan must not introduce new product behavior beyond the approved task.

### 8.4 Red Step: Write or Identify a Failing Test

The generated SKILL must include this rule:

```text
Do not implement the feature before identifying or writing the test that will verify it.
```

The Agent must do one of the following:

```text
Option A: Write a new failing automated test.
Option B: Identify an existing failing test that directly covers the task.
Option C: If strict test-first is not feasible, document why and create a test-aware validation plan before implementation.
```

For Option A or B, the Agent must run the targeted test and record:

```text
- command run
- expected failure
- actual failure
- failure output summary
- whether the failure matches the intended behavior gap
```

If the test fails for an unrelated reason, the Agent must stop or narrow the issue before implementation.

### 8.5 Green Step: Implement the Minimal Change

Implement only what is needed to pass the selected test and satisfy the task acceptance criteria.

The Agent must not:

```text
- add unrelated features
- refactor unrelated modules
- change public contracts without approval
- change schema or migration behavior unless approved
- add dependencies unless approved
- broaden user roles or permissions without approval
- weaken security/privacy constraints
```

### 8.6 Run Targeted Tests

Run the smallest relevant automated validation first.

Record:

```text
- command
- pass/fail result
- output summary
- failing test names, if any
- unresolved failure analysis, if any
```

### 8.7 Refactor Within Scope

Refactor only after the targeted tests pass.

Allowed refactoring:

```text
- remove duplication introduced by the task
- align with existing naming and structure
- improve small local readability
- simplify implementation while preserving behavior
```

Forbidden refactoring:

```text
- broad architectural reshaping
- unrelated module cleanup
- style-only churn across many files
- dependency restructuring
- public contract changes without approval
```

After refactoring, rerun relevant tests.

### 8.8 Run Broader Regression Validation

Run broader validation defined by the task, implementation prompt, or Stage 8 validation commands.

Examples:

```text
- related unit test suite
- integration tests for touched module
- E2E smoke test, if applicable
- typecheck
- lint
- build
- migration validation
- security rule tests
```

If any required validation cannot be run, record:

```text
- command not run
- reason
- risk
- suggested human/manual validation
```

### 8.9 Manual Verification, If Applicable

If automated validation is insufficient or UI/operational behavior is involved, record manual verification steps:

```text
- setup state
- user/action sequence
- expected result
- observed result
- evidence location, if any
```

### 8.10 Update Traceability

Update traceability from task to implementation evidence.

Required link pattern:

```text
Requirement → Acceptance Criteria → Test Case → Task → Changed Files → Test Evidence → Task Result
```

If traceability cannot be completed, record a traceability gap.

### 8.11 Record Evidence

Create or update the required Stage 11 artifacts.

Evidence must be specific enough for a human reviewer to determine:

```text
- what changed
- why it changed
- which tests were added or modified
- which commands were run
- which results passed or failed
- which validation was skipped and why
- what risks remain
```

### 8.12 Update Context for Next Task or Stage

Update `context_packet.md` with only the minimal operational context needed by the next implementation task or Stage 12.

Do not copy entire test logs or large code diffs into `context_packet.md`.

---

## 9. Output Artifacts

The generated SKILL must define these artifact contracts.

### 9.1 Mandatory Artifacts

For each `TASK_ID`, create or update:

```text
/workflow/11_implementation_results/11_task_result_{{TASK_ID}}.md
  Purpose: task-level implementation summary, scope record, validation summary, review gate.

/workflow/11_implementation_results/11_test_evidence_{{TASK_ID}}.md
  Purpose: red/green/refactor/regression evidence for the task.

/workflow/context/context_packet.md
  Purpose: minimal handoff context for the next task or Stage 12.

/workflow/context/TRACEABILITY_MATRIX.md
  Purpose: link task, tests, changed files, and implementation evidence.
```

### 9.2 Conditional Artifacts

Create or update when applicable:

```text
/workflow/11_implementation_results/11_manual_verification_{{TASK_ID}}.md
  if manual validation is required or automated tests are insufficient.

/workflow/11_implementation_results/11_migration_evidence_{{TASK_ID}}.md
  if database schema or data migration is implemented.

/workflow/11_implementation_results/11_api_contract_evidence_{{TASK_ID}}.md
  if API behavior, request/response shape, or integration contract is changed.

/workflow/11_implementation_results/11_security_privacy_evidence_{{TASK_ID}}.md
  if the task touches auth, authorization, personal data, sensitive data, audit logs, or external transfer.

/workflow/11_implementation_results/11_ui_evidence_{{TASK_ID}}.md
  if UI behavior or user-visible flow is changed.

/workflow/11_implementation_results/11_performance_evidence_{{TASK_ID}}.md
  if performance, scalability, query efficiency, or resource usage is part of the task definition of done.

/workflow/11_implementation_results/11_rollback_notes_{{TASK_ID}}.md
  if rollback or recovery procedure is needed for the change.
```

### 9.3 N/A Record

For each conditional artifact not produced, record in `11_task_result_{{TASK_ID}}.md`:

```text
Artifact:
Why not applicable:
Revisit if:
```

---

## 10. Required Output Structure

### 10.1 `11_task_result_{{TASK_ID}}.md`

The generated SKILL must require this structure:

```markdown
# Task Result: {{TASK_ID}} — {{TASK_TITLE}}

## 1. Status
- Status: Draft | Needs Review | Blocked | Completed Pending Human Review
- Task ID:
- Implementation prompt ID:
- Date:
- Agent/tool:

## 2. Task Summary
- Approved goal:
- Linked requirements:
- Linked acceptance criteria:
- Linked test cases:
- Definition of done:

## 3. Inputs Used
- Approved task card:
- Approved implementation prompt:
- Context files:
- Code files inspected:
- Test files inspected:

## 4. Scope Control
- Allowed changes:
- Forbidden changes:
- Scope changes requested: None | List
- Scope conflicts: None | List

## 5. Files Changed
| File | Change Type | Reason | Linked Test/Evidence |
|---|---|---|---|

## 6. Tests Added or Modified
| Test File | Test Case | Purpose | Linked Requirement/Task |
|---|---|---|---|

## 7. Tests and Commands Run
| Command | Purpose | Result | Evidence Reference |
|---|---|---|---|

## 8. TDD Summary
- Red step completed: Yes | No | Not feasible
- Failure confirmed before implementation: Yes | No | Not feasible
- Green step completed: Yes | No
- Refactor completed: Yes | No | Not needed
- Regression validation completed: Yes | No | Partial

## 9. Validation Result
- Overall result:
- Passing evidence:
- Failing evidence:
- Not-run validation:
- Manual verification:

## 10. Known Limitations
- ...

## 11. Assumptions Used
- ...

## 12. Open Questions
- ...

## 13. Risks and Follow-up Tasks
- ...

## 14. Traceability Updates
- Requirement → Acceptance Criteria → Test → Task → Evidence links updated:
- Traceability gaps:

## 15. Conditional Artifact N/A Record
| Artifact | Why Not Applicable | Revisit If |
|---|---|---|

## 16. Human Review Required
### Review Checklist
- [ ] Code change is within approved scope.
- [ ] Required tests were added or identified.
- [ ] Required validation passed or exceptions are justified.
- [ ] No unauthorized architecture/API/data/security changes were made.
- [ ] Evidence is sufficient for reviewer confidence.

### Reviewer Decision Needed
- Approve task completion | Request changes | Block task | Reopen scope/design decision
```

### 10.2 `11_test_evidence_{{TASK_ID}}.md`

The generated SKILL must require this structure:

```markdown
# Test Evidence: {{TASK_ID}} — {{TASK_TITLE}}

## 1. Evidence Summary
- Task ID:
- Test strategy reference:
- Validation command reference:
- Environment summary:

## 2. Red Step Evidence
- Test added or identified:
- Command run:
- Expected failure:
- Actual failure:
- Failure matched intended behavior gap: Yes | No
- Notes:

## 3. Green Step Evidence
- Implementation summary:
- Command run:
- Result:
- Output summary:

## 4. Refactor Evidence
- Refactor performed: Yes | No
- Reason:
- Tests rerun:
- Result:

## 5. Regression Evidence
| Command | Scope | Result | Notes |
|---|---|---|---|

## 6. Manual Verification Evidence
- Required: Yes | No
- Steps:
- Expected result:
- Observed result:
- Evidence location:

## 7. Not-Run Tests or Skipped Validation
| Validation | Reason Not Run | Risk | Recommended Follow-up |
|---|---|---|---|

## 8. Failure Log Summary
- Remaining failures:
- Failure classification: task-related | unrelated | environment | unknown
- Human action needed:
```

---

## 11. Traceability Rules

The generated SKILL must require traceability to be preserved or improved.

### 11.1 Required Links

For each task, maintain these links where applicable:

```text
Goal ID
→ Requirement ID
→ Acceptance Criteria ID
→ Domain Concept / Invariant ID
→ Architecture / Module / API / Data Component ID
→ Task ID
→ Test Case ID
→ Changed File Path
→ Test Evidence Artifact
→ Task Result Artifact
```

### 11.2 Stable ID Rules

The generated SKILL should use existing IDs from previous artifacts.

If new implementation evidence IDs are needed, use:

```text
IMPL-{{TASK_ID}}-001
TEST-EVID-{{TASK_ID}}-001
MANUAL-EVID-{{TASK_ID}}-001
TRACE-GAP-{{TASK_ID}}-001
```

### 11.3 Traceability Gaps

Record a traceability gap when:

```text
- a task lacks a linked requirement;
- a test lacks a linked acceptance criterion;
- a changed file cannot be linked to the approved task;
- implementation evidence cannot be linked to a validation method;
- the task requires behavior not present in approved requirements.
```

---

## 12. Decision / Assumption / Open Question Rules

The generated SKILL must preserve these distinctions.

### 12.1 Approved Decisions

Only explicit human approval can create approved decisions.

The Agent must not add implementation decisions to `DECISIONS.md` unless the user explicitly approves them.

### 12.2 Decision Candidates

Record as decision candidates when implementation reveals a choice requiring human review, such as:

```text
- changing API behavior
- changing data model or migration approach
- adding a new dependency
- changing security behavior
- changing user-visible workflow
- changing error semantics
- changing performance trade-offs
```

### 12.3 Working Assumptions

Use assumptions only when they are safe and clearly bounded.

Examples:

```text
Assumption: The existing test command in package scripts is the authoritative local test command.
Assumption: Existing naming patterns in the target module should be followed unless contradicted by the task card.
```

### 12.4 Open Questions

Record open questions when unresolved information may affect correctness, scope, security, or release readiness.

### 12.5 Rejected Options

Do not revive rejected architecture, data, scope, or implementation options unless the user explicitly reopens them.

---

## 13. Human Approval Gate

The generated SKILL must end each task with this human approval gate.

```markdown
## Human Approval Required

### Task Completion to Approve
- TASK_ID:
- Task result artifact:
- Test evidence artifact:

### Scope Review
- Files changed:
- Scope deviations: None | List
- Forbidden changes avoided: Yes | No

### Validation Review
- Required tests passed: Yes | No | Partial
- Required tests not run:
- Manual verification required:

### Decisions to Approve
- ...

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Risks to Review
- ...

### Recommended Reviewer Action
- Approve task completion | Request changes | Block task | Reopen prior stage decision
```

The generated SKILL must not treat task completion as approved until the human reviewer explicitly approves it.

---

## 14. Context Packet Update Rules

The generated SKILL must update `/workflow/context/context_packet.md` for the next implementation task or Stage 12.

Include only minimal operational context:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 11_tdd_implementation_loop
- Completed implementation tasks:
- Current task status:
- Next recommended task or stage:

## 2. Approved Decisions
- Only human-approved decisions.

## 3. Working Assumptions
- Assumptions used during implementation that remain relevant.

## 4. Open Questions
- Questions that may affect later implementation, review, release, security, or operations.

## 5. Rejected / Superseded Options
- Options rejected or superseded during implementation.

## 6. Constraints That Must Not Be Violated
- Approved scope constraints:
- Architecture constraints:
- Data constraints:
- Security/privacy constraints:
- Testing constraints:

## 7. Key Context for Next Task or Stage
- Minimal notes needed by the next Agent.

## 8. Required Inputs for Next Task or Stage
- Next task card or Stage 12 review inputs.
- Task result artifacts.
- Test evidence artifacts.

## 9. Do Not Do
- Do not rely on unapproved implementation outputs as final decisions.
- Do not skip review of failed or skipped validation.
- Do not broaden implementation scope based on local code observations alone.
```

---

## 15. Validation Checklist for the Generated SKILL

Before considering the generated Stage 11 SKILL usable, verify:

```text
[ ] It operates on one approved task at a time.
[ ] It requires approved Stage 9 and Stage 10 inputs.
[ ] It requires code inspection before editing.
[ ] It requires writing or identifying a failing test before implementation when feasible.
[ ] It defines a fallback test-aware validation plan when strict TDD is not feasible.
[ ] It separates Red, Green, Refactor, and Regression evidence.
[ ] It records commands run and results.
[ ] It records skipped validation with reasons and risks.
[ ] It prevents unauthorized scope expansion.
[ ] It prevents unapproved architecture/API/data/security changes.
[ ] It updates task result and test evidence artifacts.
[ ] It updates traceability to implementation evidence.
[ ] It updates context_packet.md with minimal handoff context.
[ ] It keeps assumptions separate from decisions.
[ ] It includes a human approval gate.
[ ] It includes failure handling and blocker reporting.
```

---

## 16. Failure Handling

The generated SKILL must include a blocker report format.

Use it when implementation cannot safely proceed.

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
- ...

### Affected Task / Artifact / Code Area
- ...

### Evidence Collected Before Stopping
- ...

### Safe Partial Work Completed
- ...

### Human Decision Needed
- ...

### Recommended Next Step
- ...
```

### 16.1 Blocking Conditions

Stop and produce a blocker report if:

```text
- selected TASK_ID is missing or ambiguous;
- task card is not approved;
- implementation prompt is not approved;
- allowed change scope is missing;
- required test strategy is missing and cannot be safely inferred;
- codebase cannot be inspected;
- required dependency, API, schema, or security decision is missing;
- test failure is unrelated and blocks reliable validation;
- implementation requires unapproved architecture, API, data, security, privacy, or scope changes;
- validation repeatedly fails and the reason is unknown;
- current repository state suggests human changes may be overwritten;
- secrets or sensitive files would need to be exposed or modified.
```

### 16.2 Partial Completion Rules

If some work was completed before a blocker appeared, the Agent must record:

```text
- files inspected
- files changed, if any
- tests added, if any
- tests run
- current failing state
- rollback recommendation
- whether changes should be kept, reverted, or reviewed
```

---

## 17. Do Not Do

The generated SKILL must prohibit the Agent from doing the following:

```text
- Do not implement before identifying or writing a validating test unless strict TDD is not feasible and a validation plan is recorded first.
- Do not claim tests passed without command evidence.
- Do not hide skipped validation.
- Do not broaden scope beyond the approved task.
- Do not add unrelated features.
- Do not perform broad refactors unrelated to the task.
- Do not change API contracts without approval.
- Do not change database schema or migrations without approval.
- Do not change authentication, authorization, privacy, or security behavior without approval.
- Do not add new dependencies without approval.
- Do not overwrite human changes.
- Do not treat implementation output as an approved decision.
- Do not update DECISIONS.md unless explicit human approval exists.
- Do not use rejected or superseded artifacts as source of truth.
- Do not rely on context_packet.md as the only source of truth.
- Do not mark the task complete if required evidence is missing.
```

---

## 18. Specialization Hooks

The generated SKILL may include specialization hooks without hardcoding project-specific behavior.

### 18.1 Web SaaS

May add:

```text
- route/component integration checks
- browser smoke validation
- auth/session tests
- role-based authorization tests
- API contract tests
```

### 18.2 Internal Tool

May add:

```text
- operator workflow verification
- permission checks
- audit log behavior
- admin-only behavior validation
```

### 18.3 Mobile App

May add:

```text
- platform-specific test commands
- device permission validation
- offline/sync validation
- app navigation smoke checks
```

### 18.4 AI/Data Product

May add:

```text
- dataset fixture checks
- evaluation script evidence
- model output regression checks
- reproducibility notes
- human review sampling
```

### 18.5 Regulated / Security-Sensitive

May add:

```text
- security test evidence
- audit log verification
- privacy-sensitive data handling evidence
- access-control negative tests
- compliance review flags
```

### 18.6 Brownfield / Legacy

May add:

```text
- regression baseline comparison
- compatibility test evidence
- migration risk notes
- unchanged legacy behavior confirmation
```

Specialization hooks must not weaken approval, evidence, or traceability requirements.

---

## 19. Tool Wrapper Hooks

Tool-specific wrappers may add:

```text
- command invocation conventions
- sandbox permission rules
- file edit rules
- test runner invocation format
- diff display convention
- evidence capture convention
- review UI convention
```

Tool wrappers must not change:

```text
- approved input requirements
- TDD sequence
- scope control rules
- evidence requirements
- human approval gate
- decision/assumption/open-question handling
```

---

## 20. Optional Split Guidance for Large Stage 11 SKILLs

If the actual Stage 11 SKILL becomes too large for stable execution, split it using a Stage Facade Pattern while preserving one public Stage 11 contract.

Recommended split:

```text
/skills/11_tdd_implementation_loop/
  SKILL.md                         # parent entrypoint/orchestrator
  README.md
  artifact_contract.yml

  /11a_task_preflight_and_red_test/
    SKILL.md                       # validates task, inspects code, writes/identifies failing test

  /11b_minimal_implementation_green/
    SKILL.md                       # implements smallest change and passes targeted tests

  /11c_refactor_regression_evidence/
    SKILL.md                       # refactors, runs broader validation, records evidence

  /11d_implementation_finalizer/
    SKILL.md                       # consolidates result, updates traceability/context, prepares human review
```

Rules for splitting:

```text
- Keep official Stage 11 artifacts stable.
- Downstream Stage 12 must depend only on approved Stage 11 task result and evidence artifacts.
- Internal sub-skill outputs must not become downstream source of truth unless finalized.
- The finalizer must prepare the human approval gate.
```

---

## 21. Output Requirements for the LLM Creating the Actual SKILL

When this template is used to generate the actual reusable `SKILL.md`, return:

```text
1. Complete SKILL.md content.
2. Any recommended split plan, if the generated SKILL would be too large.
3. List of mandatory artifacts.
4. List of conditional artifacts.
5. Input contract summary.
6. Validation checklist.
7. Human approval gate summary.
8. Notes on assumptions made while creating the SKILL.
```

Do not execute Stage 11 while generating the SKILL.
Do not create project artifacts under `/workflow` while generating the SKILL.
Do not invent project-specific code, tests, requirements, architecture, or data design.
```