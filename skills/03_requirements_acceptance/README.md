# 03 Requirement Acceptance SKILL

## 1. What this SKILL is for

This reusable SKILL executes Stage 3 of the Manual Agentic Coding Workflow: Requirements & Acceptance Criteria.

Use it to convert approved service goals, stakeholder context, and risk/privacy framing into testable requirements, acceptance criteria, requirement-level traceability, and Stage 4 handoff context.

This SKILL is not a project artifact. It is a reusable execution procedure stored under `/skills`. When executed, it creates or updates project artifacts under `/workflow/03_requirements` and `/workflow/context`.

## 2. When to use it

Use this SKILL after Stage 1 and Stage 2 have produced review-ready or approved artifacts:

- `/workflow/01_goal/01_service_goal.md`
- `/workflow/02_stakeholders_risk/02_stakeholders.md`
- `/workflow/02_stakeholders_risk/02_risk_privacy_screening.md`
- relevant context files under `/workflow/context`

Use it when the project needs:

- functional requirements
- non-functional requirements
- security, privacy, data, operational, and integration requirements
- acceptance criteria
- scenarios, edge cases, and negative paths
- requirement-level traceability
- context handoff for Stage 4 Domain Modeling / DDD

## 3. When not to use it

Do not use this SKILL to:

- define the service goal
- perform stakeholder or risk analysis
- create domain models, aggregates, entities, or bounded contexts
- design architecture, APIs, database schemas, UI, or implementation tasks
- write implementation prompts
- write code or test files
- approve requirements on behalf of the human developer

If the service goal, stakeholder roles, or risk/privacy framing are missing or unapproved, run or revise the earlier stages first.

## 4. Required inputs before running

The agent must check these files when they exist and must treat approved artifacts as the source of truth:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/01_goal/01_service_goal.md`
- `/workflow/02_stakeholders_risk/02_stakeholders.md`
- `/workflow/02_stakeholders_risk/02_risk_privacy_screening.md`

If required inputs are missing, draft, superseded, rejected, or conflicting, the agent must report this in `/workflow/03_requirements/result.md` and continue only when safe with explicit working assumptions.

## 5. Optional or conditional inputs

Read these only when applicable:

- `/workflow/00_intake/00_project_intake.md` — if project profile, fixed stack, delivery constraints, or project type affect requirements
- `/workflow/00_intake/00_existing_context_review.md` — if brownfield, migration, extension, or existing-system constraints exist
- `/workflow/01_goal/review_notes.md` — if Stage 1 human review comments exist
- `/workflow/02_stakeholders_risk/review_notes.md` — if Stage 2 human review comments exist
- `/workflow/03_requirements/USER_DIRECTIVES.md` — if stage-local human instructions exist
- `/workflow_templates/specializations/*.md` — if a project-type specialization is active

Do not read raw chat history, raw agent logs, superseded drafts, unrelated previous-stage drafts, implementation code, or later-stage artifacts by default.

## 6. Outputs created when the SKILL is executed

Mandatory official Stage 3 artifacts:

- `/workflow/03_requirements/03_requirements.md`
- `/workflow/03_requirements/03_acceptance_criteria.md`
- `/workflow/03_requirements/03_traceability_matrix.md`
- `/workflow/03_requirements/result.md`
- `/workflow/context/context_packet.md`

Context files updated when applicable:

- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`

Conditional artifacts, only when needed:

- `/workflow/03_requirements/03_nfr_requirements.md`
- `/workflow/03_requirements/03_security_privacy_requirements.md`
- `/workflow/03_requirements/03_scenarios_edge_cases.md`
- `/workflow/03_requirements/03_scope_candidates.md`
- `/workflow/03_requirements/03_requirements_open_questions.md`

Skipped conditional artifacts must be recorded in `result.md` with an N/A reason and a revisit condition.

## 7. Human approval requirements

Stage 3 outputs are drafts until the human developer approves them.

Human approval is required for:

- functional requirements
- non-functional requirements
- security, privacy, and data requirements
- operational and integration requirements
- acceptance criteria
- non-scope and boundary items
- assumptions that affect requirements or later design
- open questions that block domain modeling or validation
- any scope expansion proposed during requirements work

The agent must not update `/workflow/context/DECISIONS.md` unless explicit human approval exists.

## 8. How to run the SKILL in an Agentic Coding tool

1. Place the reusable SKILL at `/skills/03_requirement_acceptance/SKILL.md`.
2. Ensure the required Stage 1, Stage 2, and `/workflow/context` inputs exist.
3. Add stage-local instructions to `/workflow/03_requirements/USER_DIRECTIVES.md` if needed.
4. Start a clean or bounded agent session.
5. Instruct the agent to execute `/skills/03_requirement_acceptance/SKILL.md`.
6. Review the generated Stage 3 artifacts before allowing Stage 4 to depend on them.

Do not paste project-specific requirements into the SKILL file. Put project-specific instructions in approved artifacts, context files, or `USER_DIRECTIVES.md`.

## 9. Relationship to previous and next stages

Previous stage dependency:

- Stage 3 depends mainly on approved or review-ready outputs from Stage 1 and Stage 2.
- Stage 0 inputs are read only if project profile, brownfield constraints, or delivery constraints affect requirements.

Next stage handoff:

- Stage 4 Domain Modeling / DDD should read approved Stage 3 artifacts, especially `03_requirements.md`, `03_acceptance_criteria.md`, and `03_traceability_matrix.md`.
- Stage 4 must not depend on Stage 3 prompt history or internal sub-skill outputs.

## 10. Draft, Approved, and Needs Review

- `Draft`: Created or updated by the agent. It is not yet approved and must not be treated as source of truth.
- `Needs Review`: Ready for human review but contains unresolved questions, risks, or validation concerns.
- `Approved`: Explicitly approved by the human developer and eligible to be used by downstream stages as source of truth.

An artifact is not approved merely because the agent created it.

## 11. Common mistakes to avoid

Avoid these mistakes:

- treating agent-generated requirements as approved decisions
- turning assumptions into requirements
- writing acceptance criteria that only repeat the requirement
- adding architecture, API, database, UI, or implementation design inside requirements
- ignoring Stage 2 security/privacy findings
- hiding scope expansion inside requirements
- skipping negative paths, edge cases, role boundaries, or data/privacy conditions
- changing stable IDs without preserving history
- updating `DECISIONS.md` without explicit human approval
- making Stage 4 depend on internal Stage 3 sub-skill structure

## 12. Troubleshooting and blocker cases

Stop and produce a blocker report if:

- there is no approved or review-ready service goal
- target users, roles, or stakeholders are missing
- scope boundaries or non-goals are missing
- risk/privacy/security context is missing for a system involving personal, sensitive, regulated, privileged, or externally transferred data
- `USER_DIRECTIVES.md` conflicts with approved decisions
- required upstream artifacts are superseded or rejected
- requirements cannot be made testable without a human decision

A blocker report should explain the blocking issue, why it matters, affected artifacts or stages, safe partial work completed, and the human decision needed.

## 13. Split policy

Default: keep Stage 3 as one executable SKILL at `/skills/03_requirement_acceptance/SKILL.md`.

Split only if execution becomes too large or unreliable. If split later, preserve the same official Stage 3 artifact contract and use a nested Stage Facade Pattern:

```text
/skills/03_requirement_acceptance/
  SKILL.md
  README.md
  artifact_contract.yml

  /03a_requirement_source_review/
    SKILL.md

  /03b_requirement_decomposition/
    SKILL.md

  /03c_acceptance_criteria_writer/
    SKILL.md

  /03d_requirements_traceability_finalizer/
    SKILL.md
```

Downstream stages must depend only on approved official Stage 3 artifacts, not internal sub-skill names, internal outputs, or prompt history.

## 14. Recommended next step after successful execution

After this SKILL runs:

1. Review `/workflow/03_requirements/result.md`.
2. Approve, revise, or reject the generated requirements and acceptance criteria.
3. Resolve blocking open questions or testability concerns.
4. Record explicit approvals in the appropriate approval mechanism.
5. Proceed to Stage 4 Domain Modeling / DDD only after Stage 3 artifacts are approved or intentionally accepted as review-ready inputs.
