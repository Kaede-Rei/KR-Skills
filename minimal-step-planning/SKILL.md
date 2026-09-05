---
name: minimal-step-planning
description: Use when creating or revising 步骤.md, implementation plans, Codex execution plans, staged engineering roadmaps, or task breakdowns where scope creep, excessive steps, unnecessary experiments, premature documentation changes, or unclear acceptance criteria are risks
---

# Minimal Step Planning

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

If the request is primarily a bug, unexplained failure, or unexpected runtime behavior

**REQUIRED SUB-SKILL WHEN AVAILABLE:** Use `systematic-debugging` first and plan from evidence rather than guessed causes

If multiple materially different architectures remain plausible after reading the project

**CONDITIONAL SUB-SKILL:** Use `brainstorming`

Do not use brainstorming for bounded work with an obvious existing implementation path

If a referenced sub-skill is unavailable, perform only the minimum equivalent check needed to continue and never expand the plan merely because the dependency is missing

## Scope contract

Every plan must start with

1. one current goal
2. explicit non-goals
3. already completed baseline
4. completion criteria

Classify the task only after the context check

| Size | Main steps |
|---|---:|
| XS | 1-2 |
| S | 2-3 |
| M | 3-5 |
| L | 5-7 |
| XL | split into phases instead of one large plan |

Already completed capability belongs in the baseline section and must not count as an implementation step

## Step deletion test

For every proposed main step ask

> If this step is removed, can the current goal still be implemented and verified correctly

If yes, remove it from the main plan or move it to Later Optional

Do not create separate main steps for routine build, documentation, commit, formatting, inspection, or reporting when they can be part of the relevant implementation step

## Experiment gate

Default to zero or one hardware experiment per capability

Add another experiment only when all are true

- existing tests, static checks, simulation, recorded data, CSV or rosbag cannot establish the result
- the experiment directly proves a current completion criterion
- the experiment is not merely useful for future research or optimization

Reuse one dataset for multiple comparisons whenever technically valid

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

For important code changes, the step prompt should require `requesting-code-review` when available before final completion

Before any step is marked complete, the step prompt should require `verification-before-completion` when available

## Plan quality gate

Before returning the plan verify

- the current goal is still obvious at a glance
- no completed work is counted as unfinished work
- no step exists only because it would be nice to have
- experiments are the minimum necessary
- every step has one prompt
- prompts preserve project style
- unrelated documentation cannot be modified prematurely
- later ideas are isolated under Later Optional
- progress counts only real implementation steps

Use `STEP_TEMPLATE.md` for the required output shape
