<div align="center">

# KR-Skills

个人工程工作流 Skills 集合

> 目标是让 Codex 或其他 Agent 在真实项目中更快理解任务边界，用更少步骤完成当前目标，并基于实际证据验证结果

</div>

当前仓库优先解决两个高频问题

- 不知道该怎么描述仓库分析需求时，先让 Agent 看仓库，再帮助把真正的问题想清楚
- 已经知道要做什么时，把任务压缩成尽可能少且可验证的实施步骤，再交给 Codex 或其他 Agent 执行

---

## 当前 Skills

| Skill | 解决的问题 | 典型输入 | 主要输出 | 详细介绍 |
|---|---|---|---|---|
| `repo-analysis-intake` | 仓库分析需求还很模糊 | `帮我看看这个仓库` `我很久没看了，现在什么情况` | 基于仓库证据收敛分析目标，并继续分析或分流 | [repo-analysis-intake](#repo-analysis-intake) |
| `mini-step-plan` | 目标已经明确，需要工程实施计划 | `按这个方案给我步骤.md` `给 Codex 一个执行计划` | Compact 或 Full 实施计划，每一步附带可执行 Agent Prompt | [mini-step-plan](#mini-step-plan) |

## 推荐工作流

```text
模糊的仓库需求
        ↓
repo-analysis-intake
        ↓
明确真正要解决的问题
        │
        ├── 故障与异常
        │      ↓
        │ systematic-debugging  如果可用
        │
        ├── 多种架构仍然合理
        │      ↓
        │ brainstorming  如果确有必要
        │
        └── 已经确定要实现什么
               ↓
        mini-step-plan
               ↓
          Codex / Agent 执行
               ↓
 verification-before-completion  如果可用
```

两个 Skill 不要求每次串联

目标已经明确时可以直接使用 `mini-step-plan`

只是想恢复项目状态或检查现有实现时，可以只使用 `repo-analysis-intake`

---

## repo-analysis-intake

> Inspect first, ask only what cannot reasonably be inferred

用于用户知道自己想分析仓库，但暂时不知道应该具体问什么的场景

例如

```text
帮我分析一下这个仓库
```

```text
前两个星期忙其他事情去了
现在回来不知道这个项目做到哪里了
```

```text
这两个仓库需要融合
但我暂时不知道应该先看什么
```

### 工作方式

Agent 先读取必要的仓库证据，而不是先把一份长问卷丢回给用户

通常关注

- README 和入口文档
- 顶层目录
- docs 和计划文件
- 最近 commit
- 相关 branch PR Issue
- 构建与依赖配置
- 测试和 CI
- 与当前问题直接相关的源码

然后根据真实仓库状态给出最多三个值得继续追的方向

例如

```text
A 恢复项目状态
B 检查实现正确性
C 决定下一步
D 我也不确定，你继续替我筛
```

默认规则

- 每轮最多问一个问题
- 默认最多三轮澄清
- 能从上下文推断的信息不重复询问
- 必须允许用户选择 `我也不知道` 或让 Agent 继续判断
- 一旦真实任务足够明确就停止提问并开始分析
- 用户仍然说不清时，不无限追问，直接给出当前最有价值的证据化分析

常见收敛方向

- Context recovery
- Correctness review
- Failure diagnosis
- Architecture or integration decision
- Repository quality review
- Next-step decision

如果最终任务变成实施规划，则交给 `mini-step-plan`

目录

```text
repo-analysis-intake/
├── SKILL.md
├── TEST_CASES.md
└── agents/
    └── openai.yaml
```

---

## mini-step-plan

> Use the shortest path that can implement and verify the requested capability

用于目标已经明确，需要把工作拆成尽可能少、可以真实验收的工程步骤时

### 任务规模

| Size | 主步骤 | 默认输出 |
|---|---:|---|
| XS | 1 到 2 | Compact |
| S | 2 到 3 | Compact |
| M | 3 到 5 | Full |
| L | 5 到 7 | Full |
| XL | 先拆 Phase | 每个 Phase 单独规划 |

XS 和 S 默认使用 `COMPACT_TEMPLATE.md`

M 和 L 默认使用 `STEP_TEMPLATE.md`

XL 先拆成可以独立验收的 Phase，只详细规划当前 Phase

### Step deletion test

每一个主步骤都必须问

```text
If this step is removed, can the current goal still be implemented and verified correctly
```

如果答案是可以，则删除这个步骤或放入 Later Optional

代码阅读、架构理解、定位修改点、build、格式化、文档更新、commit 和汇报不会因为流程习惯自动成为独立主步骤

### Investigation Step Gate

只有真正存在阻塞实现的技术未知项时，才允许建立独立 Investigation Step

必须同时满足

- 存在具体未知问题
- 普通实施前检查不足以解决
- 调查有明确问题
- 调查有明确退出条件
- 调查结果会直接决定下一步实现

因此 `分析项目` `理解代码` `设计方案` `研究架构` 这类模糊步骤默认不成立

### Minimum Evidence Ladder

验证优先使用最低成本且足以证明当前完成条件的证据

```text
1 static inspection / configuration validation
2 existing unit or component tests
3 build / lint / compile
4 simulation / replay / CSV / rosbag
5 bench or subsystem hardware test
6 full real-machine test
```

低成本证据已经足够时，不继续升级验证成本

真机实验默认每个 capability 为零次或一次，只有完成条件确实依赖硬件行为时才增加

### Plan change budget

执行中发现新问题时，不直接推翻整个计划

先判断

```text
Does this block the current goal or invalidate the current plan
```

不阻塞则进入 Later Optional

确实阻塞则保留已经完成和仍然有效的步骤，只对受影响部分做最小增量修改

### Agent Prompt

每个主步骤都有自己的 Codex Prompt，并共享一个 Total Execution Prompt

主要约束包括

- 修改前先读直接相关代码
- 保持项目当前代码风格和接口模式
- 优先复用已有实现
- 不顺手重构
- 不主动新建分支或 commit push
- 只修改当前步骤真正需要的文件
- 不提前扩散 README CHANGELOG 设计文档和其他计划文档修改
- 必须报告真实执行过的验证命令和真实结果
- 没有新鲜证据不能写 PASS

仓库还保留了面向个人工作流的 Agent 输出风格偏好，这些偏好会被带入生成给 Codex 或其他 Agent 的 Prompt

目录

```text
mini-step-plan/
├── SKILL.md
├── COMPACT_TEMPLATE.md
├── STEP_TEMPLATE.md
├── TEST_CASES.md
└── agents/
    └── openai.yaml
```

---

## 使用示例

### 只知道要分析仓库

```text
使用 repo-analysis-intake

https://github.com/example/project

我有一阵子没看这个项目了
现在不知道做到什么程度了
```

Agent 应先读取仓库，再帮助恢复上下文，而不是要求用户先写完整需求

### 分析两个仓库如何融合

```text
使用 repo-analysis-intake

仓库 A
https://github.com/example/a

仓库 B
https://github.com/example/b

我需要把 A 里的某个能力融合进 B
先帮我判断两个仓库当前情况和正确性
```

Agent 应先做足以暴露关键差异的比较，再决定继续 correctness review architecture decision 或 implementation planning

### 已经知道要做什么

```text
使用 mini-step-plan

当前项目已经完成 Step1 和 Step2
现在只需要完成 Runtime 接入和最小验证
给我新的步骤.md
```

已经完成的能力必须进入 baseline，不能重新计算为实施步骤

---

## 安装与使用

每个 Skill 目录都是独立单元

将需要的 Skill 目录复制或链接到当前 Agent 能读取的 Skills 目录中即可

建议完整保留以下文件

- `SKILL.md` 定义行为
- `agents/openai.yaml` 提供 Skill 元数据
- 模板文件约束计划输出结构
- `TEST_CASES.md` 用于检查重要行为是否回归

## 仓库约定

新增或修改 Skill 时优先遵循

- 一个 Skill 只解决一个清晰问题
- 能通过已有上下文推断的信息不要再次询问
- 不因为某个工具或子 Skill 存在就强制调用
- 优先真实项目证据而不是猜测
- 优先最小可验证路径
- 已完成工作不重复进入进度统计
- 非当前目标内容进入 Optional 而不是主线
- 重要行为变化同步增加 `TEST_CASES.md`
- `agents/openai.yaml` 应直接说明 Skill 的触发场景

## 仓库结构

```text
KR-Skills/
├── README.md
├── mini-step-plan/
│   ├── SKILL.md
│   ├── COMPACT_TEMPLATE.md
│   ├── STEP_TEMPLATE.md
│   ├── TEST_CASES.md
│   └── agents/
│       └── openai.yaml
└── repo-analysis-intake/
    ├── SKILL.md
    ├── TEST_CASES.md
    └── agents/
        └── openai.yaml
```

## 当前方向

这个仓库优先服务真实工程协作，而不是建设一个大而全的 Skill 集合

后续新增 Skill 时优先从反复出现的真实工作流问题中抽取，而不是为了补齐分类而增加 Skill
