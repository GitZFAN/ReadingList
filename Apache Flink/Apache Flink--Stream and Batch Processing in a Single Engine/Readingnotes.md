# Apache Flink™: Stream and Batch Processing in a Single Engine

——Apache Flink是一个可以进行批处理和流处理的开源系统

### 1. 应用背景

传统的批处理和现有的流处理被处理为两套系统，同时现有的流处理系统或者是批流融合系统都有着以下问题：

- 高延迟
- 高复杂度
- 流处理语义不够完善

Flink提出了一个统一模型，使用统一的执行引擎能够同时处理流数据和批数据。

### 2. 系统架构

- 层级架构：

  - Libraries：基于API构建的domain-specific libraries
  - APIs：DataSetAPI 和 DATaStream API
  - Core：Flink 的 runtime engine 是 distributed dataflow engine 实质上是 streaming dataflow engine。可以执行包括DataSet APIs和DataStream APIs编写的程序
  - Deploy：Flink部署的底层环境

- 运行架构：

  Flink Client：接收程序代码，并转化为dataflow Graph，然后提交给jobManager

  - Job Manager：协调整个dataflow 的分布式执行。主要是做系统的调度和协调
  - Task Manager：负责具体operator的执行，向jobManager汇报信息，是进程级别的

### 3. 核心概念：—Streaming Dataflow

- Dataflow Graph：包括Source、Intermediate Data Stream、Operators、Sink等环节，形成的一个DAG图。

- Data Stream在producting operator 和 consumming operator之间分发的方式：
  - point-to-point：端到端
  - broadcast：广播
  - re-partition：重分区
  - fan-out：
  - merge：

- Intermediate Data Stream之间的数据交换：

  两种交换方式：pipeline 和 blocking。其中blocking主要用于批处理的情景中。

  数据交换的模式是buffer模式：其中buffer被发送的触发条件是：
      1）存满了，2）buffer的缓存时间用尽。
  当buffer较大时：flink可以实现高吞吐；反之，当buffer较小是可以实现高实时、低延迟。这一特点使得flink比较灵活。
  
  除了交换数据之外，dataflow还能交换控制事件control event。常见的control event类型：
  
  - Checkpoints barrier
  - Watermark
- Iteration barriers 
  
- Flink的容错方面：

  - 实现方式：通过checkpoints 和 重执行的方式实现了 exactly-once-possessing 一致性保证。
  - 具体方法：ABS（异步屏障快照）——Asynchronous Barrier Snapshot

### 4. Flink中的流处理

- 时间
- 状态
- 窗口
- 异步流迭代

### 5. Flink中的批处理

—通过流处理的方式实现批处理，但是做了相关的优化处理

- 查询优化
- 内存管理
- 批式迭代