# 设计系统、字体与密度

V2 将颜色、工程可视化、组件与交互分层：Kudu 提供双主题色彩骨架，Proof 提供暖白窗口参考，Taste 提供视觉组织方法，Emil / SerialArm 提供交互契约；工程状态和安全条件决定可用操作

## Token 的责任

主题原值和 V2 派生值统一维护于 [主题规范](theme-guidelines.md) 及随包 CSS；业务组件消费语义 Token，不在页面重复写十六进制色；图表与模型使用 [可视化主题](visualization-theme.md)，不把 brand-solid 当成 measured、success 或坐标轴

Primitive → Semantic → Component 三层：保留核验的源值，映射品牌/表面/状态/画布角色，再给组件定义用途；组件若没有特殊语义就复用现有 Token，不为每个实例生成独立色板；Theme Dealer 只选择已批准 Light / Dark 与目标项目明确的 override，不随机抽色；组件选型见 [组件库](component-library.md)

## Maple 的真实 Italic

使用 Maple Mono CN 的真实 Italic、Medium Italic、SemiBold Italic 资源；不要用 CSS 倾斜来伪造字形，也不要把“喜欢 JetBrains 风格连字”理解成必须再引入 JetBrains Mono

SerialArm 将真实斜体资源注册为应用自己的常规字体族，以便所有控件与日志统一使用

```css
@font-face {
  font-family: "SerialArm Maple Italic";
  src: url("fonts/maple-mono-cn-italic.woff2") format("woff2");
  font-weight: 100 449;
  font-style: normal;
  font-display: swap;
}
```

这里的 `font-style:normal` 是字体族别名策略，文件本身就是 Italic；Medium 对应 `450 549`，SemiBold 对应 `550 900`；这三个区间是静态字重资源的匹配范围，不意味着文件是可变字体

设置 `font-synthesis:none`；正文、按钮、输入框、select、技术数据与日志均使用相应字体族；保留系统与中文字体 fallback；移植时替换为目标项目资源路径，保留字体许可证，不依赖本机字体已安装

编程连字默认开启，设置提供可持久保存的开关；示例用 `!= => ->`

```css
[data-font-ligatures="on"] {
  font-variant-ligatures: common-ligatures contextual;
  font-feature-settings: "calt" 1, "liga" 1, "dlig" 1;
}
[data-font-ligatures="off"] {
  font-variant-ligatures: none;
  font-feature-settings: "calt" 0, "liga" 0, "dlig" 0;
}
```

将设置传到主窗口及相关独立窗口的实际文本节点，避免后续控件样式覆盖；用实际显示确认关闭效果，不能只改一个未被读取的属性

## 字号、数字与尺度

| 用途 | 默认基线 |
|---|---|
| 普通正文、字段、按钮 | 14px |
| 辅助说明、单位、密集元数据 | 12px |
| 局部面板标题 | 16px |
| 准备页下一步标题 | 20px |
| 页面标题 | 24px |
| 普通控件高度 / 圆角 | 36px / 8px |
| 面板圆角 / 主分区间距 | 14px / 24px |
| 参数卡片 / 嵌套组圆角 | 10px / 8px |

标题用 SemiBold Italic，分区和参数标签用 Medium Italic，正文用 Italic；资源及字重按项目真实文件选择；实时数值采用 tabular-nums，数值、符号、单位与精度统一，同列按小数点或单位对齐；时间戳按任务选择相对或绝对时间，数据新鲜度单独表达

## 三种密度

下列尺寸为 V2 建议起点，不是 Kudu 原始值；Compact 同步调整布局而非单独缩小字号，保留完整键盘操作与可辨命中区

| 密度 | 用途 | 控件高 | 表格行高 | 正文/行高 | 面板间距 | 图表内边距 | 标签-数值 |
|---|---|---|---|---|---|---|---|
| Comfortable | 引导、准备流程、低频设置 | 40px | 40px | 14/22px | 28px | 24px | 12px |
| Default | 日常总览、参数配置 | 36px | 34px | 14/20px | 24px | 20px | 8px |
| Compact | 遥测、日志、密集表格 | 32px | 28px | 13/18px | 16px | 14px | 6px |

小号辅助信息保持至少 12px 起点，保留单位和警告；减少非必要说明的常驻展示，可通过详情查看；触控或目标项目更大的命中尺寸优先，不为了 Compact 隐藏停止操作或必要条件

## 层级与构图

以间距、字号重量、表面和轻边界分层，不堆满粗体、阴影或同样大小的卡片；阴影复用主题 glass-shadow 或已有更轻组件阴影；浮层强于普通面板，高对比度环境补真实边界

按 [Art Direction](art-direction.md) 识别主要任务和视觉焦点；用 [布局配方](layout-recipes.md) 与现有 [布局契约](layout-and-navigation.md) 排列对象关系；采用过的方案记录在目标项目已有设计记录中，包括页面类型、配方、主题/密度、复用组件及原因；局部修改不另建历史数据库
