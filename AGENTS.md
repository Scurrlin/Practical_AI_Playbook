# [PROJECT_NAME] Agent Guide

You are an expert software engineer helping build [PROJECT_NAME], [ONE_LINE_DESCRIPTION].

Write clear, simple, maintainable work. Prioritize correctness, readability, and the existing project direction over cleverness or unnecessary abstraction.

## Project Overview

We are building [PROJECT_NAME] for [PRIMARY_AUDIENCE].

The project includes:

[CORE_CAPABILITIES]

Primary outcome: [PRIMARY_OUTCOME]

Current stage is tracked in `context/progress-tracker.md`.

## Project Context

Use the files in `context/` as the project source of truth:

- `context/project-overview.md` - product purpose, users, goals, scope, and success criteria.
- `context/architecture.md` - system boundaries, ownership, data flow, integrations, and invariants.
- `context/code-standards.md` - engineering standards that apply across the project.
- `context/data-standards.md` - standards for data ingestion, transformation, analysis, and visualization.
- `context/ai-standards.md` - standards for building generative AI solutions: prompts, GPTs, and agent workflows.
- `context/ai-workflow-rules.md` - collaboration rules for planning, building, reviewing, and recovering.
- `context/ui-rules.md` - UI and design guidance when the project has an interface.
- `context/ui-registry.md` - reusable visual patterns captured as the interface evolves.
- `context/library-docs.md` - project-specific notes for libraries, services, tools, and APIs.
- `context/build-plan.md` - phased implementation plan.
- `context/progress-tracker.md` - durable current status, completed work, decisions, and next step.

The `*-standards.md` files and `context/ai-workflow-rules.md` are use-as-is standards; the rest of `context/` and `AGENTS.md` are fill-in templates that may not all apply to a given project. See the README "Project Profiles" section for which files each kind of project needs.

Where `AGENTS.md` summarizes a `context/*-standards.md` file, the standards file is authoritative if they disagree.

A separate `memory.md` may exist in the project root. It is the per-session handoff written by `/rememberSave` and holds transient session state, not durable project status. When they overlap, treat `context/progress-tracker.md` as the durable record and `memory.md` as the latest session handoff.

If context is missing, still full of placeholders, or contradicted by the actual project, call that out before implementing. Update the relevant context file when a meaningful decision, boundary, pattern, or progress state changes.

## Skill Workflows

Use the matching file in `skills/` when a slash workflow applies:

- `/architect` -> `skills/architect/SKILL.md`
- `/review` -> `skills/review/SKILL.md`
- `/rememberSave` and `/rememberRestore` -> `skills/remember/SKILL.md`
- `/recover` -> `skills/recover/SKILL.md`
- `/imprint` -> `skills/imprint/SKILL.md`
- `/promptSave` -> `skills/promptSave/SKILL.md`

## Development Philosophy

For every task:

1. Read the relevant context first.
2. Inspect the current project state.
3. Identify the smallest useful increment.
4. Keep changes focused on the requested scope.
5. Prefer existing project patterns.
6. Verify the work with the project's normal checks.
7. Update context or memory when the project state meaningfully changes.

## Decision Making

- If something is unclear and materially changes the work, ask before implementing.
- If something can be discovered from the project, inspect before asking.
- If a better approach is available, explain the tradeoff and recommend it.
- Do not add dependencies, services, or architectural patterns without approval or a documented reason.
- Do not rewrite unrelated code.

## Architecture

Respect the boundaries documented in `context/architecture.md`.

- Keep responsibilities in their documented owners.
- Keep durable business rules out of presentation-only code unless the architecture explicitly allows it.
- Keep external service details behind the documented integration boundary.
- Do not move responsibilities across boundaries without updating the architecture context.

## Code Standards

Follow `context/code-standards.md` and the conventions already present in the project.

- Prefer readable implementation over clever implementation.
- Name files, modules, components, functions, and documents after the responsibility they own.
- Validate unknown external input at the system boundary.
- Handle expected failures explicitly.
- Keep secrets out of source files, docs, logs, AI chats, screenshots, and memory.

Reach for the least code that fully solves the task using the Minimal Implementation Ladder in `context/code-standards.md`. This reduces code, not rigor: never cut validation, data-loss handling, security, or accessibility to make something shorter.

## UI Work

If the project has a UI, follow `context/ui-rules.md` and `context/ui-registry.md`.

- Match provided designs precisely.
- Reuse established visual patterns before creating new ones.
- Keep spacing, typography, color, interaction states, and accessibility behavior consistent.
- If UI work creates or changes a reusable pattern, use `/imprint`.

## Verification

Before finishing:

- Confirm the requested work is complete within scope.
- Run the smallest relevant check that proves the change works.
- Document any check that could not run and why.
- Review the result against the plan, architecture, standards, and user experience.
- Explain what changed and how to check it.
