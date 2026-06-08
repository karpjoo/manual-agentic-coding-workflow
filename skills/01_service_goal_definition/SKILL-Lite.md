---
name: service_goal_definition
description: Use this skill to define why a service should exist before stakeholder/risk framing, requirements, architecture, data design, test strategy, or implementation work begins.
stage: 01_service_goal_definition
version: 1.0.0
status: draft
primary_output: /workflow/01_goal/01_service_goal.md
requires_human_approval: true
---

# Service Goal Definition SKILL

## 1. Purpose

Run Stage 1: Service Goal Definition.

Define **why the service should exist** before deciding what to build.

Core question:

> Why should this service exist, for whom, what value should it provide, and how will we know at a high level that the goal is being achieved?

This SKILL produces a service goal artifact for later stages.

This SKILL must not produce requirements, acceptance criteria, stakeholder/risk analysis, architecture, data design, test strategy, task breakdown, implementation prompts, or code.

---

## 2. When to Use

Use this SKILL when:

- Stage 0 Project Intake exists or enough initial context exists.
- A service, tool, product, research system, or internal workflow needs a clear goal.
- Stage 2 Stakeholder & Risk Framing needs a service goal input.
- A previous Stage 1 draft needs revision after review.

Do not use this SKILL when the task is requirements, stakeholder/risk analysis, architecture, data design, test strategy, implementation, or code review.

---

## 3. Operating Rules

You are a structured development assistant, not an autonomous developer.

Follow these distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ approved artifact
Agent output ≠ human approval
```

Classify all important information as one of:

- approved decision;
- decision candidate;
- working assumption;
- open question;
- risk or ambiguity;
- rejected or superseded option;
- recommendation.

Do not update `/workflow/context/DECISIONS.md` unless explicit human approval exists.

---

## 4. Input Precedence

Use this order when sources conflict:

```text
1. Current explicit user instruction
2. /workflow/01_goal/USER_DIRECTIVES.md
3. /workflow/context/APPROVAL_LOG.md and DECISIONS.md
4. /workflow/context/artifact_manifest.yml
5. /workflow/context/context_packet.md
6. Approved stage artifacts
7. Working assumptions
8. Agent inference
```

Conflict rules:

- Do not silently resolve conflicts.
- Identify conflicting sources.
- Explain the impact.
- Continue only if non-blocking.
- Stop if the conflict affects service goal, primary users, success criteria, non-goals, or major scope boundaries.

---

## 5. Inputs to Read

### Always Read When Available

Workflow context:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`
- `/workflow/context/APPROVAL_LOG.md`

Stage 0:

- `/workflow/00_intake/00_project_intake.md`
- `/workflow/00_intake/result.md`

Stage 1 directive:

- `/workflow/01_goal/USER_DIRECTIVES.md`, if available

For each input, check existence, approval state, draft status, supersession, rejection, and conflicts.

### Read If Applicable

- `/workflow/00_intake/00_existing_context_review.md` — if brownfield or existing-system work.
- `/workflow/00_intake/review_notes.md` — if Stage 0 review comments exist.
- `/workflow/01_goal/review_notes.md` — if revising Stage 1.
- Project brief, initial idea, product memo, research plan, business memo, or problem statement — if referenced.
- Specialization addendum — if activated by project profile.
- Tool wrapper — if required by execution environment.

### Do Not Read By Default

Do not read downstream artifacts, implementation files, full codebase, raw logs, superseded drafts, rejected drafts, or unrelated historical files.

---

## 6. Missing Input Handling

If Stage 0 is missing:

- report it as a potential blocker;
- check whether enough user-provided idea or directive exists;
- continue only with clearly marked assumptions if safe.

If no service idea, no Stage 0 artifact, and no user directive exist:

- do not invent a service goal;
- produce a blocker report only.

If inputs are draft or unapproved:

- use only as draft context;
- mark dependent outputs as Draft or Needs Review.

If inputs conflict:

- report the conflict;
- identify affected decisions and artifacts;
- stop when the conflict affects goal, users, success criteria, non-goals, or scope boundaries.

---

## 7. USER_DIRECTIVES.md Handling

If `/workflow/01_goal/USER_DIRECTIVES.md` exists, read it before execution.

Classify each directive as:

- approval;
- correction;
- preference;
- rejection;
- scope change;
- constraint;
- question;
- new input.

Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

---

## 8. Preflight Checklist

Before producing artifacts:

```text
[ ] Read this SKILL.md.
[ ] Read available workflow context files.
[ ] Read Stage 0 artifacts.
[ ] Check USER_DIRECTIVES.md.
[ ] Identify conditional inputs.
[ ] Verify input approval and supersession status.
[ ] Identify missing inputs.
[ ] Identify conflicts.
[ ] Identify rejected options.
[ ] Restate the Stage 1 task.
```

If a blocker exists, produce a blocker report instead of pretending completion.

---

## 9. Execution Procedure

1. Confirm that the task is Stage 1 Service Goal Definition.
2. State what this stage will not do.
3. Review Stage 0 and workflow context.
4. Apply `USER_DIRECTIVES.md`.
5. Identify missing, draft, conflicting, rejected, or superseded inputs.
6. Extract candidate problem statements.
7. Identify target users:
   - primary users;
   - secondary users;
   - excluded users or non-targets.
8. Define the core value proposition.
9. Define desired outcomes.
10. Define high-level success criteria.
11. Define non-goals and initial scope boundaries.
12. If multiple goal directions exist, create `01_goal_options.md`.
13. Recommend one goal direction only as a decision candidate.
14. Separate assumptions, open questions, risks, and rejected options.
15. Assign stable goal IDs such as `G-001`.
16. Link goals to problem, users, value, and success criteria.
17. Create or update mandatory artifacts.
18. Create conditional artifacts only when applicable.
19. Record N/A rationale for skipped conditional artifacts.
20. Update context files as needed.
21. Prepare `context_packet.md` for Stage 2.
22. End with the human approval gate.

---

## 10. Output Artifacts

### Mandatory

Create or update:

- `/workflow/01_goal/01_service_goal.md`
- `/workflow/01_goal/result.md`
- `/workflow/context/context_packet.md`

Update when applicable:

- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`

Do not update `/workflow/context/DECISIONS.md` without explicit human approval.

### Conditional

Create only if useful:

- `/workflow/01_goal/01_goal_options.md` — if multiple plausible goal directions exist.
- `/workflow/01_goal/01_success_metrics.md` — if success criteria need separate elaboration.
- `/workflow/01_goal/01_non_goals.md` — if non-goals are complex or contentious.
- `/workflow/01_goal/review_notes.md` — if summarizing human review comments.

### N/A Rule

For each skipped conditional artifact, record in `result.md`:

```text
Artifact:
Why not applicable:
Revisit if:
```

---

## 11. Required Structure: 01_service_goal.md

Create `/workflow/01_goal/01_service_goal.md` with:

```markdown
# 01 Service Goal

## 1. Status
- Status: Draft / Approved / Needs Review
- Source artifacts used:
- Source approval state:
- Approval state:
- Supersedes:

## 2. Problem Definition
- Problem statement:
- Who experiences the problem:
- Current pain or opportunity:
- Why now:
- What remains difficult without the service:

## 3. Target Users
- Primary users:
- Secondary users:
- Excluded users or non-targets:
- User uncertainties:

## 4. Core Value Proposition
- Value delivered:
- User benefit:
- Business / research / operational / organizational benefit:
- Value not pursued:

## 5. Desired Outcomes
- User outcomes:
- Project outcomes:
- Organizational or research outcomes:
- Outcome risks:

## 6. Success Criteria
- Qualitative success criteria:
- Quantitative success criteria, if available:
- High-level validation approach:
- Unresolved success criteria questions:

## 7. Non-Goals
- Explicitly out of scope:
- Deferred goals:
- Rejected or superseded goal directions:
- Scope creep risks:

## 8. Initial Scope Boundary
- What Stage 1 includes:
- What Stage 1 does not decide:
- What is deferred to later stages:
- Approved constraints inherited from Stage 0:

## 9. Initial Assumptions
| ID | Assumption | Why Needed | Risk If Wrong | How To Confirm | Status |
|---|---|---|---|---|---|

## 10. Open Questions
| ID | Question | Why It Matters | Blocking? | Next Step | Affected Stages |
|---|---|---|---|---|---|

## 11. Risks and Ambiguities
| ID | Description | Impacted Stages | Severity | Follow-Up |
|---|---|---|---|---|

## 12. Goal-Level Traceability
| Goal ID | Problem | Users | Value | Success Criteria | Assumptions | Questions | Status |
|---|---|---|---|---|---|---|---|

## 13. Human Approval Required
### Decisions to Approve
- Service goal
- Primary users
- Success criteria
- Non-goals
- Major scope boundaries

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Risks to Review
- ...

### Recommended Next Stage
- ...
```

---

## 12. Required Structure: result.md

Create `/workflow/01_goal/result.md` with:

```markdown
# Result: 01 Service Goal Definition

## 1. Task Summary

## 2. Inputs Used
| Input | Status | Approval State | Notes |
|---|---|---|---|

## 3. Outputs Created or Updated
| Artifact | Created / Updated / N/A | Notes |
|---|---|---|

## 4. Key Findings

## 5. Decision Candidates

## 6. Working Assumptions

## 7. Open Questions

## 8. Risks and Constraints

## 9. Rejected or Superseded Options

## 10. Traceability Updates

## 11. Human Approval Required

## 12. Recommended Next Step
```

---

## 13. Traceability Rules

Use stable IDs:

```text
G-001, G-002
A-001, A-002
Q-001, Q-002
R-001, R-002
```

Stage 1 traceability links only:

```text
Goal → Problem → Target Users → Core Value → Success Criteria
```

Prepare for future traceability, but do not create downstream artifacts:

```text
Goal → Requirements → Acceptance Criteria → Domain → Architecture → Data → Tasks → Tests → Evidence
```

If traceability is incomplete, record the gap.

---

## 14. Classification Rules

### Approved Decision

Only explicit human approval can approve:

- service goal;
- primary users;
- success criteria;
- non-goals;
- major scope boundaries.

### Decision Candidate

Use for Agent-recommended goal direction awaiting review.

### Working Assumption

Use for temporary beliefs needed to draft the goal.

### Open Question

Use for unresolved issues affecting later work.

### Rejected Option

Use only for explicitly rejected or superseded options.

Rules:

- Do not convert assumptions into decisions.
- Do not convert recommendations into requirements.
- Do not convert success criteria into acceptance criteria.
- Do not convert target users into stakeholder roles.
- Do not revive rejected options unless explicitly reopened.

---

## 15. Context Packet Update

Update `/workflow/context/context_packet.md` for Stage 2.

Use:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 01_service_goal_definition
- Completed stages:
- Next recommended stage: 02_stakeholder_risk_framing
- Stage 1 artifact status:

## 2. Approved Decisions
- Only explicitly approved decisions.

## 3. Working Assumptions
- ...

## 4. Open Questions
- ...

## 5. Rejected / Superseded Options
- ...

## 6. Constraints That Must Not Be Violated
- Technology:
- Security:
- Privacy:
- Scope:
- Schedule:
- Operational:

## 7. Key Context for Stage 2
- Service goal summary:
- Primary users:
- Secondary users:
- Excluded users:
- Core value:
- Success criteria summary:
- Non-goals:
- Relevant risks and ambiguities:

## 8. Required Inputs for Stage 2
- /workflow/01_goal/01_service_goal.md
- /workflow/01_goal/result.md
- /workflow/context/context_packet.md
- /workflow/context/DECISIONS.md
- /workflow/context/ASSUMPTIONS.md
- /workflow/context/OPEN_QUESTIONS.md
- /workflow/context/REJECTED_OPTIONS.md
- /workflow/context/TRACEABILITY_MATRIX.md

## 9. Do Not Do
- Do not treat draft service goals as approved.
- Do not ignore unresolved assumptions.
- Do not revive rejected goal directions.
- Do not convert target users into permission roles without Stage 2 analysis.
- Do not create requirements before Stage 3.
- Do not make architecture, data, test, or implementation decisions.
```

Keep `context_packet.md` concise. It is a navigation layer, not full project history.

---

## 16. Human Approval Gate

End with:

```markdown
## Human Approval Required

### Decisions to Approve
- Service goal
- Primary users
- Success criteria
- Non-goals
- Major scope boundaries

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Risks to Review
- ...

### Artifacts Ready for Review
- /workflow/01_goal/01_service_goal.md
- /workflow/01_goal/result.md

### Recommended Next Step
- Proceed to Stage 2 only after approval, or continue with draft status only if explicitly allowed.
```

Do not claim approval unless explicit approval exists.

---

## 17. Validation Checklist

Before completion, verify:

- [ ] Goal explains why the service should exist.
- [ ] Goal is not a feature list.
- [ ] Problem definition is explicit.
- [ ] Target users are explicit.
- [ ] Core value is clear.
- [ ] Desired outcomes are stated.
- [ ] Success criteria are high-level and reviewable.
- [ ] Success criteria are not acceptance criteria.
- [ ] Non-goals and scope boundaries are explicit.
- [ ] Assumptions are marked.
- [ ] Open questions are separated from assumptions.
- [ ] Risks and ambiguities are identified.
- [ ] Goal IDs are stable.
- [ ] Context packet is prepared for Stage 2.
- [ ] Human approval gate is present.
- [ ] No downstream stage work was performed.

---

## 18. Failure Handling

If blocked, produce:

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

Blocking cases:

- no service idea or project context;
- missing Stage 0 with no alternative context;
- conflict affecting goal, users, success criteria, non-goals, or scope;
- rejected option requested again without reopening;
- required file cannot be read;
- source artifact is superseded or rejected.

---

## 19. Specialization Hook

If active, apply specialization addenda after this SKILL:

- `web_saas`
- `internal_tool`
- `mobile_app`
- `ai_data_product`
- `regulated_security_sensitive`
- `brownfield_legacy`

Specialization may add questions or conditional artifacts, but must not replace this SKILL or weaken approval rules.

---

## 20. Tool Wrapper Hook

Tool wrappers may define commands, save locations, sandbox rules, and review workflow.

They must not change service goal reasoning, approval rules, artifact contracts, assumption handling, traceability, or Stage 1 boundaries.

---

## 21. Do Not Do

Do not:

- create requirements;
- write acceptance criteria;
- perform stakeholder/risk analysis;
- design architecture;
- choose database or technical stack unless already approved;
- create domain models;
- create data models;
- create test plans;
- create tasks;
- write implementation prompts;
- inspect or modify code;
- treat assumptions as approved decisions;
- treat target users as finalized stakeholder roles;
- collapse Stage 1 and Stage 2;
- use `context_packet.md` as the only source of truth;
- read all historical files by default;
- revive rejected options without explicit instruction;
- skip the human approval gate.

---

## 22. Completion Checklist

- [ ] Required inputs checked.
- [ ] Missing inputs reported.
- [ ] Conflicts reported.
- [ ] Draft inputs not treated as approved.
- [ ] `USER_DIRECTIVES.md` checked if available.
- [ ] Mandatory artifacts created or updated.
- [ ] Conditional artifacts created or marked N/A.
- [ ] `01_service_goal.md` follows required structure.
- [ ] `result.md` follows required structure.
- [ ] `context_packet.md` prepared for Stage 2.
- [ ] Assumptions, questions, risks, and rejected options separated.
- [ ] Goal-level traceability present or gaps recorded.
- [ ] `DECISIONS.md` not updated without approval.
- [ ] Human approval gate included.
- [ ] No downstream work performed.
