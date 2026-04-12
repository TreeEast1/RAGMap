# RAGMap

> 一个单页版的 RAG 技术发展树。  
> 重点不只是“RAG 按时间怎么演化”，而是回答 3 个问题：有哪些分支、它们各自在解决什么问题、系统能否自动选择合适路线。

![RAG 技术发展树](./assets/rag-evolution-map.svg)

## 这个仓库现在的定位

`RAGMap` 不再只讲一条线性的演进链：

- 不是只看向量检索
- 不是只看图谱检索
- 也不是把所有增强方法都塞进一个笼统的 “advanced RAG”

现在这个项目更适合被理解为：

> 一个用于理解 RAG 设计空间的中文技术地图。

它把 RAG 看成一棵会继续分叉的技术树，而不是单一答案。

## 核心判断

我现在对这个项目的主张是：

> RAG 的未来不是“所有任务都用同一种检索”，而是针对问题类型、知识结构、推理深度和成本约束，动态选择不同路线。

所以 `RAGMap` 的重点也应该升级成两层：

1. 先看不同技术枝条分别是什么
2. 再看系统能不能自动决定走哪一条枝条

## 一张图看新的 RAGMap 主线

```text
RAGMap
├── 向量检索分支
│   └── 解决：局部相关片段召回、低成本落地、标准知识库问答
├── 图检索分支
│   └── 解决：关系建模、社区摘要、全局主题理解、多跳结构查询
├── Memory / Agentic RAG 分支
│   └── 解决：长期记忆、任务分解、迭代检索、检索-推理协同
└── Auto Routing / Auto Selection 分支
    └── 解决：面对不同问题，自动选择 vector / graph / agentic 路径
```

这意味着 `RAGMap` 不只是论文导航，也可以自然演化成一个系统设计框架：

- 用什么知识组织
- 用什么检索路径
- 用不用 agent
- 什么时候自动切换模式

## 适合谁看

### 初学者

你更关心：

- 什么是基础 RAG
- 为什么只做向量检索很快就不够
- 图检索、agentic RAG、auto routing 到底差在哪

### 研究者 / 开发者

你更关心：

- 不同分支的核心问题意识是什么
- 这些方法是互斥关系，还是可以组合
- auto 模式到底应该依据什么做选择

## 为什么现在需要“技术发展树”而不是单线时间轴

单线时间轴的问题在于它容易让人误解成：

- 新方法一定全面替代旧方法
- 图一定比向量高级
- agentic 一定比普通 RAG 更好

这不对。

更真实的情况是：

- `Vector RAG` 仍然是很多业务的最优解
- `Graph RAG` 适合结构关系明显的问题
- `Agentic RAG` 更适合复杂、多步、开放式任务
- `Auto Routing` 适合面对混合型问题时做动态调度

所以 `RAGMap` 更适合画成技术树，而不是胜者通吃的时间线。

## 四条核心枝条

## 1. 向量化检索分支

最常见的基础流程仍然是：

```text
文档 -> chunking -> embedding -> retrieval -> reranking -> generation
```

它解决的是：

- 从外部知识里快速找到局部相关内容
- 以较低工程复杂度完成知识增强
- 适配 FAQ、文档问答、企业知识库等高频场景

它的优点：

- 工程成熟
- 部署简单
- 响应快
- 成本可控

它的典型短板：

- 结构关系感知弱
- 多跳推理弱
- 全局主题整合弱
- chunk 化之后容易丢上下文结构

所以它不是过时了，而是成为所有后续分支的基座。

## 2. 图检索分支

当问题不只是“找相关文本”，而是“理解实体、关系、社区、全局主题”时，图分支就开始成立。

这条分支的代表思路包括：

- `GraphRAG`
- `LightRAG`

它重点解决：

- 关系建模
- 社区级摘要
- 全局视角下的主题理解
- 多跳结构路径查询

它的价值不是简单替换向量，而是给系统增加一种新的知识组织方式。

它的典型代价：

- 构图成本高
- 更新难
- 工程链路更重
- 在线维护复杂

所以图检索不是默认方案，而是结构问题的强力分支。

## 3. Agentic RAG 分支

这条分支的核心不是“再加一个 agent 壳子”，而是把 RAG 从一次性检索改造成任务驱动的检索流程。

这条分支通常会做这些事：

- 判断问题类型
- 拆解子问题
- 多轮检索
- 选择工具
- 动态修正检索路径
- 在推理过程中继续找证据

这条线上和它相邻的代表方法包括：

- `Think-on-RAG`
- `Think-on-Graph 2.0`
- 更广义的 `reasoning-oriented RAG`

它更适合：

- 多步问题
- 开放式复杂任务
- 需要计划和中间决策的问答
- 一次 top-k 不足以解决的问题

它的代价也很明确：

- 时延更高
- 控制更复杂
- 系统稳定性更难保证
- 很依赖任务编排质量

## 4. Auto Selection / Auto Routing 分支

这是你这次提出的最重要扩展方向。

`RAGMap` 不应该只展示不同方法，还应该展示一个更强的未来命题：

> 系统是否可以先理解问题，再自动决定该走哪种 RAG 路线。

这个分支的核心不是新的单一检索算法，而是一个路由层。

它可以根据这些信号做选择：

- 问题是否偏事实查找
- 问题是否依赖实体关系
- 问题是否需要多跳推理
- 问题是否需要任务分解
- 问题是否需要长期记忆或会话状态
- 当前延迟预算和成本预算是多少

然后自动决定：

- 走 `vector-first`
- 走 `graph-first`
- 走 `agentic`
- 先粗检索再升级
- 多路召回后再融合

这条分支本质上让 `RAG` 从“固定流水线”变成“可调度系统”。

## RAGMap 现在可以表达成一个更完整的系统图景

```text
Query
  -> Query Understanding
  -> Task / Complexity / Structure Estimation
  -> Router
      -> Vector Path
      -> Graph Path
      -> Agentic Path
      -> Hybrid Path
  -> Evidence Fusion
  -> Reasoning / Generation
```

这也是为什么这个项目值得继续做。

因为很多资料只在介绍某一篇论文，而 `RAGMap` 可以专门回答：

- 这些方法之间是什么关系
- 哪些是并列分支，哪些是增强模块
- 哪些应该被系统自动选择，而不是人工拍脑袋决定

## 方法对比总表

| 分支 | 核心目标 | 典型机制 | 适合任务 | 主要代价 |
| --- | --- | --- | --- | --- |
| 向量检索 | 快速召回相关内容 | embedding + retrieval + rerank | FAQ、企业知识库、标准 QA | 结构弱、多跳弱 |
| 图检索 | 强化关系与全局组织 | graph construction + community summary | 多文档综合、关系问答、主题级问题 | 构图与维护成本高 |
| Agentic RAG | 让检索服务于任务分解与推理 | planning + iterative retrieval + tool use | 复杂任务、多步推理、开放式问题 | 时延高、控制复杂 |
| Auto Routing | 自动选路而不是固定流水线 | query classification + routing + fallback | 混合问题、动态场景、可扩展系统 | 设计与评估更复杂 |

## 代表性论文，按枝条来放

### 向量检索基座

- 基础 RAG：作为所有增强路线的共同起点

### 图检索分支

- `GraphRAG`
  - 论文：*From Local to Global: A Graph RAG Approach to Query-Focused Summarization*
  - arXiv: [2404.16130](https://arxiv.org/abs/2404.16130)
- `LightRAG`
  - 论文：*LightRAG: Simple and Fast Retrieval-Augmented Generation*
  - arXiv: [2410.05779](https://arxiv.org/abs/2410.05779)

### Memory / Agentic 相邻分支

- `HippoRAG`
  - 论文：*HippoRAG: Neurobiologically Inspired Long-Term Memory for Large Language Models*
  - arXiv: [2405.14831](https://arxiv.org/abs/2405.14831)
- `HippoRAG 2`
  - 论文：*From RAG to Memory: Non-Parametric Continual Learning for Large Language Models*
  - arXiv: [2502.14802](https://arxiv.org/abs/2502.14802)
- `Think-on-Graph 2.0`
  - 论文：*Think-on-Graph 2.0: Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation*
  - arXiv: [2407.10805](https://arxiv.org/abs/2407.10805)
- `ComoRAG`
  - 论文：*ComoRAG: A Cognitive-Inspired Memory-Organized RAG for Stateful Long Narrative Reasoning*
  - arXiv: [2508.10419](https://arxiv.org/abs/2508.10419)
- `CogitoRAG`
  - 论文：*Understand Then Memory: A Cognitive Gist-Driven RAG Framework with Global Semantic Diffusion*
  - arXiv: [2602.15895](https://arxiv.org/abs/2602.15895)

## 一条更清晰的理解顺序

如果你现在再读这个仓库，建议按这个顺序理解：

1. 先理解基础向量 RAG 为什么仍然重要
2. 再看为什么有些问题必须引入图结构
3. 然后看记忆型和 agentic 方法为什么要把检索流程动态化
4. 最后看 auto routing 为什么可能成为下一阶段真正实用的系统方向

## 我认为 RAGMap 最值得强调的句子

> RAG 的下一步不是单点替代，而是分支并存、能力组合，以及自动选路。

也就是说，未来比拼的不只是：

- 谁的召回率更高

而是：

- 谁更会组织知识
- 谁更会选择检索路线
- 谁能把 retrieval、memory、reasoning、planning 连接起来

## 这个项目接下来可以怎么继续长

如果继续更新，我建议按这个方向扩：

1. 把 `README` 继续打磨成一张真正能直接讲清技术树的首页
2. 把 `assets/rag-evolution-map.svg` 升级成更正式的技术发展树图
3. 单独补一个 `docs/auto-routing.md`，专门写 query router / strategy selector / hybrid RAG
4. 后续如果需要，再把每个分支拆成独立文档

## License

当前采用 [CC BY 4.0](./LICENSE)。

适合这个项目的原因很简单：

- 这是文档型知识仓库
- 允许转载、整理、再创作
- 只要求保留署名
