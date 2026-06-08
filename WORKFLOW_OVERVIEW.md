# Workflow Overview

This document provides a stage-by-stage overview of the Manual Agentic Coding Workflow.

For the design philosophy, see [`CONCEPT.md`](./CONCEPT.md). For the shortest hands-on path, see [`QUICKSTART.md`](./QUICKSTART.md).

## 1. What this workflow does

The Manual Agentic Coding Workflow organizes software development with coding agents into explicit stages.

Each stage:

- has a clear purpose;
- reads approved inputs from previous stages;
- produces concrete artifacts;
- separates decisions, assumptions, open questions, risks, and recommendations;
- updates context for the next stage;
- ends with a human approval gate.

The workflow is designed for experienced developers who want to use agents such as Claude Code, Codex, Antigravity, or similar tools in a controlled and inspectable process.

## 2. High-level flow

```text
Idea
→ Goal
→ Stakeholders and risks
→ Requirements and acceptance criteria
→ Domain model
→ Architecture and contracts
→ Data design
→ MVP and release slicing
→ Test strategy
→ Task breakdown
→ Implementation prompts
→ TDD implementation loop
→ Review, release, and handoff
→ Workflow retrospective and skill improvement
```

Mermaid diagram:

```mermaid
flowchart LR
  S00[00 Intake] --> S01[01 Goal]
  S01 --> S02[02 Stakeholders & Risk]
  S02 --> S03[03 Requirements]
  S03 --> S04[04 Domain Modeling]
  S04 --> S05[05 Architecture]
  S05 --> S06[06 Data Design]
  S06 --> S07[07 MVP Slicing]
  S07 --> S08[08 Test Strategy]
  S08 --> S09[09 Task Breakdown]
  S09 --> S10[10 Implementation Prompts]
  S10 --> S11[11 TDD Loop]
  S11 --> S12[12 Review & Release]
  S12 --> S13[13 Retrospective]
```

## 3. Stage summary table

| Stage | Name | Main purpose | Typical official outputs | Human approval focus |
|---:|---|---|---|---|
| 00 | Project Intake / Existing Context Review | Understand project type, existing context, constraints, and starting materials. | `00_project_intake.md`, `00_existing_context_review.md`, `context_packet.md` | Project type, fixed constraints, existing materials, forbidden changes |
| 01 | Service Goal Definition | Define why the service should exist before deciding what to build. | `01_service_goal.md`, `result.md` | Service goal, primary users, success criteria, non-goals |
| 02 | Stakeholder & Risk Framing | Identify users, roles, external systems, security, privacy, and operational risks early. | `02_stakeholders.md`, `02_risk_privacy_screening.md` | Roles, permissions, personal data direction, external transfer policy |
| 03 | Requirements & Acceptance Criteria | Convert goals into testable requirements, scenarios, edge cases, and acceptance criteria. | `03_requirements.md`, `03_acceptance_criteria.md`, `03_traceability_matrix.md` | Must-have requirements, testability, non-scope items |
| 04 | Domain Modeling / DDD | Model domain language, concepts, rules, aggregates, events, and bounded contexts. | `04_ubiquitous_language.md`, `04_domain_model.md`, `04_business_rules_invariants.md`, `04_bounded_contexts.md`, `04_domain_events.md` | Domain terms, aggregate boundaries, invariants, bounded contexts |
| 05 | Architecture & Technical Contracts | Translate requirements and domain model into architecture, module boundaries, APIs, integrations, and authorization. | `05_architecture_plan.md`, `05_module_boundaries.md`, `05_api_contracts.md`, `05_integration_contracts.md`, `05_architecture_decisions.md` | Architecture direction, API contracts, auth model, integration approach |
| 06 | Data Design | Design conceptual, logical, and physical data structures after domain and architecture are clear. | `06_conceptual_data_model.md`, `06_logical_schema.md`, `06_physical_schema.md`, `06_indexes.md`, `06_migration_plan.md`, `06_data_security_rules.md` | Schema, data ownership, security rules, migration strategy |
| 07 | MVP Scope & Release Slicing | Decide what belongs in MVP, later releases, and explicit non-scope. | `07_mvp_scope.md`, `07_release_slices.md`, `07_out_of_scope.md` | MVP scope, out-of-scope items, release order |
| 08 | Test Strategy & Validation Harness | Define validation structure before implementation begins. | `08_test_strategy.md`, `08_acceptance_tests.md`, `08_validation_commands.md`, `08_manual_test_plan.md` | Test strategy, validation commands, manual verification criteria |
| 09 | Task Breakdown | Convert approved design into small agent-executable development tasks. | `09_task_inventory.md`, `09_task_cards.md`, `09_dependency_order.md`, `09_traceability_matrix.md` | Task size, task order, definition of done |
| 10 | Implementation Prompt Writing | Convert task cards into executable coding-agent prompts. | `10_implementation_prompts.md`, `10_prompt_handoff_packets.md` | Allowed scope, forbidden changes, execution order, required evidence |
| 11 | TDD Implementation Loop | Implement task by task using test-first or test-aware development. | `11_task_result_<task_id>.md`, `11_test_evidence_<task_id>.md`, updated context | Code change scope, test evidence, requirement satisfaction |
| 12 | Review / Security / Release / Handoff | Perform final review, release readiness, deployment planning, operations, and handoff. | `12_code_review.md`, `12_security_privacy_review.md`, `12_release_readiness.md`, `12_deployment_plan.md`, `12_operations_runbook.md`, `12_documentation_handoff.md` | Release approval, deployment approval, operations responsibility |
| 13 | Workflow Retrospective & Skill Improvement | Review agent performance and improve the workflow and skills. | `13_workflow_retrospective.md`, `13_skill_improvement_backlog.md`, `13_agent_failure_patterns.md`, `13_reusable_lessons.md` | Skill improvement priorities, reusable lessons, next-project changes |

## 4. Standard stage execution loop

Every stage should follow the same basic execution protocol.

```text
1. Read the current SKILL.md.
2. Read artifact_manifest.yml if available.
3. Read context_packet.md.
4. Read DECISIONS.md.
5. Check whether USER_DIRECTIVES.md exists in the current stage folder.
6. Identify Always Read inputs.
7. Activate conditional inputs based on project profile and current context.
8. Verify that required inputs exist and are approved or clearly marked as draft.
9. Report missing, conflicting, superseded, rejected, or unapproved inputs.
10. Restate the current stage purpose.
11. Execute the stage-specific procedure.
12. Create or update required artifacts.
13. Create conditional artifacts when applicable.
14. Record N/A rationale for non-applicable conditional artifacts.
15. Separate decision candidates, assumptions, open questions, risks, and recommendations.
16. Update traceability where applicable.
17. Update context_packet.md for the next stage.
18. Update ASSUMPTIONS.md, OPEN_QUESTIONS.md, and REJECTED_OPTIONS.md as needed.
19. Do not update DECISIONS.md unless explicit human approval exists.
20. End with a human approval gate.
```

## 5. Recommended project folder structure

A project using the workflow may use this structure:

```text
/workflow
  /00_intake
  /01_goal
  /02_stakeholders_risk
  /03_requirements
  /04_domain
  /05_architecture
  /06_data
  /07_mvp_release
  /08_test_strategy
  /09_tasks
  /10_prompts
  /11_implementation_results
  /12_review_release_handoff
  /13_retrospective

/workflow/context
  artifact_manifest.yml
  context_packet.md
  DECISIONS.md
  ASSUMPTIONS.md
  OPEN_QUESTIONS.md
  REJECTED_OPTIONS.md
  TRACEABILITY_MATRIX.md
  APPROVAL_LOG.md
```

A reusable skill repository may use this structure:

```text
/skills
  /00_project_intake
  /01_service_goal_definition
  /02_stakeholder_risk_framing
  /03_requirements_acceptance
  /04_domain_modeling
  /05_architecture_contracts
  /06_data_design
  /07_mvp_release_slicing
  /08_test_strategy_validation
  /09_task_breakdown
  /10_implementation_prompt_writing
  /11_tdd_implementation_loop
  /12_review_release_handoff
  /13_workflow_retrospective

/workflow_templates
  /core
  /stages
  /specializations
  /tool_wrappers
```

## 6. Key context files

### artifact_manifest.yml

Tracks artifact existence, status, approval state, supersession, and source relationships.

The agent should check it before using prior artifacts as source of truth.

### context_packet.md

Provides the minimum operational context needed for the next stage.

It should not become a full project history.

### DECISIONS.md

Stores only human-approved decisions.

The agent should not add decisions here unless the human explicitly approved them.

### ASSUMPTIONS.md

Stores temporary assumptions that support progress but are not yet verified.

### OPEN_QUESTIONS.md

Stores unresolved questions that may affect later stages.

### REJECTED_OPTIONS.md

Stores rejected or superseded options that should not be revived unless explicitly reopened.

### TRACEABILITY_MATRIX.md

Maintains links across goals, requirements, acceptance criteria, domain concepts, architecture, data models, tasks, tests, and implementation evidence.

### APPROVAL_LOG.md

Records explicit human approvals, timestamps if available, and the artifacts or decisions approved.

## 7. Stage details

## Stage 00 — Project Intake / Existing Context Review

### Purpose

Identify whether the project is greenfield, brownfield, prototype, research tool, or extension of an existing system. The agent must not start requirements or architecture work before understanding the current context.

### Typical inputs

- initial idea;
- existing codebase notes if any;
- existing documents, diagrams, APIs, datasets, deployment settings;
- user-provided constraints;
- known forbidden changes.

### Typical outputs

```text
/workflow/00_intake/00_project_intake.md
/workflow/00_intake/00_existing_context_review.md
/workflow/00_intake/result.md
/workflow/context/context_packet.md
```

### Human gate

Approve or correct:

- project type;
- fixed technology stack;
- existing materials to use;
- forbidden change areas;
- initial constraints;
- whether the workflow should proceed to Stage 01.

## Stage 01 — Service Goal Definition

### Purpose

Define why the service should exist before deciding what to build.

### Typical inputs

- approved Stage 00 intake artifacts;
- `context_packet.md`;
- `DECISIONS.md`;
- stage-local `USER_DIRECTIVES.md` if present.

### Typical outputs

```text
/workflow/01_goal/01_service_goal.md
/workflow/01_goal/result.md
/workflow/context/context_packet.md
```

### Required content

- problem definition;
- target users;
- core value;
- success criteria;
- non-goals;
- initial assumptions;
- open questions.

### Human gate

Approve or revise:

- service goal;
- primary users;
- success criteria;
- non-goals.

## Stage 02 — Stakeholder & Risk Framing

### Purpose

Identify users, operators, administrators, external systems, regulatory concerns, security risks, and privacy risks early.

### Typical outputs

```text
/workflow/02_stakeholders_risk/02_stakeholders.md
/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
/workflow/02_stakeholders_risk/result.md
/workflow/context/context_packet.md
```

### Required content

- stakeholders;
- user roles;
- permission levels;
- sensitive data;
- personal data;
- external API or LLM data transfer;
- administrator powers;
- audit log needs;
- initial security and privacy risks.

### Human gate

Approve or revise:

- role and permission direction;
- personal or sensitive data handling direction;
- external API or LLM transfer policy;
- initial risk assumptions.

## Stage 03 — Requirements & Acceptance Criteria

### Purpose

Convert goals into functional requirements, non-functional requirements, scenarios, edge cases, and acceptance criteria.

This is where TDD begins conceptually. The agent does not write product code here, but it must produce requirements that can later be turned into tests.

### Typical outputs

```text
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/03_requirements/03_traceability_matrix.md
/workflow/03_requirements/result.md
/workflow/context/context_packet.md
```

### Recommended requirement format

```text
Requirement ID:
User Role:
Goal:
Functional Description:
Acceptance Criteria:
Edge Cases:
Related Non-Functional Requirements:
Security / Privacy Conditions:
Validation Method:
```

### Human gate

Approve or revise:

- must-have requirements;
- acceptance criteria;
- non-scope items;
- whether requirements are testable enough.

## Stage 04 — Domain Modeling / DDD

### Purpose

Model the domain before designing the database or implementation structure.

DDD in this workflow means:

- ubiquitous language;
- core domain concepts;
- entities;
- value objects;
- aggregates;
- invariants;
- state transitions;
- domain events;
- bounded contexts;
- context map.

It does not mean simply extracting database tables.

### Typical outputs

```text
/workflow/04_domain/04_ubiquitous_language.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/04_domain/04_domain_traceability_matrix.md
/workflow/04_domain/result.md
/workflow/context/context_packet.md
```

### Human gate

Approve or revise:

- domain terms;
- entities and value objects;
- aggregate boundaries;
- bounded contexts;
- business rules and invariants.

## Stage 05 — Architecture & Technical Contracts

### Purpose

Translate the domain model and requirements into system structure, module boundaries, API contracts, integration boundaries, authentication, authorization, and data flow.

### Typical outputs

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_api_contracts.md
/workflow/05_architecture/05_integration_contracts.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/05_architecture/result.md
/workflow/context/context_packet.md
```

### Required content

- architecture style;
- frontend/backend boundary;
- module boundaries;
- API contracts;
- external integrations;
- authentication and authorization flow;
- error handling policy;
- logging and observability policy;
- major trade-offs.

### Human gate

Approve or revise:

- architecture direction;
- major technical choices;
- API contracts;
- authorization model;
- external integration approach.

## Stage 06 — Data Design

### Purpose

Design data structures after domain and architecture decisions are clear.

Data design is separate from domain modeling and from implementation.

### Typical outputs

```text
/workflow/06_data/06_conceptual_data_model.md
/workflow/06_data/06_logical_schema.md
/workflow/06_data/06_physical_schema.md
/workflow/06_data/06_indexes.md
/workflow/06_data/06_migration_plan.md
/workflow/06_data/06_data_security_rules.md
/workflow/06_data/result.md
/workflow/context/context_packet.md
```

### Required content

- conceptual data model;
- logical schema;
- physical schema if applicable;
- indexes;
- query patterns;
- migration plan;
- data retention and deletion policy;
- security rules;
- access control.

### Human gate

Approve or revise:

- schema;
- data ownership;
- security rules;
- migration strategy.

## Stage 07 — MVP Scope & Release Slicing

### Purpose

Prevent uncontrolled scope expansion. Decide what belongs in the MVP, what belongs in later releases, and what is explicitly out of scope.

### Typical outputs

```text
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md
/workflow/07_mvp_release/result.md
/workflow/context/context_packet.md
```

### Scope categories

```text
Must
Should
Could
Won't / Non-scope
Later
```

### Human gate

Approve or revise:

- MVP scope;
- out-of-scope items;
- release order.

## Stage 08 — Test Strategy & Validation Harness

### Purpose

Define validation structure before implementation begins. This makes TDD and test-aware implementation practical.

### Typical outputs

```text
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
/workflow/08_test_strategy/result.md
/workflow/context/context_packet.md
```

### Required content

- unit test targets;
- integration test targets;
- E2E test targets;
- acceptance tests;
- fixture and test data strategy;
- manual verification steps;
- commands to run;
- pass/fail criteria;
- CI applicability.

### Traceability rule

```text
Requirement → Acceptance Criteria → Test Case → Task → Implementation Evidence
```

### Human gate

Approve or revise:

- test strategy;
- manual validation criteria;
- automated test scope;
- validation commands.

## Stage 09 — Task Breakdown

### Purpose

Convert the approved design into small development tasks that an agent can safely execute.

### Typical outputs

```text
/workflow/09_tasks/09_task_inventory.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_dependency_order.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/09_tasks/result.md
/workflow/context/context_packet.md
```

### Recommended task card format

```text
Task ID:
Title:
Linked Requirement:
Linked Domain Concept:
Linked API / Module:
Change Scope:
Files likely to change:
Dependencies:
Acceptance Criteria:
Required Tests:
Manual Verification:
Security/Privacy Notes:
Definition of Done:
Rollback / Recovery Notes:
```

### Human gate

Approve or revise:

- task size;
- task order;
- definition of done for each task.

## Stage 10 — Implementation Prompt Writing

### Purpose

Convert task cards into executable prompts for coding agents.

### Typical outputs

```text
/workflow/10_prompts/10_implementation_prompts.md
/workflow/10_prompts/10_prompt_handoff_packets.md
/workflow/10_prompts/result.md
/workflow/context/context_packet.md
```

### Required prompt structure

Each implementation prompt should include:

```text
1. Goal
2. Context
3. Approved Inputs
4. Files to inspect first
5. Allowed change scope
6. Forbidden changes
7. Required implementation steps
8. Required tests
9. Commands to run
10. Expected evidence
11. Output files to update
12. Next context_packet.md update instructions
```

### Human gate

Approve or revise:

- implementation prompts;
- allowed change scope;
- forbidden changes;
- execution order.

## Stage 11 — TDD Implementation Loop

### Purpose

Implement the system task by task.

This is not one large implementation stage. It is a repeated loop over approved task cards and implementation prompts.

### Per-task loop

```text
1. Read context.
2. Inspect existing code.
3. Restate the task.
4. Write or identify a failing test.
5. Run the test and confirm failure if feasible.
6. Implement the minimal change.
7. Run relevant tests.
8. Refactor.
9. Run broader regression tests.
10. Record evidence.
11. Update result.md.
12. Update context_packet.md.
```

### Typical outputs

```text
/workflow/11_implementation_results/11_task_result_<task_id>.md
/workflow/11_implementation_results/11_test_evidence_<task_id>.md
/workflow/context/context_packet.md
```

### Required result format

```text
Task ID:
Summary:
Files Changed:
Tests Added:
Tests Run:
Test Result:
Known Limitations:
Assumptions Used:
Open Questions:
Follow-up Tasks:
```

### Human gate

Review:

- code change scope;
- test evidence;
- requirement satisfaction;
- unnecessary feature additions;
- security and privacy notes.

## Stage 12 — Review / Security / Release / Handoff

### Purpose

Perform final review, security/privacy review, release readiness check, deployment planning, operations preparation, and documentation handoff.

Security and testing should already have been considered earlier. This stage is the final verification gate, not the first time security and testing appear.

### Typical outputs

```text
/workflow/12_review_release_handoff/12_code_review.md
/workflow/12_review_release_handoff/12_security_privacy_review.md
/workflow/12_review_release_handoff/12_release_readiness.md
/workflow/12_review_release_handoff/12_deployment_plan.md
/workflow/12_review_release_handoff/12_operations_runbook.md
/workflow/12_review_release_handoff/12_documentation_handoff.md
/workflow/12_review_release_handoff/result.md
/workflow/context/context_packet.md
```

### Review items

- requirements satisfaction;
- test results;
- code quality;
- performance issues;
- security issues;
- privacy issues;
- environment variables;
- deployment procedure;
- rollback procedure;
- documentation freshness.

### Human gate

Approve or reject:

- release readiness;
- deployment;
- operations responsibility;
- documentation handoff.

## Stage 13 — Workflow Retrospective & Skill Improvement

### Purpose

Review the workflow itself after a project or major release. The goal is not only to build software but also to improve the reusable skills and agentic coding process.

### Typical outputs

```text
/workflow/13_retrospective/13_workflow_retrospective.md
/workflow/13_retrospective/13_skill_improvement_backlog.md
/workflow/13_retrospective/13_agent_failure_patterns.md
/workflow/13_retrospective/13_reusable_lessons.md
/workflow/13_retrospective/result.md
/workflow/context/context_packet.md
```

### Required content

- what the agent did well;
- where the agent repeatedly failed;
- which prompts were ambiguous;
- where human judgment was essential;
- what rules should be reused;
- which `SKILL.md` files should be revised;
- which new skills should be created;
- which skills should be deleted or merged.

### Human gate

Approve or revise:

- workflow improvements;
- skill revision priorities;
- how lessons will be applied to the next project.

## 8. Running a stage

A typical agent instruction looks like this:

```text
You are working inside the Manual Agentic Coding Workflow.

Run Stage XX: <stage name>.

Use this reusable skill:
/skills/<stage_folder>/SKILL.md

Target project workflow folder:
/workflow

Follow the SKILL.md exactly.
Do not implement code unless this is Stage 11.
Read only the required and applicable inputs.
Check USER_DIRECTIVES.md if present.
Create or update only the required stage artifacts and required context files.
Separate approved decisions, decision candidates, working assumptions, open questions, risks, and recommendations.
Do not update DECISIONS.md unless explicit human approval exists.
End with a human approval gate.
```

## 9. Running a split stage

If a stage is split into sub-skills, use the parent stage folder as the public entrypoint.

Example:

```text
/skills/04_domain_modeling/
  SKILL.md
  README.md
  artifact_contract.yml
  /04a_ubiquitous_language/
  /04b_domain_concepts_entities_values/
  /04c_aggregates_rules_lifecycle/
  /04d_events_bounded_contexts/
  /04e_domain_modeling_finalizer/
```

Execution policy:

```text
1. Read the parent SKILL.md and README.md.
2. Follow the declared sub-skill execution order.
3. Run each sub-skill independently.
4. Do not treat sub-skill output as approved stage output automatically.
5. Run the finalizer sub-skill.
6. Review the official stage artifacts.
7. Approve or revise the official stage artifacts.
8. Let downstream stages depend only on approved official artifacts.
```

Downstream stages must not depend on internal sub-skill folder names, prompt history, or unapproved drafts.

## 10. Stage gate checklist

Before moving from one stage to the next, check:

```text
[ ] Required artifacts were created or updated.
[ ] Conditional artifacts were created or marked N/A with rationale.
[ ] Missing inputs were reported.
[ ] Conflicting inputs were reported.
[ ] Decision candidates are not recorded as approved decisions.
[ ] Working assumptions are clearly marked.
[ ] Open questions are recorded.
[ ] Risks are recorded.
[ ] Rejected options are recorded if applicable.
[ ] Traceability was updated where applicable.
[ ] context_packet.md was prepared for the next stage.
[ ] Human approval gate was presented.
[ ] The human approved, revised, or rejected the relevant artifacts.
```

## 11. Traceability lifecycle

Traceability grows across stages.

```text
Stage 01: Goals and success criteria
Stage 03: Requirements and acceptance criteria
Stage 04: Domain concepts, invariants, events
Stage 05: Architecture components and contracts
Stage 06: Data models and access rules
Stage 08: Test cases and validation commands
Stage 09: Task cards and dependency order
Stage 10: Implementation prompts
Stage 11: Implementation and test evidence
Stage 12: Review and release evidence
```

The goal is not to create a huge bureaucratic matrix. The goal is to prevent unexplained implementation work.

## 12. Context reset strategy

The workflow is designed to tolerate context resets.

A new session should be able to continue from files by reading:

```text
1. Current SKILL.md
2. artifact_manifest.yml
3. context_packet.md
4. DECISIONS.md
5. relevant approved source artifacts
6. USER_DIRECTIVES.md if present
```

Recommended reset points:

- after a stage is approved;
- after a split-stage finalizer is approved;
- before Stage 11 task implementation if the planning context is large;
- between independent implementation tasks;
- before Stage 12 final review.

Do not reset context if critical work exists only in chat and has not been written to artifacts.

## 13. Project profile usage

Project profiles adjust workflow strictness.

### Prototype / Research Tool

Use lighter artifacts, but keep assumptions and validation explicit.

### MVP Production

Use most stages, require test strategy, release readiness, security/privacy screening, and implementation evidence.

### Regulated / Security-Sensitive

Use stronger approval logs, threat/risk artifacts, auditability, privacy review, security tests, and release blockers.

Specialization addenda may add project-type concerns, but they should not weaken core rules.

## 14. Minimal adoption path

For a first real trial, use this path:

```text
1. Create repository and project workflow folders.
2. Add README.md and QUICKSTART.md.
3. Prepare /workflow/00_intake/initial_idea.md.
4. Run Stage 00.
5. Review and approve Stage 00 outputs.
6. Run Stage 01.
7. Continue to Stage 03 before asking the agent to write implementation code.
8. Use Stage 08 and Stage 09 before Stage 11.
9. Implement one small task through the TDD loop.
10. Record evidence and review the workflow experience.
```

This keeps the first trial small while preserving the core workflow logic.

## 15. Common mistakes

Avoid:

- running Stage 11 before requirements, scope, and validation are clear;
- treating agent-generated output as approved automatically;
- skipping `context_packet.md` updates;
- letting downstream stages depend on chat history;
- reading every previous file by default;
- ignoring draft, superseded, or rejected status;
- using unapproved artifacts as source of truth;
- creating tasks that do not map to requirements;
- creating implementation prompts without forbidden changes and validation commands;
- claiming tests passed without evidence;
- doing final security review as the first security review;
- skipping retrospective and losing lessons for the next project.

## 16. Recommended next documents

After reading this overview:

```text
1. Read CONCEPT.md for the design principles.
2. Read QUICKSTART.md for the first execution path.
3. Inspect /skills/00_project_intake/SKILL.md.
4. Run Stage 00 on a small Greenfield MVP example.
5. Add example outputs under /examples after the first successful run.
```
