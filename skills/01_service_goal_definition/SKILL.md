---
name: service_goal_definition
description: Use this skill to define why a service should exist before requirements, stakeholder/risk framing, architecture, data design, or implementation work begins.
stage: 01_service_goal_definition
version: 1.0.0
status: draft
primary_output: /workflow/01_goal/01_service_goal.md
requires_human_approval: true
---

# Service Goal Definition SKILL

## 1. Purpose

Use this SKILL to run Stage 1 of the Manual Agentic Coding Workflow: `01_service_goal_definition`.

The purpose of this stage is to define **why the service should exist** before deciding what to build. This stage turns the approved project intake context, initial idea, product concept, or problem statement into a clear service goal that can guide later stakeholder, risk, requirements, domain, architecture, data, testing, task, and implementation work.

This SKILL must produce a concrete Stage 1 project artifact:

```text
/workflow/01_goal/01_service_goal.md
```

The service goal artifact must clarify:

- problem definition;
- target users;
- core value;
- desired outcomes;
- high-level success criteria;
- non-goals;
- initial scope boundary;
- initial assumptions;
- open questions;
- risks and ambiguities;
- human approval required.

This SKILL is not a requirements, stakeholder/risk, architecture, data, testing, task breakdown, or implementation SKILL. It must stop at goal definition and prepare context for Stage 2.

---

## 2. When to Use

Use this SKILL when:

- Stage 0 Project Intake / Existing Context Review has been completed or partially completed;
- a project idea, product concept, research plan, business memo, or problem statement exists;
- the human developer needs to define the reason for the service before detailed requirements;
- the workflow needs a clear goal artifact before stakeholder and risk framing;
- an existing draft service goal needs to be reviewed, revised, or made approval-ready.

Do not use this SKILL when:

- the task is to gather project intake information from scratch;
- the task is to identify stakeholders, roles, permissions, privacy concerns, or security risks in detail;
- the task is to write requirements or acceptance criteria;
- the task is to design architecture, data models, APIs, tests, tasks, or code;
- the human developer has not provided any service idea, Stage 0 output, user directive, or project context.

If there is no service idea, no Stage 0 artifact, and no user directive, produce a blocker report instead of inventing a service goal.

---

## 3. Operating Mode

The Agent is a structured development assistant, not an autonomous product owner or final decision-maker.

Operate in this mode:

1. Read approved context before acting.
2. Identify the current stage and its boundaries.
3. Read only the necessary inputs.
4. Apply current user instructions and Stage 1 local directives.
5. Create or update explicit Stage 1 artifacts.
6. Separate facts, approved decisions, decision candidates, working assumptions, open questions, rejected options, risks, and recommendations.
7. Prepare the minimum context needed by Stage 2.
8. End with a human approval gate.

Maintain these distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```

Stage 1’s core question is:

> Why should this service exist, for whom, what value should it provide, and how will we know at a high level that the goal is being achieved?

---

## 4. Required Inputs

### 4.1 Always Read When Available

Read these workflow context files when they exist:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/APPROVAL_LOG.md
```

Read these Stage 0 artifacts when they exist:

```text
/workflow/00_intake/00_project_intake.md
/workflow/00_intake/result.md
```

Read the Stage 1 local directive file when it exists:

```text
/workflow/01_goal/USER_DIRECTIVES.md
```

### 4.2 Required Input Checks

For each input, check and report:

- whether the file exists;
- whether the artifact is approved, draft, superseded, rejected, or unknown;
- whether it conflicts with another source;
- whether it is sufficient for Stage 1;
- whether it should be treated as source of truth, draft context, assumption, or rejected context.

### 4.3 Source of Truth Rules

Use this precedence order when inputs conflict:

```text
1. Current explicit user instruction
2. /workflow/01_goal/USER_DIRECTIVES.md
3. /workflow/context/APPROVAL_LOG.md and /workflow/context/DECISIONS.md
4. /workflow/context/artifact_manifest.yml
5. /workflow/context/context_packet.md
6. Approved stage artifacts
7. Working assumptions
8. Agent inference
```

Do not silently resolve conflicts. Report them and continue only if they are non-blocking.

---

## 5. Optional / Conditional Inputs

Read these inputs only when applicable.

### 5.1 Existing-System or Brownfield Inputs

```text
/workflow/00_intake/00_existing_context_review.md
```

Read this if Stage 0 identifies the project as brownfield, existing-system, migration, modernization, extension, maintenance, or integration work.

### 5.2 Human Review Inputs

```text
/workflow/00_intake/review_notes.md
/workflow/01_goal/review_notes.md
```

Read these if Stage 0 or a previous Stage 1 draft has human review comments.

### 5.3 Project Concept Inputs

Read project-specific source documents only when referenced by Stage 0, context files, user directives, or the current user instruction. Examples:

- project brief;
- initial idea document;
- product memo;
- research plan;
- business memo;
- opportunity brief;
- user-provided problem statement;
- product concept document;
- organization or research rationale document.

### 5.4 Specialization Addenda

Read a project-type specialization addendum if the project profile activates it. Examples:

```text
/workflow_templates/specializations/web_saas.md
/workflow_templates/specializations/internal_tool.md
/workflow_templates/specializations/mobile_app.md
/workflow_templates/specializations/ai_data_product.md
/workflow_templates/specializations/regulated_security_sensitive.md
/workflow_templates/specializations/brownfield_legacy.md
```

Specialization addenda may add questions, conditional artifacts, or validation concerns. They must not replace this SKILL.

### 5.5 Tool Wrapper Inputs

Read a tool wrapper only when the execution environment requires it. Examples:

```text
/workflow_templates/tool_wrappers/claude_code_wrapper.md
/workflow_templates/tool_wrappers/codex_wrapper.md
/workflow_templates/tool_wrappers/antigravity_wrapper.md
```

Tool wrappers may define file operations, save locations, review workflow, or sandbox constraints. They must not alter service goal reasoning, approval rules, artifact contracts, assumption handling, or traceability rules.

---

## 6. Files to Read First

Read files in this order:

1. Current explicit user instruction.
2. This SKILL file.
3. `/workflow/context/artifact_manifest.yml`, if available.
4. `/workflow/context/context_packet.md`, if available.
5. `/workflow/context/DECISIONS.md`, if available.
6. `/workflow/context/APPROVAL_LOG.md`, if available.
7. `/workflow/context/ASSUMPTIONS.md`, if available.
8. `/workflow/context/OPEN_QUESTIONS.md`, if available.
9. `/workflow/context/REJECTED_OPTIONS.md`, if available.
10. `/workflow/01_goal/USER_DIRECTIVES.md`, if available.
11. `/workflow/00_intake/00_project_intake.md`, if available.
12. `/workflow/00_intake/result.md`, if available.
13. Conditional Stage 0, project brief, review, specialization, or tool wrapper inputs.

Do not read all project files by default.

---

## 7. USER_DIRECTIVES.md Handling

If `/workflow/01_goal/USER_DIRECTIVES.md` exists, read it before drafting or revising the service goal.

Classify each directive as one of:

- explicit approval;
- correction;
- preference;
- new input;
- rejection;
- scope change;
- question;
- constraint;
- review comment.

Rules:

- Apply `USER_DIRECTIVES.md` before Agent assumptions.
- Do not automatically treat every directive as a globally approved decision.
- If a directive explicitly approves a Stage 1 decision, record the approval source in `01_service_goal.md` and `result.md`.
- If a directive conflicts with `DECISIONS.md`, `APPROVAL_LOG.md`, Stage 0 artifacts, or rejected options, report the conflict.
- Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.
- Do not use `USER_DIRECTIVES.md` to bypass the human approval gate unless the directive explicitly grants approval or permission to continue with draft status.

---

## 8. Input Preflight Procedure

Before producing outputs, perform this preflight checklist and summarize the result in `/workflow/01_goal/result.md`.

```text
[ ] Confirmed this is Stage 1: 01_service_goal_definition.
[ ] Confirmed the task is goal definition, not requirements, architecture, data, test, task, or implementation work.
[ ] Read current user instruction.
[ ] Read this SKILL.md.
[ ] Checked /workflow/context/artifact_manifest.yml if available.
[ ] Checked /workflow/context/context_packet.md if available.
[ ] Checked /workflow/context/DECISIONS.md if available.
[ ] Checked /workflow/context/APPROVAL_LOG.md if available.
[ ] Checked /workflow/context/ASSUMPTIONS.md if available.
[ ] Checked /workflow/context/OPEN_QUESTIONS.md if available.
[ ] Checked /workflow/context/REJECTED_OPTIONS.md if available.
[ ] Checked /workflow/01_goal/USER_DIRECTIVES.md if available.
[ ] Checked /workflow/00_intake/00_project_intake.md if available.
[ ] Checked /workflow/00_intake/result.md if available.
[ ] Activated conditional inputs based on project profile and context.
[ ] Verified source artifact existence and approval state.
[ ] Identified missing, draft, superseded, rejected, or conflicting inputs.
[ ] Determined whether missing information is blocking or non-blocking.
[ ] Restated the Stage 1 task before drafting artifacts.
```

### Missing Input Handling

If Stage 0 intake is missing:

- report it as a potential blocker;
- explain why it matters;
- continue only if enough initial idea, project context, or user directive exists;
- mark all inferred project context as working assumptions.

If there is no service idea, no Stage 0 artifact, and no user directive:

- do not invent a service goal;
- produce a blocker report;
- request the minimum human input needed.

If inputs conflict:

- identify the conflicting sources;
- explain the impact;
- do not silently choose one source;
- stop if the conflict affects the service goal, primary users, success criteria, non-goals, or major scope boundaries.

---

## 9. Execution Procedure

Follow these steps.

### Step 1. Confirm Stage 1 Purpose

State that this stage defines why the service should exist before deciding what to build.

Also state that Stage 1 must not create:

- detailed requirements;
- acceptance criteria;
- stakeholder/risk analysis;
- domain model;
- architecture;
- data design;
- test strategy;
- task breakdown;
- implementation prompts;
- code.

### Step 2. Read Workflow Context and Stage 0 Artifacts

Use the input rules above. Identify:

- project type;
- baseline context;
- fixed constraints;
- approved decisions;
- known assumptions;
- known open questions;
- rejected options;
- forbidden change areas;
- initial project idea or concept source.

### Step 3. Check Stage 1 User Directives

Read `/workflow/01_goal/USER_DIRECTIVES.md` if available and classify its content.

### Step 4. Identify Missing, Conflicting, Draft, Superseded, or Rejected Inputs

Report all issues clearly. Decide whether each issue is blocking or non-blocking.

### Step 5. Restate the Stage 1 Task

Write a short task restatement in `result.md`, including whether the service goal will be drafted, revised, or blocked.

### Step 6. Extract Candidate Problem Statements

Identify candidate problem statements from approved context and referenced project inputs.

For each candidate, separate:

- source evidence;
- Agent interpretation;
- working assumptions;
- open questions.

Avoid turning features into the problem statement.

### Step 7. Identify Candidate Target Users

Identify:

- primary users;
- secondary users;
- excluded users or non-targets;
- uncertain user groups.

Mark each as approved, candidate, assumed, unresolved, rejected, or superseded.

Do not convert user groups into finalized stakeholder roles. Stage 2 handles stakeholders and risk framing.

### Step 8. Identify Core Value and Desired Outcomes

Identify:

- user value;
- project value;
- business, research, operational, or organizational value, if applicable;
- desired user outcomes;
- desired project outcomes;
- desired organizational or research outcomes, if applicable.

### Step 9. Draft Goal Options if Direction Is Ambiguous

If multiple plausible service goal directions exist, create:

```text
/workflow/01_goal/01_goal_options.md
```

Compare goal options by:

- problem fit;
- target user clarity;
- value clarity;
- scope control;
- alignment with approved constraints;
- risk and ambiguity;
- suitability for Stage 2.

Do not mark a recommended option as approved.

### Step 10. Recommend a Service Goal as a Decision Candidate

Select one recommended service goal only as a decision candidate.

Mark it clearly:

```text
Decision Candidate, not approved.
```

### Step 11. Define High-Level Success Criteria

Define qualitative success criteria and quantitative success criteria if available.

Success criteria must be high-level and reviewable.

Do not write acceptance criteria, test cases, or validation commands.

### Step 12. Define Non-Goals and Scope Boundaries

Define:

- explicit non-goals;
- deferred goals;
- rejected or superseded goal directions;
- major scope boundaries;
- what Stage 1 includes;
- what Stage 1 does not decide;
- what must be deferred to later stages.

### Step 13. Separate Assumptions, Open Questions, Risks, and Rejected Options

Use stable IDs:

```text
A-001, A-002, ... for assumptions
Q-001, Q-002, ... for open questions
R-001, R-002, ... for risks
G-001, G-002, ... for goals
```

Update persistent context files only when applicable.

### Step 14. Define Goal-Level Traceability

Create or update goal-level traceability connecting:

```text
Goal → Problem Statement → Target Users → Core Value → Success Criteria
```

Do not create requirements, acceptance criteria, domain, architecture, data, test, task, or implementation traceability unless such items already exist as approved upstream constraints.

### Step 15. Produce or Update Stage 1 Artifacts

Create or update:

```text
/workflow/01_goal/01_service_goal.md
/workflow/01_goal/result.md
/workflow/context/context_packet.md
```

Update these if applicable:

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Do not update `/workflow/context/DECISIONS.md` unless explicit human approval exists.

### Step 16. Prepare Context for Stage 2

Update `/workflow/context/context_packet.md` with the minimum operational context needed by Stage 2 Stakeholder & Risk Framing.

Do not perform Stage 2.

### Step 17. Present the Human Approval Gate

End with the required Human Approval section.

---

## 10. Output Artifacts

### 10.1 Mandatory Artifacts

Create or update these artifacts:

```text
/workflow/01_goal/01_service_goal.md
/workflow/01_goal/result.md
/workflow/context/context_packet.md
```

Create or update when applicable:

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

### 10.2 Conditional Artifacts

Create only when applicable:

```text
/workflow/01_goal/01_goal_options.md
```

Use when multiple plausible service goal directions exist.

```text
/workflow/01_goal/01_success_metrics.md
```

Use when success criteria require separate elaboration.

```text
/workflow/01_goal/01_non_goals.md
```

Use when non-goals are complex, contentious, or important for scope control.

```text
/workflow/01_goal/review_notes.md
```

Use when summarizing human review comments.

```text
/workflow/context/REJECTED_OPTIONS.md
```

Use when options are explicitly rejected or superseded.

### 10.3 N/A Record Rules

If a conditional artifact is not created, record this in `/workflow/01_goal/result.md`:

```markdown
| Conditional artifact | Why not applicable now | Revisit if |
|---|---|---|
| /workflow/01_goal/01_goal_options.md | ... | ... |
```

Do not silently omit conditional artifacts.

### 10.4 Artifact Status Rules

Every artifact created or updated by this SKILL must state one of:

- `Draft`
- `Needs Review`
- `Approved`
- `Blocked`

Use `Approved` only when explicit human approval exists.

---

## 11. Required Structure of `01_service_goal.md`

Create or update `/workflow/01_goal/01_service_goal.md` using this structure.

```markdown
# 01 Service Goal

## 1. Status

- Status: Draft / Approved / Needs Review / Blocked
- Stage: 01_service_goal_definition
- Primary output: /workflow/01_goal/01_service_goal.md
- Source artifacts used:
- Source approval state:
- Explicit approvals applied:
- Supersedes:
- Last updated:

## 2. Problem Definition

### Problem Statement

### Who Experiences the Problem

### Current Pain or Opportunity

### Why Now

### Evidence or Source Basis

### Uncertainty

## 3. Target Users

### Primary Users

| User group | Status | Source | Notes |
|---|---|---|---|

### Secondary Users

| User group | Status | Source | Notes |
|---|---|---|---|

### Excluded Users or Non-Targets

| User group | Reason excluded | Source | Status |
|---|---|---|---|

## 4. Core Value Proposition

### Value Delivered

### User Benefit

### Business / Research / Operational / Organizational Benefit

### Value Not Being Pursued

## 5. Desired Outcomes

### User Outcomes

### Project Outcomes

### Organizational or Research Outcomes

## 6. Success Criteria

| Criterion ID | Success criterion | Type | Status | Source | High-level validation approach |
|---|---|---|---|---|---|

Guidance:
- Type: qualitative / quantitative / mixed
- Status: approved / decision candidate / assumption / open question

## 7. Non-Goals

| Non-Goal ID | Non-goal | Reason | Status | Source |
|---|---|---|---|---|

## 8. Initial Scope Boundary

### What Stage 1 Includes

### What Stage 1 Does Not Decide

### What Must Be Deferred to Later Stages

### Approved Constraints Inherited from Stage 0

### Scope Ambiguities

## 9. Initial Assumptions

| Assumption ID | Assumption | Why it is needed | Risk if wrong | How it can be confirmed | Status |
|---|---|---|---|---|---|

## 10. Open Questions

| Question ID | Question | Why it matters | Blocking or non-blocking | Suggested next step | Affected future stages |
|---|---|---|---|---|---|

## 11. Risks and Ambiguities

| Risk ID | Description | Impacted future stages | Severity | Mitigation or follow-up |
|---|---|---|---|---|

## 12. Goal-Level Traceability

| Goal ID | Problem reference | Target users | Core value | Success criteria | Assumptions | Open questions | Status |
|---|---|---|---|---|---|---|---|

## 13. Human Approval Required

### Decisions to Approve

- Service goal:
- Primary users:
- Success criteria:
- Non-goals:
- Major scope boundaries:

### Assumptions to Confirm

### Open Questions to Resolve

### Risks to Review

### Recommended Next Stage

Proceed to Stage 2 Stakeholder & Risk Framing only after human approval, or after explicit human permission to continue with draft status.
```

---

## 12. Required Structure of `result.md`

Create or update `/workflow/01_goal/result.md` using this structure.

```markdown
# Result: 01 Service Goal Definition

## 1. Task Summary

## 2. Inputs Used

| Input | Exists | Approval state | How used | Notes |
|---|---:|---|---|---|

## 3. Missing or Unavailable Inputs

| Input | Blocking? | Why it matters | Handling |
|---|---|---|---|

## 4. Outputs Created or Updated

| Output | Created / Updated / N/A | Status | Notes |
|---|---|---|---|

## 5. Key Findings

## 6. Decision Candidates

| Decision ID | Candidate decision | Why recommended | Approval needed |
|---|---|---|---|

## 7. Working Assumptions

| Assumption ID | Assumption | Why needed | Risk if wrong | Confirmation path |
|---|---|---|---|---|

## 8. Open Questions

| Question ID | Question | Blocking? | Affected stages | Suggested next step |
|---|---|---|---|---|

## 9. Risks and Constraints

| Risk / Constraint ID | Description | Source | Impact | Follow-up |
|---|---|---|---|---|

## 10. Rejected or Superseded Options

| Option ID | Option | Rejected / Superseded | Source | Do-not-reopen condition |
|---|---|---|---|---|

## 11. N/A Records for Conditional Artifacts

| Conditional artifact | Why not applicable now | Revisit if |
|---|---|---|

## 12. Traceability Updates

| Traceability item | Status | Notes |
|---|---|---|

## 13. Human Approval Required

### Decisions to Approve

### Assumptions to Confirm

### Open Questions to Resolve

### Risks to Review

### Artifacts Ready for Review

- /workflow/01_goal/01_service_goal.md
- /workflow/01_goal/result.md

### Recommended Next Step
```

---

## 13. Traceability Rules

### 13.1 Goal IDs

Use stable goal IDs:

```text
G-001, G-002, G-003, ...
```

Do not rename goal IDs casually. If a goal is replaced, mark the previous goal as superseded or rejected rather than silently reusing the ID.

### 13.2 Required Stage 1 Traceability

Each goal must link to:

- problem statement;
- target users;
- core value proposition;
- success criteria;
- assumptions affecting the goal;
- open questions affecting the goal;
- non-goals or scope boundaries when relevant.

Recommended format:

```markdown
| Goal ID | Problem reference | Target users | Core value | Success criteria | Assumptions | Open questions | Status |
|---|---|---|---|---|---|---|---|
```

### 13.3 Future Traceability Preparation

Prepare for future links:

```text
Goal → Requirements
Goal → Acceptance Criteria
Goal → Stakeholders / Risks
Goal → MVP Scope
Goal → Test Strategy
Goal → Tasks
Goal → Implementation Evidence
```

Do not create downstream artifacts or downstream traceability prematurely.

### 13.4 TRACEABILITY_MATRIX.md Updates

If `/workflow/context/TRACEABILITY_MATRIX.md` exists, update only goal-level entries.

If it does not exist and goal-level traceability is available, create a minimal goal-level traceability section.

Do not add requirements, acceptance criteria, architecture, data, test, task, or implementation links unless they already exist as approved upstream constraints.

---

## 14. Decision / Assumption / Open Question Rules

### 14.1 Approved Decision

Use `Approved Decision` only when explicit human approval exists.

For Stage 1, explicit approval is required for:

- service goal;
- primary users;
- success criteria;
- non-goals;
- major scope boundaries.

Do not infer approval from silence, file existence, or Agent confidence.

### 14.2 Decision Candidate

Use `Decision Candidate` when recommending a goal direction, user focus, success criterion, non-goal, or scope boundary that needs human approval.

Decision candidates must appear in:

- `/workflow/01_goal/01_service_goal.md`;
- `/workflow/01_goal/result.md`;
- the final Human Approval Required section.

### 14.3 Working Assumption

Use `Working Assumption` when progress requires a temporary belief not yet confirmed.

Record:

- assumption ID;
- assumption statement;
- why it is needed;
- risk if wrong;
- how it can be confirmed.

Do not convert assumptions into service goals, requirements, or approved decisions.

### 14.4 Open Question

Use `Open Question` when unresolved information may affect:

- stakeholders;
- risks;
- requirements;
- scope;
- privacy;
- security;
- implementation direction;
- project viability.

Open questions must not be hidden inside assumptions.

### 14.5 Rejected or Superseded Option

Use `Rejected Option` or `Superseded Option` when a goal direction, user group, scope boundary, or value proposition has been explicitly rejected or replaced.

Record these in `/workflow/context/REJECTED_OPTIONS.md` if applicable.

Do not revive rejected options unless the human developer explicitly reopens them.

### 14.6 Stage 1-Specific Prohibitions

Do not:

- convert assumptions into service goals;
- convert success criteria into acceptance criteria;
- convert user groups into finalized stakeholder roles;
- convert value propositions into requirements;
- record Agent-generated recommendations in `DECISIONS.md`;
- treat draft artifacts as approved.

---

## 15. Context Packet Update Rules

Update `/workflow/context/context_packet.md` for Stage 2 Stakeholder & Risk Framing.

`context_packet.md` is a navigation layer, not a full project history. Keep it concise and point to source artifacts.

Use this structure:

```markdown
# context_packet.md

## 1. Current Project State

- Current stage: 01_service_goal_definition
- Completed stages:
- Next recommended stage: 02_stakeholder_risk_framing
- Stage 1 artifact status: Draft / Approved / Needs Review / Blocked

## 2. Approved Decisions

Only include decisions explicitly approved by the human developer.

## 3. Working Assumptions

Include assumptions relevant to Stage 2, especially those affecting users, stakeholders, privacy, security, scope, data sensitivity, external systems, or organizational constraints.

## 4. Open Questions

Include unresolved questions affecting stakeholders, security, privacy, requirements, scope, external systems, or risk analysis.

## 5. Rejected / Superseded Options

Include rejected or superseded goal directions, user groups, value propositions, success criteria, non-goals, or scope boundaries.

## 6. Constraints That Must Not Be Violated

- Technology:
- Security:
- Privacy:
- Scope:
- Schedule:
- Operational:
- Research or organizational:

## 7. Key Context for Next Stage

Include:
- service goal summary;
- primary and secondary users;
- excluded users or non-targets;
- core value proposition;
- success criteria summary;
- non-goals;
- risks and ambiguities relevant to stakeholder and risk framing.

## 8. Required Inputs for Next Stage

Stage 2 should read:

- /workflow/01_goal/01_service_goal.md
- /workflow/01_goal/result.md
- /workflow/context/context_packet.md
- /workflow/context/DECISIONS.md
- /workflow/context/ASSUMPTIONS.md
- /workflow/context/OPEN_QUESTIONS.md
- /workflow/context/REJECTED_OPTIONS.md
- /workflow/context/TRACEABILITY_MATRIX.md

Read if applicable:

- /workflow/01_goal/01_goal_options.md
- /workflow/01_goal/01_success_metrics.md
- /workflow/01_goal/01_non_goals.md
- /workflow/00_intake/00_project_intake.md
- /workflow/00_intake/result.md
- /workflow/00_intake/00_existing_context_review.md

## 9. Do Not Do

- Do not treat draft service goals as approved.
- Do not ignore unresolved assumptions.
- Do not revive rejected goal directions.
- Do not convert target users into permission roles without Stage 2 analysis.
- Do not create requirements before stakeholder and risk framing.
- Do not make architecture, data, test, task, or implementation decisions.
```

---

## 16. Human Approval Gate

End every successful or partially successful Stage 1 run with this section.

```markdown
## Human Approval Required

### Decisions to Approve

- Service goal:
- Primary users:
- Success criteria:
- Non-goals:
- Major scope boundaries:

### Assumptions to Confirm

- ...

### Open Questions to Resolve

- ...

### Risks to Review

- ...

### Artifacts Ready for Review

- /workflow/01_goal/01_service_goal.md
- /workflow/01_goal/result.md

Additional conditional artifacts, if created:

- /workflow/01_goal/01_goal_options.md
- /workflow/01_goal/01_success_metrics.md
- /workflow/01_goal/01_non_goals.md

### Recommended Next Step

Choose one:

- Approve Stage 1 and proceed to Stage 2 Stakeholder & Risk Framing.
- Revise Stage 1 before proceeding.
- Continue to Stage 2 with draft status by explicit human permission.
- Stop due to blocker.
```

Rules:

- Do not claim approval unless the human explicitly approved the item.
- Do not proceed to Stage 2 as if approval has been granted.
- If the human allows continuation with draft status, record that instruction clearly in `result.md` and `context_packet.md`.

---

## 17. Validation Checklist

Before completing Stage 1, verify:

```text
[ ] The service goal explains why the service should exist.
[ ] The goal is not merely a feature list.
[ ] The problem definition is explicit.
[ ] Target users are explicit.
[ ] Primary users are separated from secondary users.
[ ] Excluded users or non-targets are listed when relevant.
[ ] Core value is clear.
[ ] Desired outcomes are stated at a high level.
[ ] Success criteria are reviewable.
[ ] Success criteria are not detailed acceptance criteria.
[ ] Non-goals are explicit enough to reduce scope creep.
[ ] Initial scope boundaries are clear.
[ ] Approved decisions are separated from decision candidates.
[ ] Assumptions are clearly marked.
[ ] Open questions are separated from assumptions.
[ ] Risks and ambiguities are identified without performing full Stage 2 risk analysis.
[ ] Rejected or superseded options are recorded when applicable.
[ ] No requirements are prematurely created.
[ ] No acceptance criteria are prematurely written.
[ ] No stakeholder/risk analysis is performed.
[ ] No domain model is created.
[ ] No architecture or implementation choices are made.
[ ] No data model is created.
[ ] No test strategy is created.
[ ] Existing approved constraints from Stage 0 are respected.
[ ] Goal-level traceability uses stable goal IDs.
[ ] context_packet.md prepares Stage 2 without becoming a full project history.
[ ] The human approval gate is present.
[ ] Stage 2 can use the prepared context to begin stakeholder and risk framing.
```

If any checklist item fails, record the issue in `result.md` and mark the artifact as `Needs Review` or `Blocked` as appropriate.

---

## 18. Failure Handling

If Stage 1 cannot be completed safely, produce a partial result and blocker report instead of pretending completion.

Failure cases include:

- required Stage 0 context is missing and no service idea exists;
- user directive conflicts with approved decisions;
- artifact manifest marks a needed artifact as superseded or rejected;
- source artifacts conflict on service goal, primary users, success criteria, non-goals, or scope boundaries;
- project idea is too vague to define a service goal;
- privacy, security, legal, ethical, or organizational ambiguity makes goal framing unsafe;
- required files cannot be found;
- the Agent cannot determine whether an input is approved or draft.

Use this blocker report format in `/workflow/01_goal/result.md`:

```markdown
## Blocker Report

### Blocking Issue

### Why It Matters

### Affected Artifacts or Stages

### Safe Partial Work Completed

### Human Decision Needed

### Minimum Input Needed to Continue
```

If progress is possible with assumptions, proceed only with explicitly marked working assumptions and label the output as `Draft` or `Needs Review`.

---

## 19. Specialization Addendum Hook

If a project-type specialization addendum is active, apply it after the core Stage 1 procedure.

Specialization addenda may add:

- additional inputs;
- additional goal-framing questions;
- additional non-goal categories;
- additional risks and ambiguities;
- additional conditional artifacts;
- additional approval requirements.

They must not replace this SKILL or weaken its rules.

### 19.1 web_saas

Clarify, if applicable:

- customer value;
- tenant value;
- admin value;
- end-user value;
- buyer vs user distinction;
- multi-tenant boundary;
- onboarding or subscription goal assumptions.

### 19.2 internal_tool

Clarify, if applicable:

- operator value;
- organizational workflow value;
- internal process improvement;
- manual work reduced;
- reporting or audit value;
- affected internal teams.

### 19.3 mobile_app

Clarify, if applicable:

- end-user value;
- device context;
- platform constraints;
- offline or on-device expectations;
- app usage context;
- platform-specific non-goals.

### 19.4 ai_data_product

Clarify, if applicable:

- data source;
- evaluation purpose;
- model output value;
- human review value;
- decision-support vs automation boundary;
- research or production intent;
- unacceptable model failure modes at goal level.

### 19.5 regulated_security_sensitive

Clarify, if applicable:

- compliance-sensitive goals;
- privacy-sensitive goals;
- sensitive user groups;
- high-level risk boundaries;
- auditability expectations;
- forbidden uses;
- human oversight expectations.

### 19.6 brownfield_legacy

Clarify, if applicable, whether the goal is:

- replacement;
- extension;
- migration;
- modernization;
- maintenance;
- integration;
- operational stabilization.

Treat existing-system constraints as hard boundaries unless the human developer explicitly approves change.

---

## 20. Tool Wrapper Hook

Tool wrappers may specify:

- file creation commands;
- save location;
- review workflow;
- sandbox constraints;
- permission constraints;
- command invocation style;
- artifact display conventions.

Tool wrappers must not change:

- service goal reasoning;
- approval rules;
- artifact contract;
- assumption handling;
- open question handling;
- rejected option handling;
- traceability rules;
- Stage 1 boundaries.

If a tool wrapper conflicts with this SKILL, report the conflict and follow human instruction or approved workflow rules.

---

## 21. Do Not Do

Do not:

- treat the Agent as the final decision-maker;
- treat draft artifacts as approved;
- treat assumptions as approved decisions;
- treat recommendations as requirements;
- update `/workflow/context/DECISIONS.md` without explicit human approval;
- ignore `/workflow/01_goal/USER_DIRECTIVES.md`;
- ignore `/workflow/context/artifact_manifest.yml` when available;
- use superseded or rejected artifacts as current truth;
- read all historical files by default;
- use `context_packet.md` as the only source of truth;
- revive rejected options without explicit human instruction;
- collapse Stage 1 and Stage 2;
- redo Stage 0 intake unless Stage 0 is missing or insufficient;
- create requirements;
- create acceptance criteria;
- create stakeholder/risk analysis;
- create domain models;
- create architecture;
- choose database or technical stack unless already approved in Stage 0;
- create data design;
- create test strategy;
- create task breakdown;
- create implementation prompts;
- inspect or edit implementation code;
- write code;
- claim approval unless approval is explicit;
- proceed to Stage 2 as if approval has been granted.

---

## 22. Quality Checklist

Before considering this SKILL run complete, verify:

```text
[ ] Required metadata is present.
[ ] The SKILL was used for Stage 1 only.
[ ] Required inputs were checked.
[ ] Conditional inputs were activated only when applicable.
[ ] Missing input handling was applied.
[ ] USER_DIRECTIVES.md was checked if available.
[ ] Source approval states were checked.
[ ] Conflicts were reported.
[ ] /workflow/01_goal/01_service_goal.md was created or updated, unless blocked.
[ ] /workflow/01_goal/result.md was created or updated.
[ ] /workflow/context/context_packet.md was prepared for Stage 2.
[ ] ASSUMPTIONS.md was updated if assumptions exist.
[ ] OPEN_QUESTIONS.md was updated if open questions exist.
[ ] REJECTED_OPTIONS.md was updated if options were rejected or superseded.
[ ] TRACEABILITY_MATRIX.md was updated if goal-level traceability is available.
[ ] Conditional artifacts were created or marked N/A.
[ ] Approved decisions, decision candidates, assumptions, open questions, rejected options, risks, and recommendations are separated.
[ ] Goal IDs use stable IDs such as G-001.
[ ] No requirements were created.
[ ] No acceptance criteria were created.
[ ] No stakeholder/risk analysis was performed.
[ ] No architecture, data design, test strategy, task breakdown, implementation prompt, or code was created.
[ ] Human approval gate is present.
[ ] Recommended next step is clear.
```

If any item fails, document the issue in `/workflow/01_goal/result.md` and mark the Stage 1 artifact as `Needs Review` or `Blocked`.
