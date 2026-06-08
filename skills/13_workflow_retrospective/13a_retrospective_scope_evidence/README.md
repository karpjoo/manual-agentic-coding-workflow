# 13a Retrospective Scope and Evidence

## What this sub-SKILL is for

This reusable sub-SKILL is part of the Stage 13 Workflow Retrospective & Skill Improvement package.

Defines retrospective scope, included and excluded stages, evidence sources, and evidence strength before conclusions are drawn.

It is an internal execution unit. Downstream workflow stages or improvement tasks should depend on approved official Stage 13 artifacts, not on this sub-SKILL folder.

## When to use it

Use this sub-SKILL at position 1 in the Stage 13 sequence.

Core question:

```text
What evidence is available, what workflow period is being reviewed, and how strong can the retrospective conclusions safely be?
```

## When not to use it

Do not use this sub-SKILL as a standalone replacement for the full Stage 13 retrospective package. Do not use it to create product requirements, architecture, database design, implementation code, or direct SKILL revisions.

## Required inputs before running

Always check the Stage 13 parent context files, especially:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`
- `/workflow/13_retrospective/USER_DIRECTIVES.md`, if it exists

Also read the previous sub-SKILL output when applicable:

- `Parent stage entrypoint or prior approved Stage 12 context`

## Optional or conditional inputs

Read additional stage results, review notes, implementation evidence, CI reports, incident reports, tool logs, or Agent session logs only when the SKILL scope requires them and they are safe to inspect.

Do not inspect secrets, credentials, private keys, or raw private logs.

## Outputs created when the SKILL is executed

Mandatory outputs or updates:

- `/workflow/13_retrospective/13_workflow_retrospective.md` — Initial retrospective scope, evidence map, and evidence limitations.

Conditional outputs:

- None by default. Record N/A only for conditional artifacts defined by the SKILL or parent package.

## Human approval requirements

Human approval is required before this sub-SKILL's findings are treated as accepted Stage 13 findings or converted into approved workflow changes.

Typical decisions to approve:

- Retrospective type and scope
- Evidence sources considered reliable enough to use

## How to run the SKILL in an Agentic Coding tool

1. Open this `SKILL.md`.
2. Confirm parent Stage 13 scope and `USER_DIRECTIVES.md`.
3. Read required inputs and the previous sub-SKILL output when applicable.
4. Produce only the artifacts assigned to this sub-SKILL.
5. Record assumptions, open questions, risks, and decision candidates separately.
6. Prepare a concise handoff for the next sub-SKILL.

## Relationship to previous and next sub-SKILLs

Previous: `Parent stage entrypoint or prior approved Stage 12 context`

Next: `/skills/13_workflow_retrospective/13b_stage_workflow_review/SKILL.md`

The finalizer consolidates the official Stage 13 artifacts and prepares the human approval gate.

## How to interpret status values

- `Draft`: created by the Agent and not yet approved.
- `Needs Review`: ready for human inspection but not approved.
- `Approved`: explicitly approved by the human developer.

Agent output is not approval.

## Common mistakes to avoid

- Do not draw workflow conclusions before defining evidence scope.
- Do not inspect secrets or raw private logs by default.
- Do not treat this sub-SKILL output as the final approved Stage 13 result.
- Do not bypass the finalizer.

## Troubleshooting / blocker cases

If required evidence is missing, produce a blocker report or mark conclusions as hypotheses. If source artifacts conflict, report the conflict and do not merge them silently. If the previous sub-SKILL output is missing, decide whether the current sub-SKILL can run with a clearly labeled assumption or must stop.

## Recommended next step after successful execution

Run the next sub-SKILL in the Stage 13 sequence:

`/skills/13_workflow_retrospective/13b_stage_workflow_review/SKILL.md`
