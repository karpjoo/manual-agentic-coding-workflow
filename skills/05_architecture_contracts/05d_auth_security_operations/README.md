# 05d Auth, Security & Operations

## What this sub-SKILL is for

This reusable sub-skill is part of the Stage 5 `05_architecture_contracts` package. It is an internal execution unit, not a downstream source-of-truth boundary.

Define architecture-level authentication, authorization, security/privacy architecture, operational architecture, and brownfield compatibility when applicable.

## When to use it

Use this sub-skill in the Stage 5 sequence after:

```text
/skills/05_architecture_contracts/05c_technical_contracts/SKILL.md
```

and before:

```text
/skills/05_architecture_contracts/05e_architecture_finalizer/SKILL.md
```

## When not to use it

Do not run this sub-skill as a standalone workflow stage. Do not let downstream stages depend on this sub-skill directly. Do not use it to implement code, create database schema, create task cards, or write implementation prompts.

## Required inputs before running

Always read the standard workflow context files and the source artifacts specified in this sub-skill's `SKILL.md`. At minimum, the sub-skill depends on the parent Stage 5 package contract and the relevant approved prior-stage artifacts or earlier Stage 5 draft outputs.

## Optional or conditional inputs

- `/workflow/05_architecture/05_api_contracts.md` — APIs or programmatic operations exist.
- `/workflow/05_architecture/05_integration_contracts.md` — External integrations exist.
- `/workflow/05_architecture/05_event_contracts.md` — Events, background jobs, queues, notifications, or async workflows exist.
- `/workflow/00_intake/00_existing_context_review.md` — This is brownfield, migration, or existing-system extension work.

## Outputs created when the sub-SKILL is executed

### Mandatory outputs

- `/workflow/05_architecture/05_architecture_plan.md` — Architecture plan updated with auth, security, privacy, operations, and cross-cutting policies.
- `/workflow/05_architecture/05_architecture_decisions.md` — Auth/security/operations decision candidates and trade-offs.

### Conditional outputs

- `/workflow/05_architecture/05_authn_authz_model.md` — if Accounts, roles, permissions, administrators, protected resources, protected operations, or sensitive access rules exist.
- `/workflow/05_architecture/05_security_privacy_architecture.md` — if Personal data, sensitive data, external transfer, LLM/API exposure, compliance concerns, or security-sensitive workflows exist.
- `/workflow/05_architecture/05_operational_architecture.md` — if Deployment, hosting, reliability, observability, environment management, secrets, background jobs, scaling, or operations are significant.
- `/workflow/05_architecture/05_brownfield_compatibility_plan.md` — if Project modifies, extends, migrates, or integrates with an existing system.

If a conditional output is not applicable, record an N/A rationale according to the parent Stage 5 policy.

## Human approval requirements

This sub-skill may prepare decision candidates or draft artifacts, but it does not make them approved. Human approval is still required at the Stage 5 gate after `05e_architecture_finalizer` consolidates the official artifacts.

Key items requiring review:

- Authentication and authorization model
- Security/privacy architecture direction
- Operational architecture direction
- Brownfield compatibility approach if applicable

## How to run this sub-SKILL in an Agentic Coding tool

Run the corresponding `SKILL.md` file:

```text
/skills/05_architecture_contracts/05d_auth_security_operations/SKILL.md
```

Do not change the `SKILL.md` while executing it unless the human developer explicitly asks for skill revision.

## Relationship to previous and next sub-skills

Previous:

```text
/skills/05_architecture_contracts/05c_technical_contracts/SKILL.md
```

Next:

```text
/skills/05_architecture_contracts/05e_architecture_finalizer/SKILL.md
```

The finalizer is responsible for promoting the consolidated Stage 5 outputs to review-ready official artifacts.

## How to interpret status values

- `Draft`: Agent-created or revised content that has not been approved.
- `Needs Review`: Content is ready for human review, but approval is not yet granted.
- `Approved`: The human developer explicitly approved the artifact or decision.

## Common mistakes to avoid

- Do not defer all security/privacy architecture to final review.
- Do not make authorization assumptions when protected operations exist.
- Do not create data security rules that belong to Stage 6.

## Troubleshooting / blocker cases

Stop and report a blocker if required inputs are missing, source artifacts are unapproved, approved decisions conflict, or this sub-skill cannot safely preserve traceability.

## Recommended next step after successful execution

Run the next sub-skill in the Stage 5 sequence:

```text
/skills/05_architecture_contracts/05e_architecture_finalizer/SKILL.md
```
