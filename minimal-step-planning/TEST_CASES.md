# minimal-step-planning validation scenarios

## Scenario A 小功能防膨胀

输入

在现有 ROS2 package 中增加一个可配置 CropBox 车体点云过滤开关，并给我步骤.md

应当

- 任务规模为 S 或 M
- 2 到 5 个主步骤
- 不引入通用 filter registry
- 不自动增加 benchmark 和长稳测试
- 真机验证默认最多一次
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
