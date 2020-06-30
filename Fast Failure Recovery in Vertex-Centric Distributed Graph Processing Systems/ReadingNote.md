# Fast Failure Recovery in Vertex-Centric Distributed Graph Processing Systems

### 1. Source

[Wei Lu](https://dblp.org/pers/hd/l/Lu:Wei), [Yanyan Shen](https://dblp.org/pers/hd/s/Shen:Yanyan), [Tongtong Wang](https://dblp.org/pers/hd/w/Wang:Tongtong), [Meihui Zhang](https://dblp.org/pers/hd/z/Zhang:Meihui), [H. V. Jagadish](https://dblp.org/pers/hd/j/Jagadish:H=_V=), [Xiaoyong Du](https://dblp.org/pers/hd/d/Du:Xiaoyong):
**Fast Failure Recovery in Vertex-Centric Distributed Graph Processing Systems.** [IEEE Trans. Knowl. Data Eng. 31(4)](https://dblp.org/db/journals/tkde/tkde31.html#LuSWZJD19): 733-746(2019)

🔗 https://dblp.org/rec/journals/tkde/LuSWZJD19

### 2. Abstract

- 提出了一种 novel recovery scheme : 通过并行化 recomputation 方式加速 the recovery process

- 作者 develop 一种 从 failed compute nodes 上的 subgraphs 到 replaced compute nodes 的 reassignment strategy，通过合适的 leveraging the computation and communication cost，以实现最小化 the recovery latency。

- how is the **Performance** of proposed recovery scheme?

  作者在 Giraph 系统中集成 proposed recovery scheme，然后在 40 个 compute nodes 上的多种 real graph datasets 的实验结果论证了：proposed recovery scheme 确实 outperforms 已有的 recovery methods 大约 30x。

### 3. Introduction

