# Auto Routing in RAGMap

> `Auto Routing` 想解决的不是“再发明一种检索”，而是让系统先判断问题，再决定走哪种检索与推理路径。

## 为什么需要这一层

很多 RAG 系统默认只有一条固定流水线：

```text
query -> retrieve -> rerank -> generate
```

问题在于，不同 query 需要的能力并不一样：

- 有些只需要快速事实查找
- 有些依赖实体关系和全局结构
- 有些需要多步拆解和迭代检索
- 有些需要同时做多路召回再融合

所以真正合理的系统形态应该是：

```text
query -> query understanding -> router -> retrieval path -> evidence fusion -> answer
```

## 一个最小可行的路由框架

```text
User Query
  -> Intent Classifier
  -> Complexity Estimator
  -> Structure Detector
  -> Budget Controller
  -> Router
      -> Vector Path
      -> Graph Path
      -> Agentic Path
      -> Hybrid Path
  -> Evidence Fusion
  -> Generation
```

## 路由层可以看哪些信号

### 1. 问题类型

- 事实性查找
- 解释性问答
- 多跳推理
- 开放式任务
- 长上下文叙事理解

### 2. 知识结构需求

- 是否依赖实体关系
- 是否依赖跨文档主题整合
- 是否需要社区级总结
- 是否更适合局部片段匹配

### 3. 推理复杂度

- 一步可答
- 两到三跳可答
- 需要任务分解
- 需要中间验证和纠错

### 4. 成本约束

- 时延预算
- token 预算
- 外部工具调用预算
- 在线构图 / 查询预算

## 一个简单的策略映射

| Query 特征 | 更适合的路径 |
| --- | --- |
| 明确事实查找、关键词清晰、低延迟要求 | `vector-first` |
| 问题强调实体关系、组织结构、跨段关系 | `graph-first` |
| 问题本身复杂，需要拆解、规划或多轮验证 | `agentic-first` |
| 无法确定单一路径，或召回质量不稳定 | `hybrid` |

## 四种基础路径

## 1. Vector-first

```text
query -> embedding retrieval -> rerank -> answer
```

适合：

- FAQ
- 标准知识库
- 产品文档检索
- 快速问答

## 2. Graph-first

```text
query -> graph traversal / community retrieval -> evidence expansion -> answer
```

适合：

- 实体关系问答
- 多文档全局总结
- 结构化知识理解

## 3. Agentic-first

```text
query -> plan -> sub-queries -> iterative retrieval -> tool use -> synthesis
```

适合：

- 多步任务
- 开放问题
- 复杂推理
- 需要中间决策的查询

## 4. Hybrid

```text
query -> vector recall + graph recall + agentic refinement -> fusion -> answer
```

适合：

- query 类型不稳定
- 单路召回不可靠
- 需要同时兼顾局部证据和全局结构

## 一个可以继续扩的评分式路由思路

可以给每个 query 打几个分：

- `factual_score`
- `structural_score`
- `reasoning_score`
- `memory_score`
- `budget_score`

然后依据分数决定策略：

```text
if reasoning_score is high:
    use agentic path
elif structural_score is high:
    use graph path
elif factual_score is high and budget_score is tight:
    use vector path
else:
    use hybrid path
```

这里的重点不是规则本身，而是 `RAGMap` 可以把这些选择逻辑可视化。

## 为什么这条路对 RAGMap 有意义

因为 `RAGMap` 的价值不只在于介绍论文，而在于构建一种统一视角：

- 不同方法不是简单替代关系
- 它们更像不同能力模块
- 真正强的系统会先判断问题，再动态调用这些模块

所以从项目视角看，`Auto Routing` 是把 `RAGMap` 从“知识地图”推进到“系统蓝图”的关键一步。
