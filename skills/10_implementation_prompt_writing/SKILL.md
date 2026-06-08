---
name: 10_implementation_prompt_writing
description: Convert approved Stage 9 task cards into bounded, test-aware, evidence-producing implementation prompts and handoff packets for Stage 11 coding agents.
stage: 10 Implementation Prompt Writing
version: 1.0.0
status: draft
primary_output: /workflow/10_prompts/10_implementation_prompts.md
requires_human_approval: true
previous_stage: 09_task_breakdown
next_stage: 11_tdd_implementation_loop
---

# 10 Implementation Prompt Writing

## 1. Purpose

Use this SKILL to convert approved Stage 9 task cards into implementation prompts that a coding agent can execute safely in Stage 11.

This SKILL does **not** implement code. It creates bounded, test-aware, evidence-oriented prompts and handoff packets.

Every implementation prompt must make explicit:

```text
what to change / what not to change / what to inspect first / which source artifacts to trust / which tests to run / which commands to run / what evidence to report / when to stop
```

## 2. Operating Mode

The agent is a structured development assistant, not an autonomous developer.

Keep these distinctions:

```text
Agent proposal != approved decision
Agent inference != verified fact
Agent assumption != requirement
Agent draft != final artifact
Implementation prompt != implementation
```

Only explicit human approval can make prompts ready for Stage 11 execution.

## 3. Core Question

Can each approved task card become a scoped, test-aware, evidence-producing implementation prompt that a coding agent can execute without expanding scope or violating approved decisions?

## 4. When to Use / Not Use

Use this SKILL when Stage 9 task cards exist, the project is preparing for Stage 11, prompts must be executable from a fresh coding-agent session, and traceability from requirement to task to prompt to evidence must be preserved.

Do not use this SKILL for direct implementation, review, release, deployment, retrospective, or when task cards, validation strategy, architecture, data, security, or privacy constraints are too unresolved to constrain implementation prompts.

## 5. Input Precedence

When sources conflict, apply this order:

```text
1. Current explicit user instruction
2. /workflow/10_prompts/USER_DIRECTIVES.md
3. /workflow/context/APPROVAL_LOG.md and /workflow/context/DECISIONS.md
4. /workflow/context/artifact_manifest.yml
5. /workflow/context/context_packet.md
6. Approved stage artifacts
7. Working assumptions
8. Agent inference
```

Report conflicts explicitly. Stop if a conflict affects scope, architecture, data, security, privacy, tests, or execution order.

## 6. Required Inputs

### Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/09_tasks/09_task_inventory.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_dependency_order.md
/workflow/09_tasks/09_traceability_matrix.md
```

### Read If Applicable

```text
/workflow/00_intake/00_existing_context_review.md — brownfield or existing-codebase project
/workflow/04_domain/04_ubiquitous_language.md — domain terms affect prompt wording
/workflow/04_domain/04_domain_model.md — tasks touch entities, value objects, aggregates, or workflows
/workflow/04_domain/04_business_rules_invariants.md — tasks touch invariants, validation, lifecycle, or state transitions
/workflow/04_domain/04_domain_events.md — tasks touch events, async workflows, or notifications
/workflow/05_architecture/05_api_contracts.md — tasks touch APIs
/workflow/05_architecture/05_integration_contracts.md — tasks touch external services, queues, webhooks, or third-party APIs
/workflow/05_architecture/05_architecture_decisions.md — prompts must preserve approved trade-offs
/workflow/06_data/06_conceptual_data_model.md — tasks touch persistent data concepts
/workflow/06_data/06_logical_schema.md — tasks touch data shape, relations, constraints, or ownership
/workflow/06_data/06_physical_schema.md — tasks touch implementation-level schema
/workflow/06_data/06_indexes.md — tasks touch query patterns, filtering, sorting, or performance
/workflow/06_data/06_migration_plan.md — tasks require migration, seed, backfill, rollback, or compatibility work
/workflow/06_data/06_data_security_rules.md — tasks touch authorization, access control, or privacy-sensitive data
/workflow/08_test_strategy/08_acceptance_tests.md — acceptance tests are defined separately
/workflow/08_test_strategy/08_manual_test_plan.md — manual validation is required
/workflow/09_tasks/09_task_risk_notes.md — task-specific risk notes exist
/workflow/10_prompts/USER_DIRECTIVES.md — stage-local human instructions exist
```

### Do Not Read By Default

```text
raw chat history; full agent logs; unrelated drafts; superseded artifacts except to avoid reuse; rejected artifacts except to avoid revival; unpromoted internal sub-skill outputs; source code files unless needed to write inspection instructions; generated files, lockfiles, build artifacts, vendor directories unless explicitly relevant
```

### Missing Input Handling

If an input is missing, record it, explain why it matters, mark it `Blocking` or `Non-blocking`, and continue only with explicit working assumptions. Stop if the gap affects scope, architecture, data, security, privacy, validation, or task order.

## 7. USER_DIRECTIVES.md Handling

If `/workflow/10_prompts/USER_DIRECTIVES.md` exists, read it before execution and classify each directive as approval, correction, preference, rejection, scope change, implementation constraint, tool-specific instruction, formatting instruction, added input, or question.

Do not treat every directive as a global decision. Report conflicts with approved decisions. Treat scope-changing directives as decision candidates unless explicit approval exists.

## 8. Preflight Procedure

Before writing artifacts, verify:

```text
[ ] SKILL.md was read.
[ ] artifact_manifest.yml, context_packet.md, DECISIONS.md, APPROVAL_LOG.md, and USER_DIRECTIVES.md were checked when available.
[ ] Stage 9 task cards exist.
[ ] Task cards are approved or explicitly allowed for draft prompt writing.
[ ] Dependency order exists or the gap is recorded.
[ ] Validation commands exist or missing commands are recorded.
[ ] Each task has acceptance criteria or a validation method.
[ ] Source artifacts are approved or clearly marked as draft.
[ ] Superseded and rejected artifacts were not used as current truth.
[ ] Too-large, ambiguous, blocked, or unsafe task cards were identified.
```

If preflight reveals a blocker, produce a blocker report and safe partial output.

## 9. Execution Procedure

### Step 1. Confirm Scope

State that the work is Stage 10 prompt writing, not Stage 11 code implementation.

### Step 2. Build Task-to-Prompt Plan

For each task card, identify task ID, title, dependency position, priority, linked requirements, acceptance criteria, domain concepts, architecture modules, APIs, data artifacts, tests, and security/privacy notes.

Decide whether the task becomes one prompt, multiple prompts, a prompt group, or a prompt-readiness issue. Preserve approved dependency order unless a conflict exists. Mark proposed splitting or grouping as a decision candidate unless already approved.

### Step 3. Validate Prompt Readiness

Each task must have clear size, allowed change scope, forbidden changes, files/modules to inspect first, required tests, validation commands or a recorded gap, expected evidence, relevant rollback/recovery notes, security/privacy constraints, and no blocking open questions.

If a task is not ready, do not write a weak prompt. Record the issue and mark the prompt `Needs Review` or `Blocked`.

### Step 4. Write Implementation Prompts

Each prompt must include these sections:

```text
Prompt ID
Linked Task ID
Goal
Context
Approved Inputs
Files to Inspect First
Allowed Change Scope
Forbidden Changes
Required Implementation Steps
Required Tests
Commands to Run
Expected Evidence
Output Files to Update
Context Packet Update Instructions
Stop Conditions
Completion Report Format
```

### Step 5. Create Handoff Packets

For each prompt, create a handoff packet for a fresh Stage 11 agent session. Include execution order, dependencies, parallelization limits, source artifacts, inspection targets, boundaries, tests, commands, evidence, result paths, context update instructions, assumptions, questions, security/privacy notes, rollback/recovery notes, and stop conditions.

### Step 6. Update Traceability

Create or update this chain:

```text
Requirement -> Acceptance Criteria -> Validation/Test -> Task ID -> Prompt ID -> Expected Evidence -> Stage 11 Result Artifact
```

Record traceability gaps instead of inventing links.

### Step 7. Update Context Files

Update or prepare `/workflow/context/context_packet.md`, `ASSUMPTIONS.md`, `OPEN_QUESTIONS.md`, `REJECTED_OPTIONS.md`, and `TRACEABILITY_MATRIX.md` as needed. Do not update `DECISIONS.md` without explicit human approval.

### Step 8. Prepare Approval Gate

List prompts ready for review, blocked prompts, proposed splitting/grouping, assumptions, open questions, risks, and required approval items.

## 10. Output Artifacts

### Mandatory Artifacts

```text
/workflow/10_prompts/10_implementation_prompts.md — official Stage 10 implementation prompt set
/workflow/10_prompts/10_prompt_handoff_packets.md — per-prompt Stage 11 handoff packets
/workflow/10_prompts/result.md — Stage 10 summary, readiness findings, traceability updates, approval gate
/workflow/context/context_packet.md — minimal Stage 11 handoff context
```

### Conditional Artifacts

```text
/workflow/10_prompts/10_prompt_readiness_issues.md — if tasks are broad, ambiguous, blocked, unsafe, or under-specified
/workflow/10_prompts/10_prompt_execution_order.md — if prompt order refines or differs from Stage 9 dependency order
/workflow/10_prompts/10_prompt_traceability_matrix.md — if prompt-level traceability is needed beyond the global matrix
/workflow/10_prompts/10_tool_wrapper_notes.md — if tool-specific variants or execution notes are needed
/workflow/10_prompts/10_security_privacy_prompt_notes.md — if special security, privacy, logging, audit, or data-handling constraints are needed
/workflow/10_prompts/10_migration_prompt_notes.md — if migration, seed, backfill, rollback, or compatibility work is involved
```

For skipped conditional artifacts, record: `Artifact`, `Why not applicable`, and `Revisit if`.

## 11. Required Output Structures

### 10_implementation_prompts.md

```markdown
# 10 Implementation Prompts

## 1. Document Status
- Status: Draft / Needs Review / Approved
- Stage: 10 Implementation Prompt Writing
- Source Task Set:
- Prepared By:
- Last Updated:

## 2. Prompt Set Summary
- Total task cards reviewed:
- Prompts created:
- Prompts blocked:
- Prompt groups:
- Execution order source:
- Major constraints:

## 3. Prompt Execution Order
| Order | Prompt ID | Task ID | Title | Depends On | Status |
|---|---|---|---|---|---|

## 4. Implementation Prompts
### PROMPT-001 — [[Title]]
#### Linked Task
#### 1. Goal
#### 2. Context
#### 3. Approved Inputs
#### 4. Files to Inspect First
#### 5. Allowed Change Scope
#### 6. Forbidden Changes
#### 7. Required Implementation Steps
#### 8. Required Tests
#### 9. Commands to Run
#### 10. Expected Evidence
#### 11. Output Files to Update
#### 12. Context Packet Update Instructions
#### 13. Stop Conditions
#### 14. Completion Report Format
```

### 10_prompt_handoff_packets.md

```markdown
# 10 Prompt Handoff Packets

## 1. Document Status
- Status: Draft / Needs Review / Approved
- Stage: 10 Implementation Prompt Writing
- Source Prompt Set:
- Last Updated:

## 2. How to Use These Packets
Each packet is intended for a fresh Stage 11 coding-agent session.

## 3. Handoff Packets
### HANDOFF-001 — [[Prompt ID / Task ID]]
#### Execution Metadata
#### Source of Truth
#### Start-of-Session Instructions
#### Implementation Boundaries
#### Validation Requirements
#### Result Artifacts
#### Stop Conditions
#### Handoff Notes
```

### result.md

```markdown
# Result: 10 Implementation Prompt Writing

## 1. Task Summary
## 2. Inputs Used
## 3. Outputs Created or Updated
## 4. Prompt Set Summary
## 5. Prompt Readiness Findings
## 6. Decision Candidates
## 7. Working Assumptions
## 8. Open Questions
## 9. Risks and Constraints
## 10. Rejected or Superseded Options
## 11. Traceability Updates
## 12. Human Approval Required
## 13. Recommended Next Step
```

## 12. Prompt Quality Checklist

Every prompt must satisfy:

```text
[ ] Maps to one approved task card or justified prompt group.
[ ] Links to requirements and acceptance criteria when available.
[ ] Identifies required tests or validation method.
[ ] Lists files or areas to inspect before editing.
[ ] States allowed change scope.
[ ] States forbidden changes.
[ ] Includes stop conditions.
[ ] Requires evidence, not only a completion claim.
[ ] Defines Stage 11 result and test evidence paths.
[ ] Defines context_packet.md update instructions.
[ ] Does not introduce unapproved scope.
[ ] Does not override approved architecture, data, security, or release decisions.
[ ] Can be used from a fresh coding-agent session.
```

## 13. Traceability Rules

Each prompt should link:

```text
Prompt ID -> Task ID -> Requirement ID -> Acceptance Criteria ID -> Validation/Test ID -> Architecture Component or Module -> Data Artifact if applicable -> Security/Privacy Constraint if applicable -> Expected Evidence -> Stage 11 Result Artifact Path
```

Use stable IDs: `PROMPT-001`, `HANDOFF-001`, `PRI-001`, `EVIDENCE-TASK-001`. If a link cannot be made, record a traceability gap and mark the prompt `Needs Review` or `Blocked`.

## 14. Classification Rules

Use these categories:

```text
Approved Decision: explicit human approval only.
Decision Candidate: agent recommendation awaiting approval.
Working Assumption: temporary belief needed for progress.
Open Question: unresolved issue that may affect implementation.
Rejected Option: explicitly rejected or superseded prompt strategy or implementation approach.
```

Do not convert draft task cards into approved implementation scope. Do not convert suggested prompt splitting into approved execution order. Do not update `DECISIONS.md` without explicit approval.

## 15. Context Packet Update Rules

Update `/workflow/context/context_packet.md` for Stage 11 with:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 10 Implementation Prompt Writing
- Completed stages:
- Next recommended stage: 11 TDD Implementation Loop

## 2. Approved Decisions
- Only human-approved implementation prompt decisions.

## 3. Working Assumptions
- Assumptions Stage 11 must know.

## 4. Open Questions
- Implementation blockers or validation uncertainties.

## 5. Rejected / Superseded Options
- Rejected prompt strategies or implementation approaches.

## 6. Constraints That Must Not Be Violated
- Scope:
- Architecture:
- Data:
- Security:
- Privacy:
- Testing:
- Tooling:

## 7. Key Context for Next Stage
- Link to approved prompt set.
- Link to handoff packets.
- Summarize execution order.
- Summarize test and evidence expectations.

## 8. Required Inputs for Next Stage
- /workflow/10_prompts/10_implementation_prompts.md
- /workflow/10_prompts/10_prompt_handoff_packets.md
- relevant approved source artifacts named by each handoff packet

## 9. Do Not Do
- Do not implement prompts marked Draft, Needs Review, or Blocked unless explicitly instructed.
- Do not expand scope beyond each prompt.
- Do not skip required tests or evidence reporting.
```

Keep `context_packet.md` concise and link to artifacts instead of copying full prompt text.

## 16. Human Approval Gate

End with:

```markdown
## Human Approval Required

### Decisions to Approve
- Approve, reject, or revise the implementation prompt set.
- Approve prompt execution order.
- Approve task splitting or prompt grouping.
- Approve allowed change scope and forbidden changes for each prompt.
- Approve security/privacy-sensitive implementation constraints.

### Assumptions to Confirm
- Confirm assumptions used to write prompts.
- Confirm inferred or incomplete validation commands.
- Confirm tool-specific execution assumptions.

### Open Questions to Resolve
- Resolve blockers that prevent safe Stage 11 execution.
- Resolve missing test or evidence expectations.
- Resolve unclear file scope, task ownership, or module boundaries.

### Risks to Review
- Prompt too broad for one agent session.
- Prompt could cause architecture, data, test, security, or privacy drift.
- Prompt relies on unapproved or draft source artifacts.

### Artifacts Ready for Review
- /workflow/10_prompts/10_implementation_prompts.md
- /workflow/10_prompts/10_prompt_handoff_packets.md
- /workflow/10_prompts/result.md
- conditional artifacts created in this execution

### Recommended Next Step
- After approval, run Stage 11 TDD Implementation Loop using only approved prompts and handoff packets.
```

## 17. Validation Checklist

Before completion, verify:

```text
[ ] All approved task cards were reviewed.
[ ] Every prompt has a Prompt ID and Task ID.
[ ] Every prompt includes allowed and forbidden change scope.
[ ] Every prompt includes files to inspect first.
[ ] Every prompt includes tests, commands, evidence, output files, context update instructions, and stop conditions.
[ ] Prompt order is clear.
[ ] Prompt readiness issues are recorded.
[ ] Security/privacy and migration/rollback constraints are carried into relevant prompts.
[ ] Stage 11 handoff is usable from a fresh session.
[ ] Human approval gate is explicit.
```

## 18. Failure Handling

If this SKILL cannot safely complete, produce:

```markdown
## Blocker Report

### Blocking Issue
### Why It Matters
### Affected Task Cards or Prompts
### Affected Artifacts or Stages
### Safe Partial Work Completed
### Human Decision Needed
```

Common blockers: missing or unapproved task cards, overly broad tasks, missing tests or validation commands, architecture/data conflicts, unresolved security/privacy constraints, superseded or rejected source artifacts, or unclear execution order.

## 19. Do Not Do

Do not implement code, edit production files, run tests and claim evidence, create one giant prompt unless explicitly requested and marked risky, approve prompts yourself, omit forbidden changes/tests/evidence, hide missing validation commands, silently change task order, revive rejected approaches, use `context_packet.md` as the only source of truth, overwrite approved artifacts, or update `DECISIONS.md` without explicit approval.

## 20. Specialization and Tool Hooks

Specialization addenda may add constraints but must not replace this SKILL.

```text
web_saas: route/API/auth/session/browser validation constraints
internal_tool: operator workflow, admin safety, audit/manual override notes
mobile_app: platform variants, permissions, offline/sync, app build validation
ai_data_product: dataset handling, model evaluation, reproducibility, leakage checks
regulated_security_sensitive: compliance, audit log, privacy, security evidence, stronger stop conditions
brownfield_legacy: regression baseline, compatibility, no-touch areas, migration-safe boundaries
```

Tool wrappers may define invocation conventions, save locations, sandbox rules, command conventions, review workflow, and output capture. They must not change source-of-truth rules, approval rules, traceability, scope, architecture, data, security/privacy, or evidence expectations.

## 21. Split Policy

This SKILL is intentionally a single compact stage-level SKILL. Do not split it unless prompt readiness analysis, prompt authoring, tool-specific variants, or final consolidation become large enough to require separate sessions.

If splitting becomes necessary:

```text
Split internally.
Expose one public Stage 10 package.
Preserve official Stage 10 artifacts.
Require finalizer consolidation.
Make Stage 11 depend only on approved official Stage 10 artifacts.
```

## 22. Downstream Handoff Rule

Stage 11 may depend only on approved official Stage 10 artifacts:

```text
/workflow/10_prompts/10_implementation_prompts.md
/workflow/10_prompts/10_prompt_handoff_packets.md
/workflow/10_prompts/result.md
/workflow/context/context_packet.md
```

Stage 11 must not depend on prompt-writing chat history, unapproved draft prompts, internal notes not promoted to official artifacts, superseded prompt versions, or assumptions not recorded in context files.
