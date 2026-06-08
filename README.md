# Agentic Coding Workflow for Learning Agents

An educational, artifact-first workflow for students and self-learners who want to study how coding agents behave inside a structured software-development process.

This repository is **not** presented as a production-proven software development methodology. It is a learning workflow for observing, practicing, and evaluating how LLM-based coding agents such as Claude Code, Codex, Antigravity, and similar tools work when they are given structured tasks, explicit artifacts, review gates, and context handoff rules.

```text
Agentic Coding Study = structured workflow + reusable skills + observable artifacts + human review + agent failure analysis
```

## Project status

This workflow is currently best understood as an **educational and experimental framework**.

Use it to:

- learn how agents read instructions and project context;
- observe where agents make assumptions;
- practice breaking software work into staged artifacts;
- study how context, requirements, tests, and implementation prompts affect agent behavior;
- compare agent outputs across tools and sessions;
- improve your own skill at directing, reviewing, and correcting coding agents.

Do **not** treat this repository as a fully validated process for production software delivery. The workflow may still need simplification, testing, examples, and repeated use across real projects before it can be recommended as a mature development process.

## What this is

Agentic Coding Workflow for Learning Agents is a staged learning workflow inspired by software development lifecycle practices.

It helps learners study questions such as:

- How does an agent respond when requirements are vague?
- How does an agent use previous artifacts as context?
- When does an agent silently turn assumptions into decisions?
- How can human review gates reduce uncontrolled agent behavior?
- How do acceptance criteria and test plans change implementation quality?
- How does context reset affect agent performance?
- How can agent outputs be made inspectable and traceable?

The workflow does this by asking the agent to work through explicit stages and produce concrete markdown/YAML/code artifacts instead of relying only on chat history.

## What this is not

This workflow is not:

- an autonomous software engineer;
- a one-shot app generator;
- a production-certified development process;
- a guarantee that generated code is correct, secure, or maintainable;
- a replacement for software engineering education;
- a replacement for human review, testing, or judgment;
- a prompt dump;
- a claim that agents can independently manage a complete software project.

Important distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
Educational exercise ≠ production validation
```

## Who should use this

This workflow is intended for:

- students learning how coding agents work;
- educators designing exercises around agentic coding;
- self-learners studying prompt design, context management, and AI-assisted development;
- junior developers who want to practice structured software thinking with an agent;
- researchers or practitioners observing agent failure patterns;
- experienced developers who want to experiment with a more inspectable agent workflow before applying it to real projects.

This workflow may feel too heavy if you only want a quick code snippet. It may also be too immature if you need a proven process for production delivery.

## Learning goals

By using this workflow, a learner should practice:

1. turning vague ideas into explicit goals and requirements;
2. distinguishing agent suggestions from approved decisions;
3. recording assumptions and open questions instead of hiding them;
4. using artifacts as context across agent sessions;
5. designing acceptance criteria and validation steps before implementation;
6. observing how agents behave under clear versus unclear instructions;
7. reviewing and correcting agent output;
8. collecting evidence about what the agent did well or poorly;
9. improving reusable `SKILL.md` files based on observed failures.

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

High-level learning flow:

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
→ Review and handoff
→ Agent behavior retrospective and skill improvement
```

Each stage produces visible artifacts. Those artifacts make the agent's work easier to inspect, compare, challenge, and improve.

## Core concepts

### SKILL.md

A `SKILL.md` is a reusable procedure document for an agent.

It defines:

- when the skill should be used;
- which inputs the agent should read;
- which inputs are conditional;
- which files should not be read by default;
- what artifacts the agent should create or update;
- how assumptions, open questions, risks, and decision candidates should be recorded;
- what requires human review;
- how context should be handed off to the next stage.

A skill is not merely a prompt. In this repository, it is closer to a learning protocol for observing and guiding agent behavior.

### Artifact-first learning

The workflow relies on files as the observable record of agent work.

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
- `13_agent_failure_patterns.md`

Chat history can help during one session, but learning and review should depend on artifacts that can be inspected later.

### Human review gates

At the end of each stage, the agent should identify:

- decisions to review;
- assumptions to confirm;
- open questions to resolve;
- risks to discuss;
- artifacts ready for review;
- recommended next step.

For learning purposes, the review gate is not just a project management step. It is where the student studies the agent's reasoning, omissions, hidden assumptions, and failure modes.

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

This helps students study an important agentic coding problem: agents often lose, distort, or over-compress context when a conversation becomes long.

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
→ Retrospective Lesson
```

For students, traceability is useful because it exposes whether the agent's implementation is actually connected to earlier requirements and tests.

## Recommended repository structure

A reusable learning repository may use this structure:

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

A learner applying this workflow to a practice project may create a separate `/workflow` directory inside that practice project:

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
5. Mark agent assumptions, missing information, and decision candidates.
6. Continue to Stage 01 Service Goal Definition.
7. Keep notes about what the agent did well or poorly.
```

Do not start by asking an agent to implement the whole product immediately. Start by observing how it handles context, goals, requirements, and review.

## Suggested student exercises

Try the workflow with small projects such as:

- a personal task tracker;
- a simple habit logging app;
- a study note organizer;
- a flashcard generator;
- a small internal dashboard mockup;
- a toy API with authentication and validation;
- a simple AI-assisted document summarizer.

For each exercise, compare:

```text
Run A: vague prompt directly to implementation
Run B: structured workflow with artifacts and review gates
```

Then ask:

- Which run produced clearer requirements?
- Which run made assumptions more visible?
- Which run produced better tests?
- Which run was easier to review?
- Where did the agent still fail?

## How stage execution works

A normal stage execution follows this pattern:

```text
1. Read the stage SKILL.md.
2. Read the required context files.
3. Read approved or current source artifacts from previous stages.
4. Check USER_DIRECTIVES.md if it exists.
5. Identify missing or conflicting information.
6. Produce or update stage artifacts.
7. Separate decision candidates, assumptions, open questions, risks, and recommendations.
8. Update context for the next stage.
9. Present a human review gate.
10. Record learning observations about the agent's behavior.
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

For learning purposes, split stages are useful because they make it easier to study agent behavior in smaller, more focused tasks.

## Status labels

Recommended artifact status labels:

| Status | Meaning |
|---|---|
| `Draft` | Created or revised by the agent, not yet reviewed. |
| `Needs Review` | Ready for human review; may contain decisions, assumptions, or open questions. |
| `Approved` | Explicitly approved by the human reviewer for the purpose of the exercise. |
| `Superseded` | Replaced by a newer artifact or decision. |
| `Rejected` | Should not be used unless explicitly reopened by the human reviewer. |

In a learning setting, `Approved` means “approved for this exercise,” not “production certified.”

## Common mistakes to avoid

Avoid these patterns:

- presenting this workflow as production-proven before it has been validated;
- starting implementation before goals and requirements are reviewed;
- treating agent suggestions as final decisions;
- using `context_packet.md` as the only source of truth;
- reading all previous files by default;
- allowing later stages to rely on unreviewed drafts;
- skipping acceptance criteria and test strategy;
- creating implementation prompts without allowed scope, forbidden changes, required tests, and evidence requirements;
- claiming tests passed without recorded evidence;
- ignoring agent failure patterns after the exercise is complete.

## Documentation map

Suggested reading order:

```text
1. README.md
2. QUICKSTART.md
3. CONCEPT.md
4. WORKFLOW_OVERVIEW.md
5. EXECUTION_GUIDE.md, if available
6. docs/examples/*, if available
7. docs/reference/*, if available
```

If you are studying how the workflow itself is designed, also read:

```text
workflow_templates/core/core_skill_template.md
workflow_templates/stages/*.md
workflow_templates/specializations/*.md
workflow_templates/tool_wrappers/*.md
```

## Contributing

Contributions are welcome, especially if they improve the workflow as a learning tool.

Useful contributions include:

- clearer student exercises;
- simpler examples;
- agent failure pattern reports;
- improved `SKILL.md` instructions;
- comparison results across agent tools;
- better context reset practices;
- better review checklists;
- translations or classroom-friendly explanations.

When adding or changing a skill, update its `README.md` and `artifact_contract.yml` so the human-facing guide, executable skill, and structured contract remain consistent.

## License

Add your chosen license here before public distribution.
