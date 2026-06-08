---
name: 13c_agent_failure_pattern_analysis
description: Analyze evidence-backed Agent strengths, repeated failure patterns, mixed patterns, one-off issues, insufficient evidence items, and human judgment points.
stage: 13 Workflow Retrospective & Skill Improvement
parent_skill: /skills/13_workflow_retrospective/SKILL.md
subskill_id: 13c
subskill_order: 3
previous_subskill: /skills/13_workflow_retrospective/13b_stage_workflow_review/SKILL.md
next_subskill: /skills/13_workflow_retrospective/13d_skill_improvement_backlog/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/13_retrospective/13_agent_failure_patterns.md
requires_human_approval: true
external_visibility: internal
---

# 13c Agent Failure Pattern Analysis

## 1. Purpose

This sub-skill identifies how the Agent behaved across the workflow.

It separates:

```text
- Agent strengths;
- repeated failure patterns;
- mixed patterns;
- one-off issues;
- insufficient evidence items;
- human judgment points.
```

It must produce evidence-backed patterns, not vague criticism or blame.

## 2. Core Question

```text
Where did the Agent reliably help, where did it repeatedly fail, and what mitigations should future SKILLs or workflow rules include?
```

## 3. Required Inputs

### Always Read

```text
/workflow/13_retrospective/13_workflow_retrospective.md
/workflow/context/context_packet.md
/workflow/context/APPROVAL_LOG.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/13_retrospective/USER_DIRECTIVES.md, if it exists
```

### Read If Applicable

```text
/workflow/11_implementation_results/11_task_result_*.md
- if implementation behavior, task drift, or scope control is in scope.

/workflow/11_implementation_results/11_test_evidence_*.md
- if validation evidence, TDD adherence, or test claims are in scope.

/workflow/10_prompts/10_implementation_prompts.md
- if prompt ambiguity, allowed scope, forbidden changes, or command evidence is in scope.

/workflow/*/review_notes.md
- if human corrections or overrides are in scope.

agent_session_logs/*
- only if explicitly provided and safe to inspect.
```

### Do Not Read By Default

```text
- secrets, credentials, environment files;
- all raw chat logs;
- raw code diffs;
- unrelated product documents;
- private human notes not explicitly supplied for review.
```

## 4. Input Preflight Procedure

```text
[ ] Confirm evidence level from 13a.
[ ] Read workflow findings from 13b.
[ ] Identify possible Agent behavior patterns.
[ ] Determine whether each possible pattern has repeated evidence, one-off evidence, or insufficient evidence.
[ ] Do not create a failure pattern without evidence.
[ ] Identify human intervention evidence if available.
```

## 5. Execution Procedure

### Step 1. Identify Agent Strengths

Look for evidence of:

```text
- useful decomposition;
- correct use of approved context;
- clear uncertainty reporting;
- effective artifact structuring;
- helpful traceability preservation;
- strong validation discipline;
- good scope control;
- good context handoff.
```

### Step 2. Identify Failure Pattern Candidates

Look for evidence of:

```text
- premature implementation;
- silent assumption conversion;
- scope expansion;
- over-reading unrelated artifacts;
- under-reading required context;
- hallucinated source-of-truth claims;
- weak traceability;
- vague outputs;
- skipped validation evidence;
- prompt obedience failures;
- repeated need for human correction;
- context loss after session reset;
- treating draft artifacts as approved;
- reviving rejected options.
```

### Step 3. Classify Each Pattern

Use these classifications:

```text
Strength
Failure Pattern
Mixed Pattern
One-off Issue
Insufficient Evidence
```

A `Failure Pattern` requires more than one evidence point or one severe evidence-backed incident.

### Step 4. Analyze Root Cause Hypotheses

For each failure pattern, identify likely causes:

```text
- unclear SKILL instruction;
- missing input contract;
- weak output structure;
- missing do-not-do rule;
- insufficient artifact contract;
- ambiguous human directive;
- tool limitation;
- context overload;
- insufficient finalizer or review gate;
- project-specific complexity.
```

Mark root causes as hypotheses unless directly evidenced.

### Step 5. Identify Human Judgment Points

Record where human judgment was essential:

```text
- approval of goals, scope, architecture, data, release, or workflow changes;
- correction of Agent assumptions;
- prioritization of trade-offs;
- security, privacy, or compliance decisions;
- release readiness decisions;
- acceptance of technical debt;
- rejection of unnecessary complexity;
- interpretation of ambiguous domain rules.
```

### Step 6. Create Mitigation Candidates

For each pattern, propose mitigations:

```text
- SKILL instruction change;
- input contract change;
- output artifact section change;
- validation checklist change;
- approval gate change;
- finalizer requirement;
- split/merge/deprecate recommendation;
- tool wrapper note;
- human operating practice.
```

Do not convert mitigations into approved changes.

## 6. Output Artifacts

Create or update:

```text
/workflow/13_retrospective/13_agent_failure_patterns.md
```

Required structure:

```markdown
# 13 Agent Failure Patterns

## 1. Summary

## 2. Failure Pattern Index
| ID | Pattern | Frequency | Severity | Evidence | Affected Stages | Recommended Mitigation |
|---|---|---:|---|---|---|---|

## 3. Detailed Patterns

### AFP-001: [[Pattern Name]]
- Classification:
- Evidence:
- Affected stage(s):
- Root cause hypothesis:
- Why it matters:
- Mitigation:
- Skill changes suggested:
- Validation method for mitigation:
- Approval required:

## 4. Agent Strengths

## 5. Mixed Patterns

## 6. Non-Patterns / One-Off Issues

## 7. Insufficient Evidence Items

## 8. Human Judgment Points
```

Also update this section in:

```text
/workflow/13_retrospective/13_workflow_retrospective.md
```

```markdown
## 12. Agent Behavior Summary
- Agent strengths:
- Agent failure patterns:
- Mixed patterns:
- Human corrections required:

## 13. Human Judgment Summary
- Decisions only the human could make:
- Places where the Agent needed clearer constraints:
- Future approval gate recommendations:
```

### Conditional Artifact Candidates

Create or mark for finalizer creation when applicable:

```text
/workflow/13_retrospective/13_human_intervention_log.md
- if human corrections, overrides, or approval decisions are significant and evidence exists.

/workflow/13_retrospective/13_tooling_limits.md
- if tool-specific execution, sandbox, context-window, file-handling, or cost limitations contributed to patterns.
```

## 7. Traceability Rules

Use IDs:

```text
AFP-001, AFP-002    Agent Failure Pattern
```

Required links:

```text
Failure Pattern → Evidence Source
Failure Pattern → Affected Stage / Skill
Failure Pattern → Root Cause Hypothesis
Failure Pattern → Mitigation Candidate
```

Do not create a high-severity failure pattern without evidence.

## 8. Decision / Assumption / Open Question Rules

Classify:

```text
Decision Candidate: Proposed mitigation requiring approval.
Working Assumption: Hypothesis about why a pattern occurred.
Open Question: Missing evidence needed before mitigation.
Risk: Risk of recurrence if unmitigated.
```

Do not approve any mitigation.

## 9. Validation Checklist

```text
[ ] Strengths and failures are separated.
[ ] Repeated patterns and one-off issues are separated.
[ ] Insufficient evidence items are identified.
[ ] Every AFP item has an evidence source or is downgraded.
[ ] Root causes are marked as hypotheses unless verified.
[ ] Human judgment points are recorded.
[ ] Mitigation candidates are not treated as approved changes.
```

## 10. Human Approval Gate

```markdown
## Human Approval Required

### Failure Patterns to Accept as Evidence-Backed
- ...

### Patterns to Downgrade or Reclassify
- ...

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Recommended Next Step
- Run `13d_skill_improvement_backlog`.
```

## 11. Do Not Do

The Agent must not:

```text
- blame without evidence;
- infer repeated failures from one weak example;
- expose private data from logs;
- treat a mitigation as approved;
- rewrite SKILLs;
- create product requirements or implementation tasks;
- treat tool limitations as Agent failures without evidence.
```
