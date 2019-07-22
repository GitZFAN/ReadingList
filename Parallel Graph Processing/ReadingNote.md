[TOC]

# Parallel Graph Processing

### 1. Source

[Da Yan](https://dblp.org/pers/hd/y/Yan:Da), [Hang Liu](https://dblp.org/pers/hd/l/Liu:Hang):
**Parallel Graph Processing.** [Encyclopedia of Big Data Technologies 2019](https://dblp.org/db/reference/bdt/1.html#YanL19)

🔗 https://dblp.org/rec/reference/bdt/YanL19

### 2. Definition

- *parallel graph processing* 的目的：
  - 加速处理过程
  - 扩展以处理更大规模的图

- *parallel graph processing* 的应用场景：
  - 单机多核并行（multiple threads）
  - 多机器分布式集群

### 3. Overview

- modern big graph 处理系统主要关注：

  - **user-friendliness**: 

    编程接口应基于直观计算模型，算法开发人员只需关注图分析逻辑本身，而不用关心底层执行细节。

  - **efficiency**: 

    底层执行引擎应该保证：高吞吐执行、自动容错支持、高可扩展性（水平、垂直）

- 如何看待（comment）一个 **programming paradigms** and **systems** for big graph analytics？
  - **computation models** and **target applications**
  - **execution environments**

- **distributed system** 不总是 faster than **stand-alone solution**：（比如：small graph）
  - 对于 data-intensive graph analytic 任务，network communication 通常是 performance bottleneck
  - 只有当机器的数量足够大到超过它们之间的通信代价，distributed system 才是 beneficial

### 4. Key Research Findings

- Pregel-Like Systems

  - Pregel :

    - based on the **bulk synchronous parallel (BSP)** model
    - vertex + its adjacency list, comput(msgs), supersteps, "active", vote to halt.
    - 在 Pregel 中，compute() 函数可以访问当前的 superstep number，所以 Pregel algorithm 可以在不同的 superstep 中执行不同的 operations。
    - combine() : Combiner 机制
    - aggregator 机制
    - "**think-like-a-vertex**" computing model; two vertex-centric program examples :
      - Hash-Min algorithm : 计算 connected components (CCs)
      - list ranking problem : a building block of the Euler tour technique

  - **Optimizations** :

    - stable **open-source** Pregel implementation : **Giraph**, Pregel+

      these systems 基本上都做了一些具体的改进

    - GraphD : stream 处理 以 消除 memory requirement

    - GPS : 在多个机器上构造 high-degree vertex 的 mirrors

    - GraphX (Spark), Gelly (Flink) : 通过消除不同的连续操作之间的数据  exports/imports 操作，以减少 end-to-end 的 processing time

  - Block-Centric Paradigm :

    - Giraph++ : partition of vertices
    - Blogel : block(a connected subgraph)
    - GRAPE : only require users to provide sequential algorithm

    在 Block-Centric 的模型中，一个 key issue 是：如何 **track vertices**

- Shared-Memory Abstraction

  这也是 另一种的 **vertex-centric paradigm**; vertex 可以在计算运行时 直接访问 它的 **adjacent vertices and edges**.

  它只是模拟一种 shared-memory environment，其实实际的执行并不是 shared memory，反而是 distributed 或者 out of core。

  - GraphLab : 
    - partition edges among machines
    - adopts a **Gather-Apply-Scatter(GAS)** computation model
    - supports asynchronous execution

  - Stand-alone Systems : 

    - perform out-of-core graph processing to eliminate the need of huge memory space

    - GraphChi : sequential as possible

    - X-Stream : edges are streamed on local disk(s)

    - Graphene system : utilize the bandwidth of an array of SSDs

      feature the efficient execution with new hardware

- Subgraph-Centric Paradigm

  - G-thinker system : 

    It performs computation on subgraphs.

    - each subgraph is associated with a task, tasks are spawned from individual vertices, different task performs computation iteratively.
    - 程序实现主要是通过 two UDFs(User Define Function) : 
      - *compute(frontier)* : specifies how a task computes for one iteration
      - *task_spawn(v)* : specified how to create tasks according to a vertex *v*

### 5. Example of Applications

- Vertex-centric algorithms : 

  - to solve fundamental graph problems : 

    breadth-first search, list ranking, spanning tree, Euler tour, pre/post-order traversal, connected components, biconnected components, strongly connected components, etc.

  - **various real applications** : social network analysis, genome assembly.

- Subgraph-centric frameworks : 

  - **subgraph-structure** (triangle, clique, quasi-clique) **mining**, **graph matching**, motif counting in biological networks, finding social circles, personalized recommendations

### 6. Future Directions for Research

- **subgraph-centric paradigm** for **compute-intensive**(and/or recursive) **graph analytics**
- consider how to **optimize** vertex-centric and graph centric **workloads on new hardware** (such as SSDs and GPUs)
- **applications** developed on these big graph processing frameworks