# 02 Stakeholder & Risk Framing SKILL

## 1. What this SKILL is for

This reusable SKILL executes Stage 2 of the Manual Agentic Coding Workflow: **Stakeholder & Risk Framing**.

It helps an agent identify and organize the stakeholder, role, permission, data exposure, external transfer, administrator power, audit, security, privacy, abuse, compliance, and operational-risk context that must be understood before Stage 3 Requirements & Acceptance Criteria.

This SKILL produces draft project artifacts under `/workflow/02_stakeholders_risk` when executed. It does not make final decisions by itself.

## 2. When to use it

Use this SKILL after:

- Stage 0 Project Intake / Existing Context Review has produced project context.
- Stage 1 Service Goal Definition has produced a usable service goal direction.
- The next workflow step is Stage 3 Requirements & Acceptance Criteria.

Use it when you need to clarify:

- who the users, operators, administrators, reviewers, external systems, affected non-users, and risk-relevant actors are;
- what role and permission directions should constrain later requirements;
- what personal, sensitive, confidential, regulated, logged, uploaded, model-related, or externally transferred data may exist;
- what administrator or privileged actions require constraints, auditability, or approval;
- what early security, privacy, abuse, compliance, or operational risks must be carried into requirements.

## 3. When not to use it

Do not use this SKILL to:

- write final functional requirements or acceptance criteria;
- finalize RBAC, ABAC, permission implementation, or authentication design;
- design architecture, APIs, domain model, database schema, tests, tasks, UI, or release plans;
- perform a final security/privacy review;
- perform a formal threat model unless a specialization addendum explicitly requires it;
- create project-specific assumptions that are not grounded in approved inputs or clearly marked as working assumptions.

## 4. Required inputs before running

The agent should always inspect these inputs when available:

- `/workflow/context/artifact_manifest.yml`
- `/workflow/context/context_packet.md`
- `/workflow/context/DECISIONS.md`
- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/APPROVAL_LOG.md`
- `/workflow/00_intake/00_project_intake.md`
- `/workflow/01_goal/01_service_goal.md`

The most important required input is `/workflow/01_goal/01_service_goal.md`. If the service goal direction is missing, Stage 2 cannot be completed safely.

## 5. Optional or conditional inputs

The agent should read these only when applicable:

- `/workflow/00_intake/00_existing_context_review.md` for brownfield, legacy, or integration contexts.
- `/workflow/00_intake/review_notes.md` if Stage 0 review corrections exist.
- `/workflow/01_goal/review_notes.md` if Stage 1 review corrections exist.
- `/workflow/02_stakeholders_risk/USER_DIRECTIVES.md` if the human developer added stage-local instructions.
- `/workflow_templates/specializations/web_saas.md` for web SaaS or multi-user browser systems.
- `/workflow_templates/specializations/internal_tool.md` for internal staff, admin, or operations tools.
- `/workflow_templates/specializations/mobile_app.md` for mobile, local storage, device permission, push, or offline/sync concerns.
- `/workflow_templates/specializations/ai_data_product.md` for AI/ML/LLM, datasets, model outputs, labeling, or synthetic data.
- `/workflow_templates/specializations/regulated_security_sensitive.md` for regulated, high-risk, privacy-sensitive, or security-sensitive systems.
- `/workflow_templates/specializations/brownfield_legacy.md` for existing-system constraints.

## 6. Outputs created when the SKILL is executed

Mandatory project artifacts:

- `/workflow/02_stakeholders_risk/02_stakeholders.md`
- `/workflow/02_stakeholders_risk/02_risk_privacy_screening.md`
- `/workflow/02_stakeholders_risk/result.md`
- `/workflow/context/context_packet.md`

Context files updated when relevant:

- `/workflow/context/ASSUMPTIONS.md`
- `/workflow/context/OPEN_QUESTIONS.md`
- `/workflow/context/REJECTED_OPTIONS.md`
- `/workflow/context/TRACEABILITY_MATRIX.md`

Conditional artifacts, created only when applicable:

- `/workflow/02_stakeholders_risk/02_role_permission_matrix.md`
- `/workflow/02_stakeholders_risk/02_data_exposure_map.md`
- `/workflow/02_stakeholders_risk/02_external_transfer_register.md`
- `/workflow/02_stakeholders_risk/02_admin_power_review.md`
- `/workflow/02_stakeholders_risk/02_audit_accountability_needs.md`
- `/workflow/02_stakeholders_risk/02_compliance_risk_notes.md`
- `/workflow/02_stakeholders_risk/02_abuse_misuse_cases.md`

If a conditional artifact is skipped, the agent should record an N/A rationale in `result.md`.

## 7. Human approval requirements

The agent may propose, classify, and draft. The human developer must approve decisions before downstream stages treat them as source of truth.

Human approval is especially required for:

- stakeholder categories to carry into requirements;
- user role and permission direction;
- administrator or operator power direction;
- personal or sensitive data handling direction;
- external API, LLM, analytics, cloud, or third-party transfer direction;
- audit and accountability direction;
- risk assumptions that should constrain Stage 3.

Do not treat Stage 2 as approved just because artifacts exist. Artifacts are draft until explicitly approved.

## 8. How to run the SKILL in an Agentic Coding tool

A typical manual execution flow is:

1. Start from a clean or clearly bounded agent session.
2. Ask the tool to read `/skills/02_stakeholder_risk_framing/SKILL.md`.
3. Ask it to follow `/skills/02_stakeholder_risk_framing/artifact_contract.md` for artifact structure and validation.
4. Point it to the project `/workflow` folder.
5. Confirm that it should not create requirements, architecture, database, or implementation artifacts.
6. Let it execute Stage 2 and create only the Stage 2 artifacts.
7. Review the Human Approval Required section in `result.md`.
8. Approve, revise, or reject decision candidates before running Stage 3.

Generic invocation prompt:

```text
Read /skills/02_stakeholder_risk_framing/SKILL.md and execute Stage 2 for this project.
Use /skills/02_stakeholder_risk_framing/artifact_contract.md for artifact structure.
Do not execute Stage 3.
Do not create requirements, architecture, data design, tests, tasks, or implementation files.
Create or update only the Stage 2 artifacts and required context handoff files.
```

## 9. Relationship to previous and next stages

Previous stage:

- Stage 1 Service Goal Definition provides the service goal, target users, success criteria, non-goals, assumptions, and open questions.

Current stage:

- Stage 2 transforms the service goal into stakeholder, role, data, transfer, risk, and audit framing.

Next stage:

- Stage 3 Requirements & Acceptance Criteria uses the approved or clearly marked Stage 2 outputs to write testable requirements and security/privacy conditions.

Stage 3 should not treat unapproved role candidates, data handling proposals, or external-transfer assumptions as final requirements.

## 10. How to interpret status values

`Draft` means the artifact or item was created by the agent but has not been approved.

`Needs Review` means the artifact or item may be usable, but a human decision, clarification, or correction is required before relying on it.

`Approved` means the human developer explicitly approved the artifact or decision. Only approved decisions should be recorded in `DECISIONS.md`.

## 11. Common mistakes to avoid

Avoid these mistakes:

- Treating all stakeholders as end users.
- Ignoring administrators, operators, reviewers, external systems, and affected non-users.
- Treating candidate roles as final requirements.
- Designing detailed RBAC/ABAC implementation too early.
- Ignoring logs, analytics, uploaded files, model inputs/outputs, or external transfers.
- Claiming “no security risk” without evidence.
- Deferring all privacy/security thinking to the final review stage.
- Creating requirements, architecture, data design, tests, tasks, or code in Stage 2.
- Updating `DECISIONS.md` without explicit human approval.
- Using `context_packet.md` as the only source of truth.

## 12. Troubleshooting / blocker cases

Stop and produce a Blocker Report if:

- `/workflow/01_goal/01_service_goal.md` is missing;
- the service goal direction is too unclear to identify stakeholders or risks;
- the project type is unknown and materially affects privacy, security, regulation, or stakeholder scope;
- a `USER_DIRECTIVES.md` instruction conflicts with approved decisions;
- a rejected or superseded artifact is being used as current truth.

Continue with explicit working assumptions if:

- optional review notes are missing;
- optional specialization addenda are missing;
- non-critical context files such as `APPROVAL_LOG.md` or `REJECTED_OPTIONS.md` are absent;
- conditional artifacts are not applicable and N/A records are provided.

## 13. Recommended next step after successful execution

After the SKILL finishes:

1. Review `02_stakeholders.md`, `02_risk_privacy_screening.md`, conditional artifacts, and `result.md`.
2. Approve, revise, or reject the decision candidates.
3. Confirm or revise the working assumptions.
4. Resolve open questions that block Stage 3.
5. Run Stage 3 Requirements & Acceptance Criteria only after Stage 2 is sufficiently approved or explicitly allowed to proceed with marked assumptions.

## 14. Reusable files vs project artifacts

Reusable SKILL support files live under:

- `/skills/02_stakeholder_risk_framing/SKILL.md`
- `/skills/02_stakeholder_risk_framing/README.md`
- `/skills/02_stakeholder_risk_framing/artifact_contract.md`

Project execution artifacts live under:

- `/workflow/02_stakeholders_risk/...`
- `/workflow/context/...`

This README is a support file for the reusable SKILL. It is not a project artifact and does not indicate that Stage 2 has been executed.
