RAG 的演进之路：从“状态”到“记忆”

副标题： Dify x Milvus 联合技术分享
演讲者： 郑立 (Zheng Li), Dify 开源生态负责人
(Key Visual: Dify Logo + Milvus Logo)

Slide 2: RAG 的真正价值：为 LLM 构建“记忆”

LLM 的“计算” vs “记忆”：

大模型是强大的“计算”引擎 (Compute)，但它们的参数是训练好的、静态的知识。

RAG 的本质： 为 LLM 挂载一个外部的、动态的**“记忆” (Memory)**。这才是 RAG 的终局。

(引用 Latent Space/Chroma 观点) "RAG 是一个谱系 (Spectrum)"

它不是一个单一的技术点，而是一个从简单到复杂的演进过程。

核心挑战：

我们如何构建 (Build)、管理 (Manage) 和使用 (Use) 这个“记忆”？

[图示建议]: 一侧是“LLM 大脑 (静态知识)”，另一侧是“外部记忆体 (动态知识)”，中间是 RAG 这条“总线”。

Slide 3: RAG 演进谱系 (Agenda)

我们的 RAG 实践，完美印证了这个“谱系”：

Naive RAG (起点): 简单的“状态” (State) 检索

Advanced RAG (攻坚): 提升“状态”的质量

Agentic RAG (智能化): “记忆”成为 Agent 的一部分

Knowledge Pipeline (基石): 高质量“记忆”的生产线

Slide 4: 阶段一: Naive RAG (简单的“状态”检索)

架构:

[图示: Query -> Embedding -> Vector Search (Milvus) -> Chunks -> LLM]

它是什么：

将知识库暴力切片 (Fixed-size Chunking)，存入向量数据库 (如 Milvus)，作为 LLM 的“外部状态”。

问题 (The Problem):

语义割裂 (Context Fragmentation): 关键信息（比如一句话的后半句）被无情截断。

检索噪音 (Retrieval Noise): 召回了不相关或次相关的 Chunks。

“大海捞针” (Lost in the Middle): 关键信息淹没在上下文的中间。

结论： 这是一个“能用，但不好用”的、静态的、低质量的“状态”。

Slide 5: 阶段二: Advanced RAG (提升“状态”的质量)

核心目标： 解决 Naive RAG 的质量问题。

Dify 的关键实践 (1): 父子文档检索 (Parent-Child Retrieval)

(来自 Dify 博客)

解决问题： 语义割裂 与 “大海捞针” 的两难。

[图示建议]:

左侧：一个大文档 (父) [图标：完整文档]。

中间：被切分成多个精细的小块 (子) [图标：小方块]。

右侧：Query 命中一个“子块”，但系统自动取回完整的“父块”交给 LLM。

Dify 的关键实践 (2): Reranking (重排序)

[图示建议]: Milvus (召回 Top 50) -> Reranker 模型 (精排 Top 5) -> LLM。

结论： 我们开始对“状态”进行精细化运营，使其质量更高。

Slide 6: 阶段三: Agentic RAG (从“状态”到“记忆”)

核心转变 (引用 Latent Space/Chroma 观点):

RAG 不再是被动流程，而是 Agent 主动使用的工具。

“状态” (State) 开始转变为**“记忆” (Memory)**。

Agent 如何使用“记忆”：

意图识别 & 查询重写： Agent “思考”如何更好地提问。

多步推理 & 循环检索： Agent 可以“反思”检索结果，并决定下一步行动。

Dify 的实践：

Dify 的 Agent 框架将 RAG 作为一个可编排的 Tool，实现复杂的、有“记忆”的任务。

[图示建议]: 一个循环图：Agent (意图) -> 思考 (规划) -> 调用 RAG 工具 -> 获得“记忆” -> Agent (反思) -> 循环或输出。

Slide 7: 根基: Knowledge Pipeline (高质量“记忆”的生产线)

RAG 的天花板： "Garbage In, Garbage Out."

无论上层的 RAG 架构多高级 (Advanced/Agentic)，底层知识（记忆）的质量决定了一切。

(来自 Dify 博客) 传统 ETL 的痛点：

流程繁琐、手动、与应用割裂。

[痛点图示：开发者 A 重复处理数据，开发者 B 也在重复处理同样的数据]。

Dify 的解决方案： "以应用为中心" 的 Knowledge Pipeline (知识管道)

[图示建议]:

左侧 (数据源): PDF, DOCX, Web URL...

中间 (Dify 知识管道): 清洗 -> 分块 (父子) -> Embedding -> ... (可视化流程)

右侧 (索引): 写入 Milvus

Slide 8: 知识管道：实现 "一次处理，多处使用"

Dify 知识管道的核心价值：

它不再是简单的 ETL，而是高质量“记忆”的管理者。

核心价值 1: 解耦 (Decoupling)

将 "知识处理" 与 "应用开发" 解耦。

核心价值 2: 复用 (Reusability)

[图示建议]:

底层: 一个 Milvus 知识库 (e.g., "公司 2024 年财报")。

上层: 多个 Dify 应用同时调用它：

App 1: 财报分析 Agent

App 2: 智能客服

App 3: HR 助手

核心价值 3: 质量 (Quality)

集中管理和优化“记忆”，为所有上层应用提供高质量的 "弹药"。

Slide 9: Dify + Milvus: RAG 演进的最佳搭档

（Dify x Milvus 协同的核心）

在“构建 LLM 记忆”的蓝图中，Dify 和 Milvus 各司其职：

Milvus: 高性能的 "记忆基座" (Memory Base)

角色： 向量数据库 (Vector DB)。

负责： 海量“记忆”（向量、元数据）的存储、索引和高效检索 (Recall)。

价值： 稳定、可靠、可扩展。[比喻: Milvus 是高性能的“内存颗粒”]

Dify: 智能的 "记忆与应用中台" (Memory & Application Hub)

角色 1: Knowledge Pipeline (知识管道)

负责： 构建、管理、优化高质量的“记忆” (并写入 Milvus)。

角色 2: Application Engine (应用引擎)

负责： 编排、使用“记忆” (Advanced RAG, Agentic RAG)。

[比喻: Dify 是“内存管理系统”和“CPU 应用层”]

Slide 10: Dify: 一站式 LLM 应用开发平台

Dify = Knowledge Pipeline + Application Engine

核心能力：

提示词工程 (Prompt Engineering)

知识管道 (Knowledge Pipeline) (内置 RAG 引擎, 支持父子文档, Rerank)

Agent 编排 (Agent Orchestration)

全生命周期运营 (日志, 标注, 分析, Finetune)

愿景： 帮助开发者构建生产级的、高质量的 AI 应用。

Slide 11: 总结 (Summary)

RAG 是一个谱系： 它正在从“静态状态”演变为“动态记忆”。

RAG 的基石： Knowledge Pipeline (知识管道) 决定了“记忆”的质量上限。

Dify + Milvus： 提供了从 "记忆构建" (知识管道) -> "记忆存储" (Milvus) -> "记忆使用" (Dify 应用) 的端到端解决方案。

Slide 12: 谢谢 (Thank You)

Join us on GitHub! (Dify Repo link / QR Code)

联系我: banana@dify.ai

Q&A

演讲者备注 (Speaker Notes)

Slide 1: 标题页

(上台，微笑，环顾观众)

大家好！非常高兴今天能代表 Dify 参加和 Milvus 的联合分享。我是郑立，Dify 的开源生态负责人。

今天我想和大家聊聊 RAG。我知道，RAG 这个词大家可能已经听过无数次了，但我们今天想聊点不一样的——聊聊 RAG 的演进，以及它如何从一个简单的“状态”检索，演变为 LLM 的“记忆”。

Slide 2: RAG 的真正价值

我们都知道，LLM 是一个强大的“计算”引擎，它的参数里固化了海量的“静态知识”。但它本身是无状态的。

那 RAG 到底在做什么？

最开始，我们以为 RAG 只是在做“检索”。但随着行业的发展，我们越来越发现，RAG 的本质，其实是在为 LLM 挂载一个外部的、动态的“记忆”。

就像 Latent Space 在对 Chroma 的访谈里提到的，RAG 不是一个技术点，它是一个“谱系”。

今天的核心问题就是：我们开发者，到底应该如何构建、管理和使用这个“记忆”？

Slide 3: RAG 演进谱系 (Agenda)

在 Dify，我们的工程实践完美地印证了这个“谱系”的演进。

我们今天就沿着这条路，从 Naive RAG 出发，看看 RAG 是如何一步步走向“记忆”的。

Slide 4: 阶段一: Naive RAG

这是我们所有人的起点，对吧？一个简单的“Query -> Embedding -> 检索 -> 生成”的流程。

它能用吗？能用。它解决了“有无”的问题。

但大家在实践中一定很快就发现了它的问题。最典型的就是“语义割裂”，你用固定的窗口去切分文档，一句话的后半句可能就没了，上下文全丢了。然后就是“检索噪音”，召回了一堆不相关的东西。

我们称之为“低质量的、静态的状态”。这离“记忆”还差得很远。

Slide 5: 阶段二: Advanced RAG

为了解决 Naive RAG 的问题，我们进入了 Advanced RAG 阶段。

在 Dify，我们实践了非常多的策略，今天分享两个关键点。

第一个，就是 Dify 博客里详细讲过的“父子文档检索”。这是为了解决一个两难问题：你切得细（子文档），检索就准，但上下文就没了；你切得粗（父文档），上下文是全了，但检索又不准了。

我们的方法是：用“子文档”来做精准检索，一旦命中，我们把完整的“父文档”交给 LLM 去阅读。这样，我们就同时保证了“检索的准”和“上下文的全”。

第二个是 Reranking。Milvus 负责从海量数据里快速召回 Top 50，我们再用一个更小的精排模型，算出真正的 Top 5。

在 Advanced RAG 阶段，我们开始真正地“运营”我们的数据，提升“状态”的质量。

Slide 6: 阶段三: Agentic RAG

从这一步开始，RAG 发生了质变。

RAG 不再是一个被动的流程，它成为了 Agent 主动使用的一个工具。

“状态”开始真正转变为“记忆”。

在 Dify 的 Agent 框架里，Agent 可以“思考”：“用户这个问题太模糊了，我得先帮他改写一下 Query 再去检索”；它还可以“反思”：“我用 RAG 查到了 A，但根据 A 的结果，我发现我还需要去查 B”。

这就是 Agentic RAG，RAG 成为了 Agent 智能的一部分。

Slide 7: 根基: Knowledge Pipeline

Advanced RAG 很好，Agentic RAG 很智能。但我们发现了一个所有 RAG 应用的天花板。

那就是：“Garbage In, Garbage Out.”

无论你的上层架构多漂亮，你喂给 LLM 的“记忆”本身是垃圾，那结果一定是垃圾。

我们在 Dify 博客里也分享了，传统的 ETL 流程繁琐、手动，而且和应用开发完全割裂。每个开发者都在自己的小角落里重复造轮子，处理相同的数据。

这绝对不是构建高质量“记忆”的正确方式。

所以，Dify 的答案是：以应用为中心的“知识管道” (Knowledge Pipeline)。我们把数据接入、清洗、分块（包括父子文档）、Embedding 和索引，变成一个可视化的、自动化的流程。

Slide 8: 知识管道的价值

知识管道的核心价值是什么？

第一，解耦。把“知识处理”和“应用开发”彻底分开。

第二，复用。这非常关键。你[指着图示]在 Dify 里构建了一个高质量的 Milvus 知识库，比如“公司 2024 年财报”。这个知识库可以被你所有的 AI 应用同时调用——财报分析 Agent 用它，智能客服也用它。

你只需要维护这一个“记忆源”，就能保证所有应用的质量。这才是企业级的做法。

Slide 9: Dify + Milvus: 最佳搭档

讲到这里，Dify 和 Milvus 在这个架构中的关系就非常清晰了。

在“构建 LLM 记忆”这件大事上，我们是最佳搭档。

Milvus 是什么？它是高性能的“记忆基座”，是那个稳定、可靠、可扩展的“内存颗粒”。它负责存储和高效检索。

Dify 是什么？Dify 是智能的“记忆与应用中台”。

Dify 的“知识管道”负责“构建和管理”这些高质量的记忆，并写入 Milvus。
Dify 的“应用引擎”负责“编排和使用”这些记忆，去驱动 Advanced RAG 和 Agent。

Slide 10: Dify: 一站式平台

（展示 Dify UI）

这就是 Dify 平台。我们把“知识管道”和“应用引擎”整合在了一起。

你可以在 Dify 上完成从提示词工程、知识库管理（内置父子文档）、Agent 编排，到最后应用运营和标注的全生命周期。

我们的愿景，就是帮助开发者构建生产级的、高质量的 AI 应用。

Slide 11: 总结

好了，总结一下今天的分享：

第一，RAG 是一个谱系，它的终局是为 LLM 构建“记忆”。

第二，这个“记忆”的质量，取决于底层的“知识管道”。

第三，Dify + Milvus，提供了从 "记忆构建" -> "记忆存储" -> "记忆使用" 的端到端解决方案。

Slide 12: 谢谢

我们 Dify 是一个开源项目，在 GitHub 上非常活跃，欢迎大家加入我们。

感谢大家的聆听，我的邮箱是 banana@dify.ai，期待和大家交流。

(进入 Q&A)