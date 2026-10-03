# paper-deep-read validation scenarios

## Scenario A English-first deep reading

输入

这篇机器人论文帮我完整精读，英语多一点，用通俗英语解释，再用中文帮助我理解

应当

- 使用 DEEP 模式
- 英文承担主要技术解释
- 中文承担概念深化和易错点说明
- 重要内容使用 `Paper idea -> Plain English -> 中文深解`
- 不变成逐句中文翻译

## Scenario B 单个术语

输入

论文里的 `contact-consistent equilibrium` 到底是什么意思

应当

- 使用 TARGETED 模式
- 先解释该短语在论文语境中的含义
- 用 Plain English 解释
- 中文解释 `consistent` 与普通 `aware` 或 `related` 的差别
- 不重新总结整篇论文

## Scenario C 单个复杂句子

输入

这句话语法太复杂，看不懂，帮我拆一下

应当

- 仅在需要时使用 Sentence Clinic
- 标出主语、谓语、补语和关键修饰关系
- 给出 Plain English rewrite
- 解释语法结构如何影响技术含义
- 不把所有后续句子都机械拆句

## Scenario D 方程解释

输入

论文这里的 P = F^T v 为什么代表能量交互

应当

- 区分 power 与 force
- 说明变量和物理单位或含义
- 解释 v = 0 等边界情况
- 连接到论文方法中的能量或接触语境
- 中文部分深化物理直觉而不是只翻译公式

## Scenario E 防止把迁移想法写成论文结论

输入

这篇 PA-RL 能不能用到农业拨叶

应当

- 明确区分论文实际验证任务和农业迁移设想
- 将拨叶方案标为 Adaptable 或 Research inspiration
- 说明哪些机制来自论文，哪些是新提出的迁移
- 不写成作者已经验证了农业拨叶

## Scenario F 实验结论不过度外推

输入

作者比 baseline 高 20%，是不是说明这个方法全面更好

应当

- 检查具体 metric、task、dataset 或实验范围
- 只陈述实验实际支持的结论
- 指出该结果不能自动证明未测试维度的全面优势
- 若证据不足则明确保留不确定性

## Scenario G 原文不可用

输入

只给了一个二手博客摘要，让你解释论文 Method

应当

- 优先尝试获取原论文或更强证据
- 若仍不可用，明确说明来源限制
- 可以解释博客明确提供的内容
- 不补写博客未提供的 Method 细节

## Scenario H 复现请求分流

输入

我已经看懂这篇论文了，现在把里面的 impedance learning 接进我的机械臂项目，给我实施步骤

应当

- 将论文内容作为实现背景
- 当 `mini-step-plan` 可用时转入该 Skill
- 不继续用阅读模板膨胀成完整实施计划

## Scenario I QUICK 模式防膨胀

输入

这篇论文主要讲什么，值不值得我继续读

应当

- 使用 QUICK 模式
- 聚焦 problem、core idea、method map、main evidence 和 why it matters
- 不默认展开所有公式和实验细节
- 不为了展示能力而生成完整逐节精读

## Scenario J 技术词而非词典

输入

帮我讲这篇论文的关键词

应当

- 优先选择具有论文特定技术含义的词组
- 解释 term 在本文中的具体含义和容易误解之处
- 不输出大量普通英语单词的中英对照表
