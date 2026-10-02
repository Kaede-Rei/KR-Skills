---
name: mini-step-plan
description: Use when creating or revising 步骤.md, implementation plans, Codex execution plans, staged engineering roadmaps, or task breakdowns where scope creep, excessive steps, unnecessary experiments, premature documentation changes, or unclear acceptance criteria are risks
---

# Mini Step Plan

## Core principle

Keep the current engineering goal more visible than the process

A valid plan uses the shortest path that can implement and verify the requested capability without expanding it into a research program, refactor, benchmark suite, or documentation campaign

## Before planning

Perform a lightweight context check using the actual project sources available

Identify

- current implementation and stable baseline
- directly relevant files, interfaces, configuration and tests
- project code style, naming, logging and comment format
- already completed work that must not become a new step
- explicit user constraints and non-goals

Reading code, understanding architecture and locating modification points are normally preparation for a real implementation step, not standalone main steps

Create a separate investigation step only when unresolved technical uncertainty blocks implementation and cannot be removed by the normal pre-edit inspection of the implementation step

If the request is primarily a bug, unexplained failure, or unexpected runtime behavior

**REQUIRED SUB-SKILL WHEN AVAILABLE:** Use `systematic-debugging` first and plan from evidence rather than guessed causes

If multiple materially different architectures remain plausible after reading the project

**CONDITIONAL SUB-SKILL:** Use `brainstorming`

Do not use brainstorming for bounded work with an obvious existing implementation path

If a referenced sub-skill is unavailable, perform only the minimum equivalent check needed to continue and never expand the plan merely because the dependency is missing

## Scope contract

Every plan must make these four things obvious

1. one current goal
2. explicit non-goals
3. already completed baseline
4. completion criteria

Classify the task only after the context check

| Size | Main steps | Default output |
|---|---:|---|
| XS | 1-2 | Compact |
| S | 2-3 | Compact |
| M | 3-5 | Full |
| L | 5-7 | Full |
| XL | split into phases instead of one large plan | Full per phase |

Already completed capability belongs in the baseline section and must not count as an implementation step

Use `COMPACT_TEMPLATE.md` for XS and S unless the user explicitly requests a full plan

Use `STEP_TEMPLATE.md` for M and L

For XL, first split the work into independently verifiable phases and plan only the current phase in detail

## Step deletion test

For every proposed main step ask

> If this step is removed, can the current goal still be implemented and verified correctly

If yes, remove it from the main plan or move it to Later Optional

Do not create separate main steps for routine build, documentation, commit, formatting, inspection, reporting, code reading, architecture understanding, or locating modification points when they can be part of the relevant implementation step

## Investigation step gate

A standalone investigation step is allowed only when all are true

- a concrete uncertainty blocks implementation
- normal inspection inside the implementation step is insufficient
- the investigation has a specific question to answer
- the investigation has an explicit exit condition
- resolving it will directly determine the next implementation action

Do not create vague steps such as

- analyze the project
- understand the code
- design the solution
- inspect the architecture

unless one of them satisfies the gate above

## Minimum evidence ladder

Use the lowest-cost evidence that can directly establish the current completion criterion

Default ladder

1. static inspection or configuration validation
2. existing unit or component tests
3. build, lint or compile checks
4. simulation, replay, recorded dataset, CSV or rosbag
5. bench or subsystem hardware test
6. full real-machine test

Do not move to a more expensive evidence level when a lower level already proves the required criterion

A higher level is justified only when the completion criterion depends on behavior that the lower level cannot establish

Reuse one valid dataset or experiment for multiple checks whenever technically sound

## Experiment gate

Default to zero or one hardware experiment per capability

Add another experiment only when all are true

- existing tests, static checks, simulation, recorded data, CSV or rosbag cannot establish the result
- the experiment directly proves a current completion criterion
- the experiment is not merely useful for future research or optimization

## Plan change budget

During execution, new findings must not automatically cause a full plan rewrite

For every newly discovered item ask

> Does this block the current goal or invalidate the current plan

If no

- move it to Later Optional
- do not change current progress counting

If yes

- record the evidence
- make the smallest incremental plan change required
- preserve completed steps
- preserve still-valid future steps
- add, split, or revise only the minimum blocked portion

A plan may grow from S to M or M to L when evidence requires it, but it must not be replaced by a new large plan merely because new optional work was discovered

## Execution prompt contract

Every main step must contain its own Codex Prompt

Every plan must also contain one shared Total Execution Prompt that is prepended to every step prompt

The Total Execution Prompt must require the executor to

- inspect directly relevant existing code before editing
- follow the project's current code style, naming, organization, error handling, logging and comment format
- reuse existing interfaces and patterns before adding abstractions
- avoid opportunistic refactoring
- avoid branches, commits and pushes unless explicitly requested
- modify only files required by the current step
- not update README, CHANGELOG, design documents, other plans, or unrelated project documentation before the current step is complete unless that document is itself an explicit deliverable
- report changed files, actual verification commands, actual results and unverified items
- never claim PASS without fresh evidence

### Personal execution style preferences

These preferences are intentionally carried into generated Codex or other-agent prompts because this skill is designed for the repository owner's own engineering workflow

- natural-language explanations, new Markdown content and agent reports must not use Chinese full stops
- natural-language paragraph endings should not add full stops, commas, semicolons, colons, exclamation marks or question marks
- these natural-language punctuation preferences must never break C++, Python, YAML, CMake, shell, configuration syntax, generated data, existing code conventions or required comment syntax

For important code changes, the step prompt should require `requesting-code-review` when available before final completion

Before any step is marked complete, the step prompt should require `verification-before-completion` when available

## Plan quality gate

Before returning the plan verify

- the current goal is obvious at a glance
- the chosen template matches task size
- no completed work is counted as unfinished work
- no step exists only because it would be nice to have
- no vague analysis or design step bypasses the Investigation Step Gate
- evidence uses the lowest sufficient level
- experiments are the minimum necessary
- every step has one prompt
- prompts preserve project style and personal execution preferences
- unrelated documentation cannot be modified prematurely
- new findings use incremental plan changes rather than unnecessary rewrites
- later ideas are isolated under Later Optional
- progress counts only real implementation steps

Use `COMPACT_TEMPLATE.md` or `STEP_TEMPLATE.md` according to the task size
