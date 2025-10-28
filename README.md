RAG 的演进之路：从“状态”到“记忆” — Dify × Milvus

简述
- 一套基于 Reveal.js 的演讲幻灯片，面向开发者与数据平台团队，主题覆盖 Naive/Advanced/Agentic RAG、Knowledge Pipeline、外环评估与 Dify × Milvus 的协同实践。
- 视觉遵循 Dify 品牌：Dify Blue #0033FF、极简几何与弥散渐变、轻手绘纹理点缀。

快速预览
- 本地打开：`slides/index.html`
- 主题切换：在幻灯片页面按键 `1`（Swiss）/ `2`（Atelier）/ `3`（Night）
- 演讲者备注：按 `s` 打开 Presenter Notes

内容结构（15 页）
- RAG 价值（计算 vs 记忆）、谱系（Naive/Advanced/Agentic）
- Advanced RAG 三原则：混合召回（100–300 候选）→ 先精排后组装 → 尊重 Context Rot
- Agentic RAG：查询重写、多轮检索与反思、工具化编排
- Knowledge Pipeline：Ingest/Query 全链路、组件与治理（连接器、分块/富化、向量化、索引、版本与权限）
- 外环（Outer Loop）：Gold Set、CI 看板、误差分析、记忆压缩（Compaction）
- Dify × Milvus 分工、平台能力、一页争议观点 × 张力、总结、Q&A

GitHub Pages 托管
- 本仓库已准备 `docs/` 目录用于 GitHub Pages。
- 在 GitHub 仓库 Settings → Pages：
  - Source 选择 “Deploy from a branch”
  - Branch 选择 `main`（或默认分支）/ `docs` 目录
  - 保存后访问仓库提供的 Pages URL，即可在线播放 `docs/index.html`

目录说明
- `slides/`：开发目录（原始幻灯片）。
  - `slides/index.html`：主页面
  - `slides/styles/`：基础与主题样式
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

