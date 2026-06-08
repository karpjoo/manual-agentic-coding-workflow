---
name: 12_review_release_handoff_skill_template
description: Template for creating a reusable Stage 12 SKILL that performs final review, security/privacy review, release readiness, deployment planning, operations preparation, and documentation handoff.
stage: 12 Review / Security / Release / Handoff
version: 1.0.0
status: template
primary_output: /workflow/12_review_release_handoff/result.md
requires_human_approval: true
---

# Stage 12 SKILL Template: Review / Security / Release / Handoff

> Use this template to create a reusable `SKILL.md` for Stage 12 of the Manual Agentic Coding Workflow.
> This is a template, not an executable project-specific SKILL.
> Replace `[[...]]` placeholders when generating the actual reusable Stage 12 `SKILL.md`.

---

## 1. Purpose

This SKILL performs the final pre-release review and handoff stage.

It verifies whether the implemented system is ready for release by reviewing:

- requirement satisfaction;
- acceptance criteria coverage;
- implementation evidence;
- test and validation evidence;
- code quality risks;
- security and privacy risks;
- deployment readiness;
- rollback and recovery readiness;
- operational handoff readiness;
- documentation freshness.

This stage is a final verification gate. It must not be the first time security, privacy, testing, or operations are considered.

---

## 2. Core Question

```text
Is the implemented system ready for human-approved release, deployment, operation, and handoff based on approved requirements, implementation evidence, validation evidence, security/privacy constraints, and operational readiness?
```

---

## 3. When to Use

Use this SKILL when:

- Stage 11 implementation tasks have been completed or paused for release review.
- Test evidence exists for implemented tasks.
- The human developer wants to decide whether a release can proceed.
- Security, privacy, deployment, rollback, operations, and documentation need final review.
- A release candidate, MVP, internal handoff, or production deployment decision is needed.

---

## 4. When Not to Use

Do not use this SKILL when:

- requirements are still unapproved;
- MVP or release scope is unresolved;
- architecture or data design is still being actively changed;
- implementation task cards have not been executed;
- no test or validation evidence exists;
- the user is asking for implementation work rather than review;
- the goal is workflow retrospective rather than release readiness.

Use Stage 13 for workflow retrospective and skill improvement.

---

## 5. Required Inputs

### 5.1 Always Read

The generated Stage 12 SKILL should require the agent to read:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md

/workflow/01_goal/01_service_goal.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/11_implementation_results/
```

The actual generated SKILL may narrow this list if the project uses a lighter profile, but it must not skip approved requirements, release scope, test strategy, implementation evidence, or traceability.

---

### 5.2 Read If Applicable

Read the following only when applicable:

```text
/workflow/00_intake/00_existing_context_review.md
- if this is a brownfield, extension, migration, or compatibility-sensitive project.

/workflow/02_stakeholders_risk/02_risk_privacy_screening.md
- if user roles, personal data, sensitive data, regulatory concerns, external transfer, or abuse risks exist.

/workflow/04_domain/04_business_rules_invariants.md
- if domain invariants, lifecycle rules, or state transitions affect correctness or release risk.

/workflow/05_architecture/05_architecture_plan.md
- if architecture decisions affect deployment, runtime, integration, security, or rollback.

/workflow/05_architecture/05_api_contracts.md
- if APIs exist.

/workflow/05_architecture/05_integration_contracts.md
- if external integrations exist.

/workflow/06_data/06_logical_schema.md
- if persistent data exists.

/workflow/06_data/06_physical_schema.md
- if physical storage or database configuration exists.

/workflow/06_data/06_migration_plan.md
- if schema or data migration is part of the release.

/workflow/06_data/06_data_security_rules.md
- if data access rules, row-level rules, Firestore rules, storage rules, or equivalent rules exist.

/workflow/08_test_strategy/08_manual_test_plan.md
- if manual validation is required.

/workflow/10_prompts/10_implementation_prompts.md
- if implementation behavior must be reviewed against approved agent prompts.

/workflow/11_implementation_results/11_test_evidence_*.md
- if task-level test evidence files exist.

/workflow/11_implementation_results/11_task_result_*.md
- if task-level implementation result files exist.

Project deployment configuration, CI configuration, environment variable documentation, infrastructure files, or hosting settings
- if release readiness or deployment planning requires them.
```

---

### 5.3 Do Not Read By Default

Do not read by default:

```text
- raw chat history;
- raw agent scratchpads;
- full historical drafts from unrelated stages;
- superseded artifacts;
- rejected artifacts;
- unapproved implementation proposals;
- unrelated code files not needed for review;
- production secrets or secret values;
- private credentials;
- local environment files containing real secrets.
```

If secret configuration must be reviewed, inspect only variable names, expected presence, storage policy, and access policy. Do not expose or copy secret values.

---

## 6. USER_DIRECTIVES.md Handling

Before execution, check:

```text
/workflow/12_review_release_handoff/USER_DIRECTIVES.md
```

If it exists:

1. Read it before review work.
2. Classify each directive as:
   - explicit approval;
   - correction;
   - preference;
   - release scope change;
   - security/privacy constraint;
   - deployment constraint;
   - documentation requirement;
   - rejection;
   - question.
3. Apply directives before agent assumptions.
4. Report conflicts with approved decisions or release scope.
5. Do not modify `USER_DIRECTIVES.md` unless explicitly instructed.

---

## 7. Input Preflight Procedure

Before producing Stage 12 artifacts, perform this preflight:

```text
[ ] Confirm this is Stage 12: Review / Security / Release / Handoff.
[ ] Read artifact_manifest.yml if available.
[ ] Read context_packet.md.
[ ] Read DECISIONS.md and APPROVAL_LOG.md.
[ ] Check whether USER_DIRECTIVES.md exists.
[ ] Identify approved release scope.
[ ] Identify implemented task results.
[ ] Identify test and validation evidence.
[ ] Verify required inputs exist.
[ ] Verify source artifacts are approved or clearly marked as draft.
[ ] Check for superseded or rejected artifacts.
[ ] Identify missing, ambiguous, or conflicting information.
[ ] Identify whether release review is full, partial, internal-only, or production-oriented.
[ ] Restate the current release review task.
```

If release scope, implementation evidence, or validation evidence is missing, classify the issue as blocking or non-blocking before proceeding.

---

## 8. Missing Input Handling

If required inputs are missing:

```text
1. Report the missing input.
2. Explain why it matters for release readiness.
3. Mark it as Blocking or Non-Blocking.
4. If non-blocking, proceed with a clearly labeled working assumption.
5. If blocking, produce a partial review and Blocker Report.
```

Blocking examples:

```text
- No approved release scope.
- No implementation evidence for release-critical tasks.
- No validation evidence for must-have requirements.
- Security-sensitive data exists but no security/privacy review inputs exist.
- Deployment is requested but environment, configuration, or rollback information is unavailable.
- Migration is required but no migration plan or test evidence exists.
```

---

## 9. Execution Procedure

The generated Stage 12 SKILL should instruct the agent to execute the following procedure.

### Step 1. Confirm Review Boundary

Identify:

```text
- release candidate name or version, if any;
- release type: prototype, internal demo, MVP, production, migration, hotfix, or documentation handoff;
- approved MVP/release scope;
- implemented task set;
- excluded or deferred work;
- known limitations;
- unresolved open questions affecting release.
```

Do not expand the release scope.

---

### Step 2. Build Review Evidence Index

Create or update an evidence index covering:

```text
Requirement → Acceptance Criteria → Task → Implementation Evidence → Test Evidence → Release Status
```

Classify each item as:

```text
- Covered
- Partially Covered
- Not Covered
- Not Applicable
- Blocked
- Needs Human Decision
```

---

### Step 3. Review Requirement Satisfaction

For each must-have requirement in the approved release scope:

```text
1. Check linked acceptance criteria.
2. Check implementation evidence.
3. Check test evidence.
4. Check known limitations.
5. Classify release status.
6. Identify release blocker, warning, or suggestion.
```

Do not mark a requirement satisfied without evidence.

---

### Step 4. Review Test and Validation Evidence

Review:

```text
- unit test results;
- integration test results;
- E2E test results;
- manual validation results;
- security-sensitive validation;
- migration validation;
- regression testing;
- CI results, if applicable;
- commands run and pass/fail status;
- skipped tests and rationale.
```

Classify missing validation as:

```text
- Release Blocker
- Release Warning
- Acceptable with Human Approval
- Not Applicable
```

---

### Step 5. Code Quality Review

Review code quality at the level appropriate for release readiness.

Check:

```text
- unnecessary scope expansion;
- large or risky changes not tied to task cards;
- duplicated or dead code;
- unclear error handling;
- weak boundary checks;
- fragile implementation;
- excessive coupling;
- performance-sensitive code paths;
- maintainability risks;
- incomplete TODOs or temporary code;
- logging quality;
- observability gaps;
- dependency changes.
```

Do not perform a broad refactor in this stage unless explicitly instructed.

---

### Step 6. Security and Privacy Review

Review against approved security/privacy constraints.

Check:

```text
- authentication and authorization behavior;
- role and permission enforcement;
- data access rules;
- personal data handling;
- sensitive data handling;
- external API or LLM data transfer;
- secret management;
- environment variable handling;
- logging of sensitive values;
- error messages that expose internals;
- upload/download access;
- audit log requirements;
- data retention and deletion expectations;
- dependency or package risk notes;
- abuse or misuse scenarios relevant to the release.
```

Classify issues as:

```text
- Security Blocker
- Privacy Blocker
- Security Warning
- Privacy Warning
- Recommendation
- Not Applicable
```

Security/privacy assumptions must remain assumptions unless explicitly approved.

---

### Step 7. Release Readiness Review

Evaluate release readiness:

```text
- approved scope is clear;
- required implementation tasks are complete;
- required validation has passed;
- blockers are resolved or explicitly accepted;
- known limitations are documented;
- release notes can be prepared;
- environment requirements are documented;
- migration requirements are documented;
- rollback plan exists;
- monitoring or observability expectations are documented;
- support and ownership are clear.
```

Output a release readiness status:

```text
- Ready for Human Approval
- Ready with Warnings
- Not Ready: Blockers Exist
- Partial / Internal-Only Release Candidate
- Insufficient Evidence
```

---

### Step 8. Deployment Plan Review

If deployment is part of this stage, prepare or review:

```text
- target environment;
- deployment prerequisites;
- required environment variables by name, not secret value;
- build command;
- test command;
- migration command, if applicable;
- deployment steps;
- post-deployment verification;
- smoke test steps;
- rollback procedure;
- recovery procedure;
- release owner;
- deployment approval requirement.
```

Do not execute deployment unless the generated SKILL is explicitly specialized for tool-driven deployment and the human has approved it.

---

### Step 9. Operations Runbook Preparation

Prepare operational handoff guidance:

```text
- system overview for operators;
- runtime dependencies;
- key configuration points;
- monitoring signals;
- logs to inspect;
- common failure modes;
- incident response steps;
- rollback and recovery steps;
- data backup or export notes, if applicable;
- escalation path;
- ownership and maintenance responsibility.
```

---

### Step 10. Documentation Handoff Review

Review documentation freshness:

```text
- README or project setup guide;
- developer setup;
- environment variable documentation;
- API documentation;
- user-facing documentation, if applicable;
- admin/operator documentation;
- known limitations;
- release notes;
- migration notes;
- troubleshooting notes.
```

Documentation must not claim features, guarantees, or security properties that are not supported by evidence.

---

### Step 11. Classify Findings

Every finding must be classified as one of:

```text
- Release Blocker
- Security Blocker
- Privacy Blocker
- Operational Blocker
- Documentation Blocker
- Warning
- Suggestion
- Accepted Limitation Candidate
- Open Question
```

Rules:

```text
- Blockers prevent release unless explicitly accepted by the human.
- Warnings may allow release but must be visible.
- Suggestions must not be treated as required changes.
- Accepted limitation candidates require human approval.
```

---

### Step 12. Produce Stage 12 Artifacts

Create or update all mandatory artifacts and applicable conditional artifacts.

Do not silently omit conditional artifacts. If not applicable, record N/A rationale.

---

### Step 13. Update Context for Stage 13

Update `context_packet.md` for Stage 13 Workflow Retrospective & Skill Improvement.

Include only minimal operational context:

```text
- release readiness outcome;
- blockers/warnings summary;
- implementation evidence quality;
- validation evidence quality;
- agent failure patterns observed during review;
- human decisions needed before release;
- recommended retrospective focus areas.
```

---

## 10. Output Artifacts

### 10.1 Mandatory Artifacts

The generated Stage 12 SKILL should create or update:

```text
/workflow/12_review_release_handoff/12_code_review.md
/workflow/12_review_release_handoff/12_security_privacy_review.md
/workflow/12_review_release_handoff/12_release_readiness.md
/workflow/12_review_release_handoff/12_documentation_handoff.md
/workflow/12_review_release_handoff/result.md
/workflow/context/context_packet.md
```

---

### 10.2 Conditional Artifacts

Create these when applicable:

```text
/workflow/12_review_release_handoff/12_deployment_plan.md
- if deployment, hosting, environment promotion, migration, or release execution is in scope.

/workflow/12_review_release_handoff/12_operations_runbook.md
- if the system will be operated, monitored, supported, handed off, or maintained after release.

/workflow/12_review_release_handoff/12_release_notes.md
- if a versioned release, MVP release, client handoff, or production handoff is planned.

/workflow/12_review_release_handoff/12_migration_readiness.md
- if data, schema, identity, storage, or external-system migration is required.

/workflow/12_review_release_handoff/12_incident_rollback_plan.md
- if rollback, disaster recovery, or incident response requires more detail than the deployment plan.

/workflow/12_review_release_handoff/12_compliance_review.md
- if regulated, security-sensitive, privacy-sensitive, or audit-sensitive constraints apply.
```

---

### 10.3 N/A Record

For every conditional artifact not created, add an N/A record in `result.md`:

```markdown
## N/A Records

| Artifact | Why Not Applicable | Revisit If |
|---|---|---|
| 12_deployment_plan.md | [[reason]] | [[condition that would make it applicable]] |
```

---

## 11. Required Output Structure

### 11.1 `12_code_review.md`

```markdown
# 12 Code Review

## 1. Review Scope
## 2. Inputs Reviewed
## 3. Requirement Satisfaction Review
## 4. Code Quality Findings
## 5. Architecture / Module Boundary Findings
## 6. Performance and Reliability Findings
## 7. Unnecessary Scope Expansion
## 8. Blockers
## 9. Warnings
## 10. Suggestions
## 11. Evidence References
## 12. Review Conclusion
```

---

### 11.2 `12_security_privacy_review.md`

```markdown
# 12 Security and Privacy Review

## 1. Review Scope
## 2. Approved Security / Privacy Constraints
## 3. Authentication Review
## 4. Authorization Review
## 5. Data Access Review
## 6. Personal / Sensitive Data Handling
## 7. Secrets and Environment Variables
## 8. Logging and Error Exposure
## 9. External API / LLM / Third-Party Transfer
## 10. Retention, Deletion, and Audit Concerns
## 11. Security Blockers
## 12. Privacy Blockers
## 13. Warnings
## 14. Assumptions
## 15. Open Questions
## 16. Review Conclusion
```

---

### 11.3 `12_release_readiness.md`

```markdown
# 12 Release Readiness

## 1. Release Candidate Summary
## 2. Approved Release Scope
## 3. Requirement Coverage Summary
## 4. Test and Validation Summary
## 5. Known Limitations
## 6. Blockers
## 7. Warnings
## 8. Accepted Limitation Candidates
## 9. Release Readiness Status
## 10. Human Approval Required
## 11. Recommended Release Decision
```

---

### 11.4 `12_deployment_plan.md`

```markdown
# 12 Deployment Plan

## 1. Deployment Scope
## 2. Target Environment
## 3. Prerequisites
## 4. Environment Variables Required
## 5. Build and Validation Commands
## 6. Migration Steps
## 7. Deployment Steps
## 8. Post-Deployment Smoke Tests
## 9. Rollback Procedure
## 10. Recovery Procedure
## 11. Deployment Owner
## 12. Approval Required Before Execution
```

---

### 11.5 `12_operations_runbook.md`

```markdown
# 12 Operations Runbook

## 1. System Overview
## 2. Runtime Dependencies
## 3. Configuration Overview
## 4. Monitoring and Logging
## 5. Common Failure Modes
## 6. Troubleshooting Steps
## 7. Incident Response
## 8. Rollback and Recovery
## 9. Data Backup / Export Notes
## 10. Ownership and Escalation
## 11. Maintenance Notes
```

---

### 11.6 `12_documentation_handoff.md`

```markdown
# 12 Documentation Handoff

## 1. Documentation Scope
## 2. Documents Reviewed
## 3. Developer Setup Documentation
## 4. User / Admin Documentation
## 5. API / Integration Documentation
## 6. Environment and Deployment Documentation
## 7. Known Limitations Documentation
## 8. Release Notes
## 9. Documentation Gaps
## 10. Handoff Checklist
## 11. Human Approval Required
```

---

### 11.7 `result.md`

```markdown
# Result: 12 Review / Security / Release / Handoff

## 1. Task Summary
## 2. Inputs Used
## 3. Outputs Created or Updated
## 4. Release Candidate Reviewed
## 5. Overall Release Readiness Status
## 6. Blockers
## 7. Warnings
## 8. Suggestions
## 9. Security / Privacy Findings Summary
## 10. Deployment / Operations Findings Summary
## 11. Documentation Findings Summary
## 12. Decision Candidates
## 13. Working Assumptions
## 14. Open Questions
## 15. Accepted Limitation Candidates
## 16. N/A Records
## 17. Traceability Updates
## 18. Context Packet Updates
## 19. Human Approval Required
## 20. Recommended Next Step
```

---

## 12. Traceability Rules

Stage 12 must preserve or improve traceability across:

```text
Goal
→ Requirement
→ Acceptance Criteria
→ Release Scope
→ Task
→ Implementation Evidence
→ Test Evidence
→ Review Finding
→ Release Decision
```

The generated SKILL must:

```text
- preserve existing requirement IDs;
- preserve existing task IDs;
- preserve existing test IDs where available;
- link blockers to affected requirements, tasks, tests, or artifacts;
- link release readiness status to evidence;
- mark traceability gaps explicitly;
- not invent evidence that does not exist.
```

Suggested review finding IDs:

```text
REV-001, REV-002
SEC-001, SEC-002
PRIV-001, PRIV-002
REL-001, REL-002
OPS-001, OPS-002
DOC-001, DOC-002
```

---

## 13. Decision / Assumption / Open Question Rules

### 13.1 Approved Decisions

Only explicit human approval can create approved decisions.

Examples:

```text
Approved: Release version 0.1.0 may be deployed to staging.
Approved: Known limitation KL-003 is accepted for internal demo only.
```

Do not record a release as approved unless the human explicitly approves it.

---

### 13.2 Decision Candidates

Use for recommendations requiring human approval.

Examples:

```text
Candidate: Do not deploy to production until SEC-002 is resolved.
Candidate: Release as internal-only MVP with warnings REL-003 and DOC-001.
Candidate: Accept missing E2E test coverage for prototype demo only.
```

---

### 13.3 Working Assumptions

Use for temporary beliefs required for partial review.

Examples:

```text
Assumption: Release target is staging, not production.
Assumption: Deployment will be manual until CI is configured.
```

---

### 13.4 Open Questions

Use when unresolved information may affect release.

Examples:

```text
Open Question: Who owns post-release incident response?
Open Question: Is user data deletion required before MVP launch?
```

---

### 13.5 Rejected Options

Do not revive rejected release, deployment, architecture, or security options unless the human explicitly reopens them.

---

## 14. Validation Checklist

Before completing the SKILL, verify:

```text
[ ] Approved release scope was identified.
[ ] Implementation evidence was reviewed.
[ ] Test evidence was reviewed.
[ ] Must-have requirements were checked against evidence.
[ ] Security and privacy constraints were reviewed.
[ ] Environment variables were reviewed by name only, not by secret value.
[ ] Deployment readiness was reviewed if deployment is in scope.
[ ] Rollback or recovery readiness was reviewed if deployment is in scope.
[ ] Operations handoff was prepared if operation is expected.
[ ] Documentation freshness was reviewed.
[ ] Blockers, warnings, and suggestions were separated.
[ ] Accepted limitation candidates were clearly marked.
[ ] N/A records were created for skipped conditional artifacts.
[ ] Traceability gaps were recorded.
[ ] context_packet.md was prepared for Stage 13.
[ ] Human approval gate was included.
```

---

## 15. Human Approval Gate

End with:

```markdown
## Human Approval Required

### Release Decision to Approve
- [ ] Approve release as ready.
- [ ] Approve release with warnings.
- [ ] Approve internal-only or staging-only release.
- [ ] Reject release until blockers are resolved.
- [ ] Defer release decision.

### Deployment Decision to Approve
- [ ] Approve deployment plan.
- [ ] Approve rollback plan.
- [ ] Approve migration plan, if applicable.
- [ ] Approve environment readiness.

### Security / Privacy Decisions to Approve
- [ ] Accept or reject listed security warnings.
- [ ] Accept or reject listed privacy warnings.
- [ ] Confirm no unresolved blocker remains.

### Operations / Handoff Decisions to Approve
- [ ] Approve operations owner.
- [ ] Approve handoff documentation.
- [ ] Approve support and escalation expectations.

### Assumptions to Confirm
- [[list assumptions]]

### Open Questions to Resolve
- [[list open questions]]

### Artifacts Ready for Review
- /workflow/12_review_release_handoff/12_code_review.md
- /workflow/12_review_release_handoff/12_security_privacy_review.md
- /workflow/12_review_release_handoff/12_release_readiness.md
- /workflow/12_review_release_handoff/12_documentation_handoff.md
- /workflow/12_review_release_handoff/result.md
- [[conditional artifacts]]

### Recommended Next Step
- [[recommendation]]
```

---

## 16. Context Packet Update Rules

Update:

```text
/workflow/context/context_packet.md
```

Prepare it for:

```text
Stage 13 Workflow Retrospective & Skill Improvement
```

Required sections:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 12 Review / Security / Release / Handoff
- Completed stages:
- Next recommended stage: 13 Workflow Retrospective & Skill Improvement

## 2. Approved Decisions
- Only human-approved release, deployment, operations, or handoff decisions.

## 3. Working Assumptions
- Release, deployment, security, privacy, or operations assumptions not yet confirmed.

## 4. Open Questions
- Questions that may affect release, deployment, operation, documentation, or retrospective.

## 5. Rejected / Superseded Options
- Release, deployment, or handoff options that should not be reused unless reopened.

## 6. Constraints That Must Not Be Violated
- Scope:
- Security:
- Privacy:
- Deployment:
- Operations:
- Documentation:

## 7. Key Context for Next Stage
- Release readiness result.
- Review quality notes.
- Evidence quality notes.
- Agent failure patterns observed.
- Human judgment points.
- Skill/template improvement candidates.

## 8. Required Inputs for Next Stage
- /workflow/12_review_release_handoff/result.md
- /workflow/12_review_release_handoff/12_release_readiness.md
- /workflow/12_review_release_handoff/12_code_review.md
- /workflow/12_review_release_handoff/12_security_privacy_review.md
- /workflow/12_review_release_handoff/12_documentation_handoff.md
- conditional Stage 12 artifacts if created.

## 9. Do Not Do
- Do not treat release as approved unless the human explicitly approved it.
- Do not treat warnings as resolved unless evidence exists.
- Do not reopen rejected options unless the human explicitly reopens them.
```

---

## 17. Failure Handling

If Stage 12 cannot be completed safely, create a partial `result.md` with:

```markdown
## Blocker Report

### Blocking Issue
- [[issue]]

### Why It Matters
- [[release/security/privacy/deployment/operation impact]]

### Affected Artifacts or Stages
- [[artifacts/stages]]

### Safe Partial Work Completed
- [[what was reviewed]]

### Human Decision Needed
- [[decision needed]]
```

Common failure conditions:

```text
- No approved release scope.
- No implementation evidence.
- No test evidence.
- Missing security/privacy source artifacts for sensitive system.
- Deployment requested but deployment environment unknown.
- Migration required but migration plan missing.
- Unresolved blocker affects must-have requirement.
- Conflicting approved decisions.
- USER_DIRECTIVES.md conflicts with approved release scope.
```

---

## 18. Review Addendum

This is a review-related SKILL.

It must:

```text
- Review against approved requirements.
- Review against acceptance criteria.
- Review against release scope.
- Review against security and privacy constraints.
- Review against architecture and data decisions when applicable.
- Review implementation evidence.
- Review test evidence.
- Identify release blockers.
- Separate blockers, warnings, and suggestions.
- Avoid making release decisions without human approval.
```

---

## 19. Specialization Hooks

Apply project-type specialization addenda after the core and stage-specific rules.

### web_saas

May add:

```text
- hosting readiness;
- auth callback domain review;
- CORS / API exposure review;
- cookie/session configuration review;
- production environment variable review;
- analytics/privacy banner review;
- admin access review.
```

### internal_tool

May add:

```text
- operator documentation;
- access provisioning;
- audit expectations;
- workflow fallback procedure;
- organizational owner handoff.
```

### mobile_app

May add:

```text
- app store release checklist;
- versioning;
- device permission review;
- offline/sync behavior review;
- crash reporting;
- platform-specific rollback limitations.
```

### ai_data_product

May add:

```text
- model output risk review;
- dataset provenance review;
- evaluation evidence review;
- human review requirements;
- bias/error analysis;
- reproducibility record;
- model/version handoff.
```

### regulated_security_sensitive

May add:

```text
- compliance checklist;
- audit log review;
- privacy impact review;
- threat-model closure check;
- access review;
- data retention/deletion evidence;
- stronger release blockers.
```

### brownfield_legacy

May add:

```text
- regression risk review;
- backward compatibility review;
- migration safety review;
- legacy integration review;
- feature flag or staged rollout review.
```

Specialization must not weaken approval, evidence, security, privacy, or traceability rules.

---

## 20. Tool Wrapper Hooks

Tool-specific wrappers may define:

```text
- file creation commands;
- save locations;
- review UI behavior;
- CI command invocation;
- deployment command conventions;
- sandbox restrictions;
- artifact validation commands.
```

Tool wrappers must not define:

```text
- release approval rules;
- security/privacy acceptance criteria;
- requirement satisfaction decisions;
- deployment approval;
- assumption handling;
- traceability policy;
- stage boundaries.
```

---

## 21. Do Not Do

The generated Stage 12 SKILL must not:

```text
- approve the release on behalf of the human developer;
- deploy without explicit human approval;
- treat missing evidence as passing evidence;
- claim tests passed without evidence;
- expose or copy secret values;
- silently accept unresolved security or privacy issues;
- collapse blockers, warnings, and suggestions into one list;
- convert assumptions into approved decisions;
- modify approved requirements or release scope;
- reopen rejected options without explicit human instruction;
- use context_packet.md as the only source of truth;
- read all project history by default;
- perform implementation or refactoring unless explicitly instructed;
- create Stage 13 retrospective artifacts;
- treat documentation handoff as complete without checking freshness and gaps.
```

---

## 22. Template Quality Checklist

Before considering the generated Stage 12 SKILL usable, verify:

```text
[ ] Metadata is filled.
[ ] Purpose and core question are clear.
[ ] Always Read inputs are defined.
[ ] Read If Applicable inputs are defined.
[ ] Do Not Read By Default is defined.
[ ] Missing input handling is defined.
[ ] USER_DIRECTIVES.md handling is included.
[ ] Mandatory artifacts are defined.
[ ] Conditional artifacts are defined.
[ ] N/A record rule is included.
[ ] Required output structures are defined.
[ ] Traceability rules are defined.
[ ] Blockers, warnings, and suggestions are separated.
[ ] Security/privacy review is explicit.
[ ] Deployment/operations handoff is conditional but supported.
[ ] Documentation handoff is explicit.
[ ] Human approval gate is explicit.
[ ] context_packet.md update rules prepare Stage 13.
[ ] Failure handling is included.
[ ] Specialization hooks are included.
[ ] Tool wrapper hooks are included.
[ ] No project-specific assumptions are introduced.
```
