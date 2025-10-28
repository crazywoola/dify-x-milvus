RAG 的演进之路：从“状态”到“记忆” — Dify × Milvus

简述
- 一套基于 Reveal.js 的演讲幻灯片，面向开发者与数据平台团队，主题覆盖 Naive/Advanced/Agentic RAG、Knowledge Pipeline、外环评估与 Dify × Milvus 的协同实践。
- 视觉遵循 Dify 品牌：Dify Blue #0033FF、极简几何与弥散渐变、轻手绘纹理点缀。

快速预览
- 本地打开：`docs/index.html`
- 主题切换：在幻灯片页面按键 `1`（Swiss）/ `2`（Atelier）/ `3`（Night）
- 演讲者备注：按 `s` 打开 Presenter Notes


目录说明
- `docs/`：GitHub Pages 站点目录（镜像了 slides 内容）。
  - `docs/index.html`：托管入口
  - `docs/styles/`：复制的样式文件
  - `docs/assets/dify-logo.svg`：Logo 资源（发布所需的最小集）
- `assets/`：本地设计包与原始 Logo 等素材（不直接对 Pages 发布）。

品牌与排版
- 英文：Söhne / Söhne Mono（本地安装则自动使用）
- 中文：Mi Sans（回退：PingFang SC / Noto Sans SC / 等）
- 默认字号较大（h1≈118px, h2≈60–66px, 正文≈34–36px），强调可读性与舞台呈现。

自定义与扩展
- 调整强调色：`slides/styles/base.css` 与 `docs/styles/base.css` 中的 `--dify-blue`
- 添加/移除弥散渐变：给 `<section>` 增加/移除 `class="accent"`
- 添加新主题：在 `slides/docs/styles/` 新增 CSS，并在 `index.html` 的快捷键切换中注册

许可
- 幻灯片结构与代码开源；Logo 与品牌元素归 Dify 所有，请在品牌规范内使用。

