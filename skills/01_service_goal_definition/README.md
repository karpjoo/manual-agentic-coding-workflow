# Service Goal Definition SKILL

## What this SKILL is for

This reusable SKILL runs Stage 1 of the Manual Agentic Coding Workflow:

```text
01_service_goal_definition
```

Its purpose is to define **why the service should exist** before the workflow moves into stakeholder/risk framing, requirements, architecture, data design, testing, task breakdown, or implementation.

The primary project artifact created when this SKILL is executed is:

```text
/workflow/01_goal/01_service_goal.md
```

This artifact defines the problem, target users, core value, desired outcomes, success criteria, non-goals, initial assumptions, open questions, risks, and human approval items.

---

## When to use it

Use this SKILL when:

- Stage 0 Project Intake has been completed, or enough initial context exists to draft a service goal.
- A new service, product, tool, research system, internal workflow, or application needs a clear goal.
- Stage 2 Stakeholder & Risk Framing needs a goal-level input.
- A previous Stage 1 draft needs revision after human review.

---

## When not to use it

Do not use this SKILL when the task is to:

- decompose requirements;
- write acceptance criteria;
- perform stakeholder or risk analysis;
- design architecture;
- design data models;
- create test strategy;
- create implementation tasks;
- write implementation prompts;
- inspect or modify code.

Stage 1 defines the service goal only. Later stages handle the rest.

---

## Required inputs before running

The Agent should read these files when available:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
/workflow/00_intake/00_project_intake.md
/workflow/00_intake/result.md
/workflow/01_goal/USER_DIRECTIVES.md
```

The Agent must check whether each input is approved, draft, superseded, rejected, missing, or conflicting.

Only explicitly approved artifacts and decisions may be treated as source of truth.

---

## Optional or conditional inputs

The Agent may read these only when applicable:

```text
/workflow/00_intake/00_existing_context_review.md
/workflow/00_intake/review_notes.md
/workflow/01_goal/review_notes.md
project brief
initial idea document
product memo
research plan
business memo
problem statement
specialization addendum
tool wrapper
```

Examples of conditional triggers:

- Brownfield or existing-system work activates existing context review.
- Human review comments activate review notes.
- A project profile may activate a specialization addendum.
- A tool-specific environment may activate a tool wrapper.

---

## Outputs created when the SKILL is executed

Mandatory outputs:

```text
/workflow/01_goal/01_service_goal.md
/workflow/01_goal/result.md
/workflow/context/context_packet.md
```

Context files updated when applicable:

```text
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Conditional outputs:

```text
/workflow/01_goal/01_goal_options.md
/workflow/01_goal/01_success_metrics.md
/workflow/01_goal/01_non_goals.md
/workflow/01_goal/review_notes.md
```

Conditional artifacts must either be created or marked N/A in `result.md` with:

```text
Artifact:
Why not applicable:
Revisit if:
```

---

## Human approval requirements

The following Stage 1 items require explicit human approval:

- service goal;
- primary users;
- success criteria;
- non-goals;
- major scope boundaries.

The Agent may propose decision candidates, but proposals are not approved decisions.

The Agent must not update:

```text
/workflow/context/DECISIONS.md
```

unless explicit human approval exists.

---

## How to run this SKILL in an Agentic Coding tool

Use a prompt like this:

```text
Run /skills/01_service_goal_definition/SKILL.md for this project.

Use the current /workflow/context files and /workflow/00_intake outputs as inputs.

Create or update the Stage 1 project artifacts under:

/workflow/01_goal/

Do not proceed to Stage 2.
Do not create requirements, acceptance criteria, stakeholder/risk analysis, architecture, data design, test strategy, implementation tasks, or code.
End with the Human Approval Required section.
```

The Agent should produce the Stage 1 artifacts and stop at the approval gate.

---

## Relationship to previous and next stages

### Previous stage: Stage 0 Project Intake

Stage 0 provides:

- project type;
- initial context;
- fixed constraints;
- existing documents;
- forbidden change areas;
- approved or draft intake findings.

Stage 1 uses Stage 0 as context, but must not redo intake unless Stage 0 is missing or insufficient.

### Next stage: Stage 2 Stakeholder & Risk Framing

Stage 2 uses the Stage 1 goal to identify:

- stakeholders;
- roles;
- permissions;
- sensitive data;
- privacy concerns;
- external systems;
- early risks.

Stage 1 must prepare `context_packet.md` for Stage 2 but must not perform full Stage 2 analysis.

---

## How to interpret artifact status

### Draft

The artifact is usable for review but has not been approved.

### Needs Review

The artifact contains unresolved decisions, conflicts, assumptions, or open questions that require human review.

### Approved

The human developer has explicitly approved the relevant decisions. Only explicitly approved items may be treated as source of truth by downstream stages.

---

## Common mistakes to avoid

Do not:

- treat an Agent recommendation as an approved decision;
- treat assumptions as requirements;
- convert success criteria into acceptance criteria;
- convert target users into finalized stakeholder roles;
- collapse Stage 1 and Stage 2;
- read all downstream artifacts by default;
- use `context_packet.md` as the only source of truth;
- revive rejected options without explicit reopening;
- skip the human approval gate.

---

## Troubleshooting and blocker cases

The Agent should produce a blocker report when:

- no service idea or project context exists;
- Stage 0 is missing and no alternative input exists;
- inputs conflict on service goal, primary users, success criteria, non-goals, or scope boundaries;
- a rejected option is requested again without explicit reopening;
- a required file cannot be read;
- a source artifact is superseded or rejected.

Blocker reports should include:

```text
Blocking Issue
Why It Matters
Affected Artifacts or Stages
Safe Partial Work Completed
Human Decision Needed
```

---

## Recommended next step after successful execution

After the SKILL runs:

1. Review `/workflow/01_goal/01_service_goal.md`.
2. Review `/workflow/01_goal/result.md`.
3. Approve or revise:
   - service goal;
   - primary users;
   - success criteria;
   - non-goals;
   - major scope boundaries.
4. Proceed to Stage 2 only after approval, or explicitly allow Stage 2 to continue with draft status.
