# RAGMap

> 一个单页版的 RAG 演进地图。  
> 重点不是堆论文，而是回答 3 个问题：RAG 为什么会演化、每一代方法在解决什么、下一步还能往哪里走。

![RAG 演进路线图](./assets/rag-evolution-map.svg)

## 这个仓库要做什么

`RAGMap` 想做成一个适合 GitHub 首页直接阅读的中文知识仓库：

- 对初学者：快速建立从基础 RAG 到 GraphRAG / MemoryRAG / Thinking RAG 的整体认知
- 对研究者：把代表性方法放回演进链条，而不是只看论文名和指标
- 对开发者：帮助判断不同方法分别适合什么场景、带来什么成本

当前版本刻意压成 **单页 README**，避免仓库里散落太多 Markdown 文件。

## 适合谁看

### 初学者

你会更关心：

- 什么是 RAG
- 标准向量化 RAG 是怎么工作的
- 为什么基础 RAG 很快就不够用
- GraphRAG、HippoRAG、Thinking RAG 到底是在补哪里

### 研究者 / 开发者

你会更关心：

- 方法演进是否有清晰主线
- 基础 RAG、GraphRAG、LightRAG、HippoRAG、HippoRAG2、Think-on-RAG、ComoRAG、CogitoRAG 的设计差异
- 哪些方法在解决“结构组织”，哪些在解决“记忆组织”，哪些在解决“检索与推理协同”

## 一张图看 RAG 演进

```text
基础 RAG
  -> 问题：召回局部片段，但全局关系、多跳推理、证据组织不足

GraphRAG
  -> 思路：把知识组织成图，增强关系感知与全局摘要

LightRAG
  -> 思路：保留结构化收益，同时降低完整图系统的成本

HippoRAG / HippoRAG2
  -> 思路：从“检索片段”转向“记忆组织与关联访问”

Think-on-RAG
  -> 思路：从一次检索转向查询分解、动态路径与检索-推理协同

ComoRAG / CogitoRAG
  -> 思路：更进一步强调认知式记忆、全局语义扩散、复杂语义场景中的知识重排
```

## 基础 RAG：起点，也是后续一切增强的基座

最常见的基础 RAG 流程是：

```text
文档 -> chunking -> embedding -> retrieval -> reranking -> generation
```

它的价值很明确：

- 工程上简单，容易搭建
- 对 FAQ、知识库问答、文档助手类任务很有效
- 能让 LLM 接入外部知识，而不是只依赖参数记忆

但它很快会暴露几个典型问题：

- 召回不足：相似度高不代表真正有用
- 上下文碎片化：chunk 会打断原始知识结构
- 多跳推理弱：复杂问题往往不是一次 top-k 检索能解决
- 全局关系感知弱：主题级、社区级问题处理不好
- 幻觉与证据融合不稳：检索到证据不等于模型会正确使用

这正是后续各类增强型 RAG 出现的原因。

## 方法对比总表

| 方法 | 核心问题意识 | 主要机制 | 更适合什么任务 | 主要代价 |
| --- | --- | --- | --- | --- |
| 基础 RAG | 先把相关内容找回来 | chunk + vector retrieval + rerank | FAQ、企业知识库、快速落地 | 结构弱、多跳弱 |
| GraphRAG | 局部相似不等于全局理解 | 图构建、社区摘要、局部/全局搜索 | 多文档综合问答、主题级总结 | 构图和维护成本高 |
| LightRAG | 完整图系统太重 | 轻量图式结构与简化检索 | 想要结构化收益但资源有限 | 表达能力可能弱于重图 |
| HippoRAG | 检索不是记忆 | 记忆图谱 + 关联传播 | 多跳问答、长期知识组织 | 记忆构建与更新复杂 |
| HippoRAG2 | 结构化记忆不能牺牲基础事实召回 | 更深 passage integration + 在线 LLM 使用 | 同时兼顾 factual / associative / sense-making | 系统复杂度继续升高 |
| Think-on-RAG | 单次检索不够支持复杂路径 | 查询分解、迭代检索、检索-推理协同 | 复杂推理、多步问答 | 时延和控制复杂度高 |
| ComoRAG | 长叙事理解需要 stateful memory | 动态 memory workspace + reasoning cycle | 长文本叙事、多轮状态推理 | 流程复杂、计算开销更高 |
| CogitoRAG | 仅做结构检索仍会丢失语义整体性 | semantic gist + semantic diffusion + CogniRank | 复杂语义、多跳、全局语义场景 | 中间表示和评估更复杂 |

## 每一代方法到底在解决什么

| 代际 | 为什么会出现 | 它补的核心短板 | 它没有彻底解决的事 |
| --- | --- | --- | --- |
| 基础 RAG | LLM 参数知识有限，且会过时 | 外部知识接入 | 全局关系、复杂推理 |
| GraphRAG | 纯向量匹配对结构关系感知不足 | 图结构、社区级摘要、全局理解 | 图构建太重，更新困难 |
| LightRAG | GraphRAG 过重，难以普及 | 轻量化结构组织 | 深层关系表达有限 |
| HippoRAG | 知识不应只是 chunk 集合 | 记忆组织、关联访问 | 在线更新、遗忘、压缩 |
| HippoRAG2 | 记忆型方法不能只擅长复杂问题 | 同时兼顾 factual 与 associative memory | 统一评估与工程化边界 |
| Think-on-RAG | 复杂问题需要路径，不只是证据 | 查询分解、动态检索路径 | 推理控制稳定性 |
| ComoRAG / CogitoRAG | 检索、记忆、理解仍割裂 | 更认知化的知识组织和扩散 | 标准化、复杂度、评测体系 |

## 重点论文导航

下面这几篇是这版仓库重点保留的主线论文。链接优先给原文 `arXiv abs/pdf`。

### 1. GraphRAG

- 论文：*From Local to Global: A Graph RAG Approach to Query-Focused Summarization*
- arXiv Abstract: [2404.16130](https://arxiv.org/abs/2404.16130)
- PDF: [arXiv PDF](https://arxiv.org/pdf/2404.16130)
定位：

- 这是 Microsoft GraphRAG 最具代表性的起点论文之一
- 核心贡献不是“把检索换成图”这么简单，而是把 RAG 从局部匹配推进到全局主题理解和社区摘要

### 2. LightRAG

- 论文：*LightRAG: Simple and Fast Retrieval-Augmented Generation*
- arXiv Abstract: [2410.05779](https://arxiv.org/abs/2410.05779)
- PDF: [arXiv PDF](https://arxiv.org/pdf/2410.05779)
定位：

- 它代表“轻量化结构化 RAG”方向
- 重点不是复刻完整 GraphRAG，而是在效率、复杂度、效果之间做工程化折中

### 3. HippoRAG

- 论文：*HippoRAG: Neurobiologically Inspired Long-Term Memory for Large Language Models*
- arXiv Abstract: [2405.14831](https://arxiv.org/abs/2405.14831)
- PDF: [arXiv PDF](https://arxiv.org/pdf/2405.14831)
定位：

- 它是“从 RAG 走向 memory”的代表方法
- 重要之处在于提出：知识组织不该只靠向量相似度，还应该更像长期记忆系统

### 4. HippoRAG 2

- 论文：*From RAG to Memory: Non-Parametric Continual Learning for Large Language Models*
- arXiv Abstract: [2502.14802](https://arxiv.org/abs/2502.14802)
- PDF: [arXiv PDF](https://arxiv.org/pdf/2502.14802)
定位：

- 它不是简单续作，而是在回应一个关键问题：
- 结构化 / 记忆型 RAG 不能只在复杂关联任务上强，也必须兼顾基础 factual memory

### 5. Think-on-RAG

这里我用一篇最接近你这个脉络的代表作来承接“thinking-oriented RAG”：

- 论文：*Think-on-Graph 2.0: Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation*
- arXiv Abstract: [2407.10805](https://arxiv.org/abs/2407.10805)
- PDF: [arXiv PDF](https://arxiv.org/pdf/2407.10805)
为什么这样放：

- 我没有查到标题就叫 “Think-on-RAG” 的那篇标准代表论文
- 但 `Think-on-Graph 2.0` 很适合作为 “thinking-oriented / reasoning-enhanced RAG” 的代表入口，因为它强调的正是查询路径、检索-推理协同和深层线索搜集

### 6. ComoRAG

- 论文：*ComoRAG: A Cognitive-Inspired Memory-Organized RAG for Stateful Long Narrative Reasoning*
- arXiv Abstract: [2508.10419](https://arxiv.org/abs/2508.10419)
- PDF: [arXiv PDF](https://arxiv.org/pdf/2508.10419)
定位：

- 这是“认知启发 + memory-organized RAG”的一个很强代表
- 特别适合长叙事、长文本、stateful reasoning 这类不是一次检索就能解决的问题

### 7. 认知式 RAG / CogitoRAG

你给出的链接对应的是这篇：

- 论文：*Understand Then Memory: A Cognitive Gist-Driven RAG Framework with Global Semantic Diffusion*
- arXiv Abstract: [2602.15895](https://arxiv.org/abs/2602.15895)
- PDF: [arXiv PDF](https://arxiv.org/pdf/2602.15895)
- DOI: [10.48550/arXiv.2602.15895](https://doi.org/10.48550/arXiv.2602.15895)

命名说明：

- 这篇论文的标题不是 “CognitiveRAG”
- 论文摘要里提出的框架名是 **CogitoRAG**
- 但它确实非常适合放在“认知式 RAG / cognitive-style RAG”这条主线上理解

定位：

- 它试图解决“离散文本表示导致语义整体性丢失”的问题
- 关键关键词包括：`Semantic Gist`、`Query Decomposition`、`Entity Diffusion`、`CogniRank`

## 一条更清晰的阅读顺序

如果你只想用一个 README 读完整条脉络，建议按这个顺序往下看：

1. 先理解基础 RAG 的标准流程与局限
2. 再看 GraphRAG 为什么要引入图结构
3. 然后看 LightRAG 如何做复杂度折中
4. 再看 HippoRAG / HippoRAG2 如何把问题推进到 memory
5. 接着看 Think-on-RAG 如何把 retrieval 和 reasoning 绑在一起
6. 最后看 ComoRAG / CogitoRAG 如何把问题进一步推进到认知式记忆与语义扩散

## 这条演化链最重要的观察

我认为 RAG 的核心变化可以概括成一句话：

> 它正在从“把相关 chunk 找回来”演化为“把知识组织、访问、扩散、重排，并服务于复杂推理”。

换句话说，RAG 的竞争点会越来越不是：

- 谁检索更像搜索引擎

而是：

- 谁的知识组织更强
- 谁的全局关系建模更好
- 谁能把 memory、reasoning、planning 和 retrieval 接起来

## 仓库后续怎么扩

当前仓库先故意保持轻量，只保留：

- 一个 `README.md`
- 一个 `LICENSE`
- 若干占位图 `assets/*.svg`

如果后续扩展，我建议按这个顺序：

1. 先继续补 README 里的论文导航和方法比较
2. 再补一张真正可发表级别的 RAG 演进路线图
3. 最后如果内容足够多，再拆分成 `docs/`

## License

当前采用 [CC BY 4.0](./LICENSE)。

适合这个项目的原因很简单：

- 这是文档型知识仓库
- 允许转载、整理、再创作
- 只要求保留署名
