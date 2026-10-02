# repo-analysis-intake validation scenarios

## Scenario A 用户只给仓库链接

输入

帮我分析一下这个仓库 https://github.com/example/project

应当

- 先检查仓库 README、目录和少量直接相关证据
- 不先要求用户详细描述需求
- 根据仓库实际情况给出最多三个可能的分析方向
- 提供 我也不知道 之类的不确定选项

## Scenario B 很久没看项目

输入

前两个星期我忙其他去了，现在回来不知道这个项目是什么情况了

应当

- 将 Context recovery 作为高优先方向
- 检查近期提交、计划文档、当前实现和未完成线索
- 帮用户恢复 已完成 / 未完成 / 最近变化 / 下一步
- 不要求用户先回忆所有历史工作

## Scenario C 用户自己也不知道想问什么

输入

我就是感觉这里可能有问题，但我也不知道该分析什么

应当

- 进一步检查仓库证据
- 提出更具体的候选问题
- 不把需求定义工作全部推回给用户
- 最多一问一轮

## Scenario D 已明确是 Bug

输入

节点启动后有数据，但 tf 一直没有消息，帮我看看仓库

应当

- 不再询问分析类型
- 直接进入 failure diagnosis
- systematic-debugging 可用时交给它基于证据处理

## Scenario E 用户要求直接改

输入

分析这个仓库，能修的直接修好给我

应当

- action depth 直接推断为 4
- 不再询问 只分析还是修改
- 在问题和修改范围足够明确后继续执行

## Scenario F 两个仓库融合

输入

把仓库 A 的 CharuCo 标定算法融合到仓库 B 的 APP，先分析两个仓库

应当

- 初步比较两边与标定相关的实现、接口和依赖
- Architecture or integration decision 为主线
- 不进行与融合无关的完整质量审计
- 如果后续需要实施步骤，交给 mini-step-plan

## Scenario G 范围已明确不能重复问

输入

只分析 feature/arm-system 分支里的 tomato_picker 模块

应当

- 不再询问整个仓库还是某个模块
- 直接以给定分支和模块为 scope

## Scenario H 三轮后仍模糊

输入

用户连续表示不知道具体目标

应当

- 最多默认三轮澄清
- 之后停止追问
- 基于证据给出最有价值的分析
- 区分事实、推断和未知项
