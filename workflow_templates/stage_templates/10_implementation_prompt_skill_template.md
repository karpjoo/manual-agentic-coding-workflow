---
name: 10_implementation_prompt_writing_skill_template
description: Template for creating a reusable SKILL.md that converts approved task cards into bounded, test-aware implementation prompts for coding agents.
stage: 10 Implementation Prompt Writing
template_type: stage_specific_skill_template
version: 1.0.0
status: draft
primary_output: /workflow/10_prompts/10_implementation_prompts.md
requires_human_approval: true
---

# 10 Implementation Prompt Writing SKILL Template

> Use this template to create a reusable `SKILL.md` for Stage 10 of the Manual Agentic Coding Workflow.  
> This is a **template for a reusable stage SKILL**, not a project execution artifact and not an implementation prompt itself.

---

## 0. Template Use Instructions

When creating the actual `SKILL.md` from this template:

1. Preserve all core workflow rules unless the user explicitly changes the workflow design.
2. Replace template placeholders such as `[[...]]` with reusable stage-level wording, not project-specific facts.
3. Do not create project-specific requirements, architecture, database schema, UI, tests, tasks, or code.
4. Do not execute Stage 10 while writing the SKILL.
5. Keep project-specific details in approved `/workflow` artifacts, `context_packet.md`, `artifact_manifest.yml`, and `USER_DIRECTIVES.md`.
6. Treat this Stage 10 skill as the bridge between approved task planning and Stage 11 TDD implementation.

---

## 1. Purpose

Create a reusable SKILL that converts approved Stage 9 task cards into execution-ready implementation prompts for coding agents.

The Stage 10 SKILL must produce prompts that are:

- task-scoped;
- test-aware or test-first;
- traceable to approved requirements, acceptance criteria, task cards, architecture, data design, and validation strategy;
- explicit about allowed changes and forbidden changes;
- clear about files to inspect before editing;
- clear about tests and commands to run;
- clear about evidence to report after implementation;
- safe to hand off to a fresh coding-agent session.

This stage does **not** implement code. It prepares prompts for Stage 11.

---

## 2. Core Question

Can each approved task card be transformed into a bounded, test-aware, evidence-producing implementation prompt that a coding agent can execute safely without expanding scope or violating approved decisions?

---

## 3. When to Use

Use this SKILL when:

- Stage 9 task cards have been drafted and are ready to be transformed into coding-agent prompts.
- The user wants one prompt per task or per tightly related task group.
- Implementation should happen through a controlled Stage 11 TDD loop.
- The coding agent may start in a new context window and needs a self-contained handoff prompt.
- The project needs traceability from requirements to task, tests, implementation evidence, and result files.

---

## 4. When Not to Use

Do not use this SKILL when:

- Requirements, acceptance criteria, task cards, or validation strategy are missing and cannot be safely assumed.
- The user wants direct code implementation rather than implementation prompt writing.
- Task cards are too broad, unapproved, or not ordered.
- The implementation scope is still being negotiated.
- The system architecture or data model is not approved enough to constrain implementation.
- The requested output is a review, release checklist, or retrospective rather than implementation prompts.

If the user asks for direct implementation, use or create a Stage 11 implementation-loop SKILL instead.

---

## 5. Required Inputs

### 5.1 Always Read

The Stage 10 SKILL must always read or check these inputs when available:

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

### 5.2 Read If Applicable

Read these only when activated by project profile, task cards, context, manifest, or user directives:

```text
/workflow/00_intake/00_existing_context_review.md
- if this is a brownfield or existing-codebase project

/workflow/04_domain/04_ubiquitous_language.md
- if task wording or domain behavior depends on approved domain terminology

/workflow/04_domain/04_domain_model.md
- if task touches entities, value objects, aggregates, workflows, or business rules

/workflow/04_domain/04_business_rules_invariants.md
- if task touches domain invariants, lifecycle, permissions, or validation rules

/workflow/04_domain/04_domain_events.md
- if task touches event-driven behavior, async workflows, or notifications

/workflow/05_architecture/05_api_contracts.md
- if task adds, changes, or depends on APIs

/workflow/05_architecture/05_integration_contracts.md
- if task touches external services, webhooks, queues, LLM APIs, third-party APIs, or platform services

/workflow/05_architecture/05_architecture_decisions.md
- if the task may be affected by approved trade-offs or rejected architecture options

/workflow/06_data/06_conceptual_data_model.md
- if task touches persistent data concepts

/workflow/06_data/06_logical_schema.md
- if task touches database structure, document shape, relations, constraints, or data ownership

/workflow/06_data/06_physical_schema.md
- if task touches implementation-level schema details

/workflow/06_data/06_indexes.md
- if task touches query patterns, search, filtering, sorting, or performance-sensitive data access

/workflow/06_data/06_migration_plan.md
- if task requires migration, seed data, backfill, rollback, or compatibility work

/workflow/06_data/06_data_security_rules.md
- if task touches authorization, access rules, row/document security, or privacy-sensitive data

/workflow/08_test_strategy/08_acceptance_tests.md
- if acceptance-level tests are defined separately

/workflow/08_test_strategy/08_manual_test_plan.md
- if manual validation is required

/workflow/09_tasks/09_task_risk_notes.md
- if task-specific risks were separated from task cards

/workflow/10_prompts/USER_DIRECTIVES.md
- if stage-local user instructions exist
```

### 5.3 Do Not Read By Default

Do not read these by default:

```text
- full raw chat history
- full historical agent logs
- superseded artifacts
- rejected artifacts, except to avoid reviving rejected options
- unrelated draft artifacts from earlier stages
- internal sub-skill outputs that were not promoted to official approved artifacts
- source code files, unless Stage 9 or current directives require code-inspection-oriented prompt generation
- dependency lockfiles, generated files, build artifacts, or vendor directories, unless needed to write inspection instructions
```

### 5.4 Missing Input Handling

If a required input is missing:

1. Record it under `Missing Information`.
2. Explain why it matters for implementation prompt writing.
3. Mark it as `Blocking` or `Non-blocking`.
4. If non-blocking, proceed only with an explicit working assumption.
5. If the missing input affects scope, architecture, test strategy, data rules, security, privacy, or task order, stop and request human decision.
6. Do not silently create implementation prompts from incomplete or unapproved task cards.

---

## 6. USER_DIRECTIVES.md Handling

If `/workflow/10_prompts/USER_DIRECTIVES.md` exists, read it before writing or revising prompts.

Classify each directive as one of:

```text
- explicit approval
- correction
- preference
- rejection
- scope change
- implementation constraint
- tool-specific instruction
- prompt formatting instruction
- additional source input
- question
```

Rules:

- Apply user directives before agent assumptions.
- Do not treat every directive as a globally approved decision.
- If a directive conflicts with approved decisions, report the conflict.
- If a directive changes task scope, record it as a decision candidate unless explicit approval is present.
- Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

---

## 7. Input Preflight Procedure

Before producing outputs, the Stage 10 SKILL must perform this preflight:

```text
[ ] Read this SKILL.md.
[ ] Read artifact_manifest.yml if available.
[ ] Confirm Stage 9 task cards exist.
[ ] Confirm task cards are approved or clearly marked for prompt-drafting only.
[ ] Confirm dependency order exists or infer only as a clearly marked draft.
[ ] Confirm validation commands exist or record missing commands as a blocker or gap.
[ ] Confirm each task card has acceptance criteria or a traceable validation method.
[ ] Confirm required source artifacts are approved or clearly marked as draft.
[ ] Check context_packet.md for required inputs for Stage 10.
[ ] Check DECISIONS.md and APPROVAL_LOG.md for approved implementation constraints.
[ ] Check REJECTED_OPTIONS.md to avoid reviving rejected approaches.
[ ] Check USER_DIRECTIVES.md if present.
[ ] Identify task cards that are too large, ambiguous, blocked, or unsafe to convert into prompts.
[ ] Restate the Stage 10 task in one short section.
```

If preflight reveals blocking issues, produce a blocker report and safe partial output instead of pretending the prompts are ready.

---

## 8. Execution Procedure

The Stage 10 SKILL must follow this procedure.

### Step 1. Confirm Stage Purpose

Restate that the current task is to write implementation prompts, not to implement code.

### Step 2. Build the Task-to-Prompt Plan

For each approved task card:

1. Identify `Task ID`, title, task type, dependency position, and priority.
2. Identify linked requirements, acceptance criteria, tests, architecture components, data artifacts, and security/privacy notes.
3. Decide whether the task should become:
   - one implementation prompt;
   - multiple smaller prompts;
   - a prompt group with strict substeps;
   - a blocker requiring task refinement.
4. Preserve the approved dependency order unless a conflict is discovered.

### Step 3. Validate Task Readiness

For each task card, check:

```text
- Is the task small enough for one coding-agent session?
- Is the allowed change scope explicit?
- Are forbidden changes explicit?
- Are likely files or modules identified?
- Are required tests defined?
- Are commands to run identified?
- Is expected evidence defined?
- Are rollback or recovery notes included when relevant?
- Are security/privacy notes included when relevant?
- Are open questions blocking?
```

If a task is too large or ambiguous, create a prompt-readiness issue instead of silently writing a weak prompt.

### Step 4. Write Implementation Prompts

Each implementation prompt must include:

```text
1. Prompt ID
2. Linked Task ID
3. Goal
4. Context
5. Approved Inputs
6. Files to Inspect First
7. Allowed Change Scope
8. Forbidden Changes
9. Required Implementation Steps
10. Required Tests
11. Commands to Run
12. Expected Evidence
13. Output Files to Update
14. Context Packet Update Instructions
15. Stop Conditions
16. Completion Report Format
```

A prompt must never merely say “build this feature.” It must define what to change, what not to change, how to verify the change, what tests to run, and what evidence to report.

### Step 5. Create Prompt Handoff Packets

For each implementation prompt or prompt group, create a handoff packet suitable for a fresh Stage 11 agent session.

Each packet must include:

```text
- prompt_id
- linked_task_id
- recommended execution order
- short task summary
- source artifacts to read
- files or directories to inspect first
- allowed change scope
- forbidden changes
- required tests
- validation commands
- expected evidence
- result artifact path
- test evidence artifact path
- context update instructions
- known assumptions
- open questions
- stop conditions
```

### Step 6. Update Traceability

Update or prepare traceability links:

```text
Requirement
→ Acceptance Criteria
→ Validation Method / Test Case
→ Task ID
→ Implementation Prompt ID
→ Expected Evidence
→ Stage 11 Result Artifact
```

Do not invent missing requirement IDs or test IDs without marking them as gaps or proposed IDs.

### Step 7. Prepare Human Approval Gate

List:

```text
- prompts ready for approval
- prompts needing refinement
- task cards that are too broad
- missing validation commands
- missing allowed or forbidden change scope
- unresolved security/privacy concerns
- assumptions that must be confirmed before Stage 11
```

### Step 8. Update Context for Stage 11

Update `context_packet.md` with only the minimal operational context needed to execute Stage 11:

```text
- approved implementation prompt set
- execution order
- required source artifacts for Stage 11
- coding-agent constraints
- testing and validation commands
- evidence expectations
- stop conditions
- do-not-do instructions
```

Do not copy all prompt contents into `context_packet.md`; link to the official Stage 10 artifacts.

---

## 9. Output Artifacts

### 9.1 Mandatory Artifacts

The Stage 10 SKILL must create or update:

```text
/workflow/10_prompts/10_implementation_prompts.md
- Official implementation prompts for Stage 11.

/workflow/10_prompts/10_prompt_handoff_packets.md
- Per-prompt or per-task handoff packets for fresh coding-agent sessions.

/workflow/10_prompts/result.md
- Stage 10 execution summary, readiness findings, approval gate, and next-step recommendation.

/workflow/context/context_packet.md
- Minimal handoff context for Stage 11.
```

### 9.2 Conditional Artifacts

Create or update these only if applicable:

```text
/workflow/10_prompts/10_prompt_readiness_issues.md
- if task cards are too broad, ambiguous, blocked, or unsafe to convert into implementation prompts.

/workflow/10_prompts/10_prompt_execution_order.md
- if implementation prompt order differs from or refines Stage 9 dependency order.

/workflow/10_prompts/10_prompt_traceability_matrix.md
- if Stage 10 needs its own prompt-level traceability view beyond the global matrix.

/workflow/10_prompts/10_tool_wrapper_notes.md
- if prompts need tool-specific variants for Claude Code, Codex, Antigravity, or another coding agent.

/workflow/10_prompts/10_security_privacy_prompt_notes.md
- if implementation prompts need special security, privacy, logging, audit, or data-handling constraints.

/workflow/10_prompts/10_migration_prompt_notes.md
- if implementation prompts include migration, backfill, seed data, rollback, or compatibility work.
```

### 9.3 N/A Record

For every skipped conditional artifact, record:

```text
Artifact:
Why not applicable:
Revisit if:
```

---

## 10. Required Structure: `10_implementation_prompts.md`

Use this structure unless the project explicitly requires a different format.

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

### PROMPT-[[NNN]] — [[Prompt Title]]

#### Linked Task
- Task ID:
- Task title:
- Dependency order:
- Prompt status: Draft / Needs Review / Approved / Blocked

#### 1. Goal
State the exact implementation goal in one short paragraph.

#### 2. Context
Summarize only the context required to execute this task safely.

#### 3. Approved Inputs
List approved source artifacts and specific sections the Stage 11 agent must rely on.

#### 4. Files to Inspect First
List files, directories, modules, contracts, schemas, tests, or configuration files to inspect before editing.

#### 5. Allowed Change Scope
Define exactly what may be changed.

#### 6. Forbidden Changes
Define what must not be changed.

#### 7. Required Implementation Steps
Give ordered, bounded implementation steps.

#### 8. Required Tests
Specify tests to add, update, or identify before implementation.

#### 9. Commands to Run
List relevant validation commands and expected pass/fail interpretation.

#### 10. Expected Evidence
Define what evidence the Stage 11 agent must report.

#### 11. Output Files to Update
Specify result and evidence artifacts, for example:
- `/workflow/11_implementation_results/11_task_result_[[TASK-ID]].md`
- `/workflow/11_implementation_results/11_test_evidence_[[TASK-ID]].md`
- `/workflow/context/context_packet.md`

#### 12. Context Packet Update Instructions
Tell the Stage 11 agent what minimal context to add after implementation.

#### 13. Stop Conditions
List conditions that require stopping instead of guessing or expanding scope.

#### 14. Completion Report Format
Specify the exact report format Stage 11 must produce.
```

---

## 11. Required Structure: `10_prompt_handoff_packets.md`

Use this structure unless the project explicitly requires another handoff format.

```markdown
# 10 Prompt Handoff Packets

## 1. Document Status
- Status: Draft / Needs Review / Approved
- Stage: 10 Implementation Prompt Writing
- Source Prompt Set:
- Last Updated:

## 2. How to Use These Packets
Explain that each packet is intended for a fresh Stage 11 coding-agent session.

## 3. Handoff Packets

### HANDOFF-[[NNN]] — [[Prompt ID / Task ID]]

#### Execution Metadata
- Prompt ID:
- Task ID:
- Recommended order:
- Depends on:
- Can run in parallel with:
- Must not run before:

#### Source of Truth
- Approved task card:
- Requirements:
- Acceptance criteria:
- Architecture:
- Data design:
- Test strategy:
- Validation commands:

#### Start-of-Session Instructions
Tell the Stage 11 agent exactly what to read and inspect first.

#### Implementation Boundaries
- Allowed:
- Forbidden:
- Must preserve:

#### Validation Requirements
- Test-first expectation:
- Required tests:
- Commands:
- Manual verification:
- Evidence required:

#### Result Artifacts
- Task result:
- Test evidence:
- Updated context packet:

#### Stop Conditions
- Stop if:
- Ask human if:
- Record blocker if:

#### Handoff Notes
- Assumptions:
- Open questions:
- Security/privacy notes:
- Rollback/recovery notes:
```

---

## 12. Required Structure: `result.md`

The Stage 10 `result.md` must include:

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

---

## 13. Prompt Quality Rules

Every generated implementation prompt must satisfy these rules:

```text
[ ] The prompt maps to one approved task card or a clearly justified prompt group.
[ ] The prompt identifies the linked requirement and acceptance criteria.
[ ] The prompt identifies required tests or validation methods.
[ ] The prompt states files or areas to inspect before editing.
[ ] The prompt states allowed change scope.
[ ] The prompt states forbidden changes.
[ ] The prompt includes stop conditions.
[ ] The prompt requires evidence, not just a completion claim.
[ ] The prompt tells Stage 11 where to write result and test evidence.
[ ] The prompt tells Stage 11 how to update context_packet.md.
[ ] The prompt does not introduce unapproved scope.
[ ] The prompt does not override approved architecture, data, security, or release decisions.
[ ] The prompt is usable from a fresh coding-agent session.
```

---

## 14. Traceability Rules

Stage 10 must preserve or improve traceability.

### 14.1 Required Links

Each implementation prompt should link:

```text
Prompt ID
→ Task ID
→ Requirement ID
→ Acceptance Criteria ID
→ Validation/Test ID
→ Architecture Component or Module
→ Data Artifact, if applicable
→ Security/Privacy Constraint, if applicable
→ Expected Evidence
→ Stage 11 Result Artifact Path
```

### 14.2 ID Conventions

Recommended IDs:

```text
Prompt ID: PROMPT-001, PROMPT-002
Handoff Packet ID: HANDOFF-001, HANDOFF-002
Prompt Readiness Issue ID: PRI-001, PRI-002
Evidence Placeholder: EVIDENCE-TASK-001
```

### 14.3 Traceability Gaps

If a prompt cannot be linked to a requirement, test, or task:

1. Do not invent a silent link.
2. Record a traceability gap.
3. Mark the prompt as `Needs Review` or `Blocked`.
4. Add the issue to `OPEN_QUESTIONS.md` if it affects implementation.

---

## 15. Decision / Assumption / Open Question Rules

### Approved Decisions

Only explicit human approval can create approved decisions.

Examples for this stage:

```text
Approved: PROMPT-001 through PROMPT-018 are approved for Stage 11 execution.
Approved: Stage 11 must run prompts sequentially in the listed dependency order.
Approved: No implementation prompt may change authentication behavior unless explicitly scoped.
```

### Decision Candidates

Use for recommendations requiring approval.

```text
Candidate: Split TASK-014 into PROMPT-014A and PROMPT-014B because it spans backend API and UI state management.
```

### Working Assumptions

Use when progress can continue safely but information is not confirmed.

```text
Assumption: The Stage 11 agent can use the validation commands listed in 08_validation_commands.md.
```

### Open Questions

Use when unresolved information may affect implementation.

```text
Open Question: Which test command should be used for E2E validation in CI?
```

### Rejected Options

Record explicitly rejected prompt strategies.

```text
Rejected: Do not create a single large implementation prompt for all MVP tasks.
```

Rules:

- Do not convert task-card text into approved implementation scope if the task card is draft.
- Do not convert suggested prompt splitting into approved execution order without human approval.
- Do not update `DECISIONS.md` unless explicit approval exists.
- Record assumptions and open questions in the appropriate context files.

---

## 16. Context Packet Update Rules

Update `/workflow/context/context_packet.md` for Stage 11.

Required sections:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 10 Implementation Prompt Writing
- Completed stages:
- Next recommended stage: 11 TDD Implementation Loop

## 2. Approved Decisions
- Include only human-approved implementation prompt decisions.

## 3. Working Assumptions
- Include assumptions that Stage 11 must know.

## 4. Open Questions
- Include unresolved implementation blockers or validation uncertainties.

## 5. Rejected / Superseded Options
- Include rejected prompt strategies or implementation approaches that Stage 11 must not revive.

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
- Summarize test/evidence expectations.

## 8. Required Inputs for Next Stage
- `/workflow/10_prompts/10_implementation_prompts.md`
- `/workflow/10_prompts/10_prompt_handoff_packets.md`
- relevant approved source artifacts named by each handoff packet

## 9. Do Not Do
- Do not implement prompts marked Draft, Needs Review, or Blocked unless explicitly instructed.
- Do not expand scope beyond each prompt.
- Do not skip required tests or evidence reporting.
```

---

## 17. Human Approval Gate

The Stage 10 SKILL must end with this section.

```markdown
## Human Approval Required

### Decisions to Approve
- Approve, reject, or revise the implementation prompt set.
- Approve prompt execution order.
- Approve any task splitting or prompt grouping.
- Approve allowed change scope and forbidden changes for each prompt.
- Approve security/privacy-sensitive implementation constraints.

### Assumptions to Confirm
- Confirm assumptions used to write prompts.
- Confirm validation commands that were inferred or incomplete.
- Confirm any tool-specific execution assumptions.

### Open Questions to Resolve
- Resolve blockers that prevent safe Stage 11 execution.
- Resolve missing test or evidence expectations.
- Resolve unclear task ownership, file scope, or module boundary issues.

### Risks to Review
- Prompt too broad for one agent session.
- Prompt could cause architecture drift.
- Prompt could cause data model drift.
- Prompt could weaken tests, security, or privacy controls.
- Prompt relies on unapproved or draft source artifacts.

### Artifacts Ready for Review
- `/workflow/10_prompts/10_implementation_prompts.md`
- `/workflow/10_prompts/10_prompt_handoff_packets.md`
- `/workflow/10_prompts/result.md`
- conditional artifacts created in this execution

### Recommended Next Step
- After approval, run Stage 11 TDD Implementation Loop using only approved prompts and handoff packets.
```

---

## 18. Validation Checklist

Before completing Stage 10, verify:

```text
[ ] All approved task cards were reviewed.
[ ] Every generated prompt has a Prompt ID.
[ ] Every prompt links to a Task ID.
[ ] Every prompt links to requirements and acceptance criteria when available.
[ ] Every prompt includes allowed change scope.
[ ] Every prompt includes forbidden changes.
[ ] Every prompt includes files to inspect first.
[ ] Every prompt includes required tests.
[ ] Every prompt includes commands to run or records a missing command gap.
[ ] Every prompt defines expected evidence.
[ ] Every prompt defines output files to update.
[ ] Every prompt includes context_packet.md update instructions.
[ ] Every prompt includes stop conditions.
[ ] Prompt execution order is clear.
[ ] Prompt readiness issues are recorded.
[ ] Security/privacy constraints are carried into relevant prompts.
[ ] Migration/rollback instructions are carried into relevant prompts.
[ ] Stage 11 handoff is clear enough for a fresh agent session.
[ ] Human approval gate is explicit.
```

---

## 19. Failure Handling

If the SKILL cannot safely complete, produce a blocker report.

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
- ...

### Affected Task Cards or Prompts
- ...

### Affected Artifacts or Stages
- ...

### Safe Partial Work Completed
- ...

### Human Decision Needed
- ...
```

Common blockers:

```text
- Stage 9 task cards are missing.
- Task cards are not approved.
- Task cards are too broad or ambiguous.
- Required tests or validation commands are missing.
- Approved architecture or data artifacts conflict with task cards.
- Security/privacy constraints are unresolved.
- Required source artifacts are superseded or rejected.
- Prompt execution order cannot be determined safely.
```

---

## 20. Do Not Do

The Stage 10 SKILL must not:

```text
- implement code
- edit production source files
- run tests and claim implementation evidence
- create one giant prompt for all tasks unless explicitly requested and marked as risky
- convert unapproved task cards into approved implementation scope
- omit forbidden changes
- omit required tests
- omit evidence expectations
- hide missing validation commands
- silently change task order
- revive rejected implementation approaches
- use context_packet.md as the only source of truth
- overwrite approved artifacts without approval
- update DECISIONS.md without explicit human approval
- treat tool-specific instructions as architecture decisions
- add project-specific implementation details while designing the reusable SKILL
```

---

## 21. Specialization Hooks

Project-type specialization addenda may add constraints but must not replace this Stage 10 procedure.

### web_saas

May add:

```text
- route-level prompt constraints
- API endpoint prompt constraints
- auth/session prompt constraints
- deployment preview validation
- browser/E2E validation instructions
```

### internal_tool

May add:

```text
- operator workflow constraints
- admin-only safety constraints
- audit and manual override notes
```

### mobile_app

May add:

```text
- platform-specific prompt variants
- device permission constraints
- offline/sync implementation boundaries
- app-store or build validation notes
```

### ai_data_product

May add:

```text
- dataset handling constraints
- model evaluation prompts
- reproducibility requirements
- data leakage checks
- human review requirements
```

### regulated_security_sensitive

May add:

```text
- compliance review prompts
- audit log constraints
- privacy-preserving implementation rules
- security test evidence requirements
- stronger stop conditions
```

### brownfield_legacy

May add:

```text
- regression baseline checks
- compatibility constraints
- no-touch legacy areas
- migration-safe prompt structure
- incremental refactor boundaries
```

---

## 22. Tool Wrapper Hooks

Tool-specific wrappers may define:

```text
- where SKILL files are stored
- how prompts are copied into the coding agent
- how artifacts are saved
- command invocation conventions
- sandbox or permission rules
- review workflow
- output capture conventions
```

Tool wrappers must not change:

```text
- approved source-of-truth rules
- human approval rules
- traceability rules
- task scope
- architecture decisions
- data decisions
- security/privacy constraints
- required evidence expectations
```

---

## 23. Template Quality Checklist

Before accepting a Stage 10 SKILL created from this template, confirm:

```text
[ ] It follows the core SKILL structure.
[ ] It is reusable across projects.
[ ] It does not execute Stage 10 while defining the SKILL.
[ ] It defines Always Read / Read If Applicable / Do Not Read By Default inputs.
[ ] It defines missing input handling.
[ ] It defines mandatory and conditional artifacts.
[ ] It defines implementation prompt structure.
[ ] It defines handoff packet structure.
[ ] It defines traceability from Task ID to Prompt ID to expected evidence.
[ ] It includes human approval gate.
[ ] It defines Stage 11 context handoff.
[ ] It includes prompt quality checklist.
[ ] It includes failure handling.
[ ] It includes do-not-do rules.
[ ] It leaves project-specific details to artifacts and directives.
[ ] It leaves tool-specific behavior to wrappers.
```

---

## 24. Recommended Folder Placement

Recommended reusable template path:

```text
/workflow_templates/stages/10_implementation_prompt_skill_template.md
```

Recommended reusable SKILL path created from this template:

```text
/skills/10_implementation_prompt_writing/SKILL.md
```

Recommended project artifact folder when the SKILL is executed:

```text
/workflow/10_prompts/
```

---

## 25. Downstream Handoff Rule

Downstream Stage 11 must depend only on approved official Stage 10 artifacts:

```text
/workflow/10_prompts/10_implementation_prompts.md
/workflow/10_prompts/10_prompt_handoff_packets.md
/workflow/10_prompts/result.md
/workflow/context/context_packet.md
```

Stage 11 must not depend on:

```text
- prompt-writing chat history
- draft prompts not approved for execution
- internal notes not promoted to official artifacts
- superseded prompt versions
- implementation assumptions not recorded in context files
```
