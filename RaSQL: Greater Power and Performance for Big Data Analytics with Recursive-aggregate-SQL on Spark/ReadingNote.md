# **RaSQL: Greater Power and Performance for Big Data Analytics with Recursive-aggregate-SQL on Spark**

### 1. Source

[Jiaqi Gu](https://dblp.org/pers/hd/g/Gu_0001:Jiaqi), [Yugo H. Watanabe](https://dblp.org/pers/hd/w/Watanabe:Yugo_H=), [William A. Mazza](https://dblp.org/pers/hd/m/Mazza:William_A=), [Alexander Shkapsky](https://dblp.org/pers/hd/s/Shkapsky:Alexander), [Mohan Yang](https://dblp.org/pers/hd/y/Yang:Mohan), [Ling Ding](https://dblp.org/pers/hd/d/Ding:Ling), [Carlo Zaniolo](https://dblp.org/pers/hd/z/Zaniolo:Carlo):
**RaSQL: Greater Power and Performance for Big Data Analytics with Recursive-aggregate-SQL on Spark.** [SIGMOD Conference2019](https://dblp.org/db/conf/sigmod/sigmod2019.html#0001WMSYDZ19): 467-484

🔗 https://dblp.org/rec/conf/sigmod/0001WMSYDZ19

### 2. Abstract

- 什么是 RaSQL？

  **Recursive-aggregate-SQL**：可以表达 powerful queries 和 declarative algorithm。

  比如：经典的 graph algorithms 和 data mining algorithms。

- RaSQL 系统的特点？

  - A novel compiler implementation 使得 RaSQL 可以将 declarative queries 转化成 支持 aggregates in recursive queries 的 basic fix-point operator。
  - 对于 basic fix-point operator 的 A fully optimized implementation 带来了 superior performance, scalability and portability

- RaSQL system 的 performance 如何？

  RaSQL extends Spark SQL，并且 RaSQL system 的 performance 通常和 其他一些系统 相当甚至超越，（比如：Apache Giraph, GraphX and Myria）。

### 3. Introduction

