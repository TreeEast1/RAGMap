# 10. 阅读路线图

## 为什么需要路线图

RAG 相关资料很多，但如果没有顺序，读者很容易出现两个问题：

- 初学者一上来就被复杂名词淹没
- 研究者看了很多方法，却没有形成方法地图

所以这个仓库把阅读路线分成两条。

## 路线 A：初学者

### 目标

建立从“什么是 RAG”到“为什么会演化”的基本认知框架。

### 建议顺序

1. [什么是 RAG](./01-what-is-rag.md)
2. [基础 RAG](./02-basic-rag.md)
3. [为什么基础 RAG 不够](./03-why-basic-rag-is-not-enough.md)
4. [GraphRAG](./04-graphrag.md)
5. [轻量化 GraphRAG](./05-lightweight-graphrag.md)

### 读完之后你应该能回答

- RAG 最小闭环是什么
- 基础向量化 RAG 为什么有效
- 为什么它在复杂任务中会不够
- 图结构为什么会出现
- 轻量结构化方案在折中什么

## 路线 B：研究者 / 开发者

### 目标

从方法演进逻辑出发，理解设计空间与后续研究机会。

### 建议顺序

1. [为什么基础 RAG 不够](./03-why-basic-rag-is-not-enough.md)
2. [GraphRAG](./04-graphrag.md)
3. [轻量化 GraphRAG](./05-lightweight-graphrag.md)
4. [Memory / Cognitive 风格 RAG](./06-memory-rag.md)
5. [Thinking-oriented RAG](./07-thinking-rag.md)
6. [CognitiveRAG](./08-cognitiverag.md)
7. [RAG 的未来](./09-future-of-rag.md)

### 读完之后你应该能回答

- 每一代方法在补哪一块短板
- 哪些方向在解决知识组织，哪些在解决推理路径
- CognitiveRAG 在整个谱系中的位置
- 下一步研究更可能从哪里切入

## 如果你的目标是“快速搭建项目”

建议先读：

1. [基础 RAG](./02-basic-rag.md)
2. [为什么基础 RAG 不够](./03-why-basic-rag-is-not-enough.md)
3. [GraphRAG](./04-graphrag.md)

因为工程实践里最重要的第一件事，不是追最新名词，而是先知道：

- 什么时候基础 RAG 就够了
- 什么时候需要结构化增强
- 什么时候复杂系统其实不划算

## 如果你的目标是“寻找研究创新点”

建议重点读：

1. [为什么基础 RAG 不够](./03-why-basic-rag-is-not-enough.md)
2. [Memory / Cognitive 风格 RAG](./06-memory-rag.md)
3. [Thinking-oriented RAG](./07-thinking-rag.md)
4. [CognitiveRAG](./08-cognitiverag.md)
5. [RAG 的未来](./09-future-of-rag.md)

并重点思考下面几个问题：

- 检索单元还能怎么定义？
- 多跳问题的中间结构应该是什么？
- 记忆更新如何建模？
- reasoning 与 retrieval 的边界是否应该重新定义？
- 认知式重排如何落成可评估机制？

## 一个更实用的建议

阅读 RAG 方法时，不要只看：

- 名字
- 指标
- demo

更应该持续追问：

1. 它为什么出现？
2. 它解决的是哪一层问题？
3. 它新增了什么成本？
4. 它留下了什么没解决？

只要沿着这 4 个问题读，方法地图会越来越清楚。
