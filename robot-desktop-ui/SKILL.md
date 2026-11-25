---
name: robot-desktop-ui
description: 设计、实现与评审机器人桌面工作台的双主题视觉、工程数据图表、SVG、布局、状态与连接、模型及交互；采用森林绿 Calm Control 与 SerialArm 交互契约，适用于 Electron、Web UI、Qt，不用于无界面控制算法或实时控制调参
---

# Robot Desktop UI V2

Botanical Engineering：以 Kudu Calm Control 的森林绿 Light / Dark 为主题骨架，Proof 暖白窗口为视觉参考，保留 Maple CN Italic、SerialArm 与 Emil 的连续交互；Taste 用于构图、组件与资产组织，具体来源见 [sources.md](references/sources.md)

## 责任与优先级

- 当前用户要求和项目明确约束优先；工程语义与安全条件优先于视觉选择；本包 V2 视觉覆盖旧配色，SerialArm 交互契约继续沿用
- 用户要评审、分析或待审核方案时保持只读；要求实现时完成相关代码、调用路径与验证，不停在计划
- 新建或整体重构采用完整设计体系；局部任务只修改相关界面与必要调用路径，保留业务行为和已有工作
- UI 修改不授权连接、使能或移动实体机器人；数据、命令条件和停止结果使用项目真实来源

## 核心契约

1. 使用统一双主题 Token、森林绿主操作与对应 brand-ink、琥珀金辅助强调、真实 Maple Italic；Reference 紫色与 Success 绿色分开；工程对象不随品牌换色
2. 按主要任务确定页面类型、布局配方与一个主要视觉焦点；页面骨架、子页导航和四象限操作栏一致；窄窗口重排保持操作可达
3. 每个交互都有合适的 hover、pressed、focus 和 disabled；反馈范围与实际命中范围一致
4. 切换、折叠和浮层使用可打断的连续动效；不等待动画提交操作，不叠加旧正文，不重播普通数据刷新
5. 折叠保留编辑器与滚动连续性；菜单再次触发可关闭；快扫描采用按钮锚定的非阻塞状态反馈
6. 模型预加载、跨页保留、隐藏暂停、显示恢复；按真实失效条件重建，避免重复资源创建与无效绘制
7. 区分环境、会话、机器人状态，以及配置、应用、测量、验证和保存；文案直接表达动作、原因和实际结果
8. 保留键盘、焦点、状态播报及减少动态等偏好；具体无障碍符合性以目标界面实际检查为准

## 按需读取

入口不要求加载全部资料；依据本次影响面读取对应模块，跨模块问题再补相关资料

| 本次工作 | 读取 |
| --- | --- |
| 字体、密度、尺度、Token 分层 | [design-system.md](references/design-system.md) |
| Light / Dark、品牌与状态映射、主题迁移 | [theme-guidelines.md](references/theme-guidelines.md) |
| 页面视觉方向、确定性 Dealer 与方案记录 | [art-direction.md](references/art-direction.md) |
| Dashboard、Workspace、Telemetry 等布局选择 | [layout-recipes.md](references/layout-recipes.md) |
| 机器人工作站组件接口、状态和复用 | [component-library.md](references/component-library.md) |
| 视觉资产分类、来源、背景与效果预算 | [visual-assets.md](references/visual-assets.md) |
| 模型、遥测、标定、拓扑视觉焦点 | [visual-moments.md](references/visual-moments.md) |
| 图表语义、线型、图例、画布与模型颜色 | [visualization-theme.md](references/visualization-theme.md) |
| 图标盘点、SVG 规范与工程示意 | [iconography-and-svg.md](references/iconography-and-svg.md) |
| 外壳、主页面、子页、状态栏、参数或模型布局 | [layout-and-navigation.md](references/layout-and-navigation.md) |
| 按钮、折叠、菜单、选择器、提示与浮层 | [components-and-feedback.md](references/components-and-feedback.md) |
| 切换、spring、拖动、折叠跳顶、动画卡顿 | [motion-and-scroll.md](references/motion-and-scroll.md) |
| 机器人状态、操作条件、串口和连接反馈 | [robot-state-and-connection.md](references/robot-state-and-connection.md) |
| 模型加载、跨页重建、渲染性能、参考叠影 | [model-lifecycle-and-performance.md](references/model-lifecycle-and-performance.md) |
| 按钮文案、错误、状态含义、键盘与无障碍 | [copy-and-accessibility.md](references/copy-and-accessibility.md) |
| 整体方案、评审、原型比较、工具取舍、偏好沉淀 | [workflows.md](references/workflows.md) |
| 视觉截图、质量门槛、行为与性能证据 | [verification.md](references/verification.md) |
| 上游覆盖、规则冲突、设计来源与许可 | [sources.md](references/sources.md) |

## 完成工作

复用目标项目现有组件、tokens、动效与测试入口；不因本包涉及某项能力就添加库、拆分服务或重建组件框架

实现后验证实际改动的行为；报告改了什么、验证了什么，以及影响使用的未解决问题；不把源码阅读或静态截图写成已经验证过真实交互

本包只有一个技能入口；表中的模块是按需参考，不是需要另外安装的技能或平台子命令；用于维护本包的行为场景见 [TEST_CASES.md](TEST_CASES.md)

本次版本的文件变化与已执行验证见 [V2_UPGRADE_REPORT.md](V2_UPGRADE_REPORT.md)；应用实际视觉、交互和性能验收独立于技能包验证
