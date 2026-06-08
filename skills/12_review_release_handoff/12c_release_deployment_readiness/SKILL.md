---
name: 12c_release_deployment_readiness
description: Review release readiness, deployment prerequisites, environment configuration, migration readiness, rollback/recovery, smoke tests, and release notes.
stage: 12 Review / Security / Release / Handoff
parent_skill: /skills/12_review_release_handoff/SKILL.md
subskill_id: 12c
subskill_order: 3
previous_subskill: /skills/12_review_release_handoff/12b_security_privacy_review/SKILL.md
next_subskill: /skills/12_review_release_handoff/12d_operations_documentation_handoff/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/12_review_release_handoff/12_release_readiness.md
requires_human_approval: true
external_visibility: internal
---

# 12c Release / Deployment Readiness

## 1. Purpose

This sub-SKILL reviews whether the release candidate is operationally ready for human-approved release and deployment.

It covers:

- release readiness status;
- deployment prerequisites;
- target environment;
- build and validation commands;
- environment variable requirements by name only;
- migration readiness;
- rollback and recovery readiness;
- smoke test plan;
- release notes.

This sub-SKILL prepares deployment and release planning artifacts, but must not execute deployment without explicit human instruction and approval.

## 2. Core Question

```text
Can this release candidate be safely released or deployed, and what blockers, warnings, rollback requirements, migration concerns, and human approvals remain?
```

## 3. Required Inputs

### Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md

/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/09_tasks/09_task_cards.md
/workflow/11_implementation_results/
/workflow/12_review_release_handoff/12_code_review.md
/workflow/12_review_release_handoff/12_security_privacy_review.md
```

### Read If Applicable

```text
/workflow/00_intake/00_existing_context_review.md
- if brownfield, migration, extension, or compatibility-sensitive.

/workflow/05_architecture/05_architecture_plan.md
- if deployment/runtime structure depends on architecture decisions.

/workflow/05_architecture/05_integration_contracts.md
- if integrations require deployment configuration or external readiness.

/workflow/06_data/06_migration_plan.md
- if data/schema migration is required.

/workflow/06_data/06_data_security_rules.md
- if deployment includes access/security rule changes.

/workflow/08_test_strategy/08_manual_test_plan.md
- if manual validation or smoke testing is required.

/workflow/11_implementation_results/11_test_evidence_*.md
- if release validation evidence exists.

CI configuration, deployment configuration, infrastructure files, hosting settings, package scripts
- if release readiness requires them.

Project documentation for environment variables
- if deployment requires environment variables.
```

### Do Not Read By Default

```text
- production secrets or secret values;
- private credentials;
- raw logs with sensitive data;
- unrelated source files;
- superseded deployment notes;
- rejected release plans.
```

## 4. USER_DIRECTIVES.md Handling

Check:

```text
/workflow/12_review_release_handoff/USER_DIRECTIVES.md
```

Classify directives related to release target, deployment permission, environment, schedule, rollback, migration, or accepted limitations.

Do not treat a directive as deployment approval unless it explicitly approves deployment.

## 5. Input Preflight Procedure

```text
[ ] Identify release candidate and release target.
[ ] Identify release type: prototype, internal demo, staging, production, migration, hotfix, or documentation handoff.
[ ] Check release scope.
[ ] Check code review blockers.
[ ] Check security/privacy blockers.
[ ] Check validation evidence.
[ ] Check deployment target and prerequisites.
[ ] Check migration requirement.
[ ] Check rollback/recovery expectations.
[ ] Check environment variable documentation by name only.
```

Blocking preflight issues:

```text
- release target unknown;
- release scope unapproved;
- unresolved code/security/privacy blocker;
- no validation evidence for must-have behavior;
- migration required but no migration plan;
- deployment requested but environment/prerequisites unknown;
- rollback required but no rollback strategy.
```

## 6. Execution Procedure

### Step 1. Confirm Release Candidate

Record:

```text
release candidate name/version if any
release target
release type
included scope
excluded/deferred scope
known limitations
review status from 12a and 12b
```

### Step 2. Summarize Release Readiness Evidence

Review:

```text
implemented tasks
passed tests
manual validation
skipped tests and rationale
known failures
open blockers
warnings
accepted limitation candidates
```

### Step 3. Classify Overall Release Status

Use one of:

```text
Ready for Human Approval
Ready with Warnings
Not Ready: Blockers Exist
Partial / Internal-Only Release Candidate
Insufficient Evidence
```

### Step 4. Prepare Deployment Plan if Applicable

If deployment is in scope, document:

```text
target environment
deployment owner
prerequisites
environment variables required by name only
build command
validation command
migration command if applicable
deployment steps
post-deployment smoke tests
rollback procedure
recovery procedure
approval required before execution
```

Do not execute deployment.

### Step 5. Prepare Migration Readiness if Applicable

If migration exists, check:

```text
migration purpose
affected data/schema
backup/export plan
dry-run or test evidence
rollback/repair strategy
owner
risk level
human approval needed
```

### Step 6. Prepare Rollback / Incident Plan if Needed

If deployment or migration risk exists, document:

```text
rollback trigger
rollback steps
recovery steps
data repair considerations
communication owner
post-rollback validation
```

### Step 7. Prepare Release Notes if Applicable

If release notes are needed, draft:

```text
release summary
included changes
known limitations
migration notes
operator notes
user/admin notes
security/privacy notes
rollback notes
```

Do not overclaim features or guarantees.

## 7. Output Artifacts

### Mandatory Artifacts

```text
/workflow/12_review_release_handoff/12_release_readiness.md
```

### Conditional Artifacts

```text
/workflow/12_review_release_handoff/12_deployment_plan.md
- if deployment, hosting, environment promotion, or release execution is in scope.

/workflow/12_review_release_handoff/12_migration_readiness.md
- if data, schema, identity, storage, or external-system migration is required.

/workflow/12_review_release_handoff/12_incident_rollback_plan.md
- if rollback, recovery, or incident response requires more detail than the deployment plan.

/workflow/12_review_release_handoff/12_release_notes.md
- if a versioned release, client handoff, internal MVP release, or production handoff is planned.
```

If a conditional artifact is not created, record N/A rationale for finalizer.

## 8. Required Output Structure

### `12_release_readiness.md`

```markdown
# 12 Release Readiness

## 1. Release Candidate Summary
## 2. Approved Release Scope
## 3. Inputs Reviewed
## 4. Requirement Coverage Summary
## 5. Test and Validation Summary
## 6. Code Review Summary
## 7. Security / Privacy Review Summary
## 8. Known Limitations
## 9. Blockers
## 10. Warnings
## 11. Accepted Limitation Candidates
## 12. Conditional Artifact N/A Notes
## 13. Release Readiness Status
## 14. Human Approval Required
## 15. Recommended Release Decision
## 16. Handoff to 12d Operations / Documentation Handoff
```

### `12_deployment_plan.md`

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

## 9. Traceability Requirements

Preserve links:

```text
Release Scope → Task → Validation Evidence → Release Readiness Status → Release Decision Candidate
```

Use IDs:

```text
REL-001, REL-002, ...
DEP-001, DEP-002, ...
MIG-001, MIG-002, ...
ROLL-001, ROLL-002, ...
```

## 10. Validation Checklist

```text
[ ] Release candidate and target were identified.
[ ] Release scope was checked.
[ ] Code review findings were considered.
[ ] Security/privacy findings were considered.
[ ] Test/validation evidence was summarized.
[ ] Deployment plan was created if applicable.
[ ] Migration readiness was created if applicable.
[ ] Rollback/recovery plan was created if applicable.
[ ] Release notes were created if applicable.
[ ] Conditional artifact N/A notes were recorded.
[ ] No deployment was executed without approval.
[ ] Secret values were not exposed.
```

## 11. Human Approval Gate

This sub-SKILL prepares release and deployment decision candidates.

End with:

```markdown
## Human Review Needed

### Release Decision Candidates
- ...

### Deployment Decision Candidates
- ...

### Migration / Rollback Decisions
- ...

### Accepted Limitation Candidates
- ...

### Open Questions
- ...

### Recommended Next Sub-SKILL
- Run `/skills/12_review_release_handoff/12d_operations_documentation_handoff/SKILL.md`.
```

## 12. Context Handoff to Next Sub-SKILL

At the end of `12_release_readiness.md`, include:

```markdown
## Handoff to 12d Operations / Documentation Handoff

### Release Readiness Status
### Operational Risks
### Documentation Needed Before Handoff
### Known Limitations to Document
### Deployment / Rollback Notes Operators Need
### Open Questions Affecting Operations or Documentation
```

## Decision / Assumption / Open Question Rules

Use these classifications consistently:

```text
Approved Decision
- Only explicit human approval may create this.

Decision Candidate
- A recommended release, security, deployment, operations, or documentation decision awaiting human approval.

Working Assumption
- A temporary belief used only to continue safe partial work.

Open Question
- An unresolved issue that may affect release, deployment, security, privacy, operations, documentation, or retrospective.

Rejected Option
- An option explicitly rejected or superseded. Do not revive it unless the human reopens it.

Recommendation
- Agent advice. It is not a decision.
```

Do not update `DECISIONS.md` unless explicit human approval exists.

## Failure Handling

If the SKILL cannot be completed safely, create a partial output with:

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
- ...

### Affected Artifacts or Stages
- ...

### Safe Partial Work Completed
- ...

### Human Decision Needed
- ...
```

Do not pretend completion when required evidence is missing.

## Do Not Do

The agent must not:

- approve release, deployment, or risk acceptance on behalf of the human developer;
- silently turn assumptions into decisions;
- treat unapproved drafts as source of truth;
- use superseded or rejected artifacts as current truth;
- expose secret values;
- claim tests passed without evidence;
- mark a blocker as resolved without evidence;
- update `DECISIONS.md` without explicit human approval;
- create README.md or artifact_contract.yml unless explicitly requested.
