# 05a Architecture Drivers & Options

## What this sub-SKILL is for

This reusable sub-skill is part of the Stage 5 `05_architecture_contracts` package. It is an internal execution unit, not a downstream source-of-truth boundary.

Extract architecture drivers, define system context, compare architecture options, and draft recommended architecture direction as a decision candidate.

## When to use it

Use this sub-skill in the Stage 5 sequence after:

```text
/skills/04_domain_modeling/SKILL.md
```

and before:

```text
/skills/05_architecture_contracts/05b_system_module_boundaries/SKILL.md
```

## When not to use it

Do not run this sub-skill as a standalone workflow stage. Do not let downstream stages depend on this sub-skill directly. Do not use it to implement code, create database schema, create task cards, or write implementation prompts.

## Required inputs before running

Always read the standard workflow context files and the source artifacts specified in this sub-skill's `SKILL.md`. At minimum, the sub-skill depends on the parent Stage 5 package contract and the relevant approved prior-stage artifacts or earlier Stage 5 draft outputs.

## Optional or conditional inputs

- `/workflow/00_intake/00_project_intake.md` — Project profile, fixed stack, hosting, platform, or constraints are unclear from context.
- `/workflow/00_intake/00_existing_context_review.md` — Project is brownfield, legacy, migration, or existing-system extension work.
- `/workflow/04_domain/04_domain_traceability_matrix.md` — Stage 4 produced a separate domain traceability matrix.
- `/workflow/04_domain/result.md` — Stage 4 contains architecture-relevant warnings, assumptions, or handoff notes.

## Outputs created when the sub-SKILL is executed

### Mandatory outputs

- `/workflow/05_architecture/05_architecture_plan.md` — Draft architecture plan, drivers, system context, options, and recommended direction.
- `/workflow/05_architecture/05_architecture_decisions.md` — Initial architecture decision candidates and option trade-offs.

### Conditional outputs

- None beyond this sub-skill's mandatory outputs.

If a conditional output is not applicable, record an N/A rationale according to the parent Stage 5 policy.

## Human approval requirements

This sub-skill may prepare decision candidates or draft artifacts, but it does not make them approved. Human approval is still required at the Stage 5 gate after `05e_architecture_finalizer` consolidates the official artifacts.

Key items requiring review:

- Architecture style and direction
- Major technical choices
- Architecture option recommendation

## How to run this sub-SKILL in an Agentic Coding tool

Run the corresponding `SKILL.md` file:

```text
/skills/05_architecture_contracts/05a_architecture_drivers_options/SKILL.md
```

Do not change the `SKILL.md` while executing it unless the human developer explicitly asks for skill revision.

## Relationship to previous and next sub-skills

Previous:

```text
/skills/04_domain_modeling/SKILL.md
```

Next:

```text
/skills/05_architecture_contracts/05b_system_module_boundaries/SKILL.md
```

The finalizer is responsible for promoting the consolidated Stage 5 outputs to review-ready official artifacts.

## How to interpret status values

- `Draft`: Agent-created or revised content that has not been approved.
- `Needs Review`: Content is ready for human review, but approval is not yet granted.
- `Approved`: The human developer explicitly approved the artifact or decision.

## Common mistakes to avoid

- Do not mark recommended architecture as approved.
- Do not design detailed database schema.
- Do not implement code.

## Troubleshooting / blocker cases

Stop and report a blocker if required inputs are missing, source artifacts are unapproved, approved decisions conflict, or this sub-skill cannot safely preserve traceability.

## Recommended next step after successful execution

Run the next sub-skill in the Stage 5 sequence:

```text
/skills/05_architecture_contracts/05b_system_module_boundaries/SKILL.md
```
