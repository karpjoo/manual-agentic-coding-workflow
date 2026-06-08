# 01 Service Goal Skill Template

This file is a **stage-specific SKILL template** for the Manual Agentic Coding Workflow.

It is used at design time to create a future executable reusable SKILL for Stage 1.  
It is not itself an executable `SKILL.md`, and it must not be run directly as a project execution prompt.

---

## 1. Template Metadata

| Field | Value |
|---|---|
| Template name | `01_service_goal_skill_template` |
| Target stage | `01_service_goal_definition` |
| Template status | Draft |
| Template layer | Stage-Specific Skill Template |
| Intended future executable SKILL path | `/skills/01_service_goal_definition/SKILL.md` |
| Intended primary project artifact | `/workflow/01_goal/01_service_goal.md` |
| Approval required | Yes |
| Default project baseline | Greenfield MVP production project |
| Depends on core template | Yes. This template extends the core skill template and must not replace or weaken it. |
| Project-specific content allowed | No |
| Executable artifact creation allowed | No. This template only defines the contract for future execution. |

This template defines only the Stage 1-specific extension.  
The future executable SKILL must also follow the shared core rules for input precedence, artifact handling, approval gates, context updates, failure handling, and decision / assumption / open question separation.

---

## 2. Stage Purpose

Stage 1 defines **why the service should exist** before the workflow decides what to build. Its purpose is to convert the initial project context, idea, or opportunity into a clear service goal that can guide all later stages.

This stage should clarify the problem, the target users, the core value proposition, desired outcomes, high-level success criteria, non-goals, initial assumptions, and open questions. It should help the human developer decide whether the project direction is meaningful, reviewable, and bounded enough to proceed.

Stage 1 is not a requirements stage. It must not produce detailed functional requirements, acceptance criteria, domain models, architecture decisions, data models, test plans, task cards, or implementation prompts. Those belong to later stages.

The future executable Stage 1 SKILL should produce a concrete project artifact that Stage 2 can use for stakeholder and risk framing. The output may remain in draft status until the human developer explicitly approves the service goal, primary users, success criteria, non-goals, and major scope boundaries.

---

## 3. Core Question

Stage 1 must answer the following central question:

> Why should this service exist, for whom, what value should it provide, and how will we know at a high level that the goal is being achieved?

Supporting questions:

- What problem, opportunity, or need motivates the service?
- Who is the service primarily for?
- What user, business, research, operational, or organizational value should the service provide?
- What high-level outcomes would indicate that the service is succeeding?
- What should explicitly not be included in the service goal?
- What assumptions are being used to draft the goal?
- What open questions must be resolved before later stages can safely make requirements, risk, architecture, data, or implementation decisions?

---

## 4. Stage Position in the Workflow

### 4.1 What Stage 1 Receives from Stage 0

Stage 1 receives initial context from Stage 0 Project Intake / Existing Context Review, including:

- project type;
- greenfield, brownfield, prototype, research tool, or production MVP classification;
- fixed constraints;
- existing documents or references;
- already-approved decisions;
- known forbidden change areas;
- initial project idea or source material;
- context handoff prepared for Stage 1;
- human review notes, if any.

Stage 1 must use Stage 0 as context, but must not redo project intake unless Stage 0 is missing, contradictory, or insufficient for defining a service goal.

### 4.2 What Stage 1 Must Produce

Stage 1 must define a clear service goal artifact containing:

- problem definition;
- target users;
- core value proposition;
- desired outcomes;
- high-level success criteria;
- non-goals;
- initial scope boundary;
- assumptions;
- open questions;
- risks and ambiguities;
- human approval items.

The primary future project artifact is:

- `/workflow/01_goal/01_service_goal.md`

The future executable SKILL must also produce or update supporting workflow context artifacts as defined in this template.

### 4.3 What Stage 1 Must Pass to Stage 2

Stage 1 must prepare enough context for Stage 2 Stakeholder & Risk Framing to identify:

- stakeholders;
- user roles;
- operators and administrators;
- external systems;
- sensitive or personal data concerns;
- privacy concerns;
- early security risks;
- scope risks;
- unresolved questions affecting stakeholders or risk.

Stage 1 must not perform full stakeholder analysis or full risk analysis. It should only prepare the goal-level context that Stage 2 needs.

### 4.4 What Stage 1 Must Not Decide

Stage 1 must not decide:

- detailed functional requirements;
- acceptance criteria;
- detailed user stories;
- finalized stakeholder roles or permission models;
- domain entities, aggregates, or bounded contexts;
- architecture style;
- frontend/backend boundaries;
- database choice or schema;
- API contracts;
- test strategy;
- release slicing;
- implementation tasks;
- code changes.

Exception: if Stage 0 already contains explicitly approved constraints, Stage 1 may reference them as constraints but must not reinterpret or expand them.

---

## 5. Always Read Inputs

The future executable Stage 1 SKILL should always check and read the following files when available.

Availability, artifact status, approval state, supersession state, and conflicts must be checked before using any file as source of truth.

### 5.1 Workflow Context Files

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/APPROVAL_LOG.md`

### 5.2 Stage 0 Inputs

- `/workflow/00_intake/00_project_intake.md`
- `/workflow/00_intake/result.md`

### 5.3 Stage 1 Local Human Directives

- `/workflow/01_goal/USER_DIRECTIVES.md`, if available

### 5.4 Reading Rules

The future executable SKILL must:

- confirm whether each file exists;
- confirm whether source artifacts are approved, draft, superseded, rejected, or unknown;
- use approved decisions as source of truth;
- treat unapproved artifacts as draft context only;
- treat assumptions as assumptions, not decisions;
- treat open questions as unresolved, not implicitly answered;
- treat rejected options as forbidden unless explicitly reopened by the human developer;
- report conflicts instead of silently resolving them.

---

## 6. Read If Applicable Inputs

The future executable Stage 1 SKILL should read the following only when applicable.

### 6.1 Brownfield or Existing-System Inputs

- `/workflow/00_intake/00_existing_context_review.md` — if Stage 0 identifies a brownfield project, existing system, migration, modernization, extension, or maintenance project.
- Existing system overview, product documentation, or codebase summary — if Stage 0 references these as approved inputs.

### 6.2 Human Review Inputs

- `/workflow/00_intake/review_notes.md` — if Stage 0 has human review comments.
- `/workflow/01_goal/review_notes.md` — if revising a previous Stage 1 draft after human review.

### 6.3 Project Idea or Concept Inputs

Read referenced documents if they exist and are identified by Stage 0, context files, or user directives:

- project brief;
- initial idea document;
- product memo;
- research plan;
- business memo;
- opportunity brief;
- user-provided problem statement;
- user-provided product concept document;
- market, organization, or research rationale document.

### 6.4 Specialization Addenda

Read specialization addenda if the project profile activates them, for example:

- `/workflow_templates/specializations/web_saas.md`
- `/workflow_templates/specializations/internal_tool.md`
- `/workflow_templates/specializations/mobile_app.md`
- `/workflow_templates/specializations/ai_data_product.md`
- `/workflow_templates/specializations/regulated_security_sensitive.md`
- `/workflow_templates/specializations/brownfield_legacy.md`

Specialization addenda may add questions, context needs, or conditional artifacts, but must not replace this Stage 1 template.

### 6.5 Tool Wrapper Inputs

Read tool wrapper guidance only if the execution environment requires it, for example:

- Claude Code wrapper;
- Codex wrapper;
- Antigravity wrapper;
- other agentic coding tool wrapper.

Tool wrappers may define file commands and execution conventions, but must not alter Stage 1 reasoning, approval rules, artifact contracts, assumption handling, or traceability rules.

---

## 7. Do Not Read By Default

Stage 1 should not read the following by default:

- downstream requirements artifacts;
- acceptance criteria artifacts;
- domain modeling artifacts;
- architecture artifacts;
- data design artifacts;
- MVP release slicing artifacts;
- test strategy artifacts;
- task breakdown artifacts;
- implementation prompt artifacts;
- implementation files;
- full codebase;
- raw agent logs;
- superseded drafts;
- rejected drafts;
- unrelated historical files;
- unrelated project artifacts from prior projects.

Stage 1 is a goal-definition stage, not an implementation, design, or requirements stage.

Reading too much downstream or implementation material can cause the Agent to prematurely design the solution, revive rejected options, or convert technical assumptions into service goals. The future executable SKILL should read only the inputs necessary to define the reason for the service and prepare Stage 2 context.

---

## 8. Missing Input Handling

The future executable Stage 1 SKILL must handle missing inputs explicitly.

### 8.1 Stage 0 Missing

If `/workflow/00_intake/00_project_intake.md` or `/workflow/00_intake/result.md` is missing:

- report the missing Stage 0 input as a potential blocker;
- explain why Stage 0 matters for defining the service goal;
- check whether enough initial idea, user directive, or approved context exists to continue safely;
- if continuing, mark all inferred context as working assumptions;
- do not claim that Stage 0 has been completed.

### 8.2 Enough Initial Context Exists

If Stage 0 is incomplete but there is enough user-provided initial idea or project context:

- continue only with clearly labeled assumptions;
- record assumptions in the Stage 1 artifact and `/workflow/context/ASSUMPTIONS.md`;
- record missing or uncertain information in `/workflow/context/OPEN_QUESTIONS.md`;
- mark the Stage 1 artifact as `Draft` or `Needs Review`.

### 8.3 No Service Idea or Context Exists

If there is:

- no service idea;
- no Stage 0 artifact;
- no user directive;
- no project brief;
- no product concept;
- no problem statement;

then the future executable SKILL must produce a blocker report rather than inventing a service goal.

The blocker report should include:

- missing input;
- why it matters;
- affected artifacts or stages;
- minimum human input needed;
- safe partial work completed, if any.

### 8.4 Conflicting Inputs

If Stage 0 artifacts, context files, `USER_DIRECTIVES.md`, approved decisions, or rejected options conflict:

- report the conflict explicitly;
- identify all conflicting sources;
- explain the impact on the service goal;
- do not silently choose one source;
- continue only if the conflict does not affect the service goal, target users, success criteria, non-goals, or major scope boundaries;
- otherwise mark the issue as blocking and request human decision.

### 8.5 Draft or Unapproved Inputs

If an input is available but not approved:

- use it only as draft context;
- do not record it as an approved decision;
- identify which conclusions depend on the draft input;
- request human approval if the draft input affects the service goal.

---

## 9. Mandatory Artifacts

This template does not create project artifacts. It defines the contract that the future executable Stage 1 SKILL must follow.

The future executable SKILL must create or update the following project artifacts:

### 9.1 Primary Stage Artifact

- `/workflow/01_goal/01_service_goal.md` — primary Stage 1 service goal artifact.

### 9.2 Stage Result Artifact

- `/workflow/01_goal/result.md` — execution summary, findings, decisions to approve, assumptions, open questions, risks, traceability updates, and recommended next step.

### 9.3 Context Handoff Artifact

- `/workflow/context/context_packet.md` — minimal operational context for Stage 2.

### 9.4 Persistent Context Artifacts

Update or create when applicable:

- `/workflow/context/ASSUMPTIONS.md` — if working assumptions exist.
- `/workflow/context/OPEN_QUESTIONS.md` — if open questions exist.
- `/workflow/context/TRACEABILITY_MATRIX.md` — if goal-level traceability is available.

### 9.5 Important Rules

- Do not update `/workflow/context/DECISIONS.md` unless there is explicit human approval.
- Do not treat the existence of `01_service_goal.md` as approval.
- Do not mark the service goal as approved unless approval is explicit.
- If an artifact is updated, record what changed and why in `result.md`.

---

## 10. Conditional Artifacts

The future executable Stage 1 SKILL may create or update the following conditional artifacts.

- `/workflow/01_goal/01_goal_options.md` — if multiple plausible service goal directions exist.
- `/workflow/01_goal/01_success_metrics.md` — if success criteria require separate elaboration.
- `/workflow/01_goal/01_non_goals.md` — if non-goals are complex, contentious, or central to scope control.
- `/workflow/01_goal/review_notes.md` — if human review comments are summarized.
- `/workflow/context/REJECTED_OPTIONS.md` — if goal directions, scope options, user groups, or value propositions are explicitly rejected or superseded.

Conditional artifacts should be created only when they reduce ambiguity, improve reviewability, or preserve important context for later stages.

---

## 11. N/A Record Rules

If a conditional artifact is not created, the future executable SKILL must record the N/A rationale in `/workflow/01_goal/result.md`.

For each skipped conditional artifact, record:

- artifact name;
- why it is not applicable now;
- what future condition would make it applicable.

Example N/A record format:

| Conditional artifact | N/A rationale | Revisit if |
|---|---|---|
| `/workflow/01_goal/01_goal_options.md` | Only one plausible service goal direction was identified from approved inputs. | Human developer introduces alternative goal directions or conflicting value propositions. |
| `/workflow/01_goal/01_success_metrics.md` | Success criteria were simple enough to include in `01_service_goal.md`. | Quantitative metrics become complex, contested, or tied to research/business evaluation. |
| `/workflow/01_goal/01_non_goals.md` | Non-goals were simple enough to include in `01_service_goal.md`. | Scope boundaries become contentious or require detailed exclusion rationale. |

Do not silently omit conditional artifacts.

---

## 12. Required Structure of `01_service_goal.md`

The future executable Stage 1 SKILL must create or update `/workflow/01_goal/01_service_goal.md` using the following structure.

# 01 Service Goal

## 1. Status

Include:

- `Draft`, `Approved`, or `Needs Review`;
- source artifacts used;
- source approval state;
- whether the service goal itself has been explicitly approved;
- date or execution identifier, if available;
- whether the artifact supersedes a previous version.

## 2. Problem Definition

Include:

- problem statement;
- who experiences the problem;
- current pain, opportunity, inefficiency, unmet need, or research motivation;
- why now;
- what would remain difficult or costly without the service.

Do not turn the problem statement into a feature list.

## 3. Target Users

Include:

- primary users;
- secondary users;
- excluded users or non-targets;
- uncertainty about user groups;
- whether each user group is approved, candidate, assumed, or unresolved.

Do not convert target users into finalized stakeholder roles. That belongs to Stage 2.

## 4. Core Value Proposition

Include:

- value delivered by the service;
- user benefit;
- business, research, operational, educational, organizational, or social benefit, if applicable;
- why the value matters;
- what value is explicitly not being pursued.

## 5. Desired Outcomes

Include:

- user outcomes;
- project outcomes;
- organizational or research outcomes, if applicable;
- outcomes that would justify continuing the project;
- outcomes that would make the service direction questionable if not achieved.

## 6. Success Criteria

Include:

- qualitative success criteria;
- quantitative success criteria, if available;
- high-level validation approach;
- whether each criterion is approved, candidate, assumed, or unresolved.

Success criteria must remain high-level. Do not write detailed acceptance criteria or tests in Stage 1.

## 7. Non-Goals

Include:

- explicitly out-of-scope goals;
- deferred goals;
- rejected or superseded goal directions;
- scope boundaries intended to reduce scope creep;
- non-goals requiring human approval.

## 8. Initial Scope Boundary

Include:

- what Stage 1 includes;
- what Stage 1 does not decide;
- what must be deferred to later stages;
- any approved constraints inherited from Stage 0;
- any scope ambiguity that must be resolved before requirements or architecture work.

## 9. Initial Assumptions

Use this structure:

| Assumption ID | Assumption | Why it is needed | Risk if wrong | How it can be confirmed | Status |
|---|---|---|---|---|---|

Rules:

- Use stable IDs such as `A-001`, `A-002`.
- Mark assumptions as working assumptions.
- Do not convert assumptions into goals or decisions.
- Record assumptions in `/workflow/context/ASSUMPTIONS.md` when applicable.

## 10. Open Questions

Use this structure:

| Question ID | Question | Why it matters | Blocking or non-blocking | Suggested next step | Affected future stages |
|---|---|---|---|---|---|

Rules:

- Use stable IDs such as `Q-001`, `Q-002`.
- Separate open questions from assumptions.
- Record unresolved questions in `/workflow/context/OPEN_QUESTIONS.md` when applicable.

## 11. Risks and Ambiguities

Use this structure:

| Risk ID | Description | Impacted future stages | Severity | Mitigation or follow-up |
|---|---|---|---|---|

Stage 1 risks should remain goal-level risks and ambiguities. Do not perform full Stage 2 risk analysis.

## 12. Human Approval Required

Include:

### Decisions to Approve

- service goal;
- primary users;
- success criteria;
- non-goals;
- major scope boundaries.

### Assumptions to Confirm

- assumptions that affect the goal, users, success criteria, non-goals, or later scope.

### Open Questions to Resolve

- questions that may affect stakeholders, risks, requirements, scope, architecture, data, testing, or implementation.

### Recommended Next Stage

- proceed to Stage 2 Stakeholder & Risk Framing only after the human developer approves or explicitly allows continuation with draft status.

---

## 13. Required Structure of `result.md`

The future executable Stage 1 SKILL must create or update `/workflow/01_goal/result.md` using the following structure.

# Result: 01 Service Goal Definition

## 1. Task Summary

Summarize what Stage 1 attempted to do.

## 2. Inputs Used

List:

- files read;
- approval state of each source artifact;
- unavailable inputs;
- draft inputs used;
- rejected or superseded inputs avoided;
- user directives applied.

## 3. Outputs Created or Updated

List:

- mandatory artifacts created or updated;
- conditional artifacts created or updated;
- conditional artifacts marked N/A;
- context files updated.

## 4. Key Findings

Summarize the main problem, target users, value proposition, and goal direction.

## 5. Decision Candidates

List Agent-recommended decisions awaiting human approval.

Decision candidates may include:

- recommended service goal;
- recommended primary users;
- recommended success criteria;
- recommended non-goals;
- recommended major scope boundaries.

## 6. Working Assumptions

List assumptions used to draft the service goal.

Each assumption must include:

- ID;
- statement;
- why it was needed;
- risk if wrong;
- how to confirm it.

## 7. Open Questions

List unresolved questions.

Each question must include:

- ID;
- question;
- why it matters;
- blocking or non-blocking status;
- affected future stages;
- suggested next step.

## 8. Risks and Constraints

List:

- goal-level risks;
- ambiguity risks;
- constraints inherited from Stage 0;
- constraints that must not be violated in later stages.

## 9. Rejected or Superseded Options

List any explicitly rejected or superseded:

- service goal directions;
- target user groups;
- value propositions;
- scope boundaries;
- success criteria;
- non-goals.

Do not include options merely not selected unless they were explicitly rejected or superseded.

## 10. Traceability Updates

List:

- goal IDs created;
- links from goals to problem statements;
- links from goals to target users;
- links from goals to success criteria;
- traceability gaps;
- whether `/workflow/context/TRACEABILITY_MATRIX.md` was updated.

## 11. Human Approval Required

Use the Stage 1 approval gate structure defined in this template.

## 12. Recommended Next Step

Recommend one of:

- approve Stage 1 and proceed to Stage 2;
- revise Stage 1 before proceeding;
- continue to Stage 2 with draft status by explicit human permission;
- stop due to blocker.

---

## 14. Traceability Requirements

The future executable Stage 1 SKILL must introduce goal-level traceability without creating downstream artifacts prematurely.

### 14.1 Goal IDs

Use stable goal IDs:

- `G-001`
- `G-002`
- `G-003`

Do not rename goal IDs casually after they are introduced. If a goal is superseded, preserve the old ID and mark it superseded rather than silently reusing it.

### 14.2 Required Goal-Level Links

Each goal should link to:

- problem statement;
- target users;
- core value proposition;
- success criteria;
- non-goals or scope boundaries, when relevant;
- assumptions and open questions affecting the goal.

Recommended traceability structure:

| Goal ID | Problem reference | Target users | Core value | Success criteria | Assumptions | Open questions | Status |
|---|---|---|---|---|---|---|---|

### 14.3 Future Traceability Preparation

Stage 1 must prepare future traceability from:

- Goal → Requirements;
- Goal → Acceptance Criteria;
- Goal → Stakeholder / Risk Analysis;
- Goal → MVP Scope;
- Goal → Test Strategy;
- Goal → Implementation Evidence.

However, Stage 1 must not create those downstream links unless approved upstream constraints already exist.

### 14.4 Prohibited Premature Traceability

Do not create:

- requirements;
- acceptance criteria;
- domain concepts;
- architecture components;
- data models;
- test cases;
- tasks;
- implementation evidence links.

Exception: if such items already exist as approved upstream constraints, Stage 1 may reference them as constraints but must not expand them.

---

## 15. Decision / Assumption / Open Question Rules

The future executable Stage 1 SKILL must classify all major statements using the following rules.

### 15.1 Approved Decision

Use only when there is explicit human approval.

For Stage 1, the following can become approved decisions only through explicit human approval:

- service goal;
- primary users;
- success criteria;
- non-goals;
- major scope boundaries.

A draft artifact, Agent recommendation, or inferred project direction is not approval.

### 15.2 Decision Candidate

Use when the Agent recommends a goal direction, user focus, success criterion, non-goal, or scope boundary that awaits human review.

Decision candidates must be presented clearly under the human approval gate.

### 15.3 Working Assumption

Use when a temporary belief is needed to draft the service goal.

Examples:

- assumed primary user group;
- assumed organizational value;
- assumed MVP production baseline;
- assumed project urgency;
- assumed service boundary.

Working assumptions must remain assumptions until confirmed. They must not be written as approved facts.

### 15.4 Open Question

Use when unresolved information may affect:

- stakeholders;
- risks;
- requirements;
- privacy;
- security;
- scope;
- implementation direction;
- project viability.

Open questions must not be hidden inside assumptions.

### 15.5 Rejected Option

Use when a goal direction, user group, scope boundary, or value proposition is explicitly rejected by the human developer or superseded by an approved artifact.

Rejected options must be recorded so they are not revived later unless explicitly reopened.

### 15.6 Recommendations

Recommendations are Agent suggestions, not decisions. They may be useful, but they require review before becoming approved decisions.

### 15.7 Stage 1-Specific Rules

The future executable SKILL must not:

- convert assumptions into service goals;
- convert success criteria into acceptance criteria;
- convert target users into finalized stakeholder roles;
- convert value propositions into requirements;
- convert non-goals into implementation prohibitions without later validation;
- record Agent recommendations in `DECISIONS.md`;
- treat a draft `01_service_goal.md` as approved.

---

## 16. Stage-Specific Procedure

The future executable Stage 1 SKILL should follow this procedure.

1. Confirm Stage 1 purpose.
   - State that the task is to define why the service should exist.
   - State that the task is not requirements, architecture, data, test, or implementation work.

2. Read workflow context and Stage 0 artifacts.
   - Read required context files when available.
   - Read Stage 0 intake artifacts.
   - Check artifact status, approval state, supersession, and rejected options.

3. Check `USER_DIRECTIVES.md`.
   - Read `/workflow/01_goal/USER_DIRECTIVES.md` if it exists.
   - Classify directives as approval, correction, preference, rejection, scope change, or question.
   - Report conflicts with approved decisions.

4. Identify missing, conflicting, draft, superseded, or rejected inputs.
   - Report missing inputs.
   - Mark blockers.
   - Avoid superseded or rejected sources.
   - Continue with assumptions only when safe.

5. Restate the Stage 1 task.
   - Provide a short restatement of what will be produced.
   - Identify whether the artifact will be draft or potentially approvable.

6. Extract candidate problem statements.
   - Identify the problem, opportunity, pain, or research motivation.
   - Separate source facts from inferred problem statements.
   - Avoid turning features into the problem definition.

7. Identify candidate target users.
   - Identify primary, secondary, and excluded users.
   - Mark whether each is approved, candidate, assumed, or unresolved.
   - Do not finalize stakeholder roles.

8. Identify core value and desired outcomes.
   - Identify user value.
   - Identify business, research, operational, or organizational value if applicable.
   - Separate value claims from assumptions.

9. Draft service goal candidates if direction is ambiguous.
   - Create `/workflow/01_goal/01_goal_options.md` if multiple plausible directions exist.
   - Compare goal candidates by problem fit, user value, clarity, scope control, and risk.

10. Select a recommended goal only as a decision candidate.
    - Mark the recommended goal as `Decision Candidate`.
    - Do not mark it approved without human approval.

11. Define high-level success criteria.
    - Include qualitative criteria.
    - Include quantitative criteria only if available or reasonably inferable as assumptions.
    - Keep success criteria high-level.
    - Do not write acceptance criteria.

12. Define non-goals and scope boundaries.
    - Identify explicit exclusions.
    - Identify deferred goals.
    - Identify rejected or superseded goal directions.
    - Keep boundaries reviewable.

13. Separate assumptions, open questions, risks, and rejected options.
    - Use stable IDs.
    - Update persistent context files when applicable.
    - Avoid mixing unresolved questions with assumptions.

14. Define goal-level traceability.
    - Assign goal IDs.
    - Link goals to problem statements, target users, and success criteria.
    - Record traceability gaps.

15. Produce or update Stage 1 artifacts.
    - Create or update `01_service_goal.md`.
    - Create or update `result.md`.
    - Create conditional artifacts if needed.
    - Record N/A rationale for skipped conditional artifacts.

16. Prepare `context_packet.md` for Stage 2.
    - Include only the minimal operational context needed by Stage 2.
    - Point to source artifacts instead of copying them in full.
    - Include Do Not Do instructions for the next Agent.

17. Present the human approval gate.
    - List decisions to approve.
    - List assumptions to confirm.
    - List open questions to resolve.
    - List risks to review.
    - Recommend next step.

---

## 17. Stage-Specific Validation Checklist

Before completing Stage 1, the future executable SKILL must check:

- [ ] The service goal explains why the service should exist.
- [ ] The goal is not merely a feature list.
- [ ] The problem definition is explicit.
- [ ] The target users are explicit.
- [ ] Primary users are separated from secondary users.
- [ ] Excluded users or non-targets are listed when relevant.
- [ ] The core value proposition is clear.
- [ ] Desired outcomes are stated at a high level.
- [ ] Success criteria are reviewable.
- [ ] Success criteria are not detailed acceptance criteria.
- [ ] Non-goals are explicit enough to reduce scope creep.
- [ ] Initial scope boundaries are clear.
- [ ] Assumptions are clearly marked.
- [ ] Open questions are separated from assumptions.
- [ ] Risks and ambiguities are identified without performing full Stage 2 risk analysis.
- [ ] Rejected or superseded options are recorded when applicable.
- [ ] No requirements are prematurely created.
- [ ] No acceptance criteria are prematurely written.
- [ ] No domain model is prematurely created.
- [ ] No architecture or implementation choices are prematurely made.
- [ ] Existing approved constraints from Stage 0 are respected.
- [ ] Goal-level traceability uses stable goal IDs.
- [ ] `context_packet.md` prepares Stage 2 without becoming a full project history.
- [ ] The human approval gate is present.
- [ ] Stage 2 can begin stakeholder and risk framing from the prepared context.

---

## 18. Stage-Specific Human Approval Gate

The future executable Stage 1 SKILL must end with the following approval section.

## Human Approval Required

### Decisions to Approve

- Service goal
- Primary users
- Success criteria
- Non-goals
- Major scope boundaries

### Assumptions to Confirm

List assumptions that affect:

- service goal;
- user focus;
- value proposition;
- success criteria;
- non-goals;
- scope boundaries;
- later stakeholder or risk framing.

### Open Questions to Resolve

List questions that may affect:

- stakeholders;
- roles;
- permissions;
- privacy;
- security;
- requirements;
- scope;
- implementation direction;
- project viability.

### Risks to Review

List goal-level risks and ambiguities that need human review before proceeding.

### Artifacts Ready for Review

- `/workflow/01_goal/01_service_goal.md`
- `/workflow/01_goal/result.md`

Also include any conditional artifacts created, for example:

- `/workflow/01_goal/01_goal_options.md`
- `/workflow/01_goal/01_success_metrics.md`
- `/workflow/01_goal/01_non_goals.md`

### Recommended Next Step

Use one of the following:

- Proceed to Stage 2 Stakeholder & Risk Framing after the human developer approves Stage 1.
- Proceed to Stage 2 with draft status only if the human developer explicitly allows continuation.
- Revise Stage 1 before proceeding.
- Stop due to blocker and request missing input or decision.

The future executable SKILL must not imply approval unless approval has been explicitly given.

---

## 19. Next `context_packet.md` Rules

Stage 1 must prepare `/workflow/context/context_packet.md` for Stage 2 Stakeholder & Risk Framing.

`context_packet.md` is a navigation layer, not the sole source of truth. It must be concise and must point to source artifacts.

### 19.1 Required Context Packet Content for Stage 2

Include:

## 1. Current Project State

- Current stage: `01_service_goal_definition`
- Completed stages:
- Next recommended stage: `02_stakeholder_risk_framing`
- Stage 1 artifact status: Draft / Approved / Needs Review

## 2. Approved Decisions

Include only explicitly approved decisions.

Do not list decision candidates as approved decisions.

## 3. Working Assumptions

Include assumptions relevant to Stage 2, especially those affecting:

- user groups;
- stakeholders;
- operators;
- administrators;
- privacy;
- security;
- external systems;
- data sensitivity;
- organizational constraints;
- project scope.

## 4. Open Questions

Include open questions affecting:

- stakeholders;
- security;
- privacy;
- requirements;
- scope;
- external systems;
- risk analysis.

## 5. Rejected / Superseded Options

Include rejected or superseded:

- service goal directions;
- user groups;
- value propositions;
- scope boundaries;
- success criteria;
- non-goals.

## 6. Constraints That Must Not Be Violated

Include constraints inherited from Stage 0 or approved during Stage 1, such as:

- technology constraints;
- business constraints;
- research constraints;
- privacy constraints;
- security constraints;
- operational constraints;
- schedule or budget constraints;
- forbidden change areas.

## 7. Key Context for Stage 2

Include the minimum context Stage 2 needs:

- service goal summary;
- primary and secondary users;
- excluded users or non-targets;
- core value proposition;
- success criteria summary;
- non-goals;
- risks and ambiguities relevant to stakeholder and risk framing.

## 8. Required Inputs for Stage 2

Stage 2 should read at minimum:

- `/workflow/01_goal/01_service_goal.md`
- `/workflow/01_goal/result.md`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`

Stage 2 may also read:

- `/workflow/01_goal/01_goal_options.md`, if created.
- `/workflow/01_goal/01_success_metrics.md`, if created.
- `/workflow/01_goal/01_non_goals.md`, if created.
- Stage 0 artifacts, if stakeholder or risk framing depends on intake constraints.

## 9. Do Not Do

Include Do Not Do instructions for Stage 2, such as:

- Do not treat draft service goals as approved.
- Do not ignore unresolved assumptions.
- Do not revive rejected goal directions.
- Do not convert target users into permission roles without analysis.
- Do not create requirements before stakeholder and risk framing is complete.
- Do not make architecture, data, or implementation decisions.

---

## 20. Specialization Addendum Hooks

Project-type specializations may extend Stage 1 by adding questions, conditional inputs, conditional artifacts, or validation concerns.

Specialization addenda must not replace the Stage 1 template. They must not weaken approval rules, artifact contracts, assumption handling, or traceability requirements.

### 20.1 `web_saas`

May add prompts to clarify:

- customer value;
- tenant value;
- admin value;
- end-user value;
- buyer vs user distinction;
- multi-tenant scope boundaries;
- SaaS onboarding assumptions.

### 20.2 `internal_tool`

May add prompts to clarify:

- operator value;
- organizational workflow value;
- internal process improvement;
- manual work reduced;
- reporting or audit value;
- affected internal teams.

### 20.3 `mobile_app`

May add prompts to clarify:

- end-user value;
- device context;
- platform constraints;
- offline or on-device expectations;
- app usage context;
- platform-specific non-goals.

### 20.4 `ai_data_product`

May add prompts to clarify:

- data source;
- evaluation purpose;
- model output value;
- human review value;
- decision-support vs automation boundary;
- research or production intent;
- unacceptable model failure modes at goal level.

### 20.5 `regulated_security_sensitive`

May add prompts to clarify:

- compliance-sensitive goals;
- privacy-sensitive goals;
- sensitive user groups;
- high-level risk boundaries;
- auditability expectations;
- forbidden uses;
- human oversight expectations.

### 20.6 `brownfield_legacy`

May add prompts to clarify whether the goal is:

- replacement;
- extension;
- migration;
- modernization;
- maintenance;
- integration;
- operational stabilization.

It may also require existing system constraints to be treated as hard boundaries unless the human developer explicitly approves change.

---

## 21. Tool Wrapper Notes

Claude Code, Codex, Antigravity, or other tool wrappers may specify:

- file creation commands;
- save location;
- review workflow;
- sandbox constraints;
- permission constraints;
- command invocation style;
- tool-specific artifact display conventions.

Tool wrappers must not change:

- service goal reasoning;
- approval rules;
- artifact contract;
- assumption handling;
- open question handling;
- rejected option handling;
- traceability rules;
- Stage 1 boundaries;
- the distinction between template, executable SKILL, and project artifact.

Tool wrappers may help execute the future SKILL, but they must not decide the service goal.

---

## 22. Anti-Patterns to Avoid

The future executable Stage 1 SKILL must avoid:

- creating requirements during Stage 1;
- writing acceptance criteria during Stage 1;
- designing architecture during Stage 1;
- choosing database or technical stack during Stage 1 unless already approved in Stage 0;
- designing UI flows during Stage 1;
- creating domain models during Stage 1;
- creating data models during Stage 1;
- creating test plans during Stage 1;
- creating implementation tasks during Stage 1;
- treating success criteria as detailed tests;
- treating assumptions as approved decisions;
- treating Agent recommendations as approved decisions;
- treating all target users as finalized stakeholder roles;
- collapsing Stage 1 and Stage 2;
- redoing Stage 0 intake unnecessarily;
- using `context_packet.md` as the only source of truth;
- reading all downstream artifacts by default;
- reviving rejected options without explicit human instruction;
- creating executable `SKILL.md` inside this template task;
- creating project artifacts during template design;
- copying the entire core template into the stage template;
- weakening the core template’s approval, traceability, or failure-handling rules.

---

## 23. Template Quality Checklist

Before this Stage 1 template is used to create a future executable reusable SKILL, check:

- [ ] The file is a stage-specific template, not an executable SKILL.
- [ ] It does not create project-specific content.
- [ ] It defines Stage 1 purpose and core question.
- [ ] It defines Stage 1’s position between Stage 0 and Stage 2.
- [ ] It defines Always Read inputs.
- [ ] It defines Read If Applicable inputs.
- [ ] It defines Do Not Read By Default.
- [ ] It defines missing input handling.
- [ ] It defines mandatory artifacts.
- [ ] It defines conditional artifacts.
- [ ] It defines N/A record rules.
- [ ] It defines the required structure of `01_service_goal.md`.
- [ ] It defines the required structure of `result.md`.
- [ ] It defines traceability requirements.
- [ ] It defines decision / assumption / open question handling.
- [ ] It defines rejected option handling.
- [ ] It defines the Stage-specific procedure.
- [ ] It defines the Stage-specific validation checklist.
- [ ] It defines the human approval gate.
- [ ] It defines next `context_packet.md` rules.
- [ ] It prepares Stage 2 without performing Stage 2.
- [ ] It leaves hooks for specialization addenda.
- [ ] It leaves hooks for tool wrappers.
- [ ] It does not weaken the core template.
- [ ] It does not create `/skills/01_service_goal_definition/SKILL.md`.
- [ ] It does not create `/workflow/01_goal/01_service_goal.md`.
- [ ] It does not create `artifact_contract.yml`.
- [ ] It does not create `README.md`.
