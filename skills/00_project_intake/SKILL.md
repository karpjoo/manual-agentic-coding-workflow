---
name: project-intake
description: Use this skill at the beginning of a Manual Agentic Coding Workflow to classify the project, inventory existing context, identify fixed constraints, initialize workflow context files, and prepare the next stage without starting requirements, architecture, or implementation work.
stage: Stage 0 - Project Intake / Existing Context Review
version: 1.0.0
status: draft
primary_output: /workflow/00_intake/00_project_intake.md
requires_human_approval: true
---

# Project Intake Skill

## 1. Purpose

Use this skill to establish the trustworthy starting context for a software development project before moving into service goal definition, stakeholder/risk analysis, requirements, domain modeling, architecture, data design, task breakdown, or implementation.

This skill determines:

- whether the project is new or based on an existing system;
- what project type and project profile best describe the work;
- what user-provided context already exists;
- what decisions have already been explicitly approved by the human developer;
- what is still only a working assumption;
- what documents, code, tests, data, infrastructure, and deployment settings already exist;
- what technology stack, tools, platforms, or constraints are fixed;
- what areas must not be changed;
- what early security, privacy, regulatory, operational, or research concerns are visible;
- whether a deeper existing-codebase review is needed before the next stage;
- what minimal context must be passed to the next stage.

The goal is not to design the system yet. The goal is to prevent later stages from relying on vague, missing, stale, or unapproved context.

---

## 2. When to Use

Use this skill when:

- starting a new Manual Agentic Coding Workflow;
- receiving a new project idea from the human developer;
- entering a repository or project folder for the first time;
- deciding whether the work is greenfield, brownfield, prototype, research, migration, maintenance, or extension work;
- initializing `/workflow` and `/workflow/context` artifacts;
- preparing Stage 1 Service Goal Definition;
- deciding whether a deeper codebase-context-review skill must run before Stage 1.

Do not use this skill to:

- finalize service goals;
- decompose requirements;
- write acceptance criteria;
- perform DDD/domain modeling;
- design architecture, APIs, data schemas, or infrastructure;
- break down implementation tasks;
- write implementation prompts;
- edit production code.

---

## 3. Agent Role and Operating Mode

You are a structured development assistant operating inside a human-controlled workflow.

You must:

1. Read approved context before acting.
2. Identify the current stage and task.
3. Read only the necessary inputs.
4. Respect current user instructions and stage-local directives.
5. Produce explicit artifacts.
6. Separate facts, approved decisions, decision candidates, working assumptions, risks, and open questions.
7. Update the context needed by the next stage.
8. End with a human approval gate.

Use these distinctions throughout the stage:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```

---

## 4. Input Precedence Rules

When inputs conflict, use this precedence order:

```text
1. Current explicit user instruction
2. /workflow/00_intake/USER_DIRECTIVES.md
3. /workflow/context/APPROVAL_LOG.md and /workflow/context/DECISIONS.md
4. /workflow/context/artifact_manifest.yml
5. /workflow/context/context_packet.md
6. Approved stage artifacts
7. Working assumptions
8. Agent inference
```

Conflict handling:

- Do not silently resolve conflicts.
- Report the conflict explicitly.
- Identify which sources conflict.
- Explain the likely downstream impact.
- Continue only if the conflict is non-blocking.
- If the conflict affects scope, architecture, data, privacy, security, implementation, release, or forbidden change areas, stop and request a human decision.

---

## 5. Required Inputs

Stage 0 may be the first workflow stage, so many workflow files may not exist yet. Missing workflow context files are expected during an initial run and should not automatically block progress.

### 5.1 Always Check / Read If Present

Check these inputs and read them if they exist:

```text
- Current explicit user instruction or initial project description
- /workflow/00_intake/USER_DIRECTIVES.md
- /workflow/00_intake/review_notes.md
- /workflow/context/artifact_manifest.yml
- /workflow/context/context_packet.md
- /workflow/context/DECISIONS.md
- /workflow/context/ASSUMPTIONS.md
- /workflow/context/OPEN_QUESTIONS.md
- /workflow/context/REJECTED_OPTIONS.md
- /workflow/context/TRACEABILITY_MATRIX.md
- /workflow/context/APPROVAL_LOG.md
```

If a file does not exist because the workflow is being initialized, record that as expected absence.

### 5.2 Read If Applicable

Read these only when relevant to the current project context:

```text
- README.md — if a repository or project folder exists
- docs/, documentation/, design/, planning/, product/, specs/ — if documentation folders exist
- package.json, pyproject.toml, requirements.txt, pubspec.yaml, go.mod, pom.xml, build.gradle, Cargo.toml — if stack detection is needed
- firebase.json, firestore.rules, firestore.indexes.json — if Firebase is present or mentioned
- vercel.json, netlify.toml, Dockerfile, docker-compose.yml, k8s/, terraform/, infra/ — if deployment or infrastructure context exists
- .env.example or sanitized config examples — if environment setup is relevant
- tests/, e2e/, integration test folders — if an existing codebase has tests
- CI configuration files — if release or validation workflow already exists
- product brief, research plan, grant proposal, PRD, user interview notes — if provided by the user
- dataset description, data dictionary, labeling guide — if the project may be an AI/data product or research tool
- compliance, privacy, security, or legal notes — if the project may handle personal, sensitive, regulated, or external data
```

### 5.3 Do Not Read By Default

Do not read these unless the user explicitly asks or the Stage 0 preflight shows they are necessary:

```text
- full source code tree when only high-level intake is needed
- raw logs unless the project is debugging or incident-oriented
- large datasets
- generated build artifacts
- dependency lockfiles unless dependency state must be confirmed
- old drafts or superseded planning documents unless referenced as current
- unrelated previous project artifacts
- private secrets or local environment files containing credentials
```

---

## 6. USER_DIRECTIVES.md Handling

If `/workflow/00_intake/USER_DIRECTIVES.md` exists, read it before executing the stage-specific procedure.

Treat it as stage-local human instruction. It may contain:

- user requirements;
- preferences;
- explicit approvals;
- rejections;
- corrections to previous agent output;
- scope changes;
- review comments;
- additional constraints;
- questions the agent must answer.

Rules:

- Apply `USER_DIRECTIVES.md` before agent assumptions.
- Do not automatically treat every directive as a globally approved decision.
- Distinguish explicit approval from preference, correction, rejection, new requirement, or question.
- If it conflicts with `DECISIONS.md` or `APPROVAL_LOG.md`, report the conflict.
- Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

---

## 7. Input Preflight Procedure

Before producing outputs, perform this preflight.

```text
[ ] Confirm this is Stage 0 Project Intake / Existing Context Review.
[ ] Determine whether this is an initial run, rerun, context initialization, or finalization before Stage 1.
[ ] Read the current explicit user instruction.
[ ] Check whether /workflow/00_intake exists.
[ ] Check whether /workflow/context exists.
[ ] Check whether /workflow/00_intake/USER_DIRECTIVES.md exists and read it if present.
[ ] Check whether /workflow/00_intake/review_notes.md exists and read it if present.
[ ] Check artifact_manifest.yml if present.
[ ] Check context_packet.md if present.
[ ] Check DECISIONS.md and APPROVAL_LOG.md if present.
[ ] Identify whether existing Stage 0 artifacts are approved, draft, superseded, or absent.
[ ] Identify whether a repository, codebase, documentation set, dataset, or deployment context exists.
[ ] Identify explicit user decisions, constraints, preferences, and forbidden areas.
[ ] Identify visible security, privacy, data, LLM/API, compliance, or operational risk signals.
[ ] Determine whether conditional inputs should be read.
[ ] Identify missing, ambiguous, draft, superseded, rejected, or conflicting inputs.
[ ] Restate the current Stage 0 task before continuing.
```

If a blocking issue is found, produce a blocker report and safe partial artifacts instead of pretending completion.

---

## 8. Missing Input Handling

Classify missing information as one of:

```text
- expected absence for a new Stage 0 run
- non-blocking gap
- blocking gap
- human approval needed
- deeper review needed
```

Rules:

- Missing workflow context files are non-blocking when this is the first workflow run.
- Missing initial project description is blocking unless the user explicitly asks only for repository or context inventory.
- Missing technology stack is non-blocking at intake but must be recorded as an open question unless already fixed.
- Missing codebase access is blocking only if the project is brownfield, extension, migration, maintenance, or codebase-review oriented.
- Missing security/privacy details are non-blocking at intake but must be recorded when personal, sensitive, regulated, LLM/API, or external data may exist.
- Missing approval is not the same as rejection; mark unapproved items as candidates, assumptions, or open questions.

---

## 9. Project Classification Model

Classify the project using two complementary dimensions.

### 9.1 Development Context Type

Use one or more of:

```text
- greenfield
- brownfield
- prototype
- research tool
- extension of existing system
- migration / modernization
- maintenance / bug-fix oriented
- exploratory / feasibility study
```

### 9.2 Project Profile

Use one or more of:

```text
- lightweight prototype
- MVP production
- production system
- regulated / security-sensitive
- web SaaS
- internal tool
- mobile app
- AI / data product
- developer tooling
- educational / learning project
```

### 9.3 Classification Rules

- Mark classifications as decision candidates unless the human has explicitly approved them.
- Explain evidence for each classification.
- Record confidence as high, medium, or low.
- Record uncertainty when classification is ambiguous.
- Avoid assuming greenfield when existing code, deployment, users, or data are mentioned.
- Avoid assuming production readiness when the user requested a prototype, research tool, or exploratory project.
- Use classification to determine which specialization hooks may be needed later.

Use this table format:

```markdown
| Dimension | Candidate Classification | Evidence | Confidence | Approval Status |
|---|---|---|---|---|
```

---

## 10. Stage-Specific Execution Procedure

### Step 1. Establish Intake Mode

Determine whether this run is:

```text
- initial project intake
- intake rerun after user correction
- existing codebase context review trigger
- project profile selection
- workflow context initialization
- intake finalization before Stage 1
```

### Step 2. Collect Starting Context

Identify and summarize:

```text
- user-provided project idea or request
- existing documents
- existing codebase or repository status
- existing tests
- existing deployment or infrastructure
- existing data, dataset, or database
- existing users, operators, or stakeholders mentioned
- existing technology stack
- explicitly fixed tools, platforms, frameworks, databases, or hosting decisions
- explicitly forbidden changes or non-negotiable constraints
```

### Step 3. Classify Project Type and Profile

Create the project classification table. Treat classification as a decision candidate unless explicitly approved.

### Step 4. Separate Approved Decisions, Candidates, and Assumptions

Separate and record:

```text
- facts found in source inputs
- explicitly approved decisions
- decision candidates needing approval
- working assumptions
- open questions
- rejected or superseded options
- risks and constraints
```

### Step 5. Identify Early Risk Signals

Record early screening-level signals for:

```text
- personal data
- sensitive data
- regulated data
- authentication or authorization needs
- external API calls
- LLM/API data transfer
- dataset or model risks
- payment or financial data
- audit/logging needs
- operational reliability concerns
- deployment or environment constraints
```

Do not perform a full security/privacy review in Stage 0. Only identify risk signals and hand them off to later stages.

### Step 6. Decide Whether Existing Context Review Is Needed

Create `/workflow/00_intake/00_existing_context_review.md` if any of the following are true:

```text
- existing codebase is present
- existing deployment is present
- existing database, production data, or dataset is present
- project modifies, extends, migrates, or maintains an existing system
- user asks to preserve compatibility
- user says some areas must not be changed
- existing tests or CI must be respected
```

If it is not needed, record an N/A rationale in `result.md` and `00_project_intake.md`.

### Step 7. Create or Update Required Artifacts

Create or update the mandatory and conditional artifacts listed in this skill.

If workflow context files do not exist, initialize them conservatively.

### Step 8. Prepare Next-Stage Handoff

Determine the recommended next step:

```text
- Stage 1 Service Goal Definition
- deeper codebase-context-review skill
- additional human clarification before continuing
- project profile / specialization confirmation
```

Update `context_packet.md` with only the minimum context needed for the next step.

### Step 9. Present Human Approval Gate

End with a human approval section. Do not proceed as if approval has been granted.

---

## 11. Output Artifacts

### 11.1 Mandatory Artifacts

Create or update:

```text
/workflow/00_intake/00_project_intake.md
/workflow/00_intake/result.md
/workflow/context/context_packet.md
```

### 11.2 Conditional Artifacts

Create or update when applicable:

```text
/workflow/00_intake/00_existing_context_review.md
  if existing code, documents, tests, deployment, data, or infrastructure must be understood before later stages

/workflow/context/artifact_manifest.yml
  if artifact tracking is enabled, absent, or needs initialization

/workflow/context/ASSUMPTIONS.md
  if working assumptions are introduced or changed

/workflow/context/OPEN_QUESTIONS.md
  if unresolved questions affect later stages

/workflow/context/REJECTED_OPTIONS.md
  if the user explicitly rejected or superseded an option

/workflow/context/TRACEABILITY_MATRIX.md
  if traceability tracking is enabled or should be initialized

/workflow/context/APPROVAL_LOG.md
  only if explicit human approval is provided and the workflow uses approval logging
```

### 11.3 N/A Record

For each skipped conditional artifact, record:

```text
- artifact name
- why it is not applicable now
- what future condition would make it applicable
```

Example:

```text
Artifact: /workflow/00_intake/00_existing_context_review.md
N/A Reason: No existing codebase, deployment, production data, compatibility constraint, or forbidden change area has been provided.
Revisit If: The user provides repository access, migration context, existing system constraints, or forbidden change areas.
```

---

## 12. Required Output Structures

### 12.1 `/workflow/00_intake/00_project_intake.md`

Use this structure:

```markdown
# 00 Project Intake

## 1. Intake Summary

## 2. Source Inputs Reviewed

## 3. Project Type Classification

| Dimension | Candidate Classification | Evidence | Confidence | Approval Status |
|---|---|---|---|---|

## 4. Project Profile Candidates

## 5. Existing Context Inventory

### 5.1 Documents
### 5.2 Codebase
### 5.3 Tests
### 5.4 Data / Dataset
### 5.5 Infrastructure / Deployment
### 5.6 External Services / APIs / LLMs

## 6. Explicitly Approved Decisions

## 7. Decision Candidates Needing Approval

## 8. Working Assumptions

## 9. Open Questions

## 10. Fixed Constraints

### 10.1 Technology Constraints
### 10.2 Scope Constraints
### 10.3 Security / Privacy Constraints
### 10.4 Operational Constraints
### 10.5 Schedule / Resource Constraints

## 11. Forbidden Change Areas

## 12. Early Risk Signals

## 13. Specialization Hooks to Consider

## 14. N/A Records

## 15. Recommended Next Step
```

### 12.2 `/workflow/00_intake/00_existing_context_review.md`

When applicable, use this structure:

```markdown
# 00 Existing Context Review

## 1. Review Scope

## 2. Existing System Summary

## 3. Existing Codebase Inventory

## 4. Existing Documentation Inventory

## 5. Existing Tests and Validation

## 6. Existing Data / Database / Dataset Context

## 7. Existing Deployment / Infrastructure Context

## 8. Compatibility Constraints

## 9. Areas That Must Not Be Changed

## 10. Known Risks or Fragile Areas

## 11. Required Inputs for Later Stages

## 12. Open Questions for Human Review
```

### 12.3 `/workflow/00_intake/result.md`

Use this structure:

```markdown
# Result: Stage 0 Project Intake

## 1. Task Summary

## 2. Inputs Used

## 3. Outputs Created or Updated

## 4. Project Classification Summary

## 5. Key Findings

## 6. Decision Candidates

## 7. Working Assumptions

## 8. Open Questions

## 9. Risks and Constraints

## 10. Rejected or Superseded Options

## 11. N/A Records

## 12. Traceability Updates

## 13. Context Packet Update Summary

## 14. Human Approval Required

## 15. Recommended Next Step
```

### 12.4 `/workflow/context/context_packet.md`

Use this structure:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: Stage 0 Project Intake
- Completed stages:
- Next recommended stage:
- Intake status: draft / ready for approval / approved / blocked

## 2. Approved Decisions
- Only decisions explicitly approved by the human developer.

## 3. Working Assumptions
- Project type assumptions.
- Project profile assumptions.
- Stack assumptions.
- Existing-context assumptions.

## 4. Open Questions
- Questions that may affect later stages.

## 5. Rejected / Superseded Options
- Options rejected or superseded during intake.

## 6. Constraints That Must Not Be Violated
- Technology:
- Security:
- Privacy:
- Scope:
- Schedule:
- Operational:
- Existing-system compatibility:

## 7. Key Context for Next Stage
- Minimal project summary.
- Project type/profile candidate.
- Existing context summary.
- Fixed decisions and constraints.
- Early risks.
- What the next stage should focus on.

## 8. Required Inputs for Next Stage
- /workflow/00_intake/00_project_intake.md
- /workflow/00_intake/00_existing_context_review.md, if applicable
- /workflow/context/DECISIONS.md, if available
- /workflow/context/ASSUMPTIONS.md, if available
- /workflow/context/OPEN_QUESTIONS.md, if available
- Essential source documents identified during intake.

## 9. Do Not Do
- Do not treat assumptions as approved decisions.
- Do not start architecture or implementation without approved goals and requirements.
- Do not ignore forbidden change areas.
- Do not use superseded or rejected artifacts.
```

---

## 13. Decision / Assumption / Open Question Rules

Classify information carefully.

### Approved Decision

Use only when there is explicit human approval.

Examples:

```text
Approved: The project will use Firebase Auth.
Approved: The MVP is a web application, not a mobile app.
```

### Decision Candidate

Use when recommending or identifying something that needs approval.

Example:

```text
Candidate: Treat this as a greenfield MVP production project.
```

### Working Assumption

Use when progress requires a temporary assumption.

Example:

```text
Assumption: No existing production users exist because no deployed system was mentioned.
```

### Open Question

Use when unresolved information may affect later stages.

Example:

```text
Open Question: Does the system process personal data or only anonymized records?
```

### Rejected Option

Use only when the human explicitly rejected or superseded an option.

Example:

```text
Rejected: Do not use a relational database for the MVP unless reopened by the human developer.
```

Rules:

- Do not convert assumptions into decisions.
- Do not convert recommendations into requirements.
- Do not revive rejected options unless explicitly reopened by the human.
- Do not record agent-generated decisions in `DECISIONS.md`.
- Record assumptions and open questions in their proper files when applicable.

---

## 14. Traceability Rules

Stage 0 does not create requirement-level traceability.

Preserve lightweight intake traceability from:

```text
User-provided source
→ intake finding
→ decision candidate / assumption / open question / constraint
→ affected future stage
```

If `TRACEABILITY_MATRIX.md` is initialized, use this lightweight structure:

```markdown
| Trace ID | Source | Intake Finding | Classification | Affected Future Stage | Status |
|---|---|---|---|---|---|
```

Rules:

- Do not create requirement IDs unless the user explicitly provided already-approved requirements.
- Do not convert user ideas into requirements.
- Do not map to tests, tasks, or implementation evidence yet.
- Mark future traceability needs for Stage 1 and Stage 3.

---

## 15. Specialization Hooks

Identify possible specialization addenda for later stages. Do not execute full specialization procedures inside Stage 0.

### 15.1 Web SaaS Hook

Activate if the project includes a web app, hosted service, authenticated users, admin console, API backend, or multi-tenant behavior.

Record possible later needs:

```text
- authentication
- authorization roles
- hosting/deployment
- API boundary
- data access rules
- observability
```

### 15.2 Mobile App Hook

Activate if native or cross-platform mobile development is mentioned.

Record possible later needs:

```text
- platform targets
- app store/release constraints
- device permissions
- offline/sync behavior
- push notifications
```

### 15.3 AI / Data Product Hook

Activate if datasets, ML models, LLMs, evaluation, labeling, synthetic data, or research experiments are mentioned.

Record possible later needs:

```text
- data provenance
- dataset access
- labeling policy
- evaluation metrics
- reproducibility
- model risk
- human review
```

### 15.4 Regulated / Security-Sensitive Hook

Activate if personal, sensitive, legal, medical, financial, educational, biometric, child-related, workplace-monitoring, or confidential data is mentioned.

Record possible later needs:

```text
- privacy impact review
- threat model
- audit logging
- access control
- data retention/deletion
- release blockers
```

### 15.5 Brownfield / Legacy Hook

Activate if an existing codebase, production system, deployed app, migration, compatibility requirement, or forbidden change area exists.

Record possible later needs:

```text
- codebase-context-review
- compatibility constraints
- regression baseline
- migration risks
- fragile modules
- existing test coverage
```

---

## 16. Validation Checklist

Before completing this skill, verify:

```text
[ ] Project type candidate is identified or uncertainty is clearly recorded.
[ ] Project profile candidate is identified or uncertainty is clearly recorded.
[ ] Existing context has been inventoried at the appropriate depth.
[ ] Existing-context review has been created or explicitly marked N/A.
[ ] Fixed technology decisions are separated from technology preferences.
[ ] Forbidden change areas are recorded when present.
[ ] Approved decisions are separated from assumptions and recommendations.
[ ] Open questions are recorded with downstream impact.
[ ] Early security/privacy/data/LLM/external API risk signals are recorded when visible.
[ ] No requirements, architecture, data model, task plan, or implementation work has been started.
[ ] Mandatory artifacts are created or updated.
[ ] Conditional artifacts are created or marked N/A.
[ ] context_packet.md contains only the minimum context needed by the next stage.
[ ] Human approval items are clearly listed.
```

---

## 17. Human Approval Gate

End the stage with this approval section.

```markdown
## Human Approval Required

### Decisions to Approve
- Project context type:
- Project profile:
- Greenfield / brownfield / prototype / research / extension / migration / maintenance classification:
- Fixed technology stack, if any:
- Source documents, code, tests, data, or deployment context to treat as trusted inputs:
- Forbidden change areas:
- Initial security/privacy/data/operational constraints:
- Whether deeper codebase-context-review is needed:
- Next recommended stage:

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Risks to Review
- ...

### Artifacts Ready for Review
- /workflow/00_intake/00_project_intake.md
- /workflow/00_intake/00_existing_context_review.md, if applicable
- /workflow/00_intake/result.md
- /workflow/context/context_packet.md

### Recommended Next Step
- ...
```

Rules:

- Do not claim approval unless the human explicitly provided it.
- Do not proceed to Stage 1 as if approval has been granted.
- If the human asks to continue without formal approval, record that instruction clearly.
- Do not update `DECISIONS.md` or `APPROVAL_LOG.md` unless explicit approval exists.

---

## 18. Failure Handling

If the skill cannot be completed safely, produce a partial result and blocker report.

Use this structure:

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

Failure cases include:

```text
- no project description and no repository/context to inspect
- required existing-code access is unavailable for brownfield/extension/migration work
- user directive conflicts with approved decision
- artifact manifest marks a needed artifact as superseded or rejected
- privacy/security constraint is too ambiguous to continue safely
- current task asks for requirements, architecture, or implementation before intake approval
```

If progress is possible with assumptions, mark those assumptions explicitly.

---

## 19. Do Not Do

Do not:

```text
- treat a vague idea as an approved project goal
- treat a suggested stack as an approved stack
- assume the project is greenfield when existing code or deployment is mentioned
- assume production readiness when the user asked for a prototype or research tool
- start requirements before intake is approved
- start architecture before project type and constraints are understood
- read the entire source tree by default
- ignore existing tests, deployment, data, or compatibility constraints in brownfield work
- record agent-inferred project classification as an approved decision
- use context_packet.md as the only source of truth
- skip N/A records for conditional artifacts
- fail to identify whether specialization addenda should be considered
- modify production code
- claim validation or approval that did not happen
```

---

## 20. Completion Criteria

This skill is complete when:

```text
[ ] /workflow/00_intake/00_project_intake.md exists and follows the required structure.
[ ] /workflow/00_intake/result.md exists and follows the required structure.
[ ] /workflow/context/context_packet.md is created or updated for the next stage.
[ ] /workflow/00_intake/00_existing_context_review.md is created or marked N/A.
[ ] Assumptions, open questions, rejected options, and approval needs are separated.
[ ] Early risk signals are recorded when visible.
[ ] The next recommended step is clearly stated.
[ ] Human approval is requested.
```
