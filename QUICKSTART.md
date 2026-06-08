# Quick Start

This guide shows the shortest practical path for trying the Manual Agentic Coding Workflow with a coding agent.

The goal is not to make an agent build a full product immediately. The goal is to create approved project context and move through the workflow one stage at a time.

## 1. Prerequisites

You need:

- a coding agent or LLM-based development tool, such as Claude Code, Codex, Antigravity, or a similar agentic coding environment;
- a target project folder;
- this workflow repository available locally or as reference material;
- enough human review time to approve, revise, or reject the agent's outputs.

You do not need to prepare every workflow artifact manually before starting. Stage 00 creates the initial project intake artifacts.

## 2. Understand the basic rule

Do not begin with:

```text
Build this app.
```

Begin with:

```text
Use the Stage 00 Project Intake skill to understand this project, create the required intake artifacts, identify assumptions and open questions, and prepare context for Stage 01.
```

The workflow is designed around explicit artifacts and human approval gates.

## 3. Prepare the target project folder

Inside the target project, create the workflow folders.

Recommended initial structure:

```text
/workflow
  /00_intake
  /01_goal
  /02_stakeholders_risk
  /03_requirements
  /04_domain
  /05_architecture
  /06_data
  /07_mvp_release
  /08_test_strategy
  /09_tasks
  /10_prompts
  /11_implementation_results
  /12_review_release_handoff
  /13_retrospective

/workflow/context
  artifact_manifest.yml
  context_packet.md
  DECISIONS.md
  ASSUMPTIONS.md
  OPEN_QUESTIONS.md
  REJECTED_OPTIONS.md
  TRACEABILITY_MATRIX.md
  APPROVAL_LOG.md
```

At the beginning, the context files may be empty placeholders. The agent should update them as the workflow progresses.

Minimum placeholder files:

```text
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
```

## 4. Prepare the initial project idea

Create a short file such as:

```text
/workflow/00_intake/initial_idea.md
```

Suggested content:

```markdown
# Initial Project Idea

## Product or system idea
Describe the system you want to build.

## Target users
Describe who may use it.

## Main problem
Describe the problem it should solve.

## Known constraints
List fixed technologies, schedule constraints, privacy concerns, budget limits, or non-negotiable decisions.

## Existing materials
List any existing code, documents, diagrams, notes, APIs, datasets, or deployment environments.

## What the agent must not do yet
For example: do not write production code, do not choose a database, do not invent requirements, do not create UI screens yet.
```

Keep this short. Stage 00 is responsible for turning this into structured intake artifacts.

## 5. Run Stage 00 Project Intake

Open your coding agent in the target project folder.

Give it a prompt like this:

```text
You are working inside the Manual Agentic Coding Workflow.

Run Stage 00 Project Intake.

Use this reusable skill:
/skills/00_project_intake/SKILL.md

Target project workflow folder:
/workflow

Initial input:
/workflow/00_intake/initial_idea.md

Follow the SKILL.md exactly.
Do not implement code.
Do not create architecture, database schema, UI, or tasks yet.
Create or update only the Stage 00 artifacts and required context files.
Separate approved decisions, decision candidates, working assumptions, open questions, risks, and recommendations.
End with a human approval gate.
```

Adjust paths to match your actual repository layout.

## 6. Review Stage 00 outputs

After Stage 00, inspect the generated artifacts.

Typical outputs may include:

```text
/workflow/00_intake/00_project_intake.md
/workflow/00_intake/00_existing_context_review.md
/workflow/00_intake/result.md
/workflow/context/context_packet.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
```

Review these carefully:

- Did the agent classify the project correctly?
- Did it identify fixed technology choices correctly?
- Did it avoid making unapproved product decisions?
- Did it record missing information as open questions?
- Did it record temporary guesses as assumptions rather than decisions?
- Did it prepare useful context for Stage 01?

## 7. Approve, revise, or reject decisions

Do not treat the agent's Stage 00 output as automatically approved.

You should explicitly mark what you approve.

For example, update `APPROVAL_LOG.md` or `DECISIONS.md` manually with entries such as:

```markdown
# APPROVAL_LOG.md

## 2026-06-08 — Stage 00 Project Intake

Approved:
- Project type: Greenfield MVP.
- Initial target: web application.
- Fixed stack: not yet decided.

Rejected:
- Do not assume mobile app support for MVP.

Needs clarification:
- Whether user accounts are required in the first release.
```

Only explicit human approval should become an approved decision.

## 8. Run Stage 01 Service Goal Definition

After Stage 00 is reviewed, run Stage 01.

Prompt template:

```text
You are working inside the Manual Agentic Coding Workflow.

Run Stage 01 Service Goal Definition.

Use this reusable skill:
/skills/01_service_goal_definition/SKILL.md

Target project workflow folder:
/workflow

Before producing outputs, read:
- /workflow/context/context_packet.md
- /workflow/context/DECISIONS.md
- /workflow/context/ASSUMPTIONS.md
- /workflow/context/OPEN_QUESTIONS.md
- /workflow/00_intake/00_project_intake.md
- /workflow/00_intake/result.md

Follow the SKILL.md exactly.
Do not implement code.
Do not create requirements, architecture, database schema, UI, or tasks yet.
Create or update only the Stage 01 artifacts and required context files.
End with a human approval gate.
```

Expected Stage 01 output:

```text
/workflow/01_goal/01_service_goal.md
/workflow/01_goal/result.md
/workflow/context/context_packet.md
```

## 9. Continue stage by stage

Recommended execution order:

```text
00 Project Intake
→ 01 Service Goal Definition
→ 02 Stakeholder & Risk Framing
→ 03 Requirements & Acceptance Criteria
→ 04 Domain Modeling / DDD
→ 05 Architecture & Technical Contracts
→ 06 Data Design
→ 07 MVP Scope & Release Slicing
→ 08 Test Strategy & Validation Harness
→ 09 Task Breakdown
→ 10 Implementation Prompt Writing
→ 11 TDD Implementation Loop
→ 12 Review / Security / Release / Handoff
→ 13 Workflow Retrospective & Skill Improvement
```

Do not skip directly from idea to implementation unless you are intentionally doing an exploratory spike.

If you skip a stage, record why it was skipped and what risks that creates.

## 10. How to handle context reset

You can start a new agent session between stages.

The new session should not rely on previous chat history. It should read the required files:

```text
1. Current stage SKILL.md
2. /workflow/context/context_packet.md
3. /workflow/context/DECISIONS.md
4. /workflow/context/ASSUMPTIONS.md
5. /workflow/context/OPEN_QUESTIONS.md
6. Required approved artifacts from previous stages
7. Stage-local USER_DIRECTIVES.md if it exists
```

This is one of the main reasons the workflow uses artifacts instead of long conversations as the source of truth.

## 11. How to use USER_DIRECTIVES.md

For stage-specific human instructions, create:

```text
/workflow/<stage_folder>/USER_DIRECTIVES.md
```

Use it for:

- corrections to agent output;
- additional constraints;
- explicit rejections;
- review comments;
- preferred direction;
- questions the agent must answer;
- scope changes for the current stage.

Example:

```markdown
# USER_DIRECTIVES.md

For this stage:
- Treat the first release as a web MVP only.
- Do not assume mobile support.
- Consider authentication likely, but not yet approved.
- Flag any requirement involving personal data for human review.
```

The agent should read `USER_DIRECTIVES.md` before executing the stage.

## 12. How to run a split stage

Some stages are split into multiple sub-skills.

Example:

```text
/skills/04_domain_modeling/
  SKILL.md
  /04a_ubiquitous_language/SKILL.md
  /04b_domain_concepts_entities_values/SKILL.md
  /04c_aggregates_rules_lifecycle/SKILL.md
  /04d_events_bounded_contexts/SKILL.md
  /04e_domain_modeling_finalizer/SKILL.md
```

Run them in the defined order.

Important rule:

```text
The stage is not ready for downstream use until the finalizer has run and the official stage artifacts have been reviewed and approved.
```

Downstream stages should depend on approved official artifacts under `/workflow`, not on internal sub-skill outputs.

## 13. Minimal useful workflow path

For a small greenfield MVP, the minimum useful path is usually:

```text
00 Intake
01 Goal
02 Stakeholder & Risk
03 Requirements & Acceptance Criteria
05 Architecture & Contracts
07 MVP Scope
08 Test Strategy
09 Task Breakdown
10 Implementation Prompts
11 TDD Implementation Loop
12 Review & Release
13 Retrospective
```

You may simplify, but do not remove:

- explicit goals;
- testable requirements;
- human approval gates;
- implementation evidence;
- context handoff;
- review before release.

## 14. Implementation starts at Stage 11, not before

Before Stage 11, the agent may draft plans, requirements, models, contracts, tests, and prompts.

It should not make production code changes unless you explicitly authorize an exploratory spike.

In Stage 11, each task should follow a TDD or test-aware loop:

```text
1. Read task context.
2. Inspect existing code.
3. Restate the task and allowed change scope.
4. Write or identify the failing test.
5. Confirm failure if feasible.
6. Implement the minimal change.
7. Run relevant tests.
8. Refactor if needed.
9. Run broader validation if feasible.
10. Record implementation and test evidence.
```

If strict test-first implementation is not feasible, the agent should explain why and create a validation plan before coding.

## 15. Troubleshooting

### The agent wants to implement too early

Stop and restate the current stage boundary.

Use this instruction:

```text
Do not implement code in this stage. Produce only the artifacts required by the current SKILL.md and end with a human approval gate.
```

### The agent treats assumptions as decisions

Correct the output and update `ASSUMPTIONS.md` or `OPEN_QUESTIONS.md`.

Use this instruction:

```text
Reclassify unapproved decisions as decision candidates or working assumptions. Do not record them as approved decisions unless explicitly approved by the human developer.
```

### The agent reads too many files

Point it back to the skill input contract.

Use this instruction:

```text
Read only Always Read inputs and conditionally applicable inputs defined by the SKILL.md. Do not read full historical artifacts or unrelated drafts by default.
```

### The stage output is too vague

Ask for concrete artifacts.

Use this instruction:

```text
Revise the output so that each required artifact has concrete sections, explicit assumptions, open questions, risks, decision candidates, and next-stage context.
```

### The next stage does not know what to read

Update `context_packet.md`.

It should include:

```text
Current Project State
Approved Decisions
Working Assumptions
Open Questions
Rejected / Superseded Options
Constraints That Must Not Be Violated
Key Context for Next Stage
Required Inputs for Next Stage
Do Not Do
```

## 16. Stage completion checklist

Before moving to the next stage, confirm:

```text
[ ] Required artifacts were created or updated.
[ ] Missing inputs were recorded.
[ ] Assumptions are clearly labeled.
[ ] Decision candidates are not treated as approved decisions.
[ ] Open questions are recorded.
[ ] Risks are visible.
[ ] Rejected options are recorded if applicable.
[ ] Traceability was updated if applicable.
[ ] context_packet.md was prepared for the next stage.
[ ] Human approval gate is present.
[ ] The human developer approved, revised, or rejected key decisions.
```

## 17. Recommended next step

After completing this quick start:

1. Run Stage 00 and Stage 01 on a small real or sample project.
2. Review whether the generated artifacts are useful enough to continue.
3. Improve the relevant `SKILL.md`, `README.md`, or `artifact_contract.yml` if the agent behavior was unclear.
4. Continue to Stage 02 only after the service goal is reviewed.
