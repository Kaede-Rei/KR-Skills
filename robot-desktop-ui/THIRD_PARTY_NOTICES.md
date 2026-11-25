# Third-party notices

本 skill 的部分设计与交互指引根据 Emil Kowalski 与 Leonxlnx 的 skills 改写；主题原始属性提取自 AdventDevInc/kudu 的 Calm Control；机器人交互与工程语义对照 SerialArm-Core，V2 更新日期为 2026-11-25；固定上游版本、实际提取范围和迁移去向见 [references/sources.md](references/sources.md)

下列 MIT 声明保留各自来源的权利与条件；本文件不将第三方照片、字体、品牌标志、目标应用源码或所有随包文件统一改授为 MIT

## Emil Kowalski / skills

Source: [emilkowalski/skills](https://github.com/emilkowalski/skills/tree/0f2e23b32bb1265e84cff8d3e75785fec953fb1b)

```text
MIT License

Copyright (c) 2026 Emil Kowalski

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Maple Mono

字体由目标应用按其 SIL Open Font License 1.1 引入；本 skill 仅记录使用方式与来源，不附带字体文件或字体的衍生二进制；分发实际字体时应同时保留官方版权和 OFL 文本

## AdventDevInc / kudu

Source: [AdventDevInc/kudu](https://github.com/AdventDevInc/kudu/tree/4fb0dbdc51f65362b966d327c781dd2a874e0f00)

主题属性来源为该提交 `src/renderer/src/globals.css` 的最终 Calm Control 定义（Dark L272–333、Light L335–396）；原始属性用于本包主题资产与规范，新增 Reference、focus、品牌交互或工程映射分别标为本包定义

```text
MIT License

Copyright (c) 2026 Advent Development Inc

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Leonxlnx / taste-skill

Source: [Leonxlnx/taste-skill 2.5.1](https://github.com/Leonxlnx/taste-skill/tree/f6b76575f949707b4e3c37cd86cb44b0b98643e8)

本包改写其视觉分类、设计系统、组件组织、资产元数据与视觉验收方法；不分发其整套网站模板、照片、Shader、品牌图标或运行时脚本

```text
MIT License

Copyright (c) 2026 Leonxlnx

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

Taste 的 MIT 适用于相应上游软件与文档；其 `references/icons.md` 和 `photos.md` 另列图标、品牌商标与图片来源：例如 CC0、MIT、ISC、Unsplash、CC BY、CC BY-SA 或 Public Domain；本包没有复制这些资源，也不以仓库 MIT 替代具体资产的许可

## SerialArm-Core、Lucide 与 Proof 参考

SerialArm-Core 根 `LICENSE` 为 GNU GPL version 3 文本；本包记录项目既有交互、模型生命周期、工程语义与资产出处，没有复制分发其应用源码、内联 SVG 路径或品牌图片

补充核对的 SerialArm-Core 提交 `fde62519882e866c5d53640b56941869fc93cf7c` 在 `apps/launcher/renderer/app.js` 中标记导航图标来自 [Lucide](https://github.com/lucide-icons/lucide/tree/6412db11042737a4b10a97315cccc3bd4f3f838c)，完整声明位于该应用 `packaging/linux/licenses/lucide.txt`，含 Lucide ISC 与 Feather MIT；本包仅列来源，不附带该图标集，目标应用复用时沿用具体图标的声明

Codex Proof 仅作为用户方案指定的视觉参考；本次未取得可独立核验的官方完整色板、SVG 资源或许可，不分发 Proof 界面源码、字体、图标或品牌标志；`window-chrome #f5f3ed` 标为用户方案的融合参考值

## 本包原创工程 SVG 与预览

本次为本包新增的独立工程 SVG（`assets/icons/`、`assets/diagrams/`）以 [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) 发布；它们是本次原创示例，不复制 SerialArm、Lucide、Proof 或第三方品牌路径；此 CC0 声明仅适用于这些新增 SVG

主题预览与组件示例是本包编写的示意内容，使用的 Kudu 原始属性保持上述来源与 MIT 声明；预览并非来自 Codex Proof 或真实设备截图；派生自 Emil、Taste 的指引继续保留对应 MIT 声明，字体和第三方资产继续适用各自许可

本次新增的主题派生映射、预览布局、合成曲线及其截图按上述 MIT 条款随包提供；预览内联的原创工程 SVG 仍适用 CC0-1.0；截图不分发系统字体二进制，也不更改各来源原有许可
