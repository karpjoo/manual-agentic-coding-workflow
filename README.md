# MACOW: Manual Agentic Coding Workflow

**MACOW** stands for **Manual Agentic Coding Workflow**.

MACOW is an educational and experimental workflow for students, self-learners, and instructors who want to study how coding agents behave inside a structured software-development-like process.

This repository is not presented as a production-proven development methodology. It is a learning framework for observing, practicing, and improving the way humans interact with LLM-based coding agents such as Claude Code, Codex, Antigravity, or similar tools.

```text
MACOW = Manual Agentic Coding Workflow
      = structured learning workflow + reusable skills + explicit artifacts + human review gates
```

## Why the name MACOW?

The name **MACOW** was chosen because it is short, memorable, and directly expands to the core idea of the project:

```text
Manual     → the human remains in control
Agentic    → the workflow studies and uses coding agents
Coding     → the exercises are grounded in software development tasks
Workflow   → the process is staged, repeatable, and artifact-based
```

In this repository, **MACOW** always means **Manual Agentic Coding Workflow**.

The word “manual” is important. MACOW does not assume that an agent should autonomously own the software process. Instead, it uses a manual, inspectable, stage-by-stage structure so learners can observe how agents interpret context, make assumptions, produce artifacts, and recover from mistakes.

## Current status

MACOW is currently an **educational and experimental workflow**.

It is suitable for:

- studying agentic coding behavior;
- practicing structured prompting and artifact-based collaboration;
- observing agent failure patterns;
- learning how context, assumptions, requirements, tests, and review gates affect agent output;
- comparing vague prompting with staged workflow execution.

It is not yet validated as:

- a production-ready software development methodology;
- a replacement for professional engineering judgment;
- a guarantee that generated code or design artifacts are correct, secure, or complete.

Use MACOW as a learning environment first. If you adapt it for real software projects, review and test all outputs carefully.

## What this is

MACOW is a staged workflow for learning how to use coding agents in a controlled and inspectable way.

It helps learners practice how to:

- turn an initial idea into goals, requirements, domain models, architecture notes, tasks, tests, prompts, and review artifacts;
- ask agents to produce explicit markdown/YAML/code artifacts instead of vague chat summaries;
- distinguish agent proposals from approved human decisions;
- keep project state in files instead of relying only on chat history;
- observe how agents handle missing information, conflicting instructions, and context resets;
- connect requirements, DDD concepts, TDD ideas, security/privacy concerns, and review evidence across a staged process.

The learner remains the owner of the exercise. The agent drafts, analyzes, proposes, implements, and verifies inside structured boundaries.

## What this is not

MACOW is not:

- an autonomous software engineer;
- a one-shot app generator;
- a prompt dump;
- a production-certified SDLC framework;
- a guarantee that generated code is correct, secure, or deployable;
- a process where agent output automatically becomes an approved decision.

Important distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```

These distinctions are central to the learning purpose of MACOW.

## Who should use this

MACOW is intended for:

- students learning how coding agents behave;
- self-learners experimenting with agentic coding workflows;
- instructors designing exercises around LLM-based development tools;
- researchers or educators interested in agent failure patterns, context management, and human-agent collaboration;
- developers who want to study agentic coding in a low-risk educational setting before applying similar ideas to real projects.

MACOW may feel too heavy if you only want a quick answer, a short code snippet, or a one-time prototype.

## Learning goals

MACOW is designed to help learners ask questions such as:

- How does an agent interpret incomplete requirements?
- When does an agent silently turn assumptions into decisions?
- How does artifact-based context compare with long chat history?
- What happens when the same stage is rerun after human feedback?
- How does requiring acceptance criteria change implementation quality?
- How does test-first or test-aware prompting affect coding behavior?
- What kinds of review gates reduce agent drift?
- Where does human judgment remain essential?

A useful MACOW exercise does not only ask, “Did the agent build something?” It also asks, “What did the agent assume, miss, overgenerate, forget, or improve?”

## Workflow at a glance

MACOW is organized into 14 stages.

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

Each stage produces explicit artifacts. Those artifacts become learning evidence and, after human review, input for the next stage.

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
- what requires human review;
- how context must be handed off to the next stage.

A skill is not merely a prompt. In MACOW, a skill is closer to a reusable learning procedure for observing agent behavior.

### Artifact-first learning

MACOW relies on files as the source of operational context.

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

Chat history can help during one session, but downstream stages should depend on reviewed artifacts, not on previous conversation memory.

### Human review gates

At the end of each stage, the agent should identify:

- decisions to approve;
- assumptions to confirm;
- open questions to resolve;
- risks to review;
- artifacts ready for review;
- recommended next step.

For MACOW learning exercises, a review gate is not only a project-control mechanism. It is also a learning checkpoint where students can inspect how the agent reasoned and where it may have gone wrong.

### Context management

MACOW uses persistent context files such as:

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

This makes MACOW useful for studying what happens when an agent session is reset and restarted from files only.

### Traceability

MACOW encourages traceability across the learning exercise:

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

Traceability helps learners see whether an agent preserves intent across stages or drifts away from the approved context.

## Recommended repository structure

A reusable MACOW repository may use this structure:

```text
/
  README.md
  QUICKSTART.md
  CONCEPT.md
  WORKFLOW_OVERVIEW.md
  EXECUTION_GUIDE.md
  REPOSITORY_STRUCTURE.md
  GLOSSARY.md
  FAQ.md
  CONTRIBUTING.md
  LICENSE

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

A learning project using MACOW may create a separate `/workflow` directory inside the target project:

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

The shortest learning path is:

```text
1. Prepare a small practice project idea.
2. Create /workflow and /workflow/context folders.
3. Run Stage 00 Project Intake with an agent.
4. Review the generated artifacts.
5. Mark decision candidates, assumptions, and open questions.
6. Continue to Stage 01 Service Goal Definition.
7. Keep notes about where the agent performed well or failed.
```

Do not start by asking an agent to implement the product immediately. Start by creating context and artifacts that can be inspected.

## How stage execution works

A normal MACOW stage execution follows this pattern:

```text
1. Read the stage SKILL.md.
2. Read the required context files.
3. Read reviewed source artifacts from previous stages.
4. Check USER_DIRECTIVES.md if it exists.
5. Identify missing or conflicting information.
6. Produce or update stage artifacts.
7. Separate approved decisions, decision candidates, assumptions, open questions, risks, and recommendations.
8. Update context for the next stage.
9. Present a human review gate.
10. Record what the learner observed about the agent's behavior.
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

Downstream stages must depend only on reviewed official stage artifacts, not on internal sub-skill folders, prompt history, or unreviewed draft outputs.

## Status labels

Recommended artifact status labels:

| Status | Meaning in MACOW |
|---|---|
| `Draft` | Created or revised by the agent, not yet reviewed. |
| `Needs Review` | Ready for human review; may contain decisions, assumptions, or open questions. |
| `Approved` | Approved for the current learning exercise. This does not mean production-certified. |
| `Superseded` | Replaced by a newer artifact or decision. |
| `Rejected` | Should not be used unless explicitly reopened by the learner or instructor. |

## Suggested learning exercises

MACOW can be used for exercises such as:

- compare a vague one-shot prompt with a staged MACOW execution;
- run the same stage twice with different `USER_DIRECTIVES.md` files and compare outputs;
- ask the agent to proceed with incomplete inputs and inspect its assumptions;
- intentionally introduce a conflict between artifacts and observe how the agent reports it;
- clear the agent context and restart from `context_packet.md` and approved artifacts;
- inspect whether implementation tasks remain traceable to requirements and tests;
- run Stage 13 to create a retrospective of agent strengths, weaknesses, and failure patterns.

## Common mistakes to avoid

Avoid these patterns:

- treating MACOW as a production-certified development process;
- starting implementation before goals and requirements are reviewed;
- treating agent suggestions as final decisions;
- using `context_packet.md` as the only source of truth;
- reading all previous files by default;
- allowing downstream stages to rely on unreviewed drafts;
- skipping acceptance criteria and test strategy;
- creating implementation prompts without allowed scope, forbidden changes, required tests, and evidence requirements;
- claiming tests passed without recorded evidence;
- reviving rejected options without explicit human approval;
- focusing only on whether the agent produced code instead of studying how and why it produced that code.

## Documentation map

Suggested reading order:

```text
1. README.md
2. QUICKSTART.md
3. CONCEPT.md
4. WORKFLOW_OVERVIEW.md
5. EXECUTION_GUIDE.md
6. docs/reference/stage_00_project_intake.md
7. docs/reference/stage_01_service_goal_definition.md
8. docs/concepts/*.md as needed
```

If you are extending MACOW, read:

```text
workflow_templates/core/core_skill_template.md
workflow_templates/stages/*.md
workflow_templates/specializations/*.md
workflow_templates/tool_wrappers/*.md
```

## Contributing

Contributions should preserve the core learning principles:

- artifact-first execution;
- human review gates;
- clear distinction between decisions, assumptions, and recommendations;
- stable stage boundaries;
- traceability from goals to implementation evidence;
- context-reset tolerance;
- reusable skills rather than project-specific prompts;
- explicit recording of agent failure patterns and learning observations.

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
