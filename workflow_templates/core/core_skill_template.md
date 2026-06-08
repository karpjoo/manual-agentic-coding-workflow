# Core Skill Template for Manual Agentic Coding Workflow

> This template defines the minimum common rules that every `SKILL.md` in the Manual Agentic Coding Workflow must follow.  
> Stage-specific reasoning, project-type specialization, and tool-specific execution details must be added outside this core template.

---

## 0. Template Scope

This Core Skill Template defines the common operating contract for all workflow skills.

Every stage-specific `SKILL.md` must follow this template, but must not copy large unrelated procedures into the core section.

This template covers:

- agent role and operating mode
- input precedence
- artifact reading rules
- `USER_DIRECTIVES.md` handling
- decision / assumption / open question separation
- output artifact rules
- `context_packet.md` update rules
- traceability expectations
- human approval gate
- failure handling
- do-not-do rules

This template does not define:

- detailed requirements writing methods
- DDD aggregate design methods
- API contract design methods
- database schema design methods
- TDD implementation loop details
- security review checklist details
- project-type-specific rules
- tool-specific command conventions

Those belong in:

- Stage-Specific Skill Template
- Reusable Stage `SKILL.md`
- Optional Specialization Addendum
- Tool-Specific Wrapper

---

## 1. Required Metadata

Every `SKILL.md` must start with metadata.

```yaml
---
name: [[skill-name]]
description: [[when this skill should be used]]
stage: [[stage number and stage name]]
version: 1.0.0
status: draft
primary_output: [[primary artifact path]]
requires_human_approval: true
---
```

Metadata rules:

- `name` must be stable and reusable.
- `description` must explain when to use the skill, not what project it is for.
- `stage` must identify the workflow stage.
- `primary_output` must point to the main artifact this skill creates or updates.
- `requires_human_approval` should normally be `true` unless the skill is purely informational or mechanical.

---

## 2. Agent Role and Operating Mode

The agent is not an autonomous developer.

The agent is a structured development assistant operating inside a human-controlled workflow.

The agent must:

1. Read approved context before acting.
2. Identify the current stage and task.
3. Read only the necessary inputs.
4. Respect current user instructions and stage-local directives.
5. Produce explicit artifacts.
6. Separate facts, approved decisions, assumptions, proposals, risks, and open questions.
7. Update the context needed by the next stage.
8. Ask for human review where approval is required.

The agent must follow these distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```

---

## 3. Input Precedence Rules

When inputs conflict, use this precedence order:

```text
1. Current explicit user instruction
2. Stage-local USER_DIRECTIVES.md
3. APPROVAL_LOG.md / DECISIONS.md
4. artifact_manifest.yml
5. context_packet.md
6. Approved stage artifacts
7. Working assumptions
8. Agent inference
```

Conflict handling:

- Do not silently resolve conflicts.
- Report the conflict explicitly.
- Identify which sources conflict.
- Explain the likely impact.
- Continue only if the conflict is non-blocking.
- If the conflict affects scope, architecture, data, privacy, security, implementation, or release, stop and request human decision.

---

## 4. Standard Files to Check

Every skill must check the following files when they exist:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
```

The stage-specific skill must define which previous stage artifacts are:

```text
Always Read
Read If Applicable
Do Not Read By Default
```

The agent must not read all historical artifacts by default.

---

## 5. USER_DIRECTIVES.md Handling

If a `USER_DIRECTIVES.md` file exists in the current stage folder, the agent must read it before executing the skill.

Example location:

```text
/workflow/[[stage-folder]]/USER_DIRECTIVES.md
```

Rules:

- Treat `USER_DIRECTIVES.md` as stage-local human instruction.
- Apply it before agent assumptions.
- Do not automatically treat every directive as a globally approved decision.
- Distinguish between:
  - explicit approval
  - correction
  - preference
  - new requirement
  - rejection
  - scope change
  - question
- If a directive conflicts with approved decisions, report it as a conflict.
- Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

---

## 6. Input Contract

Every stage-specific skill must define an input contract using this structure.

```markdown
## Required Inputs

### Always Read
- [[path]]
- [[path]]

### Read If Applicable
- [[path]] — if [[condition]]
- [[path]] — if [[condition]]

### Do Not Read By Default
- full historical agent logs
- superseded artifacts
- rejected artifacts
- unrelated previous stage drafts
- implementation files not needed for the current stage

### Missing Input Handling
If a required input is missing:
1. Report the missing input.
2. Explain why it matters.
3. Mark it as blocking or non-blocking.
4. If non-blocking, proceed with a clearly labeled working assumption.
5. If blocking, stop and request human input.
```

Only approved artifacts may be used as source of truth unless the user explicitly requests exploratory work.

---

## 7. Input Preflight Procedure

Before producing outputs, the agent must perform a preflight check.

```text
[ ] Read the current SKILL.md.
[ ] Read artifact_manifest.yml if available.
[ ] Read context_packet.md if available.
[ ] Read DECISIONS.md if available.
[ ] Check whether USER_DIRECTIVES.md exists.
[ ] Identify Always Read inputs.
[ ] Identify conditional inputs activated by project profile or context.
[ ] Verify required inputs exist.
[ ] Verify source artifacts are approved or clearly marked as draft.
[ ] Check for superseded or rejected artifacts.
[ ] Identify missing, ambiguous, or conflicting information.
[ ] Restate the current task in one short section before proceeding.
```

If preflight reveals a blocking issue, the agent must not continue as if the issue were resolved.

---

## 8. Execution Procedure

Every skill must follow this general execution procedure.

```text
1. Confirm the current stage and purpose.
2. Read required context and approved source artifacts.
3. Apply USER_DIRECTIVES.md if present.
4. Identify missing information and uncertainty.
5. Execute the stage-specific procedure.
6. Produce or update required artifacts.
7. Produce conditional artifacts if applicable.
8. Record N/A rationale for non-applicable conditional artifacts.
9. Separate decisions, assumptions, open questions, risks, and recommendations.
10. Update context_packet.md for the next stage.
11. Update ASSUMPTIONS.md, OPEN_QUESTIONS.md, and REJECTED_OPTIONS.md as appropriate.
12. Do not update DECISIONS.md unless explicit human approval exists.
13. Present a human approval gate.
```

The stage-specific skill may add more detailed steps, but must not remove these core steps.

---

## 9. Output Artifact Contract

Every stage-specific skill must define its output artifact contract.

```markdown
## Output Artifacts

### Mandatory Artifacts
- [[path]] — [[purpose]]
- [[path]] — [[purpose]]

### Conditional Artifacts
- [[path]] — if [[condition]]
- [[path]] — if [[condition]]

### N/A Record
If a conditional artifact is not applicable, record:
- artifact name
- why it is not applicable
- what change would make it applicable later
```

Artifact rules:

- Outputs must be concrete markdown, YAML, JSON, code, or test evidence files.
- Avoid vague summaries as the only output.
- Do not overwrite approved artifacts without explicitly preserving prior decisions or noting supersession.
- If revising an artifact, indicate what changed and why.
- If an artifact is draft, label it as draft.
- If an artifact requires approval, state that it is not approved yet.

---

## 10. Required Result Structure

Unless a stage-specific skill defines a stronger structure, each `result.md` should include:

```markdown
# Result: [[skill-name]]

## 1. Task Summary

## 2. Inputs Used

## 3. Outputs Created or Updated

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

## 11. Decision / Assumption / Open Question Rules

The agent must classify information carefully.

### Approved Decision

Use only when there is explicit human approval.

Examples:

```text
Approved: The project will use Firebase Auth.
Approved: MVP will include only admin review, not public user accounts.
```

### Decision Candidate

Use when the agent recommends a decision that needs human approval.

```text
Candidate: Use role-based access control with Admin, Reviewer, and Viewer roles.
```

### Working Assumption

Use when progress requires a temporary assumption.

```text
Assumption: The first release targets a web MVP, not a mobile app.
```

### Open Question

Use when unresolved information may affect later work.

```text
Open Question: Should expert reviewers be able to revise submitted evaluations?
```

### Rejected Option

Use when an option has been explicitly rejected or superseded.

```text
Rejected: Do not use a relational database for the MVP unless reopened by the human developer.
```

Rules:

- Do not convert assumptions into decisions.
- Do not convert recommendations into requirements.
- Do not revive rejected options unless the human explicitly reopens them.
- Do not record agent-generated decisions in `DECISIONS.md`.
- Record assumptions and open questions in their proper files.

---

## 12. Traceability Rules

Every skill should preserve or improve traceability where applicable.

Traceability may link:

```text
Goal
→ Requirement
→ Acceptance Criteria
→ Domain Concept
→ Architecture Component
→ Data Model
→ Task
→ Test
→ Implementation Evidence
```

Rules:

- Do not break existing IDs without reason.
- If new IDs are introduced, use a stable naming convention.
- If requirements, tasks, tests, or artifacts are changed, update traceability.
- If traceability cannot be completed, record the gap under Open Questions or Traceability Gaps.

Stage-specific skills must define the exact traceability links required for that stage.

---

## 13. Context Packet Update Rules

Every skill must update or prepare `context_packet.md` for the next stage.

`context_packet.md` is not a full project history. It is the minimal operational context needed by the next stage.

The update must include:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage:
- Completed stages:
- Next recommended stage:

## 2. Approved Decisions
- Only human-approved decisions.

## 3. Working Assumptions
- Temporary assumptions not yet confirmed.

## 4. Open Questions
- Questions that may affect future stages.

## 5. Rejected / Superseded Options
- Options that should not be reused unless reopened.

## 6. Constraints That Must Not Be Violated
- Technology:
- Security:
- Privacy:
- Scope:
- Schedule:
- Operational:

## 7. Key Context for Next Stage
- Minimal context needed by the next skill.

## 8. Required Inputs for Next Stage
- Artifacts the next stage should read.

## 9. Do Not Do
- Actions or assumptions the next agent must avoid.
```

Rules:

- Keep it concise.
- Do not copy entire artifacts into `context_packet.md`.
- Use it as a navigation layer, not as the sole source of truth.
- Point to source artifacts where details live.
- Include only context useful for the next stage.

---

## 14. Human Approval Gate

Every skill must end with a human approval section unless explicitly marked otherwise.

Use this structure:

```markdown
## Human Approval Required

### Decisions to Approve
- ...

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Risks to Review
- ...

### Artifacts Ready for Review
- ...

### Recommended Next Step
- ...
```

Rules:

- Do not claim approval unless the human explicitly provided it.
- Do not proceed to the next stage as if approval has been granted.
- If the user asks the agent to continue without approval, record that instruction clearly.
- Human approval is required for major changes to:
  - service goal
  - MVP scope
  - non-goals
  - roles and permissions
  - personal data handling
  - external API or LLM transfer
  - domain terminology
  - architecture direction
  - database schema
  - API contracts
  - release order
  - implementation prompts
  - deployment
  - workflow improvement priorities

---

## 15. Failure Handling

If the skill cannot be completed safely, the agent must produce a partial result instead of pretending completion.

Failure cases include:

- required approved input is missing
- artifact conflict exists
- user directive conflicts with approved decision
- project scope is ambiguous
- security or privacy issue blocks progress
- required file cannot be found
- implementation validation cannot be run
- source artifact is superseded or rejected

Failure response must include:

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

If progress is possible with assumptions, the assumptions must be explicitly marked.

---

## 16. Do Not Do

The agent must not:

- treat itself as the final decision-maker
- use unapproved drafts as source of truth
- silently turn assumptions into requirements
- silently turn recommendations into decisions
- ignore `USER_DIRECTIVES.md`
- ignore `artifact_manifest.yml`
- use superseded or rejected artifacts as current truth
- read all historical files by default
- use `context_packet.md` as the only source of truth
- overwrite approved decisions without approval
- revive rejected options without explicit instruction
- skip human approval gates
- produce vague summaries instead of concrete artifacts
- claim tests passed without evidence
- claim implementation is complete without validation
- mix tool-specific execution rules into domain or stage logic
- mix project-type specialization rules into the core template
- add stage-specific design methods into this core template

---

## 17. Stage-Specific Extension Hook

Each stage-specific skill must extend this core template by defining:

```markdown
## Stage-Specific Extension

### Stage Purpose

### Core Question

### Always Read Inputs

### Read If Applicable Inputs

### Do Not Read By Default

### Stage-Specific Procedure

### Mandatory Artifacts

### Conditional Artifacts

### Required Output Structure

### Traceability Requirements

### Validation Checklist

### Human Approval Gate

### Next Context Packet Rules
```

The stage-specific extension must not weaken the core rules.

---

## 18. Specialization Addendum Hook

If a project-type specialization addendum exists, the skill must apply it after reading the core and stage-specific rules.

Examples:

```text
web_saas.md
mobile_app.md
ai_data_product.md
regulated_security_sensitive.md
brownfield_legacy.md
internal_tool.md
```

Specialization may add:

- additional inputs
- additional questions
- additional artifacts
- additional validation requirements
- additional risks
- additional approval requirements

Specialization must not replace the stage-specific skill.

---

## 19. Tool Wrapper Hook

Tool-specific wrappers may define:

- file locations
- command conventions
- sandbox or permission rules
- review UI behavior
- artifact save conventions
- tool-specific execution notes

Tool wrappers must not define domain, requirement, architecture, data, or test strategy decisions.

---

## 20. Core Quality Checklist

Before a `SKILL.md` is considered usable, check:

```text
[ ] It preserves the agent-as-assistant role.
[ ] It separates approved decisions, assumptions, open questions, risks, and recommendations.
[ ] It defines input precedence.
[ ] It defines Always Read / Read If Applicable / Do Not Read By Default.
[ ] It defines missing input handling.
[ ] It checks USER_DIRECTIVES.md.
[ ] It checks artifact_manifest.yml.
[ ] It avoids using context_packet.md as the sole source of truth.
[ ] It defines mandatory and conditional artifacts.
[ ] It requires N/A records for skipped conditional artifacts.
[ ] It defines result.md expectations.
[ ] It defines context_packet.md update rules.
[ ] It includes human approval gate.
[ ] It includes failure handling.
[ ] It includes do-not-do rules.
[ ] It leaves stage-specific methods to stage-specific skills.
[ ] It leaves project-type concerns to specialization addenda.
[ ] It leaves tool-specific behavior to tool wrappers.
```
