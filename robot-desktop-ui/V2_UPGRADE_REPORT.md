# Robot Desktop UI V2 升级与验证记录

日期：2026-11-25；输入方案：`Robot-Desktop-UI-V2_视觉体系升级方案_Codex实施Prompt.md`（2026-11-22）

本次交付是 KR-Skills 内 `robot-desktop-ui` 的技能与随包资产升级；完成森林绿双主题、工程可视化、Taste 视觉组织、SVG、来源许可和验收指引；没有修改 SerialArm、AT-System-Integration、已安装技能或真实设备；仓库原有 README 修改与未跟踪技能目录作为输入保留，未提交或推送

## 修改前后清单与摘要

修改前基线：14 个技能文件 + 根 README，共 15 个文件；已在修改前读取并保存本地内容快照；修改后：29 个技能文件 + 根 README，共 30 个文件；15 个既有文件修改、15 个新增，无删除或移动

| 原有文件 | 本次处理 | 原职责与升级摘要 |
|---|---|---|
| 仓库根 `README.md` | 修改 | 替换旧橙色介绍，补 V2 主题、资产、路由和目录树；其他 Skill 保留 |
| [SKILL.md](SKILL.md) | 修改 | V2 入口、责任顺序、18 个按需参考和交付记录 |
| [TEST_CASES.md](TEST_CASES.md) | 修改 | 保留原交互场景，调整旧视觉预期，新增 16–24 共九项 V2 场景 |
| [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) | 修改 | 保留 Emil/Maple；补 Kudu/Taste MIT 全文、SerialArm 与原创资产边界 |
| [agents/openai.yaml](agents/openai.yaml) | 修改 | 更新 V2 发现说明与默认调用提示，保持自动发现方式 |
| [references/components-and-feedback.md](references/components-and-feedback.md) | 修改 | 原控件交互保留；替换品牌 hover 与选中配色 |
| [references/copy-and-accessibility.md](references/copy-and-accessibility.md) | 修改 | 保留状态/键盘语义；更新对比度路由，补内容构图 |
| [references/design-system.md](references/design-system.md) | 修改 | 颜色路由分层，原字体规则保留，新增三密度与数值尺度 |
| [references/layout-and-navigation.md](references/layout-and-navigation.md) | 修改 | 原布局保留；补配方路由、连接动作品牌映射 |
| [references/model-lifecycle-and-performance.md](references/model-lifecycle-and-performance.md) | 修改 | 原规则保留并统一句读，追加主题变化不得重建资源的规则 |
| [references/motion-and-scroll.md](references/motion-and-scroll.md) | 仅清理段末标点 | 两组 spring、单新正文、滚动测量、减少动态规则及代码均保留 |
| [references/robot-state-and-connection.md](references/robot-state-and-connection.md) | 修改 | 状态、条件、扫描生命周期完整保留；仅连接按钮品牌表达更新 |
| [references/sources.md](references/sources.md) | 修改 | 保留 Emil 19 项映射；补固定来源、Taste 迁移、资产盘点与许可 |
| [references/verification.md](references/verification.md) | 修改 | 保留原行为检查入口；新增截图、对比度、性能与分层 Finish Gate |
| [references/workflows.md](references/workflows.md) | 修改 | 接入 Art Direction / 配方；更新已被 V2 替换的视觉历史 |

新增文件

- [V2_UPGRADE_REPORT.md](V2_UPGRADE_REPORT.md)
- [assets/diagrams/coordinate-frame.svg](assets/diagrams/coordinate-frame.svg)
- [assets/icons/joint-axis.svg](assets/icons/joint-axis.svg)
- [assets/theme-previews/index.html](assets/theme-previews/index.html)
- [assets/theme-previews/preview-narrow.jpg](assets/theme-previews/preview-narrow.jpg)
- [assets/theme-previews/preview-wide.jpg](assets/theme-previews/preview-wide.jpg)
- [assets/theme/calm-control.css](assets/theme/calm-control.css)
- [references/art-direction.md](references/art-direction.md)
- [references/component-library.md](references/component-library.md)
- [references/iconography-and-svg.md](references/iconography-and-svg.md)
- [references/layout-recipes.md](references/layout-recipes.md)
- [references/theme-guidelines.md](references/theme-guidelines.md)
- [references/visual-assets.md](references/visual-assets.md)
- [references/visual-moments.md](references/visual-moments.md)
- [references/visualization-theme.md](references/visualization-theme.md)

## 保留的交互和行为契约

- 两组临界阻尼 spring 的响应尺度、速度继承、打断与结束条件；直接拖动跟手，真实遥测不补间
- hover / pressed / focus / disabled / selected、紧凑命中区、键盘和输入法组合守卫
- 单新正文进入、稳定页头/安全栏/画布、相同 key 刷新不重播
- disclosure 保留编辑器、嵌套高度变化、测量期间滚动恢复、自然 clamp 与焦点返回
- 菜单同触发器再点关闭、外部关闭、Escape、对象与锚点一致；长列表有界滚动
- 快扫描锚定非阻塞反馈、零结果语义、成功约 1600ms / 失败约 3000ms、固定 expiresAt、重建不续期
- Core / 会话 / 机器人三层状态、连接与使能分离、停放/失能/恢复的真实命令条件与事实
- 模型预加载、共享 preparation Promise、generation、跨页复用、隐藏暂停、显示恢复、场景独立快照与按所有权释放
- 数值快照、COM 与纹理复用、同帧绘制合并、原有资源失效条件及性能比较方式
- reduced-motion、减少透明度、高对比度偏好、焦点与状态播报；V2 颜色修改不改变这些行为

`motion-and-scroll.md` 仅清理段末标点，动效规则与代码保留；模型生命周期保留原规则并追加主题契约，统一清理句读；其余交互文件仅做品牌表述、引用、新增视觉规则及标点的必要更新

## 主题与 Taste 对照

完整 59 对上游 Token 及本包映射见 [主题规范](references/theme-guidelines.md)，实际值在 [CSS](assets/theme/calm-control.css)；Taste 各能力、上游文件和本包去向见 [来源迁移表](references/sources.md#能力迁移对照)

| 角色 | 旧规则 | V2 Light / Dark |
|---|---|---|
| 默认品牌 | 亮橙主操作白字 | `#173f34 / #d6e6dc`，前景 `#f8f2e5 / #15382e` |
| 页面 / Surface | Proof 衍生旧色表 | `#f5f0e6 / #101713`；`#fffdf7 / #17231e` |
| 窗口外观 | 旧 SerialArm 暖白 | 方案融合参考 `#f5f3ed` / Kudu `#101713`；非官方 Proof Token |
| 辅助强调 | 与主品牌混用 | 琥珀 `#f3b64b / #e9b553`，与警告职责分开 |
| Success | 旧状态绿 | Kudu `#1f6b4c / #68c997` |
| Reference | 青绿，易混淆正常状态 | 紫 `#6254a5 / #b5a9f0`，配短虚线与菱形 |
| Hover / active / focus / 状态层 | 旧组件定义 | 本包显式派生层，与 59 对 Kudu 原值分开维护 |
| 图表 / 模型 | 容易与界面色共用 | 独立 viz-*；XYZ、Joint Axis、COM 原工程色保留 |

Taste 的视觉方向、设计系统、确定性 Dealer、组件接口、六类资产、背景效果预算、四类工程焦点、内容构图、截图/质量门槛和性能记录均有可发现的对应模块；不迁移网站 Hero / Footer、照片数量、随机抽色、紫色禁令或排斥正文斜体的规则

## 已执行验证

| 验证 | 方法与结果 |
|---|---|
| Skill 结构 | 运行 `skill-creator/scripts/quick_validate.py` 指向本技能；结果 `Skill is valid!` |
| 原始来源与 Token | 固定 Kudu `4fb0dbd`，独立源码抽取与随包 CSS 比较；Light/Dark 各 59 项原名原值一致，共 118 值 |
| Token 关系 | 每主题 119 个变量均能解析；无缺失引用或变量环；品牌、Reference、状态和 viz 分层检查完成 |
| 对比度 | sRGB 相对亮度；文字/状态目标 4.5:1，focus/控件边界/系列按适用 3:1；每主题 67 组，共 134 组，无低于所设目标的组合 |
| SVG | 两文件 XML、viewBox、title、desc、无外部资源依赖通过；内联预览检查 currentColor 在双主题继承，图标 16/18/20/24px 可见 |
| 预览渲染 | Codex 内置浏览器实际打开离线 HTML，检查 CSS 计算值、Light Default / Dark Compact、图例线型、状态文字、XYZ、输入边界及焦点样例 |
| 窗口截图 | 1800×900 宽窗口和 680×900 窄窗口；无页面横向溢出；图表与工程区窄窗上下重排；截图生成并逐张检查 |
| 行为契约 | 比对修改前快照；动效规则与代码保留，模型生命周期和原状态/组件/布局章节均保留；中文句号与段末标点已统一清理；这属于文档契约核对 |
| 前向试用 | 独立代理仅按入口按需读取：A 为 720px Qt 四路数据遥测页提供可审核方案；B 评审主题重建、语义混色、动画延迟命令、错误资产许可；均守住只读范围并明确实际验证状态；未预先读取测试预期 |
| 引用与文本 | 入口直达 18 个 reference；检查全部本地文件链接、文本行尾空格及 `git diff --check` |

本次检查脚本在临时目录执行，没有给技能新增测试框架；两项前向试用覆盖实际决策示例，不计作执行了全部 24 项行为场景

| 对比度样本 | Light | Dark |
|---|---|---|
| brand-ink / brand-solid | 10.47:1 | 9.90:1 |
| brand-ink / brand-hover | 8.42:1 | 8.64:1 |
| brand-ink / brand-active | 7.08:1 | 7.78:1 |
| 文字与状态所检组合最低值 | 4.54:1（Info hover / Page） | 4.71:1（Error hover / Surface） |

透明状态底按 page-bg / surface / viz-canvas 分别合成；初次计算发现部分状态文字不足 4.5:1，已仅调整新增 `*-foreground` 向 text-primary 混合（Light 10% / Dark 8%），指示点与原始 Kudu 基色保留；最终 134 组结果基于该修正版本

截图： [宽窗口](assets/theme-previews/preview-wide.jpg)；[窄窗口](assets/theme-previews/preview-narrow.jpg)；可直接打开 [离线预览](assets/theme-previews/index.html)

## 未执行的应用验收

本次没有目标应用改动，因此未运行 SerialArm 实际交互、硬件、真实三维加载/跨页/隐藏/释放、GPU 性能或全部业务页面截图矩阵；这些是目标应用实施时 [verification.md](references/verification.md) 的验收项；随包预览使用系统字体 fallback，不分发 Maple 字体文件，不能据此认定目标应用字体资源或连字开关已验证

固定 XYZ/COM 等工程色按语义保留，细小工程对象在浅底的识别仍需轮廓/标签和真实模型验证；disabled、未使用的上游文字角色、其他透明叠层及目标项目 override 不在上述 134 配对结论内；应用的整体 WCAG 符合性需实际组件与操作证据，不由本包纯色计算替代

Proof 原始导出及官方 SVG 未提供并核实，已按方案参考值记录；Taste 照片/Shader/第三方图标没有随包复制；固定来源与完整 MIT 声明见 [sources.md](references/sources.md) 和 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)

## 使用与分发

完整 `robot-desktop-ui/` 为可安装单元，包含入口、agents、references、资产和许可；复制或链接到目标 Agent 技能目录即可；主题 CSS 作为目标项目 Token 层参考，不能只复制 CSS 就宣称应用 V2 升级完成

本次分发包为 `robot-desktop-ui-v2-2026-11-25.zip`，顶层是 `robot-desktop-ui/`；包内容与当前目录逐文件核对，不含临时源码下载、私人资料或目标应用资源
