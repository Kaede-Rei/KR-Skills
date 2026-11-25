# 设计基线、能力覆盖与来源

这是一个技能入口下的特化能力集合；入口、references 与随包资产共同构成本包，不通过嵌套 SKILL.md 注册子技能，也不要求安装其他设计 skills

- V2 更新日期：2026-11-25
- 用户提供方案：`Robot-Desktop-UI-V2_视觉体系升级方案_Codex实施Prompt.md`，方案日期 2026-11-22，版本 `V2.0 Proposal`
- 本次迁移定位：Botanical Engineering；Kudu 提供主题色彩，Proof 提供窗口视觉参考，Taste 提供视觉构成与资产组织方法，Emil 保持交互工程基线，机器人系统决定工程语义与真实状态

## 基线与解释顺序

1. 当前用户要求和目标项目明确约束
2. 本包记录的机器人状态、模型生命周期与 SerialArm-Core 交互契约
3. 目标项目现有、适合当前任务的实现与检查方法
4. 上游经验，用于补充上述约束没有决定的实现选择

本次用户方案替换旧视觉品牌决策，未替换既有交互与工程语义；记录基线不表示自动追随仓库未来所有改动；更新本包时核对实际行为和用户确认结果，修正对应模块

## SerialArm-Core

- 仓库：`SerialArm-Core`
- 已审定 UI 基线：`76326c00aa29ed9a80aa2d202896b28f28f01eb6`，提交标题为 `fix(gui): 修复切换残影并优化模型复用与串口反馈`
- 本包创建日期：2026-11-14
- 交互与工程行为对照上述版本源码；2026-11-25 的 V2 视觉规则以本次用户方案为准
- 本次补充资产核对版本：`fde62519882e866c5d53640b56941869fc93cf7c`（2026-11-16，`refactor!: 重构机械臂接入流程、参数配置与双路径停放策略`）；仅用于说明当前图标来源，不自动将其后续业务改动升级为本包契约

下表路径相对于 SerialArm-Core 仓库根目录；它们是可复核来源，不是运行本 skill 所需的本机绝对路径

| 规范 | 实现来源 |
| --- | --- |
| 历史 Proof 衍生表面、旧橙色主题及原语义映射；V2 品牌和主题改用下述 Kudu 基线 | `apps/launcher/renderer/styles.css` |
| 真实 Maple CN Italic、连字、控件尺度、hover/focus、统一 disclosure、减少动态等偏好 | `apps/launcher/renderer/studio.css` |
| 外壳和页面骨架 | `apps/launcher/renderer/studio-shell.css`、`app.js` 的 `shell`、`pageHead`、`render` |
| 工作页、四象限机器人操作栏、子页导航和文档式任务内容 | `apps/launcher/renderer/studio-workspace.css`、`app.js` 的 `robotOperationHtml`、`workspaceLayoutHtml` |
| 全宽准备内容、顶部参数检查、分组导航与模型关节预览 | `apps/launcher/renderer/studio-inspector.css` |
| 菜单 invoker 和串口选择、扫描结果浮层、固定到期时间 | `app.js` 的菜单与 `connectionPort*`、`scanConnectionPorts` 路径，`studio-connection.css` |
| 临界阻尼重定向、新正文进入、折叠自然高度测量和滚动恢复 | `apps/launcher/renderer/studio-motion.js` |
| Profile 预加载、generation、跨页保留、按槽恢复视角与可见性 | `app.js` 的 `loadModelData`、`prepareModelPreview`、`suspendModelPreview`、`attachModelPreview`、`preloadAvailableProfileModel` |
| 暂停/挂载/恢复、COM 对象复用、帧数值快照、资源释放 | `apps/launcher/renderer/model-view.js` |
| 数据驱动的状态和可读错误 | `app.js`、`error-i18n.js`；规范取实际状态语义，不把所有现存文案认定为不可改的标准 |
| 模型/界面验证方法 | `apps/launcher/scripts/studio-ui-fixture.cjs`、`render-studio-ui.cjs`、`verify-model-lifecycle.cjs`、`verify-model-ghost.cjs` |
| 字体资源来源与许可 | `apps/launcher/renderer/fonts/README.md`、`fonts/OFL.txt` |

### V2 视觉替换与保留的设计选择

- 2026-11-14 的旧方案采用明亮暖白、亮橙主操作白字，并否决当时的低饱和绿主色；2026-11-22 用户方案明确替换这一视觉决策，V2 正式采用森林绿品牌与完整 Calm Control 双主题；旧否决记录仅作历史，不再约束 V2
- Light 品牌为 `#173f34 / #f8f2e5`，Dark 品牌为 `#d6e6dc / #15382e`（背景 / 前景）；原 `#ff7b35`、`#e25507` 不再承担默认品牌、主操作或选中导航；琥珀金保留为辅助强调，设备状态由各自语义表达
- 字体使用真实 Maple CN Italic，提供编程连字开关；不是单纯给默认字体合成斜体
- 准备页改为全宽后续工具区；参数页把检查放上方全宽区域；不恢复旧窄信息侧栏
- 参数组可以用卡片；工作台内部用轻分隔结构；统一折叠语法而不是强制全界面卡片化
- 页面替换不保留旧正文退出层；只让新正文短 spring 进入
- 快扫描采用按钮锚定状态浮层，不阻塞页面；Profile 三维预加载仍可使用必要的加载阻塞
- 模型跨页保留、隐藏暂停；渲染优化针对重复计算、对象和纹理重建，而非先降低画质

### 工程颜色与图标资产盘点

基线 `apps/launcher/renderer/model-view.js` L512–590、L776 的工程颜色保留；它们不参与品牌换色

| 工程对象 | 已核对值 |
| --- | --- |
| XYZ 坐标轴 | X `#ef4444`、Y `#22c55e`、Z `#3b82f6` |
| Joint Axis | 受控 `#ff9f1a`、普通 `#8b93a3`；固定关节 origin `#b0b6c2` |
| Link COM / raw inertia | `#ff4f87` |
| Effective COM / inertia | COM `#ffb02e`、inertia `#ffa928` |
| Total COM | `#22d3a6` |
| 选中 Joint Axis | `#ffd166`，同时改变轴长与端点尺度 |

| 资产 | 核对结果与分发边界 |
| --- | --- |
| 基线普通 UI 图标 | `app.js` 的 `paths` / `Object.assign(paths, …)` 内联路径集与 `icon()`，使用 `viewBox="0 0 24 24"`；基线源码没有独立 Proof SVG 来源声明 |
| 当前导航图标 | 补充核对版本的 `app.js` L48–49 明确标注 [Lucide](https://github.com/lucide-icons/lucide/tree/6412db11042737a4b10a97315cccc3bd4f3f838c)，提交 `6412db11042737a4b10a97315cccc3bd4f3f838c`；许可声明位于 `packaging/linux/licenses/lucide.txt`，含 ISC 与 Feather MIT |
| 折叠符号 | `studio-motion.js` 中内联 chevron；沿用组件语法，不提取为所谓官方 Proof 图标 |
| 品牌图片 | `robotArtwork()` / `associationArtwork()` 引用 `renderer/brand/arm.png`、`association.png`；属于应用品牌资产，本包不复制或改授许可 |
| 字体 | `renderer/fonts/README.md` 与 `OFL.txt`；详见下方字体记录 |

SerialArm-Core 根 `LICENSE` 是 GNU GPL version 3 文本；本包记录其既有行为、颜色与来源，不复制分发其源码、品牌图片或内联路径；Lucide 的独立许可也不等同于 SerialArm 整仓库许可；后续确需复用具体资产时，核对实际文件及随附声明

## Kudu Calm Control

- [上游仓库](https://github.com/AdventDevInc/kudu)
- 核对日期：2026-11-25
- 固定版本：[4fb0dbdc51f65362b966d327c781dd2a874e0f00](https://github.com/AdventDevInc/kudu/tree/4fb0dbdc51f65362b966d327c781dd2a874e0f00)
- 源文件：[src/renderer/src/globals.css](https://github.com/AdventDevInc/kudu/blob/4fb0dbdc51f65362b966d327c781dd2a874e0f00/src/renderer/src/globals.css)
- 提取范围：`/* Calm Control design tokens */` 注释 L271 之后的 `:root` L272–333 和 `.light` L335–396；每套 59 个 CSS 自定义属性，覆盖 page、sidebar、titlebar、card、subtle、hover、active、elevated、overlay、flyout、toast、text、brand、nav、border、accent、semantic、gauge、grid、glass、scrollbar、selection 与 glow
- 不提取文件前段已被覆盖的旧主题或旧 `@theme` 琥珀色常量；后段组件的特例也不混入全局原始色表
- 许可：[MIT](https://github.com/AdventDevInc/kudu/blob/4fb0dbdc51f65362b966d327c781dd2a874e0f00/LICENSE)，Copyright (c) 2026 Advent Development Inc；完整文本见 [THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md)

### 原始值与本包迁移层

| 内容 | 来源与边界 |
| --- | --- |
| 59 对原始 Light / Dark 属性 | 原名原值保留在 [calm-control.css](../assets/theme/calm-control.css)；`surface` 等产品语义可映射 `card-bg`，不得称改名后就是上游原名 |
| 品牌与主操作职责 | 上游已有 `brand-solid/ink/surface/border`；本包将主要操作映射到 `brand-solid/ink` 是本次用户方案的迁移决策；上游 `.calm-action-card.primary` L1225–1229 实际使用 `accent/text-on-accent` |
| Hover / active | 上游有 `bg-hover`、`bg-hover-2`、`bg-active` 和 `accent-hover`，没有 `brand-hover`、`brand-active` 原始属性；新增品牌交互映射须标注为本包派生值 |
| 语义色 | 原始 `success/warning/danger/info` 分别为 Light `#1f6b4c/#875506/#b33e37/#356f8d`、Dark `#68c997/#e9b553/#ee766c/#76a9d5`；其 foreground、indicator、surface、border、icon 分层属于本包映射，不是上游已有全套变量 |
| Focus | 上游 L398–400 为 `outline: 2px solid rgba(245,158,11,.6)`、offset `2px`；L3053–3056 的 `.service-row:focus-visible` 单独用 `brand-solid`；上游没有统一 `focus-ring` 属性，本包 focus token 是适配定义 |
| Reference | `#6254a5` / `#b5a9f0` 来自用户 V2 方案；不是 Kudu 状态色；背景、边框和图表线型按本包适配 |
| Canvas、backdrop、状态表面与额外按钮层 | 上游基础 token 未直接提供的完整工程职责由本包定义，并与原始表分开记录；不得把建议值伪装成来源仓库值 |

`accent` 与 `warning` 在 Dark 都是 `#e9b553`，上游数值相同；本包仍将“辅助强调”与“警告”作为不同职责，通过文字、图标、组件位置和状态样式区分

## Codex Proof 视觉参考

Proof 在本包仅提供暖白窗口、深灰文字与克制 SVG 呈现的视觉方向；不构造第二套全局主题，也不覆盖 Kudu 的页面、侧栏、内容表面

- 方案中的 `window-chrome: #f5f3ed` 是用户方案提供的暖白融合参考值；不是本次核验得到的官方 Codex Proof token
- SerialArm 基线 `styles.css` 的 Light 实际为 `bg #faf9f5`、`side #f3f1eb`、`card #fffefa`、`text #2f312d`；`#f5f3ed` 在该文件中是 Dark 正文色；这些历史实现不证明存在一份官方 Proof 完整色板
- 用户方案说明 `#3d755d` 曾来自 `accentSource=custom` 的 Proof 导出；本次未找到并检查该原始导出，因此只保留其来源说明，不把它当官方默认值
- 本次未获得可独立核验的 Proof SVG 原始文件及许可；不随包分发 Codex Proof 图标、字体或界面源码；本包工程 SVG 的来源另列

## Taste 2.5.1

- [上游仓库](https://github.com/Leonxlnx/taste-skill)
- 核对日期：2026-11-25
- 固定版本：[f6b76575f949707b4e3c37cd86cb44b0b98643e8](https://github.com/Leonxlnx/taste-skill/tree/f6b76575f949707b4e3c37cd86cb44b0b98643e8)
- `v2.5.1` 为 annotated tag；tag 对象 `45ed32d8fa7ebbcd7ebd4e570e40bb1feed14018`，解析到上述 commit；`.codex-plugin/plugin.json` 的 `version` 为 `2.5.1`
- 实际技能目录：`skills/taste-skill/`；`SKILL.md` 的 frontmatter 名称为 `design-taste-frontend`；目录名称和技能名称并不相同
- 许可：[MIT](https://github.com/Leonxlnx/taste-skill/blob/f6b76575f949707b4e3c37cd86cb44b0b98643e8/LICENSE)，Copyright (c) 2026 Leonxlnx；完整文本见 [THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md)

### 已核对的结构

下列路径相对于上游 `skills/taste-skill/`，用于复核迁移依据，不要求使用者安装 Taste

- `references/` 共 22 份：`backgrounds.md`、`cards.md`、`copy-moves.md`、`copy-registers.md`、`copy-tells.md`、`copy-voice.md`、`copy.md`、`diagrams.md`、`effects-creative.md`、`effects-objects.md`、`effects-usage.md`、`gate.md`、`icons.md`、`layout-v4.md`、`moments.md`、`motion.md`、`perf.md`、`photos.md`、`scenes.md`、`sections-library.md`、`sections.md`、`system.md`
- `library/`：`palettes.json`、`type.json`
- `assets/`：`backgrounds/`、`components/`、`diagrams/`、`effects/`、`icons/`、`layout/`、`moments/`、`motion/`、`objects/`、`photos/`、`scenes/`、`ui/`；另有 `starter.html`、`system.css`、`system.js`
- `scripts/`：`consistency.mjs`、`copy-lint.mjs`、`effects.mjs`、`gate.mjs`、`icons.mjs`、`moments.mjs`、`perf.mjs`、`photos.mjs`、`shoot.mjs`、`start.mjs` 及 `fx-gallery.template.html`、`fx-lab.template.html`

### 能力迁移对照

| Taste 能力与具体依据 | 本包迁移位置与适配 |
| --- | --- |
| Art Direction：`SKILL.md` 的按业务分类与 `references/sections.md` | [art-direction.md](art-direction.md)：按 Dashboard、Workspace、Telemetry、Configuration、Diagnostics、Calibration、Model Inspector 区分主要阅读与操作职责 |
| Design System：`references/system.md`、`assets/system.css/js`、`library/palettes.json`、`type.json` | [design-system.md](design-system.md)、[theme-guidelines.md](theme-guidelines.md)：采用 Kudu 色彩、Maple 字体及工程密度，不复制网站默认 palette / 字体 / 巨型标题 |
| Dealers：`assets/layout/deal.mjs`、`scripts/start.mjs`、`scripts/moments.mjs` | [layout-recipes.md](layout-recipes.md)：保留“先分类、再选适用结构”，按任务、数据、窗口与面板职责作确定性选择；不随机决定工程布局或轮换品牌 |
| Component Library：`references/cards.md`、`sections-library.md`、`assets/ui/`、`components/` | [component-library.md](component-library.md)：记录组件职责、结构、数据、状态、键盘与主题；使用真实工程内容，复用既有控件行为 |
| Visual Assets：`references/icons.md`、`photos.md`、`diagrams.md` 与各资产目录 | [visual-assets.md](visual-assets.md)、[iconography-and-svg.md](iconography-and-svg.md)：工程 SVG、图表、模型视口、流程图分类及元数据；不引入网站照片配额或整套第三方资产 |
| Backgrounds / Effects / Scenes：`references/backgrounds.md`、`effects-usage.md`、`effects-creative.md`、`effects-objects.md`、`scenes.md` | [visual-assets.md](visual-assets.md)、[visualization-theme.md](visualization-theme.md)：低干扰画布、状态与空间说明；效果预算服从遥测、模型与桌面性能 |
| Visual Moments：`references/moments.md`、`assets/moments/` | [visual-moments.md](visual-moments.md)：模型焦点、标定证据、遥测差异、拓扑关系；不自动加入 Hero 进入、滚动编排或网页展示效果 |
| Copy Composition：`references/copy.md`、`copy-voice.md`、`copy-moves.md`、`copy-registers.md`、`copy-tells.md` | [copy-and-accessibility.md](copy-and-accessibility.md)：标题、单位、图例、空状态、动作与结果；不采用营销标题、网站字数配额和虚构业务事实 |
| Browser Check / Finish Gate：`references/gate.md`、`scripts/consistency.mjs`、`gate.mjs` | [verification.md](verification.md)、[workflows.md](workflows.md)：双主题、实际窗口、状态、键盘、对比度和截图核验；不安装或执行上游网站 Stop hook |
| Performance / Shoot：`references/perf.md`、`scripts/perf.mjs`、`shoot.mjs` | [verification.md](verification.md)、[model-lifecycle-and-performance.md](model-lifecycle-and-performance.md)：记录运行环境、前后证据、实际耗时与模型生命周期；网站传输配额和四 WebGL context 上限不自动变成机器人工作站指标 |

### 明确排除与许可边界

不迁移网站 Hero、One Section Per Screen、照片数量、Footer / Booking、每页固定数量展示时刻、紫色禁令、仅引用文字可斜体、随机配色和网站强制动效；Reference 紫色、Maple Italic、短连续 spring 与机器人真实状态均按本包契约执行

本次改写视觉设计方法并保留 MIT 声明，不复制 Taste 的完整网站模板、照片、Shader、品牌图标或运行时脚本；上游 `references/icons.md` 单独列出 `logos` / Simple Icons 的 CC0、vscode-icons 的 MIT、Lucide 的 ISC，并注明品牌商标边界；`references/photos.md` 记录 Unsplash 和 Commons 的 CC0、CC BY、CC BY-SA、Public Domain 等来源；这些第三方资产不因位于 MIT 仓库内而统一改授 MIT

## 本包新增资产与派生文档

- `assets/theme/calm-control.css` 的原始主题属性派生自上述 Kudu 范围；额外工程与交互 token 是本包适配定义，不能回标为 Kudu 原值；随包保留 Kudu MIT 声明
- 本包新增的独立工程 SVG（`assets/icons/`、`assets/diagrams/`）为本次原创示例，以 [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) 发布；不含 SerialArm 内联路径、Lucide 图标、Proof 图标或品牌标志的复制品
- `assets/theme-previews/` 与组件示例是本包编写的主题与工程状态示意；示例布局和内容属于本包新增内容，引用的主题 token 仍按 Kudu 来源标识；预览不构成 Codex Proof 官方界面或真实设备界面的来源证据
- 基于 Taste、Emil 改写的指引随包保留各自 MIT 版权和许可；本次原创 SVG 的 CC0 不覆盖这些派生文档、Kudu token、字体、第三方品牌或目标应用资产
- 本页记录来源核验与迁移决定；实际 UI、视觉、性能和机器人行为的验收证据由具体项目按 [verification.md](verification.md) 记录

## Emil Kowalski skills

- [上游仓库](https://github.com/emilkowalski/skills)
- 核对版本：[0f2e23b32bb1265e84cff8d3e75785fec953fb1b](https://github.com/emilkowalski/skills/tree/0f2e23b32bb1265e84cff8d3e75785fec953fb1b)
- 核对日期：2026-11-14
- 许可证：MIT，Copyright (c) 2026 Emil Kowalski；完整许可见 [THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md)

下面列出该版本全部 19 项；路径为上游 `skills/<名称>/SKILL.md`，按用途合并到本包，不要求运行时再读原文

| 上游名称 | 特化去向 |
| --- | --- |
| `apple-design` | 设计系统、组件、可打断 spring、直接操作、空间关系与无障碍 |
| `emil-design-eng` | 控件反馈、层级、浮层来源感和相关动效选择 |
| `animate` | `motion-and-scroll.md` 的建立、打断和结束规则 |
| `choreograph` | 稳定外壳与变化正文的协调；结构和滚动同步，不叠加旧业务正文 |
| `gestures` | 直接跟随、指针捕获、输入取消和释放后的连续性；不向机器人状态加入虚假惯性 |
| `animation-performance` | 动效与模型的实际热点、重算、布局成本和绘制生命周期 |
| `animation-vocabulary` | 组件与反馈术语，帮助将描述对应到正确控件及行为 |
| `review-animations` | 有触发条件和可复核依据的只读评审 |
| `improve-animations` | 整体问题梳理与可执行改进方案；交付模式由当前用户要求决定 |
| `find-animation-opportunities` | 补即时反馈、空间关系和状态转换，避免无目的装饰 |
| `remove-animations` | 移除等待、无用 stagger、重播与重复绘制，保留确认过的产品动效 |
| `prototype` | 复用产品 tokens 的隔离方案比较与选定后接入 |
| `break-ui` | 有界的长文本、空数据、缺失资源、数值、列表及窄窗口检查 |
| `learn-taste` | 沉淀最终确认的修正、原因和来源；不把每次尝试都升级为规范 |
| `pick-ui-library` | 先检查现有组件和原生能力，具体缺口才决定依赖 |
| `ask-sonner` | 反馈的位置、进行/成功/失败状态、更新与关闭；本包不强制 Sonner API |
| `mobile-native` | 提取输入、视口、滚动和平台语义；移动 Web 专用修复不在本版范围 |
| `animate-expo` | 提取直接操作、状态连续性和主线程负载经验；不提供 Expo/Reanimated 专用 API 指南 |
| `write-swift` | 提取状态建模、资源身份和先测量再优化的经验；不提供完整 Swift 语言或并发迁移指导 |

Apple 风格经验在这里指上游对设计原则的解释及本项目实际落地，不把上游文章等同于 Apple 官方对本应用的认证

### 已特化的冲突规则

| 上游通用建议 | 本包决定 |
| --- | --- |
| 同一容器内新旧视图交叉淡入淡出 | 业务正文立即替换，只对新内容短进入；避免已观察到的残影 |
| 高频或键盘操作绝对不动画 | 保留用户确认的短连续 spring；输入、焦点和命令不等待；减少动态时静态完成 |
| 快于约 300ms 的操作不显示 spinner | 扫描 pending 可显示 spinner，快请求直接显示结果，不人为延时，结果具有独立可读生存期 |
| 广泛应用玻璃、透明材质，或一律用 raised shadow | 采用 SerialArm 暖白层级、克制阴影和细分隔；已有 card、row、轻量 disclosure 各有用途 |
| 以某些 React 库作为默认实现 | 先使用项目技术栈与现有原生能力；依赖不是设计契约 |
| 用 blur 掩盖不完美的内容切换 | 修复重建、重播与旧 DOM 叠加，不以模糊文本隐藏问题 |
| 将统一时间上限视作所有 spring 的固定 duration | 沿用两组实际 response，区分响应与自然收敛；按实际交互检查节奏 |
| 每次按固定模板、固定数量或并行代理完整审计 | 按本次影响面选择工作方式和验证，结束条件由请求与实际问题决定 |

## 字体

基线使用 Maple Mono 官方 v7.9 的 Maple Mono CN Italic、MediumItalic、SemiBoldItalic；官方资源入口：[MapleMono-CN.zip](https://github.com/subframe7536/maple-font/releases/download/v7.9/MapleMono-CN.zip)

SerialArm 将完整 TTF 转换为 WOFF2，保留原字形与 GSUB；实际编程连字主要由 `calt` 提供，不能只开启 `liga` 就声称连字已实现

字体为 SIL Open Font License 1.1；本 skill 不分发字体二进制；目标应用实际引入文件时保留其官方 OFL 和版权信息，已有正确资源则复用

## Skill 结构依据

采用一个简短入口加按需参考：[OpenAI Skills 文档](https://learn.chatgpt.com/docs/build-skills)、[支持资源与工作边界](https://developers.openai.com/plugins/build/skills)

每次使用不必重新联网取上游；只有更新来源、实现超出本包已覆盖的具体技术问题时才按需查阅最新官方资料；不自动下载或安装整个上游集群
