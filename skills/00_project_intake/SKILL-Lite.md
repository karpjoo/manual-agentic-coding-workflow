---
name: project-intake
description: Execute Stage 0 to classify project context, review existing inputs, capture constraints, and prepare next-stage handoff.
stage: "00 Project Intake / Existing Context Review"
version: 2.2.0
status: reusable
primary_output: "/workflow/00_intake/00_project_intake.md"
requires_human_approval: true
---

# Project Intake Skill

Use this skill at the beginning of a workflow, or when Stage 0 must be rerun after user correction. It establishes trustworthy starting context before service goal, requirements, domain modeling, architecture, data design, task breakdown, or implementation.

## 1. Operating Rules

The agent is a structured assistant, not the final decision-maker. Keep these separate:

```text
approved decision / decision candidate / working assumption / open question / rejected option / risk / recommendation
```

Never convert agent proposals, inferences, assumptions, or outputs into human-approved decisions.

## 2. Files to Check First

Check these files if they exist:

```text
/skills/00_project_intake/artifact_contract.yml
/skills/00_project_intake/README.md
/workflow/00_intake/USER_DIRECTIVES.md
/workflow/00_intake/review_notes.md
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/APPROVAL_LOG.md
```

Use `artifact_contract.yml` as the official Stage 0 artifact contract when present. If it conflicts with this `SKILL.md`, report the conflict. `README.md` is human guidance only.

## 3. Input Precedence

```text
1. Current explicit user instruction
2. /workflow/00_intake/USER_DIRECTIVES.md
3. APPROVAL_LOG.md / DECISIONS.md
4. artifact_manifest.yml
5. context_packet.md
6. Approved artifacts
7. Working assumptions
8. Agent inference
```

Do not silently resolve conflicts. Report sources, impact, and whether progress is blocked.

## 4. Input Contract

### Always Check

```text
- current user instruction or initial project description
- USER_DIRECTIVES.md, if present
- workflow context files, if present
- artifact_contract.yml, if present
```

### Read If Applicable

```text
- project README/docs, if a project folder exists
- package/build/config files, if stack detection is needed
- deployment/infra files, if deployment context exists
- tests or CI files, if an existing codebase exists
- dataset/model/evaluation notes, if AI/data product context exists
- privacy/security/compliance notes, if sensitive or regulated data may exist
```

### Do Not Read By Default

```text
- entire source tree
- large datasets
- raw logs
- generated artifacts
- credential or secret files
- superseded/rejected artifacts
- unrelated historical drafts
```

Missing workflow context files are usually non-blocking in the first Stage 0 run. Missing initial project description is blocking unless the user only requested repository inventory.

## 5. Stage Scope

In scope:

```text
project/profile classification; existing document/code/test/data/deployment inventory; fixed stack and forbidden change capture; decision/assumption/question separation; early security/privacy/data/external API/LLM risk signal detection; deeper codebase-review decision; next-stage handoff
```

Out of scope:

```text
service goal finalization; requirements; acceptance criteria; domain modeling; architecture/API/database design; task breakdown; implementation prompts; code modification
```

## 6. Classification

Classify using both dimensions:

```text
Development context type:
greenfield / brownfield / prototype / research tool / extension / migration / maintenance / exploratory

Project profile:
lightweight prototype / MVP production / production system / regulated-security-sensitive / web SaaS / internal tool / mobile app / AI-data product / developer tooling / educational project
```

For each classification, provide evidence, confidence, and approval status. Treat it as a decision candidate unless explicitly approved.

## 7. Execution Procedure

### Step 1. Preflight

```text
1. Confirm this is Stage 0.
2. Read current user instruction.
3. Read USER_DIRECTIVES.md if present.
4. Read artifact_contract.yml if present.
5. Check existing workflow context files if present.
6. Identify missing, draft, superseded, rejected, or conflicting inputs.
7. Decide whether progress is safe, blocked, or possible with assumptions.
```

### Step 2. Establish Intake Mode

Identify the run type:

```text
initial intake / intake rerun / existing-context review trigger / project-profile selection / context initialization / intake finalization
```

### Step 3. Collect Starting Context

Summarize only available information: project idea, documents, codebase status, tests, deployment, data/datasets, mentioned users/operators, fixed stack, forbidden areas, risks, and constraints.

### Step 4. Classify and Separate

Create clear sections for:

```text
approved decisions / decision candidates / working assumptions / open questions / rejected or superseded options / risks and constraints
```

### Step 5. Decide Existing Context Review Need

Create `/workflow/00_intake/00_existing_context_review.md` if existing code, deployment, data, compatibility constraints, migration context, maintenance work, or forbidden change areas exist. Otherwise record an N/A rationale.

### Step 6. Produce Artifacts

Create or update at minimum:

```text
/workflow/00_intake/00_project_intake.md
/workflow/00_intake/result.md
/workflow/context/context_packet.md
```

Follow `artifact_contract.yml` for full mandatory/conditional artifact rules. Do not update `DECISIONS.md` unless explicit human approval exists.

### Step 7. Present Approval Gate

End with decisions to approve, assumptions to confirm, open questions, risks, artifacts ready for review, and recommended next step.

## 8. Output Requirements

`00_project_intake.md` must include:

```text
Intake Summary; Source Inputs Reviewed; Project Type Classification; Project Profile Candidates; Existing Context Inventory; Explicitly Approved Decisions; Decision Candidates; Working Assumptions; Open Questions; Fixed Constraints; Forbidden Change Areas; Early Risk Signals; Specialization Hooks; Recommended Next Step
```

`result.md` must include:

```text
Task Summary; Inputs Used; Outputs Created or Updated; Project Classification Summary; Key Findings; Decision Candidates; Working Assumptions; Open Questions; Risks and Constraints; N/A Records; Context Packet Update Summary; Human Approval Required; Recommended Next Step
```

`00_existing_context_review.md`, when applicable, must summarize review scope, existing system/code/docs/tests/data/deployment, compatibility constraints, forbidden areas, known risks, required later inputs, and open questions.

## 9. Context Packet Rules

Update `/workflow/context/context_packet.md` as concise next-stage handoff, not full project history. Required sections:

```text
Current Project State; Approved Decisions; Working Assumptions; Open Questions; Rejected/Superseded Options; Constraints That Must Not Be Violated; Key Context for Next Stage; Required Inputs for Next Stage; Do Not Do
```

Point to source artifacts instead of copying them.

## 10. Human Approval Required

End every run with:

```markdown
## Human Approval Required

### Decisions to Approve
- Project type
- Project profile
- Fixed technology stack, if any
- Source inputs to trust
- Forbidden change areas
- Initial security/privacy/data/operational constraints
- Whether to proceed to Stage 1 or deeper codebase-context review

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

Do not claim approval unless the user explicitly provides it.

## 11. Final Validation

Before finishing, verify:

```text
[ ] Project type/profile is identified or uncertainty is recorded.
[ ] Existing context is inventoried at appropriate depth.
[ ] Existing-context review is created or marked N/A.
[ ] Decisions, assumptions, recommendations, and questions are separated.
[ ] Fixed constraints and forbidden areas are recorded.
[ ] Early risk signals are recorded when visible.
[ ] No later-stage work was started.
[ ] Mandatory artifacts are created or updated.
[ ] context_packet.md is concise and next-stage oriented.
[ ] Human approval gate is present.
```

## 12. Failure Handling

If blocked, create a partial `result.md` with: `Blocking Issue`, `Why It Matters`, `Affected Artifacts or Stages`, `Safe Partial Work Completed`, and `Human Decision Needed`.

If progress continues with assumptions, label them clearly.

## 13. Do Not Do

```text
- Do not treat a vague idea as an approved project goal.
- Do not treat a suggested stack as an approved stack.
- Do not assume greenfield when existing code or deployment is mentioned.
- Do not start requirements, architecture, data design, tasks, or implementation.
- Do not read the entire source tree by default.
- Do not record agent inference as approval.
- Do not skip N/A records for conditional artifacts.
- Do not ignore artifact_contract.yml when present.
- Do not use context_packet.md as the sole source of truth.
```
