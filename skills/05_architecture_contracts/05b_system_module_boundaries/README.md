# 05b System & Module Boundaries

## What this sub-SKILL is for

This reusable sub-skill is part of the Stage 5 `05_architecture_contracts` package. It is an internal execution unit, not a downstream source-of-truth boundary.

Define runtime, system, frontend/backend/service, and module boundaries based on the drafted architecture direction.

## When to use it

Use this sub-skill in the Stage 5 sequence after:

```text
/skills/05_architecture_contracts/05a_architecture_drivers_options/SKILL.md
```

and before:

```text
/skills/05_architecture_contracts/05c_technical_contracts/SKILL.md
```

## When not to use it

Do not run this sub-skill as a standalone workflow stage. Do not let downstream stages depend on this sub-skill directly. Do not use it to implement code, create database schema, create task cards, or write implementation prompts.

## Required inputs before running

Always read the standard workflow context files and the source artifacts specified in this sub-skill's `SKILL.md`. At minimum, the sub-skill depends on the parent Stage 5 package contract and the relevant approved prior-stage artifacts or earlier Stage 5 draft outputs.

## Optional or conditional inputs

- `/workflow/04_domain/04_domain_traceability_matrix.md` — Domain-to-architecture mapping requires additional detail.
- `/workflow/00_intake/00_existing_context_review.md` — Existing module boundaries or compatibility constraints affect architecture.

## Outputs created when the sub-SKILL is executed

### Mandatory outputs

- `/workflow/05_architecture/05_module_boundaries.md` — Module and component inventory, responsibilities, public interfaces, dependencies, and forbidden dependencies.
- `/workflow/05_architecture/05_architecture_plan.md` — Architecture plan updated with boundary implications.
- `/workflow/05_architecture/05_architecture_decisions.md` — Architecture decisions updated with boundary-related candidates.

### Conditional outputs

- None beyond this sub-skill's mandatory outputs.

If a conditional output is not applicable, record an N/A rationale according to the parent Stage 5 policy.

## Human approval requirements

This sub-skill may prepare decision candidates or draft artifacts, but it does not make them approved. Human approval is still required at the Stage 5 gate after `05e_architecture_finalizer` consolidates the official artifacts.

Key items requiring review:

- Frontend/backend/service boundaries
- Module boundaries
- Dependency rules and forbidden dependencies

## How to run this sub-SKILL in an Agentic Coding tool

Run the corresponding `SKILL.md` file:

```text
/skills/05_architecture_contracts/05b_system_module_boundaries/SKILL.md
```

Do not change the `SKILL.md` while executing it unless the human developer explicitly asks for skill revision.

## Relationship to previous and next sub-skills

Previous:

```text
/skills/05_architecture_contracts/05a_architecture_drivers_options/SKILL.md
```

Next:

```text
/skills/05_architecture_contracts/05c_technical_contracts/SKILL.md
```

The finalizer is responsible for promoting the consolidated Stage 5 outputs to review-ready official artifacts.

## How to interpret status values

- `Draft`: Agent-created or revised content that has not been approved.
- `Needs Review`: Content is ready for human review, but approval is not yet granted.
- `Approved`: The human developer explicitly approved the artifact or decision.

## Common mistakes to avoid

- Do not create modules without traceable responsibility.
- Do not use future data design artifacts as source of truth.
- Do not collapse domain model into database tables.

## Troubleshooting / blocker cases

Stop and report a blocker if required inputs are missing, source artifacts are unapproved, approved decisions conflict, or this sub-skill cannot safely preserve traceability.

## Recommended next step after successful execution

Run the next sub-skill in the Stage 5 sequence:

```text
/skills/05_architecture_contracts/05c_technical_contracts/SKILL.md
```
