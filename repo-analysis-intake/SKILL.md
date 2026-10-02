---
name: repo-analysis-intake
description: Use when the user asks to analyze, inspect, review, understand, compare, continue, or diagnose a software or robotics repository but has not yet clearly defined what they want to learn or accomplish. Inspect the repository first, then guide the user through the minimum number of concise choices needed to discover the actual analysis goal.
---

# Repo Analysis Intake

## Core principle

Do not require the user to know how to formulate a repository analysis request

The repository itself should provide most of the context needed to discover useful questions

Inspect first

Ask only what cannot reasonably be inferred

Guide the user toward the problem they actually want solved

## Trigger examples

Use this skill for requests such as

- 帮我分析一下这个仓库
- 看看这个项目现在什么情况
- 我很久没看这个项目了
- 帮我看看这里有没有问题
- 分析一下这两个仓库
- 我不知道现在应该从哪里继续
- 看一下这个项目下一步应该做什么
- 我想改这个项目但还没想清楚怎么改

Do not require the user to provide a complete analysis specification before inspecting the repository

## 1 Repository first

Before asking clarification questions inspect the directly available repository evidence

Prefer checking only information relevant to understanding the current project state

Typical sources include

- README and project entry documents
- top-level directory structure
- docs and plan files
- recent commits
- active branches when relevant
- recent pull requests
- open issues when relevant
- build and dependency files
- tests
- CI configuration
- directly relevant source modules

Do not perform an exhaustive repository audit before understanding the user's goal

The purpose of this first inspection is to generate better questions

If the user provided multiple repositories, branches or versions, perform only enough initial comparison to expose the meaningful differences before asking what they care about

## 2 Generate candidate intentions

Based on actual repository evidence identify up to three likely analysis directions

Typical intent categories include

### Context recovery

Determine

- what the project currently does
- what has already been completed
- what remains unfinished
- what changed recently
- where development should resume

### Correctness review

Determine whether the current

- architecture
- algorithm
- control flow
- interfaces
- configuration
- assumptions

appear technically correct

### Failure diagnosis

Investigate

- runtime errors
- incorrect behavior
- build failures
- integration failures
- hardware/software inconsistencies

Use `systematic-debugging` when available

### Architecture or integration decision

Analyze questions such as

- how two repositories should be integrated
- whether an existing abstraction is appropriate
- whether a component should be reused or replaced
- how functionality should be migrated

### Repository quality

Inspect when relevant

- maintainability
- duplicated implementations
- CI
- tests
- documentation
- dependency organization
- version management

### Next-step decision

Determine the smallest high-value next action based on the current state

## 3 Ask one question at a time

Never start with a long questionnaire

Ask at most one decision question per response

Prefer choices derived from repository evidence rather than generic categories

A good first question has this shape

```text
我初步看下来，目前最值得继续追的是三个方向

A 恢复项目状态：现在已经做到哪、哪些还没完成
B 检查实现正确性：当前架构和关键逻辑有没有明显问题
C 决定下一步：接下来应该优先推进什么
D 我也不确定，你继续替我筛

你现在更接近哪一个
```

Always provide an uncertainty option such as

- 我也不知道
- 你替我判断
- 都不是

If the user chooses uncertainty, inspect further and propose more concrete questions

Never respond with only

```text
请详细描述你的需求
```

when repository evidence can be used to narrow the problem

## 4 Determine desired action depth

Once the primary question is approximately known, determine how far the user wants the task to proceed if this is not already clear

Use a compact choice such as

```text
你希望我做到哪一层

1 只分析并给结论
2 分析后给出推荐方案
3 分析后生成实施步骤
4 能直接修改的就继续完成
```

Infer this from the user's request whenever possible

Do not ask when the answer is already obvious

If the user asks to modify or complete the repository directly, do not stop at a recommendation merely to ask whether to continue

## 5 Ask scope only when necessary

Only ask a scope question when different scopes would materially change the result

Possible scopes include

- entire repository
- recent changes
- one branch
- one module
- one feature
- two branches
- two repositories

Do not ask the user to select scope when the repository link, conversation context, branch, error, file or previous work already identifies it

## 6 Maximum clarification budget

Default maximum

- 3 clarification turns
- 1 question per turn

Most requests should require only 1 or 2

Exceed this only when continuing without clarification would create a meaningful risk of solving the wrong problem

If the user still cannot define the goal after the clarification budget, stop asking and provide the most useful evidence-based analysis you can, clearly separating facts, interpretations and unresolved uncertainty

## 7 Analysis contract

Before deep analysis internally establish

- primary question
- relevant repository scope
- expected deliverable
- known constraints
- explicit non-goals when important

If these are sufficiently clear, stop asking questions and begin analysis

Do not require the user to formally approve an analysis contract unless a major ambiguity remains

## 8 Analysis output

Adapt the final analysis to the actual request

Prefer

### Current state

What the repository currently appears to be doing

### Evidence

Important files, code paths, commits, configurations or runtime evidence supporting the conclusions

### Findings

Only findings relevant to the user's actual question

Separate

- confirmed facts
- likely interpretations
- unresolved uncertainty

### Recommended next action

State the smallest useful continuation

If the user requested an implementation plan, invoke `mini-step-plan` when available

If the user requested execution and the modification is sufficiently clear, continue to implementation rather than stopping after analysis

## 9 Handoff rules

Use `systematic-debugging` when the primary goal becomes failure diagnosis

Use `mini-step-plan` when the primary goal becomes implementation planning

Use repository comparison when the task involves two branches, versions or repositories

Use `brainstorming` only when multiple materially different architectures remain plausible after repository inspection

Do not invoke additional processes merely because they are available

The user's current goal remains more important than the workflow

## Quality gate

Before continuing verify

- the repository was inspected before asking the user to describe it
- questions were generated from repository evidence
- no unnecessary questionnaire was used
- no already-known context was requested again
- an uncertainty option was provided when asking the user to choose
- clarification stopped once the real task became clear
- the requested action depth was inferred when possible
- the resulting analysis directly answers the discovered goal
