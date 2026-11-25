# 双主题与状态 Token

采用 Kudu Calm Control 最后生效定义；完整可复用 CSS 为 [calm-control.css](../assets/theme/calm-control.css)，核验版本、范围和许可见 [sources.md](sources.md) 与 [第三方声明](../THIRD_PARTY_NOTICES.md)

## 原始色彩骨架

下表只列上游原始变量；`card-bg` 在本包映射为 `surface`，`titlebar-bg` 保留原值；上游根为 Dark、`.light` 覆盖为 Light，本包仅将默认入口改为 Light 与 `data-theme` 选择器，不混入更早的旧主题定义

| Kudu Token | Light | Dark |
|---|---|---|
| `page-bg` | `#f5f0e6` | `#101713` |
| `sidebar-bg` | `#f5f0e6` | `#101713` |
| `titlebar-bg` | `#f5f0e6` | `#101713` |
| `card-bg` | `#fffdf7` | `#17231e` |
| `bg-subtle` | `rgba(23, 63, 52, 0.035)` | `rgba(237, 244, 239, 0.035)` |
| `bg-subtle-2` | `rgba(23, 63, 52, 0.055)` | `rgba(237, 244, 239, 0.055)` |
| `bg-hover` | `rgba(23, 63, 52, 0.07)` | `rgba(237, 244, 239, 0.07)` |
| `bg-hover-2` | `rgba(23, 63, 52, 0.1)` | `rgba(237, 244, 239, 0.09)` |
| `bg-active` | `rgba(23, 63, 52, 0.13)` | `rgba(237, 244, 239, 0.12)` |
| `bg-elevated` | `#eee7d9` | `#1d2c25` |
| `bg-overlay` | `#e4dccd` | `#25372f` |
| `flyout-bg` | `rgba(255, 253, 247, 0.98)` | `rgba(18, 29, 24, 0.97)` |
| `toast-bg` | `rgba(255, 253, 247, 0.97)` | `rgba(23, 35, 30, 0.96)` |
| `text-primary` | `#17372f` | `#edf3ef` |
| `text-secondary` | `#365249` | `#c8d4cd` |
| `text-muted` | `#3f5a51` | `#a9bbb1` |
| `text-dim` | `#4b655c` | `#91a59b` |
| `text-faint` | `#526b62` | `#82978d` |
| `text-ghost` | `rgba(23, 55, 47, 0.66)` | `rgba(237, 243, 239, 0.62)` |
| `text-ghost-2` | `rgba(23, 55, 47, 0.76)` | `rgba(237, 243, 239, 0.72)` |
| `text-on-accent` | `#293219` | `#26331f` |
| `toast-text` | `#17372f` | `#edf3ef` |
| `brand-solid` | `#173f34` | `#d6e6dc` |
| `brand-ink` | `#f8f2e5` | `#15382e` |
| `brand-surface` | `rgba(23, 63, 52, 0.09)` | `rgba(101, 164, 135, 0.14)` |
| `brand-border` | `rgba(23, 63, 52, 0.18)` | `rgba(132, 190, 163, 0.22)` |
| `nav-active-bg` | `#173f34` | `#274b3f` |
| `nav-active-fg` | `#f8f2e5` | `#f3f7f4` |
| `nav-inactive-fg` | `#557067` | `#c4d2ca` |
| `nav-icon-fg` | `#6c817a` | `#9fb2a8` |
| `nav-section-fg` | `#5a7169` | `#a9bbb1` |
| `border-subtle` | `rgba(23, 63, 52, 0.065)` | `rgba(225, 239, 230, 0.055)` |
| `border-default` | `rgba(23, 63, 52, 0.1)` | `rgba(225, 239, 230, 0.08)` |
| `border-medium` | `rgba(23, 63, 52, 0.14)` | `rgba(225, 239, 230, 0.11)` |
| `border-strong` | `rgba(23, 63, 52, 0.2)` | `rgba(225, 239, 230, 0.16)` |
| `border-stronger` | `rgba(23, 63, 52, 0.28)` | `rgba(225, 239, 230, 0.22)` |
| `accent` | `#f3b64b` | `#e9b553` |
| `accent-hover` | `#e7a938` | `#f2c46d` |
| `accent-muted-bg` | `rgba(243, 182, 75, 0.16)` | `rgba(233, 181, 83, 0.11)` |
| `accent-muted-border` | `rgba(197, 135, 31, 0.28)` | `rgba(233, 181, 83, 0.24)` |
| `success` | `#1f6b4c` | `#68c997` |
| `warning` | `#875506` | `#e9b553` |
| `danger` | `#b33e37` | `#ee766c` |
| `info` | `#356f8d` | `#76a9d5` |
| `gauge-track` | `rgba(23, 63, 52, 0.09)` | `rgba(225, 239, 230, 0.08)` |
| `grid-line` | `rgba(23, 63, 52, 0.065)` | `rgba(225, 239, 230, 0.055)` |
| `glass-bg` | `#fffdf7` | `#17231e` |
| `glass-border` | `rgba(23, 63, 52, 0.1)` | `rgba(225, 239, 230, 0.09)` |
| `glass-inset` | `rgba(255, 255, 255, 0.72)` | `rgba(255, 255, 255, 0.025)` |
| `glass-shadow` | `0 1px 2px rgba(41, 50, 25, 0.035), 0 10px 30px rgba(41, 50, 25, 0.045)` | `0 1px 2px rgba(0, 0, 0, 0.16), 0 10px 28px rgba(0, 0, 0, 0.09)` |
| `glass-hover-bg` | `#fff` | `#1b2923` |
| `glass-hover-border` | `rgba(23, 63, 52, 0.2)` | `rgba(225, 239, 230, 0.17)` |
| `glass-hover-inset` | `rgba(255, 255, 255, 0.95)` | `rgba(255, 255, 255, 0.04)` |
| `glass-hover-shadow` | `0 2px 5px rgba(41, 50, 25, 0.06), 0 16px 34px rgba(41, 50, 25, 0.075)` | `0 2px 5px rgba(0, 0, 0, 0.18), 0 14px 34px rgba(0, 0, 0, 0.12)` |
| `scrollbar-thumb` | `rgba(23, 63, 52, 0.14)` | `rgba(225, 239, 230, 0.12)` |
| `scrollbar-thumb-hover` | `rgba(23, 63, 52, 0.26)` | `rgba(225, 239, 230, 0.22)` |
| `selection-bg` | `rgba(243, 182, 75, 0.34)` | `rgba(233, 181, 83, 0.28)` |
| `glow-amber` | `transparent` | `transparent` |
| `glow-blue` | `transparent` | `transparent` |

## V2 明确新增的映射

下列为本包设计决定，不标作 Kudu 或 Codex 官方值

| Token | Light | Dark | 用法 |
|---|---|---|---|
| `surface` | `var(--card-bg)` | 同左 | 常规内容面板 |
| `window-chrome` | `#f5f3ed` | `#101713` | Light 来自方案的 Proof 暖白融合参考，Dark 沿用 Kudu titlebar |
| `brand-hover` | #294d42 | #c7d8ce | brand-solid 向 brand-ink 混合 8% |
| `brand-active` | #36584d | #bbcec4 | 同上混合 14% |
| `focus-ring` | `brand-solid` | `brand-solid` | 2px outline，offset 3px；不是上游琥珀 outline 的原值 |
| `control-border` | `text-muted` | `text-muted` | 需要 3:1 边界识别的输入控件；弱装饰分隔不承担此责任 |
| `overlay-scrim` | `rgba(23,55,47,.24)` | `rgba(0,0,0,.48)` | 模态遮罩，区别于实体 bg-overlay 表面 |
| `reference` | `#6254a5` | `#b5a9f0` | 参考数据，非设备状态 |
| `error` | `var(--danger)` | 同左 | 对齐 Error 命名；上游名称为 danger |

主操作采用 brand-solid / brand-ink，包括 hover 与 pressed；森林绿替代旧橙色默认主品牌；琥珀金是辅助强调，配 text-on-accent；Dark accent 和 warning 同值，必须用作用域、图标及文字区分，不能把辅助强调解释为警告

侧栏使用 nav-active-* 并保留当前项语义；子页用品牌下划线；互斥字段用 segmented control；局部明确要求的旧品牌素材单独登记，不混入全局 Token

## 语义状态完整结构

| 语义 | Light 基色 | Dark 基色 | 适用 | 图标语义示例 |
|---|---|---|---|---|
| success | `#1f6b4c` | `#68c997` | 已确认正常或验证通过 | check-circle |
| warning | `#875506` | `#e9b553` | 真实警告、过期、部分完成 | triangle-alert |
| error | `#b33e37` | `#ee766c` | 故障、失败、危险动作 | circle-x / octagon-alert |
| info | `#356f8d` | `#76a9d5` | 信息、下一步 | info |
| reference | `#6254a5` | `#b5a9f0` | 参考与对照数据 | layers，图表配虚线与菱形 |

每种语义均有 `*-foreground`、`*-indicator`、`*-surface`、`*-border`、`*-icon`、`*-hover`、`*-focus`，已在 CSS 展开为具体值：indicator / icon / focus 采用基色；foreground 将基色向 text-primary 混合 Light 10% / Dark 8%，提高叠层文字对比；surface 为基色 Light 8% / Dark 12% 的透明叠层，border 为 30% / 40%，hover 为 12% / 18%；这是 V2 扩展，不是 Kudu 原始状态变量；Reference Light 底约为方案候选 `#f0edfa` 的方向，但本包采用按实际表面合成的紫色叠层

状态图标优先沿用已有图标库，上表是角色而非新库依赖；图标和标签共同表达含义；透明 surface 必须叠在明确的 page-bg / surface / viz-canvas 上，border 只是辅助，不能作为唯一可辨边界；交互状态芯片使用自身 hover 与 focus，警告/失败不能因 hover 变成品牌成功色

“有参数”“已配置”“已测量”“验证通过”按真实数据分别映射，见 [状态与连接](robot-state-and-connection.md)；Reference 不进入机器人状态机；XYZ、Joint Axis、COM 不使用这些状态变量，见 [可视化主题](visualization-theme.md)

## 表面与主题切换

Page 用 page-bg；Chrome 用 window-chrome；Sidebar 用 sidebar-bg；Workspace 承载页面任务；Surface 用 surface；Elevated 可用 bg-elevated 或 flyout-bg；Overlay 区分 bg-overlay 与 overlay-scrim；Canvas 使用独立 viz-canvas

bg-elevated 与 bg-overlay 的名字不保证“越高越亮”；层级同时用边界、留白、遮挡关系和克制阴影表达；glass-* 名称来自上游，其中 glass-bg 是不透明色；不意味着应全局增加 blur

Web 将 CSS 接入现有 Token 层，在主窗口和独立窗口的主题根设置 `data-theme="light|dark"`；旧 `--primary` 等别名在实际消费点映射到 brand-solid / brand-ink，删除重复旧色源；Qt 使用同名语义的 palette / stylesheet 映射，不要求 DOM；仅主题变化更新样式和现有材质，保留焦点、编辑值、选中项和模型实例

## 对比度与验收

普通文字目标 AA 4.5:1，大文字 3:1；必要非文本图形和控件状态按适用 3:1 检查；disabled 单独记录；色值、透明合成、hover、pressed、selected、focus、错误、警告、Reference 都按最终显示组合评估，不能凭色板宣称整个应用符合 WCAG

[双主题预览](../assets/theme-previews/index.html) 仅验证随包样例与资产，未连接业务或真实机器人；完整截图矩阵与应用 Finish Gate 见 [verification.md](verification.md)，本次计算结果见 [升级报告](../V2_UPGRADE_REPORT.md)
