# Stage-Specific Skill Template: Stage 0 Project Intake / Existing Context Review

> Target path: `/workflow_templates/stage_templates/00_project_intake_skill_template.md`  
> Template type: Stage-specific skill template  
> This is **not** an executable `SKILL.md`.  
> This template defines only the Stage 0 extension that will later be combined with the Core Skill Template to create `/skills/00_project_intake/SKILL.md`.

---

## 1. Stage Purpose

Stage 0 identifies the starting context of the project before any service goal, requirement, domain model, architecture, data design, task breakdown, or implementation work begins.

The purpose of this stage is to determine:

- whether the project is new or based on an existing system;
- what project profile should guide later workflow behavior;
- what user-provided context already exists;
- what decisions have already been approved by the human developer;
- what is still only a working assumption;
- what documents, code, tests, infrastructure, or deployment settings already exist;
- what technology stack or tool choices are fixed;
- what areas must not be changed;
- what early security, privacy, regulatory, operational, or research constraints are visible;
- what the next stage must read and must avoid assuming.

This stage prevents the agent from starting requirements, architecture, database design, or implementation work before understanding the current project context.

---

## 2. Core Question

```text
What is the trustworthy starting context for this project, and what must later stages treat as approved, assumed, unknown, rejected, fixed, or forbidden?
```

Supporting questions:

```text
Is this a greenfield project, brownfield project, prototype, research tool, product MVP, extension, migration, or maintenance effort?
What context has the human developer already provided?
What existing artifacts, code, infrastructure, tests, or deployment settings exist?
Which technology choices are already fixed?
Which areas are explicitly out of scope or forbidden to change?
Which decisions are approved and which are only assumptions?
Which project-type specialization addenda should be activated later?
What information should Stage 1 Service Goal Definition receive?
```

---

## 3. Stage Scope

### In Scope

The Stage 0 reusable SKILL created from this template may:

- classify the project type and project profile;
- inventory user-provided documents, existing artifacts, and available codebase context;
- identify fixed decisions, constraints, and forbidden change areas;
- identify early security, privacy, regulatory, operational, or data concerns;
- identify whether a deeper codebase-context-review skill is needed before Stage 1;
- initialize or update Stage 0 project-intake artifacts;
- initialize or update workflow context files when they do not exist;
- prepare the minimum context required by the next stage;
- request human approval for project type, project profile, fixed constraints, and next-step direction.

### Out of Scope

The Stage 0 reusable SKILL created from this template must not:

- define final service goals;
- decompose requirements;
- write acceptance criteria;
- perform domain modeling;
- design architecture or API contracts;
- design database schema or data access rules;
- create task breakdowns;
- write implementation prompts;
- modify production code;
- make irreversible decisions about technology, scope, privacy, or architecture without human approval.

---

## 4. Project Classification Model

The Stage 0 SKILL must classify the project using two complementary dimensions.

### 4.1 Development Context Type

Use one or more of the following:

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

### 4.2 Project Profile

Use one or more of the following:

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

### 4.3 Classification Rules

The SKILL must:

```text
- mark the classification as a decision candidate unless the human has explicitly approved it;
- explain evidence for each classification;
- list uncertainty when classification is ambiguous;
- activate relevant specialization hooks based on classification;
- avoid assuming greenfield when existing code, deployment, users, or data are mentioned;
- avoid assuming production readiness when the user only requested a prototype or research tool.
```

---

## 5. Input Contract

### 5.1 Always Read Inputs

For a new workflow run, Stage 0 may have few or no existing workflow files. The generated SKILL must still check for the following inputs and read them when present:

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
- /workflow/context/APPROVAL_LOG.md
```

If these files do not exist because this is the first workflow stage, the SKILL must treat their absence as expected, not automatically as an error.

### 5.2 Read If Applicable Inputs

The generated SKILL must read the following only when the project context indicates relevance:

```text
- README.md — if a repository or project folder exists
- docs/, documentation/, design/, planning/, product/, specs/ — if documentation folders exist
- package.json, pyproject.toml, requirements.txt, pubspec.yaml, go.mod, pom.xml, build.gradle, Cargo.toml — if codebase or technology stack detection is needed
- firebase.json, firestore.rules, firestore.indexes.json — if Firebase is present or mentioned
- vercel.json, netlify.toml, Dockerfile, docker-compose.yml, k8s/, terraform/, infra/ — if deployment or infrastructure context exists
- .env.example, config examples, secrets policy documents — if environment or secret handling is relevant
- tests/, e2e/, integration test folders — if an existing codebase has tests
- CI configuration files — if release or validation workflow already exists
- existing product brief, research plan, grant proposal, PRD, user interview notes — if provided by the user
- dataset description, data dictionary, labeling guide — if project may be an AI/data product or research tool
- compliance, privacy, security, or legal notes — if project handles personal, sensitive, regulated, or external data
```

### 5.3 Do Not Read By Default

The generated SKILL must not read the following by default:

```text
- full source code tree when only high-level intake is needed
- raw logs unless the project is explicitly debugging or incident-oriented
- large datasets
- generated build artifacts
- dependency lockfiles unless stack or dependency state must be confirmed
- old drafts or superseded planning documents unless referenced as current by the user or artifact manifest
- unrelated previous project artifacts
- private secrets or local environment files containing credentials
```

### 5.4 Missing Input Handling

If expected intake information is missing, the generated SKILL must classify the missing item as one of:

```text
- expected absence for a new Stage 0 run
- non-blocking gap
- blocking gap
- human approval needed
- deeper review needed
```

Rules:

```text
- Missing workflow context files are non-blocking when this is the first workflow run.
- Missing initial project description is blocking unless the user explicitly asks only for repository/context inventory.
- Missing technology stack is non-blocking for early intake but must be recorded as an open question unless already fixed.
- Missing existing-code access is blocking only if the project is classified as brownfield, extension, migration, maintenance, or codebase review.
- Missing security/privacy details are non-blocking at intake but must be recorded when personal, sensitive, regulated, or external data may exist.
```

---

## 6. Stage-Specific Preflight Additions

In addition to the core preflight procedure, the Stage 0 SKILL must check:

```text
[ ] Is this the first workflow stage or a rerun of Stage 0?
[ ] Does /workflow/00_intake already contain approved or draft intake artifacts?
[ ] Does artifact_manifest.yml mark any Stage 0 artifact as approved, superseded, or rejected?
[ ] Is there an existing repository or only a project idea?
[ ] Has the user explicitly fixed any technology stack, platform, database, hosting, language, framework, or tool?
[ ] Has the user explicitly forbidden changes to any system area?
[ ] Are there personal data, sensitive data, regulated data, external API, LLM, or model/data concerns?
[ ] Is a separate codebase-context-review skill needed before Stage 1?
[ ] Is the next recommended stage Stage 1 Service Goal Definition, or should intake continue?
```

---

## 7. Stage-Specific Procedure

The generated SKILL must perform the following Stage 0-specific procedure.

### Step 1. Establish Intake Mode

Determine whether the run is:

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
- existing data or datasets
- existing users, operators, or stakeholders mentioned
- existing technology stack
- explicitly fixed tools, platforms, frameworks, databases, or hosting decisions
- explicitly forbidden changes or non-negotiable constraints
```

### Step 3. Classify Project Type and Profile

Produce a classification table:

```text
Dimension | Candidate Classification | Evidence | Confidence | Approval Status
```

The classification must remain a decision candidate unless explicitly approved.

### Step 4. Identify Approved Decisions vs Assumptions

Separate:

```text
- explicitly approved decisions
- decision candidates
- working assumptions
- open questions
- rejected or superseded options
- risks and constraints
```

### Step 5. Identify Early Risk Signals

Record early signals only at screening depth:

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

Do not perform a full security/privacy review in Stage 0.

### Step 6. Determine Whether Existing Context Review Is Needed

Create or skip `/workflow/00_intake/00_existing_context_review.md` based on conditions.

Create it if any of the following are true:

```text
- existing codebase is present
- existing deployment is present
- existing database or production data is present
- project modifies, extends, migrates, or maintains an existing system
- user asks to preserve compatibility
- user says some areas must not be changed
- existing tests or CI must be respected
```

If skipped, record an N/A rationale.

### Step 7. Prepare Stage 0 Artifacts

Create or update mandatory and conditional artifacts according to the artifact contract.

### Step 8. Prepare Next-Stage Handoff

Determine whether the next recommended step is:

```text
- Stage 1 Service Goal Definition
- a deeper codebase-context-review skill
- additional user clarification before continuing
- project profile / specialization confirmation
```

Then update `context_packet.md` with only the minimum operational context needed for the next step.

---

## 8. Output Artifact Contract

### 8.1 Mandatory Artifacts

The generated SKILL must produce or update:

```text
/workflow/00_intake/00_project_intake.md
/workflow/00_intake/result.md
/workflow/context/context_packet.md
```

### 8.2 Conditional Artifacts

The generated SKILL must produce or update these when applicable:

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
  if goal or project-context traceability has already started or needs initialization

/workflow/context/APPROVAL_LOG.md
  only if explicit human approval is provided and the workflow uses approval logging
```

### 8.3 N/A Record Rules

For each skipped conditional artifact, record:

```text
- artifact name
- reason it is not applicable now
- condition that would make it applicable later
```

Example:

```text
Artifact: /workflow/00_intake/00_existing_context_review.md
N/A Reason: No existing codebase, deployment, production data, or compatibility constraint has been provided.
Revisit If: User provides repository access, migration context, existing system constraints, or forbidden change areas.
```

---

## 9. Required Output Structure

### 9.1 `/workflow/00_intake/00_project_intake.md`

The generated SKILL must require the following structure:

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

## 14. Recommended Next Step
```

### 9.2 `/workflow/00_intake/00_existing_context_review.md`

When applicable, the generated SKILL must require:

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

### 9.3 `/workflow/00_intake/result.md`

The generated SKILL must require:

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

## 10. N/A Records

## 11. Context Packet Update Summary

## 12. Human Approval Required

## 13. Recommended Next Step
```

---

## 10. Traceability Requirements

Stage 0 is not expected to create requirement-level traceability yet.

However, the generated SKILL must preserve early traceability from:

```text
User-provided source
→ intake finding
→ decision candidate / assumption / open question / constraint
→ next-stage handoff item
```

If `TRACEABILITY_MATRIX.md` is initialized, use lightweight entries such as:

```text
Trace ID | Source | Intake Finding | Classification | Affected Future Stage | Status
```

Rules:

```text
- Do not create requirement IDs in Stage 0 unless the user explicitly provided already-approved requirements.
- Do not convert user ideas into requirements.
- Do not map to tests, tasks, or implementation evidence yet.
- Mark future traceability needs for Stage 1 and Stage 3.
```

---

## 11. Stage-Specific Validation Checklist

The generated SKILL must validate that:

```text
[ ] Project type candidate is identified or the uncertainty is clearly recorded.
[ ] Project profile candidate is identified or the uncertainty is clearly recorded.
[ ] Existing context has been inventoried at the appropriate depth.
[ ] Existing-code review has been created or explicitly marked N/A.
[ ] Fixed technology decisions are separated from technology preferences.
[ ] Forbidden change areas are recorded when present.
[ ] Approved decisions are separated from assumptions and recommendations.
[ ] Open questions are recorded with downstream impact.
[ ] Early security/privacy/data/LLM/external API risk signals are recorded when visible.
[ ] No requirements, architecture, data model, task plan, or implementation work has been started.
[ ] Mandatory artifacts are created or updated.
[ ] Conditional artifacts are created or marked N/A.
[ ] `context_packet.md` contains only the minimum context needed by the next stage.
[ ] Human approval items are clearly listed.
```

---

## 12. Stage-Specific Human Approval Gate

The generated SKILL must end Stage 0 with a human approval request.

### 12.1 Decisions to Approve

Require approval for:

```text
- project context type
- project profile
- whether this is greenfield, brownfield, prototype, research tool, extension, migration, or maintenance
- fixed technology stack, if any
- existing documents, code, tests, data, and deployment context to treat as source inputs
- forbidden change areas
- initial security/privacy/data/operational constraints
- whether a deeper codebase-context-review step is needed
- next recommended stage
```

### 12.2 Assumptions to Confirm

Require confirmation for assumptions such as:

```text
- defaulting to greenfield MVP production
- assuming no existing codebase
- assuming no production data
- assuming no regulated or sensitive data
- assuming default stack is undecided
- assuming Stage 1 Service Goal Definition should be next
```

### 12.3 Open Questions to Resolve

Open questions must be grouped by downstream impact:

```text
- affects Stage 1 Service Goal
- affects Stage 2 Stakeholder / Risk
- affects Stage 3 Requirements
- affects Stage 5 Architecture
- affects Stage 6 Data Design
- affects Stage 8 Test Strategy
- affects Stage 11 Implementation
```

---

## 13. Next `context_packet.md` Rules

The generated SKILL must update or prepare `/workflow/context/context_packet.md` for the next stage.

For Stage 0, the next context packet must include:

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
- Any source documents that Stage 0 identified as essential.

## 9. Do Not Do
- Do not treat assumptions as approved decisions.
- Do not start architecture or implementation without approved goals and requirements.
- Do not ignore forbidden change areas.
- Do not use superseded or rejected artifacts.
```

Rules:

```text
- Keep the context packet concise.
- Do not copy all of 00_project_intake.md into context_packet.md.
- Use source artifact paths for details.
- If Stage 1 is next, include only the context needed to define the service goal.
- If codebase-context-review is next, include the exact code/doc/infrastructure areas to inspect first.
```

---

## 14. Specialization Addendum Hooks

The generated SKILL must identify possible specialization addenda but must not apply their full procedures inside Stage 0.

### 14.1 Web SaaS Hook

Activate when the project includes web app, hosted service, authenticated users, admin console, API backend, or multi-tenant behavior.

Record possible later needs:

```text
- authentication
- authorization roles
- hosting/deployment
- API boundary
- data access rules
- observability
```

### 14.2 Mobile App Hook

Activate when native or cross-platform mobile app development is mentioned.

Record possible later needs:

```text
- platform targets
- app store/release constraints
- device permissions
- offline/sync behavior
- push notifications
```

### 14.3 AI / Data Product Hook

Activate when datasets, ML models, LLMs, evaluation, labeling, synthetic data, or research experiments are mentioned.

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

### 14.4 Regulated / Security-Sensitive Hook

Activate when personal, sensitive, legal, medical, financial, educational, biometric, child-related, workplace-monitoring, or confidential data is mentioned.

Record possible later needs:

```text
- privacy impact review
- threat model
- audit logging
- access control
- data retention/deletion
- release blockers
```

### 14.5 Brownfield / Legacy Hook

Activate when an existing codebase, production system, deployed app, migration, compatibility requirement, or forbidden change area exists.

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

## 15. Anti-Patterns / Do Not Do

The generated SKILL must explicitly prevent the following Stage 0 anti-patterns:

```text
- treating a vague idea as an approved project goal
- treating a suggested stack as an approved stack
- assuming the project is greenfield when existing code or deployment is mentioned
- assuming production readiness when the user asked for a prototype or research tool
- starting requirements before intake is approved
- starting architecture before project type and constraints are understood
- reading the entire source tree by default
- ignoring existing tests, deployment, data, or compatibility constraints in brownfield work
- recording agent-inferred project classification as an approved decision
- using context_packet.md as the only source of truth
- skipping N/A records for conditional artifacts
- failing to identify whether a specialization addendum should be considered
```

---

## 16. Template Quality Checklist

Before this Stage 0 template is used to generate `/skills/00_project_intake/SKILL.md`, verify:

```text
[ ] It defines Stage 0 purpose without repeating the core template.
[ ] It defines a clear core question.
[ ] It defines Stage 0-specific input contracts.
[ ] It handles missing initial workflow files correctly.
[ ] It distinguishes project type from project profile.
[ ] It defines mandatory and conditional artifacts.
[ ] It includes N/A record rules.
[ ] It defines required output structures.
[ ] It prevents requirements, architecture, data design, and implementation work.
[ ] It defines traceability at intake level only.
[ ] It defines validation criteria.
[ ] It defines a Stage 0 human approval gate.
[ ] It defines next context_packet.md update rules.
[ ] It includes specialization hooks without embedding full specialization logic.
[ ] It remains reusable across projects.
[ ] It is context-reset tolerant.
```
