# 05e Architecture Finalizer

## What this sub-SKILL is for

This reusable sub-skill is part of the Stage 5 `05_architecture_contracts` package. It is an internal execution unit, not a downstream source-of-truth boundary.

Consolidate Stage 5 official artifacts, resolve contradictions, finalize traceability, update context handoff, and prepare the human approval gate.

## When to use it

Use this sub-skill in the Stage 5 sequence after:

```text
/skills/05_architecture_contracts/05d_auth_security_operations/SKILL.md
```

and before:

```text
/skills/06_data_design/SKILL.md
```

## When not to use it

Do not run this sub-skill as a standalone workflow stage. Do not let downstream stages depend on this sub-skill directly. Do not use it to implement code, create database schema, create task cards, or write implementation prompts.

## Required inputs before running

Always read the standard workflow context files and the source artifacts specified in this sub-skill's `SKILL.md`. At minimum, the sub-skill depends on the parent Stage 5 package contract and the relevant approved prior-stage artifacts or earlier Stage 5 draft outputs.

## Optional or conditional inputs

- `/workflow/05_architecture/05_api_contracts.md` — APIs or programmatic interfaces exist.
- `/workflow/05_architecture/05_integration_contracts.md` — External integrations exist.
- `/workflow/05_architecture/05_event_contracts.md` — Events or async workflows exist.
- `/workflow/05_architecture/05_authn_authz_model.md` — Authn/authz model is applicable.
- `/workflow/05_architecture/05_security_privacy_architecture.md` — Security/privacy architecture is applicable.
- `/workflow/05_architecture/05_operational_architecture.md` — Operational architecture is applicable.
- `/workflow/05_architecture/05_brownfield_compatibility_plan.md` — Brownfield compatibility is applicable.

## Outputs created when the sub-SKILL is executed

### Mandatory outputs

- `/workflow/05_architecture/05_architecture_traceability_matrix.md` — Final Stage 5 traceability matrix linking requirements, domain model, architecture components, contracts, data implications, and test implications.
- `/workflow/05_architecture/result.md` — Stage 5 consolidated result, outputs created, decision candidates, assumptions, open questions, risks, N/A items, and approval gate.
- `/workflow/context/context_packet.md` — Minimal operational context for Stage 6 Data Design.

### Conditional outputs

- None beyond this sub-skill's mandatory outputs.

If a conditional output is not applicable, record an N/A rationale according to the parent Stage 5 policy.

## Human approval requirements

This sub-skill may prepare decision candidates or draft artifacts, but it does not make them approved. Human approval is still required at the Stage 5 gate after `05e_architecture_finalizer` consolidates the official artifacts.

Key items requiring review:

- Final Stage 5 artifact set
- Architecture traceability
- Stage 6 Data Design handoff
- All remaining Stage 5 decision candidates

## How to run this sub-SKILL in an Agentic Coding tool

Run the corresponding `SKILL.md` file:

```text
/skills/05_architecture_contracts/05e_architecture_finalizer/SKILL.md
```

Do not change the `SKILL.md` while executing it unless the human developer explicitly asks for skill revision.

## Relationship to previous and next sub-skills

Previous:

```text
/skills/05_architecture_contracts/05d_auth_security_operations/SKILL.md
```

Next:

```text
/skills/06_data_design/SKILL.md
```

The finalizer is responsible for promoting the consolidated Stage 5 outputs to review-ready official artifacts.

## How to interpret status values

- `Draft`: Agent-created or revised content that has not been approved.
- `Needs Review`: Content is ready for human review, but approval is not yet granted.
- `Approved`: The human developer explicitly approved the artifact or decision.

## Common mistakes to avoid

- Do not approve decisions on behalf of the human developer.
- Do not hide contradictions among Stage 5 artifacts.
- Do not make Stage 6 depend on sub-skill internals.

## Troubleshooting / blocker cases

Stop and report a blocker if required inputs are missing, source artifacts are unapproved, approved decisions conflict, or this sub-skill cannot safely preserve traceability.

## Recommended next step after successful execution

Run the next sub-skill in the Stage 5 sequence:

```text
/skills/06_data_design/SKILL.md
```
