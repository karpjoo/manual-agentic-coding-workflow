# Manual Agentic Coding Workflow

A structured, artifact-first workflow for using coding agents in human-controlled software development.

This repository is not a collection of magic prompts. It is a reusable workflow for experienced developers who want to use LLM-based coding agents such as Claude Code, Codex, Antigravity, or similar tools inside an inspectable software development process.

```text
Agentic Coding = structured workflow + reusable skills + human approval gates + traceable artifacts
```

## What this is

Manual Agentic Coding Workflow is a staged SDLC-style process for developing software with coding agents.

The workflow helps a human developer:

- turn an initial idea into approved goals, requirements, domain models, architecture, tasks, tests, implementation prompts, and release artifacts;
- keep agent work inspectable through explicit markdown/YAML/code artifacts;
- separate approved decisions from agent assumptions and recommendations;
- preserve context across agent sessions without relying on chat history;
- integrate requirements, DDD, TDD, security, privacy, review, and release handoff into one repeatable process.

The human developer remains the owner of the software process. The agent drafts, analyzes, proposes, implements, and verifies inside structured boundaries.

## What this is not

This workflow is not:

- an autonomous software engineer;
- a one-shot app generator;
- a prompt dump;
- a replacement for human engineering judgment;
- a guarantee that generated code is correct, secure, or production-ready;
- a process where agent output automatically becomes an approved decision.

Important distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```

## Who should use this

This workflow is intended for developers who:

- already understand software development and want to use coding agents more systematically;
- want to study how agents reason, fail, recover, and improve;
- want a repeatable process for greenfield MVPs, internal tools, web applications, AI/data products, or similar systems;
- want to keep project state in files rather than in a long chat conversation;
- want to preserve traceability from goals to requirements, tests, tasks, and implementation evidence.

This workflow may feel too heavy if you only need a small one-off code snippet or a quick prototype with no review, testing, or handoff needs.

## Workflow at a glance

The workflow is organized into 14 stages.

```text
[00] Project Intake / Existing Context Review
[01] Service Goal Definition
[02] Stakeholder & Risk Framing
[03] Requirements & Acceptance Criteria
[04] Domain Modeling / DDD
[05] Architecture & Technical Contracts
[06] Data Design
[07] MVP Scope & Release Slicing
[08] Test Strategy & Validation Harness
[09] Task Breakdown
[10] Implementation Prompt Writing
[11] TDD Implementation Loop
[12] Review / Security / Release / Handoff
[13] Workflow Retrospective & Skill Improvement
```

High-level flow:

```text
Idea
→ Goal
→ Stakeholders and risks
→ Requirements and acceptance criteria
→ Domain model
→ Architecture and contracts
→ Data design
→ MVP and release slicing
→ Test strategy
→ Task breakdown
→ Implementation prompts
→ TDD implementation loop
→ Review, release, and handoff
→ Workflow retrospective and skill improvement
```

Each stage produces explicit artifacts. Those artifacts become the input for the next stage after human review and approval.

## Core concepts

### SKILL.md

A `SKILL.md` is a reusable procedure document for an agent.

It defines:

- when the skill should be used;
- which inputs the agent must read;
- which inputs are conditional;
- which files should not be read by default;
- what artifacts the agent must create or update;
- how assumptions, open questions, risks, and decision candidates must be recorded;
- what requires human approval;
- how context must be handed off to the next stage.

A skill is not merely a prompt. It is closer to a reusable operating procedure.

### Artifact-first workflow

The workflow relies on files as the source of operational truth.

Typical artifacts include:

- `01_service_goal.md`
- `03_requirements.md`
- `03_acceptance_criteria.md`
- `04_domain_model.md`
- `05_architecture_plan.md`
- `08_test_strategy.md`
- `09_task_cards.md`
- `10_implementation_prompts.md`
- `11_test_evidence_<task_id>.md`
- `12_release_readiness.md`

Chat history can help during one session, but downstream stages should depend on approved artifacts, not on previous conversation memory.

### Human approval gates

At the end of each stage, the agent must identify:

- decisions to approve;
- assumptions to confirm;
- open questions to resolve;
- risks to review;
- artifacts ready for review;
- recommended next step.

The human developer decides what becomes approved project direction.

### Context management

The workflow uses persistent context files such as:

```text
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
```

`context_packet.md` is not a complete project history. It is a concise navigation layer that tells the next stage what it needs to know and which artifacts it should read.

### Traceability

The workflow encourages traceability across the development process:

```text
Goal
→ Requirement
→ Acceptance Criteria
→ Domain Concept
→ Architecture Component
→ Data Model
→ Task
→ Test
→ Implementation Evidence
```

This helps prevent design drift, uncontrolled scope expansion, and implementation without validation.

## Recommended repository structure

A reusable workflow repository may use this structure:

```text
/
  README.md
  QUICKSTART.md
  WORKFLOW_OVERVIEW.md
  EXECUTION_GUIDE.md
  REPOSITORY_STRUCTURE.md
  GLOSSARY.md
  FAQ.md
  CONTRIBUTING.md

/docs
  /concepts
  /usage
  /reference
  /examples

/workflow_templates
  /core
  /stages
  /specializations
  /tool_wrappers

/skills
  /00_project_intake
  /01_service_goal_definition
  /02_stakeholder_risk_framing
  /03_requirements_acceptance
  /04_domain_modeling
  /05_architecture_contracts
  /06_data_design
  /07_mvp_release_slicing
  /08_test_strategy_validation
  /09_task_breakdown
  /10_implementation_prompt_writing
  /11_tdd_implementation_loop
  /12_review_release_handoff
  /13_workflow_retrospective
```

A project using this workflow may create a separate `/workflow` directory inside the target project:

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

## How to start

Read [`QUICKSTART.md`](./QUICKSTART.md) first.

The shortest path is:

```text
1. Prepare a target project folder.
2. Create /workflow and /workflow/context folders.
3. Run Stage 00 Project Intake with an agent.
4. Review the generated artifacts.
5. Approve, revise, or reject decision candidates.
6. Continue to Stage 01 Service Goal Definition.
```

Do not start by asking an agent to implement the product immediately. Start by creating approved context and artifacts.

## How stage execution works

A normal stage execution follows this pattern:

```text
1. Read the stage SKILL.md.
2. Read the required context files.
3. Read approved source artifacts from previous stages.
4. Check USER_DIRECTIVES.md if it exists.
5. Identify missing or conflicting information.
6. Produce or update stage artifacts.
7. Separate approved decisions, decision candidates, assumptions, open questions, risks, and recommendations.
8. Update context for the next stage.
9. Present a human approval gate.
```

The agent should not read every historical file by default. Each skill defines what to always read, what to read only if applicable, and what not to read unless explicitly needed.

## Split stages and stage facade pattern

Some stages may be too large for one skill. In that case, the stage can be split into internal sub-skills.

Example:

```text
/skills/04_domain_modeling/
  SKILL.md
  README.md
  artifact_contract.yml

  /04a_ubiquitous_language/
  /04b_domain_concepts_entities_values/
  /04c_aggregates_rules_lifecycle/
  /04d_events_bounded_contexts/
  /04e_domain_modeling_finalizer/
```

The parent stage remains the public interface. Internal sub-skills are implementation details.

Downstream stages must depend only on approved official stage artifacts, not on internal sub-skill folders, prompt history, or unapproved draft outputs.

## Status labels

Recommended artifact status labels:

| Status | Meaning |
|---|---|
| `Draft` | Created or revised by the agent, not yet approved. |
| `Needs Review` | Ready for human review; may contain decisions, assumptions, or open questions. |
| `Approved` | Explicitly approved by the human developer. Downstream stages may rely on it. |
| `Superseded` | Replaced by a newer artifact or decision. |
| `Rejected` | Should not be used unless explicitly reopened by the human developer. |

## Common mistakes to avoid

Avoid these patterns:

- starting implementation before goals and requirements are approved;
- treating agent suggestions as final decisions;
- using `context_packet.md` as the only source of truth;
- reading all previous files by default;
- allowing downstream stages to rely on unapproved drafts;
- skipping acceptance criteria and test strategy;
- creating implementation prompts without allowed scope, forbidden changes, required tests, and evidence requirements;
- claiming tests passed without recorded evidence;
- reviving rejected options without explicit human approval.

## Documentation map

Suggested reading order:

```text
1. README.md
2. QUICKSTART.md
3. WORKFLOW_OVERVIEW.md
4. EXECUTION_GUIDE.md
5. docs/reference/stage_00_project_intake.md
6. docs/reference/stage_01_service_goal_definition.md
7. docs/concepts/*.md as needed
```

If you are extending the workflow, read:

```text
workflow_templates/core/core_skill_template.md
workflow_templates/stages/*.md
workflow_templates/specializations/*.md
workflow_templates/tool_wrappers/*.md
```

## Contributing

Contributions should preserve the core principles:

- artifact-first execution;
- human approval gates;
- clear distinction between decisions, assumptions, and recommendations;
- stable stage boundaries;
- traceability from goals to implementation evidence;
- context-reset tolerance;
- reusable skills rather than project-specific prompts.

When adding or changing a skill, update its `README.md` and `artifact_contract.yml` so the human-facing guide, executable skill, and structured contract remain consistent.

## Author

Karpjoo Jeong  
Konkuk University & Research Institute for Human-Centric Smart Infrastructure  
Email: karpjoo@gmail.com

The affiliation is provided for identification only and does not imply institutional endorsement of this educational workflow.

## License and Free Use

This project is released under **CC0 1.0 Universal**.

You may use, copy, modify, distribute, adapt, translate, or incorporate this workflow into your own learning materials or projects for any purpose, without asking for permission.

Attribution is appreciated but not required.

See [`LICENSE`](./LICENSE) for the full CC0 1.0 Universal text.

## Educational Disclaimer

This repository is an educational and experimental workflow for studying agentic coding, coding agents, and artifact-based software development processes.

It is not a production-proven development methodology. The workflow, skills, prompts, templates, and examples should be reviewed and adapted carefully before being used in real software projects.

The materials are provided as-is, without warranty or guarantee of correctness, completeness, security, reliability, or fitness for a particular purpose.
