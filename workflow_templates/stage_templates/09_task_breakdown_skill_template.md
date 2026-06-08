# 09_task_breakdown_skill_template.md

> Stage-Specific SKILL Template for Manual Agentic Coding Workflow
> Target stage: **09_task_breakdown**
> This is a template for creating a reusable executable `SKILL.md`.
> This template is not itself a project artifact and must not be executed as a workflow stage.

---

## 1. Template Purpose

This template defines the stage-specific extension for creating a reusable SKILL that performs **Stage 9: Task Breakdown**.

Stage 9 converts approved requirements, MVP scope, architecture, data design, and validation strategy into small, ordered, traceable development tasks that can later be transformed into implementation prompts.

The resulting executable SKILL should help an Agent produce development task artifacts that are:

* small enough for agentic implementation;
* tied to approved requirements and acceptance criteria;
* test-first or test-aware;
* ordered by dependency;
* scoped to avoid uncontrolled implementation;
* explicit about files likely to change;
* connected to validation commands and evidence expectations;
* ready for Stage 10 implementation prompt writing.

---

## 2. Stage Purpose

Stage 9 exists to answer:

> “Given the approved product scope, architecture, data design, and validation strategy, what small, ordered, test-aware development tasks should be executed by coding agents?”

This stage must not implement code.
This stage must not write final implementation prompts.
This stage prepares the structured task inventory that Stage 10 will convert into executable implementation prompts.

---

## 3. Core Question

The SKILL created from this template must answer:

```text
How should the approved MVP/release scope be decomposed into safe, traceable, dependency-ordered implementation tasks, each with clear acceptance criteria, required tests, change scope, and definition of done?
```

Supporting questions:

```text
- Which approved requirements belong to the current MVP or release slice?
- Which architecture modules, APIs, data structures, or security rules are affected?
- What tasks are needed to implement the approved behavior?
- Which tasks are prerequisites for others?
- Which tasks can be executed independently?
- Which tasks are too large and must be split further?
- Which tests or validation methods are required for each task?
- Which tasks require extra security, privacy, migration, or rollback attention?
- Which task cards are ready for Stage 10 implementation prompt writing?
```

---

## 4. Stage Folder

Recommended project execution folder:

```text
/workflow/09_tasks
```

Recommended reusable SKILL folder:

```text
/skills/09_task_breakdown
```

Recommended stage template path:

```text
/workflow_templates/stage_templates/09_task_breakdown_skill_template.md
```

---

## 5. Always Read Inputs

The executable SKILL created from this template must always read the following if available:

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
/workflow/05_architecture/05_module_boundaries.md

/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/07_mvp_release/07_out_of_scope.md

/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_acceptance_tests.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/08_test_strategy/08_manual_test_plan.md
```

Rationale:

```text
Stage 9 must decompose only approved scope into tasks.
It must preserve requirement, architecture, release, and validation traceability.
It must know what is out of scope before creating tasks.
```

---

## 6. Read If Applicable Inputs

The executable SKILL created from this template must read these inputs only when the condition applies.

```text
/workflow/04_domain/04_ubiquitous_language.md
- Read if domain terminology affects task naming, business rules, or test scenarios.

/workflow/04_domain/04_domain_model.md
- Read if domain entities, value objects, aggregates, or workflows affect task boundaries.

/workflow/04_domain/04_business_rules_invariants.md
- Read if invariants, lifecycle rules, or state transitions require implementation tasks or tests.

/workflow/04_domain/04_domain_events.md
- Read if event publishing, event handling, async workflows, or integration behavior exists.

/workflow/04_domain/04_bounded_contexts.md
- Read if module boundaries or cross-context interactions affect task ordering.

/workflow/05_architecture/05_api_contracts.md
- Read if APIs, endpoints, RPCs, webhooks, or service contracts exist.

/workflow/05_architecture/05_integration_contracts.md
- Read if external systems, third-party APIs, queues, jobs, or LLM/API integrations exist.

/workflow/05_architecture/05_architecture_decisions.md
- Read if implementation tasks must respect specific technical decisions or trade-offs.

/workflow/06_data/06_conceptual_data_model.md
- Read if persistent domain data exists.

/workflow/06_data/06_logical_schema.md
- Read if database collections, tables, documents, or relationships affect tasks.

/workflow/06_data/06_physical_schema.md
- Read if physical schema, storage layout, or implementation-level persistence is defined.

/workflow/06_data/06_indexes.md
- Read if query performance, filtering, sorting, or pagination tasks exist.

/workflow/06_data/06_migration_plan.md
- Read if schema migration, seed data, data backfill, compatibility, or rollout tasks are needed.

/workflow/06_data/06_data_security_rules.md
- Read if authorization, row/document-level security, privacy, or access control tasks exist.

/workflow/00_intake/00_existing_context_review.md
- Read if this is a brownfield, legacy, extension, refactor, migration, or integration project.

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- Read if security, privacy, compliance, role, or permission risks affect task design.

/workflow/02_stakeholders_risk/02_stakeholders.md
- Read if user roles, operators, admins, reviewers, or external actors affect task boundaries.
```

---

## 7. Do Not Read By Default

The executable SKILL must not read the following unless explicitly instructed:

```text
- full raw agent chat history;
- superseded stage artifacts;
- rejected artifacts;
- exploratory drafts not marked as approved;
- implementation source files, unless brownfield task decomposition requires codebase awareness;
- generated code or test files from Stage 11, because Stage 9 normally occurs before implementation;
- unrelated stage result files that do not affect task boundaries;
- internal sub-skill outputs from previous stages unless promoted to official approved stage artifacts.
```

---

## 8. Missing Input Handling

The executable SKILL must classify missing inputs as blocking or non-blocking.

### Blocking Missing Inputs

The following are normally blocking:

```text
- missing approved requirements;
- missing approved acceptance criteria;
- missing approved MVP or release scope;
- missing test strategy or validation commands;
- missing architecture plan when tasks require module or API boundaries;
- missing artifact approval status when draft and approved artifacts conflict;
- missing out-of-scope list when scope boundaries are unclear.
```

If a blocking input is missing, the SKILL must produce a blocker report and stop before creating final task cards.

### Non-Blocking Missing Inputs

The following may be non-blocking if clearly marked:

```text
- missing optional domain events when the project has no event-driven behavior;
- missing migration plan when no persistent data exists;
- missing integration contract when there are no external integrations;
- missing data security rules when no data access control exists;
- missing brownfield review when the project is confirmed greenfield.
```

For each non-blocking missing input, the SKILL must:

```text
1. record the missing input;
2. explain why it is non-blocking;
3. state the working assumption used;
4. add a revisit condition if future scope changes.
```

---

## 9. USER_DIRECTIVES.md Handling

The executable SKILL must check:

```text
/workflow/09_tasks/USER_DIRECTIVES.md
```

If present, it must be read before task decomposition.

The SKILL must classify each directive as one of:

```text
- explicit approval;
- correction;
- preference;
- rejection;
- scope change;
- task ordering instruction;
- task size instruction;
- technology constraint;
- security/privacy constraint;
- validation requirement;
- question to answer.
```

Rules:

```text
- USER_DIRECTIVES.md takes precedence over agent inference.
- USER_DIRECTIVES.md does not automatically override approved decisions.
- If a directive conflicts with approved scope, architecture, data design, or test strategy, report the conflict.
- Do not modify USER_DIRECTIVES.md unless explicitly instructed.
```

---

## 10. Stage-Specific Procedure

The executable SKILL created from this template must perform the following procedure.

### Step 1. Preflight and Source Validation

```text
1. Read the current SKILL.md.
2. Read artifact_manifest.yml if available.
3. Read context_packet.md.
4. Read DECISIONS.md and APPROVAL_LOG.md if available.
5. Check USER_DIRECTIVES.md.
6. Confirm required Stage 3, Stage 5, Stage 7, and Stage 8 inputs.
7. Verify which inputs are approved, draft, superseded, rejected, or missing.
8. Report conflicts before task generation.
```

### Step 2. Restate Current Stage Boundary

The SKILL must restate:

```text
- Stage 9 purpose;
- approved release slice or MVP scope being decomposed;
- what is explicitly out of scope;
- what Stage 9 will not do.
```

### Step 3. Extract Task Sources

From approved artifacts, identify:

```text
- in-scope requirements;
- acceptance criteria;
- release slice membership;
- architecture modules;
- API contracts;
- data models;
- security/privacy constraints;
- validation commands;
- acceptance tests;
- manual verification steps;
- unresolved questions affecting implementation tasks.
```

### Step 4. Build Requirement-to-Implementation Map

Create an intermediate mapping from:

```text
Requirement
→ Acceptance Criteria
→ Domain Concept / Business Rule
→ Architecture Module / API / Data Component
→ Validation Method
→ Candidate Task(s)
```

This mapping may be included in the traceability artifact or in a dedicated section of the task inventory.

### Step 5. Generate Candidate Tasks

Create candidate tasks from the mapping.

Task candidates should be formed around coherent implementation increments such as:

```text
- setup or scaffolding required before feature work;
- domain logic;
- API contract implementation;
- data schema or migration;
- UI or interaction flow;
- integration behavior;
- authorization or security rule;
- validation/test harness;
- observability or operational support;
- documentation or developer handoff if needed for implementation.
```

### Step 6. Split Oversized Tasks

Any task is too large if it:

```text
- touches too many unrelated modules;
- combines schema, API, UI, and tests without a reason;
- cannot be validated independently;
- has unclear acceptance criteria;
- contains multiple unrelated requirements;
- would require a broad prompt with vague change scope;
- cannot be completed safely by an agent in one bounded implementation loop.
```

Split large tasks into smaller tasks while preserving traceability.

### Step 7. Assign Stable Task IDs

Use stable IDs:

```text
TASK-001
TASK-002
TASK-003
```

Optional prefix for release slice:

```text
MVP-TASK-001
R1-TASK-001
R2-TASK-001
```

The chosen convention must be recorded and used consistently.

### Step 8. Create Task Cards

Each task card must include:

```text
Task ID:
Title:
Release Slice:
Task Type:
Linked Requirement(s):
Linked Acceptance Criteria:
Linked Domain Concept(s):
Linked Architecture Component(s):
Linked API / Contract:
Linked Data Artifact(s):
Linked Test Case(s):
Change Scope:
Files or Areas Likely to Change:
Files or Areas Not to Change:
Dependencies:
Preconditions:
Implementation Notes:
Required Tests:
Validation Commands:
Manual Verification:
Security / Privacy Notes:
Observability / Logging Notes:
Definition of Done:
Rollback / Recovery Notes:
Open Questions:
```

### Step 9. Order Tasks by Dependency

Create a dependency order that considers:

```text
- foundation before feature work;
- schema/migration before data-dependent logic;
- domain logic before API/UI behavior when applicable;
- API contract before frontend integration when applicable;
- authentication/authorization before protected flows;
- validation harness before or alongside implementation;
- high-risk tasks before dependent tasks when risk reduction is needed;
- release slice order approved in Stage 7.
```

### Step 10. Identify Parallelizable Tasks

Mark tasks as:

```text
- sequential;
- parallelizable;
- blocked;
- requires human decision;
- requires prior spike or investigation.
```

Parallelization must not violate dependency order or shared file safety.

### Step 11. Update Traceability

Update the traceability matrix so that each task links to:

```text
- requirement ID;
- acceptance criteria ID or reference;
- domain concept or invariant if applicable;
- architecture component if applicable;
- data artifact if applicable;
- test or validation method;
- future implementation evidence placeholder.
```

### Step 12. Produce Stage Outputs

Create or update all mandatory artifacts and any applicable conditional artifacts.

### Step 13. Prepare Human Approval Gate

List:

```text
- task cards ready for approval;
- task order requiring approval;
- tasks needing further split;
- blocked tasks;
- assumptions used;
- open questions;
- risks;
- recommendations for Stage 10.
```

### Step 14. Update Context for Stage 10

Update or prepare `context_packet.md` with only the minimum context needed for Stage 10 implementation prompt writing.

---

## 11. Mandatory Output Artifacts

The executable SKILL created from this template must create or update:

```text
/workflow/09_tasks/09_task_inventory.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_dependency_order.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/09_tasks/result.md
/workflow/context/context_packet.md
```

### 11.1 09_task_inventory.md

Purpose:

```text
A compact inventory of all implementation tasks in the approved MVP or release slice.
```

Required sections:

```text
# 09 Task Inventory

## 1. Scope Basis
## 2. Task ID Convention
## 3. Task Summary Table
## 4. Task Type Classification
## 5. Requirement Coverage Summary
## 6. Release Slice Coverage Summary
## 7. Blocked or Deferred Tasks
## 8. Out-of-Scope Items Not Converted to Tasks
## 9. Notes for Stage 10
```

Task summary table columns:

```text
Task ID
Title
Release Slice
Primary Requirement
Task Type
Dependency Status
Validation Method
Risk Level
Ready for Prompt Writing
```

### 11.2 09_task_cards.md

Purpose:

```text
Detailed task cards that Stage 10 can convert into implementation prompts.
```

Required structure for each card:

```text
## TASK-XXX: [Task Title]

### 1. Task Summary
### 2. Release Slice
### 3. Task Type
### 4. Linked Requirement(s)
### 5. Linked Acceptance Criteria
### 6. Linked Domain Concept(s)
### 7. Linked Architecture Component(s)
### 8. Linked API / Contract
### 9. Linked Data Artifact(s)
### 10. Linked Test Case(s)
### 11. Change Scope
### 12. Files or Areas Likely to Change
### 13. Files or Areas Not to Change
### 14. Dependencies
### 15. Preconditions
### 16. Implementation Notes
### 17. Required Tests
### 18. Validation Commands
### 19. Manual Verification
### 20. Security / Privacy Notes
### 21. Observability / Logging Notes
### 22. Definition of Done
### 23. Rollback / Recovery Notes
### 24. Open Questions
```

### 11.3 09_dependency_order.md

Purpose:

```text
A safe execution order for task implementation.
```

Required sections:

```text
# 09 Dependency Order

## 1. Ordering Principles
## 2. Sequential Task Chain
## 3. Parallelizable Task Groups
## 4. Blocked Tasks
## 5. Human Decision Required Before Execution
## 6. Risk-Based Ordering Notes
## 7. Recommended Stage 10 Prompt Writing Order
```

### 11.4 09_traceability_matrix.md

Purpose:

```text
Stage-local traceability from approved requirements and tests to tasks.
```

Required columns:

```text
Requirement ID
Acceptance Criteria
Release Slice
Domain Concept / Rule
Architecture Component
Data Artifact
Test / Validation Method
Task ID
Implementation Evidence Placeholder
Traceability Status
```

### 11.5 result.md

Purpose:

```text
Summarize Stage 9 execution and approval needs.
```

Required sections:

```text
# Result: 09 Task Breakdown

## 1. Task Summary
## 2. Inputs Used
## 3. Outputs Created or Updated
## 4. Scope Basis
## 5. Key Findings
## 6. Task Breakdown Summary
## 7. Dependency Summary
## 8. Traceability Updates
## 9. Decision Candidates
## 10. Working Assumptions
## 11. Open Questions
## 12. Risks and Constraints
## 13. Rejected or Superseded Options
## 14. Human Approval Required
## 15. Recommended Next Step
```

---

## 12. Conditional Output Artifacts

Create these only if applicable.

```text
/workflow/09_tasks/09_migration_tasks.md
- Create if schema migration, data migration, seed data, compatibility, rollback, or data backfill tasks exist.

/workflow/09_tasks/09_security_privacy_tasks.md
- Create if access control, authorization, privacy, audit logging, data retention, sensitive data, or compliance-sensitive tasks exist.

/workflow/09_tasks/09_integration_tasks.md
- Create if external API, webhook, queue, scheduled job, LLM/API integration, or third-party system tasks exist.

/workflow/09_tasks/09_frontend_backend_coordination.md
- Create if frontend and backend work must be coordinated across contracts, schemas, or staged rollout.

/workflow/09_tasks/09_risk_reduction_spikes.md
- Create if implementation requires research, prototype, technical spike, unknown library behavior, performance investigation, or feasibility validation.
```

---

## 13. N/A Record Rules

If a conditional artifact is not applicable, record this in `result.md` under:

```text
## Conditional Artifacts Not Created
```

For each omitted conditional artifact, include:

```text
Artifact:
Why Not Applicable:
Revisit If:
Source Basis:
```

Example structure:

```text
Artifact: /workflow/09_tasks/09_migration_tasks.md
Why Not Applicable: No persistent schema changes were identified in the approved MVP scope.
Revisit If: Future release introduces database schema changes or data backfill.
Source Basis: Approved Stage 6 data design and Stage 7 MVP scope.
```

---

## 14. Traceability Requirements

The executable SKILL must preserve and improve traceability.

Required links:

```text
Requirement → Acceptance Criteria → Release Slice → Task
Requirement → Acceptance Criteria → Test / Validation Method → Task
Domain Rule / Invariant → Required Test → Task, if applicable
Architecture Component / API Contract → Task, if applicable
Data Artifact / Security Rule → Task, if applicable
Task → Future Implementation Prompt Placeholder
Task → Future Implementation Evidence Placeholder
```

Rules:

```text
- Do not create tasks that cannot be traced to approved scope unless clearly marked as enabling/infrastructure tasks.
- Enabling tasks must explain which later task or validation need they support.
- Do not drop approved must-have requirements without recording a traceability gap.
- Do not create implementation tasks for out-of-scope items.
- Do not create tasks for rejected options.
- If a requirement has no task, mark it as Coverage Gap.
- If a task has no requirement, mark it as Enabling Task, Risk Reduction Task, or Invalid Candidate.
```

---

## 15. Task Sizing Rules

A task is acceptable when:

```text
- it has a single clear purpose;
- it has a bounded change scope;
- it has explicit acceptance criteria;
- it has required tests or validation steps;
- it can be reviewed independently;
- it can produce observable evidence;
- it does not require hidden assumptions;
- it does not mix unrelated features;
- it is small enough for a coding agent to execute safely.
```

A task must be split when:

```text
- it combines unrelated requirements;
- it spans too many modules without a clear integration reason;
- it includes both broad infrastructure and feature behavior;
- it cannot be validated without implementing several other tasks first;
- it has vague wording such as “build the system” or “implement the feature”;
- it lacks a clear definition of done.
```

---

## 16. Task Type Taxonomy

The executable SKILL may classify tasks using these types:

```text
- setup / scaffolding;
- domain logic;
- API / contract;
- frontend / UI;
- backend / service;
- data schema / persistence;
- migration / seed data;
- security / authorization;
- privacy / compliance;
- integration / external system;
- validation / test harness;
- observability / logging;
- documentation / handoff;
- risk reduction spike;
- refactor / cleanup;
- release preparation.
```

Use only applicable types.

---

## 17. Stage-Specific Validation Checklist

Before completion, verify:

```text
[ ] Required approved inputs were checked.
[ ] Missing or draft inputs were reported.
[ ] Out-of-scope items were not converted into tasks.
[ ] Every must-have requirement has at least one task or a recorded coverage gap.
[ ] Every task has a stable task ID.
[ ] Every task has linked requirement(s) or is explicitly marked as an enabling/risk-reduction task.
[ ] Every task has linked acceptance criteria or validation basis.
[ ] Every task has required tests or manual validation.
[ ] Every task has a definition of done.
[ ] Every task has bounded change scope.
[ ] Every task identifies likely files or areas to change, where knowable.
[ ] Every task identifies files or areas not to change when relevant.
[ ] Security/privacy-sensitive tasks are marked.
[ ] Migration-sensitive tasks are marked.
[ ] Integration-sensitive tasks are marked.
[ ] Task order respects dependencies.
[ ] Parallelizable groups do not share unsafe overlapping change areas.
[ ] Traceability matrix has been updated.
[ ] context_packet.md has been prepared for Stage 10.
[ ] Human approval gate is explicit.
```

---

## 18. Stage-Specific Human Approval Gate

The executable SKILL must end with:

```markdown
## Human Approval Required

### Decisions to Approve
- Task inventory
- Task card set
- Task dependency order
- Task sizing and split decisions
- Tasks marked as enabling or risk-reduction tasks
- Tasks deferred from MVP or current release
- Stage 10 prompt writing order

### Assumptions to Confirm
- Any task boundary assumption
- Any implementation order assumption
- Any missing input workaround
- Any inferred file or module ownership
- Any inferred validation method

### Open Questions to Resolve
- Requirements without clear implementation path
- Tasks blocked by architecture, data, or test ambiguity
- Tasks requiring human scope judgment
- Tasks requiring technology or library confirmation

### Risks to Review
- Large or cross-cutting tasks
- Security/privacy-sensitive tasks
- Migration-sensitive tasks
- Integration-sensitive tasks
- Tasks with unclear rollback
- Tasks with weak validation evidence

### Artifacts Ready for Review
- /workflow/09_tasks/09_task_inventory.md
- /workflow/09_tasks/09_task_cards.md
- /workflow/09_tasks/09_dependency_order.md
- /workflow/09_tasks/09_traceability_matrix.md
- /workflow/09_tasks/result.md

### Recommended Next Step
- After human approval, proceed to Stage 10 Implementation Prompt Writing using the approved task cards and dependency order.
```

---

## 19. Next context_packet.md Rules

The executable SKILL must update or prepare:

```text
/workflow/context/context_packet.md
```

The update must be concise and include only information needed by Stage 10.

Required sections:

```text
# context_packet.md

## 1. Current Project State
- Current stage: 09_task_breakdown
- Completed stages:
- Next recommended stage: 10_implementation_prompt_writing

## 2. Approved Decisions
- Only human-approved decisions relevant to Stage 10.

## 3. Working Assumptions
- Task-related assumptions not yet confirmed.

## 4. Open Questions
- Questions that may block prompt writing or implementation.

## 5. Rejected / Superseded Options
- Scope or implementation options that must not be revived.

## 6. Constraints That Must Not Be Violated
- Scope constraints
- Architecture constraints
- Data constraints
- Security/privacy constraints
- Test/validation constraints
- Release ordering constraints

## 7. Key Context for Next Stage
- Approved task inventory location
- Approved task cards location
- Approved dependency order location
- Required validation command references
- Known blockers or high-risk tasks

## 8. Required Inputs for Next Stage
- /workflow/09_tasks/09_task_inventory.md
- /workflow/09_tasks/09_task_cards.md
- /workflow/09_tasks/09_dependency_order.md
- /workflow/09_tasks/09_traceability_matrix.md
- /workflow/08_test_strategy/08_validation_commands.md
- /workflow/context/TRACEABILITY_MATRIX.md
- any applicable architecture, API, data, security, or test artifacts referenced by task cards

## 9. Do Not Do
- Do not write implementation prompts for unapproved task cards.
- Do not expand MVP scope while writing implementation prompts.
- Do not ignore task dependencies.
- Do not omit tests or validation evidence from implementation prompts.
- Do not treat assumptions as approved implementation decisions.
```

---

## 20. Decision / Assumption / Open Question Rules

The executable SKILL must separate:

```text
Approved Decision:
- Only explicit human-approved decisions from DECISIONS.md, APPROVAL_LOG.md, or current user instruction.

Decision Candidate:
- Agent-proposed task boundary, task order, deferred task, or risk-reduction spike requiring approval.

Working Assumption:
- Temporary inference needed to create task candidates, such as likely module ownership or validation command applicability.

Open Question:
- Unresolved issue that may affect task scope, order, implementation prompt writing, validation, security, or release readiness.

Rejected Option:
- Explicitly rejected feature, technical path, task, release scope, or implementation approach.

Recommendation:
- Agent suggestion that must not be recorded as approved.
```

Rules:

```text
- Do not update DECISIONS.md unless explicit human approval exists.
- Do not silently treat draft Stage 9 outputs as approved.
- Do not convert inferred tasks into approved implementation work.
- Do not revive rejected features or implementation approaches.
```

---

## 21. Specialization Hooks

The executable SKILL may be extended by project-type specialization addenda.

### web_saas

May add:

```text
- frontend/backend/API coordination tasks;
- auth/session/role-based access tasks;
- deployment environment task grouping;
- analytics/observability tasks;
- production readiness tasks.
```

### internal_tool

May add:

```text
- operator workflow tasks;
- admin control tasks;
- audit and manual override tasks;
- low-friction deployment or maintenance tasks.
```

### mobile_app

May add:

```text
- platform-specific task grouping;
- offline/sync task sequencing;
- device permission tasks;
- app release or store readiness tasks.
```

### ai_data_product

May add:

```text
- dataset preparation tasks;
- model evaluation tasks;
- reproducibility tasks;
- human review tasks;
- model risk and error analysis tasks.
```

### regulated_security_sensitive

May add:

```text
- compliance evidence tasks;
- audit logging tasks;
- privacy review tasks;
- threat mitigation tasks;
- release-blocking security tasks.
```

### brownfield_legacy

May add:

```text
- codebase discovery tasks;
- compatibility tasks;
- regression protection tasks;
- incremental refactor tasks;
- migration and rollback tasks.
```

Specializations must not:

```text
- override approval rules;
- change official artifact paths without explicit instruction;
- treat project-specific assumptions as approved decisions;
- bypass validation or traceability requirements.
```

---

## 22. Tool Wrapper Hooks

Tool wrappers may define:

```text
- how to open the SKILL in Claude Code, Codex, Antigravity, or similar tools;
- where to save artifacts;
- how to run repository-specific checks;
- how to handle sandbox or permission limitations;
- how to request human review in the tool UI.
```

Tool wrappers must not define:

```text
- task scope;
- product requirements;
- architecture decisions;
- data design decisions;
- security/privacy policy;
- validation criteria;
- approval rules.
```

---

## 23. Do Not Do

The executable SKILL created from this template must not:

```text
- implement code;
- write Stage 10 implementation prompts;
- invent requirements not present in approved inputs;
- convert out-of-scope items into tasks;
- create tasks for rejected options;
- ignore approved release slices;
- ignore validation strategy;
- create tasks without required tests or validation;
- create broad tasks such as “build backend” or “implement frontend”;
- use context_packet.md as the sole source of truth;
- use unapproved draft artifacts as source of truth unless explicitly instructed;
- update DECISIONS.md without explicit human approval;
- treat task cards as approved before human review;
- read all prior workflow files by default;
- change official artifact paths without explicit instruction;
- create project-specific content while designing the reusable SKILL itself.
```

---

## 24. Failure Handling

If the executable SKILL cannot safely complete Stage 9, it must produce a blocker report.

Required blocker report structure:

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
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
- approved MVP scope is missing;
- approved requirements are missing;
- acceptance criteria are not testable;
- Stage 8 validation strategy is missing;
- architecture is too ambiguous to define task boundaries;
- task decomposition would require scope expansion;
- task dependency order depends on unresolved technical decisions;
- conflict exists between USER_DIRECTIVES.md and approved stage artifacts.
```

---

## 25. Minimum Acceptance Criteria for Generated SKILL.md

A reusable executable `SKILL.md` generated from this template is acceptable only if:

```text
[ ] It follows the core SKILL structure.
[ ] It clearly identifies Stage 9 Task Breakdown.
[ ] It defines Always Read inputs.
[ ] It defines Read If Applicable inputs.
[ ] It defines Do Not Read By Default inputs.
[ ] It defines missing input handling.
[ ] It defines mandatory Stage 9 artifacts.
[ ] It defines conditional Stage 9 artifacts.
[ ] It defines N/A record rules.
[ ] It defines task card format.
[ ] It defines task sizing rules.
[ ] It defines dependency ordering rules.
[ ] It defines traceability links from requirements/tests to tasks.
[ ] It defines context handoff to Stage 10.
[ ] It includes human approval gate.
[ ] It prohibits implementation and prompt writing.
[ ] It can run from files only in a fresh Agent session.
[ ] It avoids project-specific content.
```

---

## 26. Recommended Next Step

After creating this stage-specific template:

```text
1. Use it with the core skill template to create:
   /skills/09_task_breakdown/SKILL.md

2. Then create support files separately:
   /skills/09_task_breakdown/README.md
   /skills/09_task_breakdown/artifact_contract.yml

3. Do not execute Stage 9 until the reusable SKILL and support files are finalized.
```
