# mini-step-plan validation scenarios

## Scenario A 小功能防膨胀

输入

在现有 ROS2 package 中增加一个可配置 CropBox 车体点云过滤开关，并给我步骤.md

应当

- 任务规模为 S 或 M
- 若判定为 S，默认使用 Compact 模板
- 2 到 5 个主步骤
- 不引入通用 filter registry
- 不自动增加 benchmark 和长稳测试
- 真机验证默认最多一次且只有在低成本证据不足时才需要
- 每一步都有 Codex Prompt

## Scenario B 已完成功能不能重复算步骤

输入

项目已经有 TaskConstraintProjector 和单元测试，现在只需要接入 Runtime

应当

- Projector 放入已完成基线
- 不把重写 Projector 作为新步骤
- 主线聚焦 Runtime 接入和最小验证

## Scenario C 文档防扩散

输入

实现一个 driver 参数修复，并生成步骤.md

应当

- 总 Prompt 禁止在当前步骤完成前主动更新 README、CHANGELOG、设计文档和其他计划
- 如果 README 不是当前交付物，不单独创建文档步骤

## Scenario D 异常问题

输入

ROS2 节点有数据但 /tf 没有消息，给我修复步骤

应当

- 先要求 systematic-debugging when available
- 不基于猜测直接给修复方案
- 根据证据生成最小步骤

## Scenario E 禁止伪分析步骤

输入

给现有驱动增加一个串口超时参数并生成计划

不应当

- Step 1 分析项目
- Step 2 理解现有架构
- Step 3 设计方案

应当

- 将必要代码阅读放入第一个真实实施步骤的前置动作
- 只有出现阻塞实现的明确技术不确定性时才创建 Investigation Step

## Scenario F 最低成本证据阶梯

输入

修改一个纯 YAML 配置默认值，已有配置加载测试可以直接覆盖该字段

应当

- 优先运行现有配置测试
- 不要求仿真或真机测试
- 不因为 更保险 自动增加硬件实验

## Scenario G 新发现问题不重写计划

输入

三步计划已完成前两步，执行第三步时发现一个不影响当前目标的日志格式问题

应当

- 日志格式问题进入 Later Optional
- 保留前两步已完成状态
- 不重写整个计划
- 第三步继续围绕当前目标执行

## Scenario H 个人执行风格保留

输入

生成供 Codex 执行的步骤.md

应当

- Total Execution Prompt 保留自然语言和 Markdown 的个人标点偏好
- 标点偏好不得破坏代码、YAML、CMake、shell、配置或项目既有注释语法
