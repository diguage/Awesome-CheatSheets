[![返回目录](https://parg.co/UCb)](https://github.com/wxyyxc1992/Awesome-CheatSheet)

# 分布式系统概述与理论基础

分布式架构是数据库发展的大势所趋。分布式架构显著提升大容量数据存储和管理能力，既保障面对大量用户的高并发需求，又保障了面对业务变化的弹性增长能力。分布式数据库的使用成本，也远低于传统数据库。由于分布式架构主要使用 PC 服务器与内置盘，因此几乎全部新型分布式数据库均使用多副本技术来保障数据的可靠性与安全性。

现代服务端架构，都可以称为分布式系统

微服务，分布式存储，分布式计算

Fallacies of Distributed Computing

网络是稳定的。网络传输的延迟是零。网络的带宽是无穷大。网络是安全的。网络的拓扑不会改变。只有一个系统管理员。传输数据的成本为零。整个网络是同构的。

# CAP

CAP 定理是分布式系统设计中最基础，也是最为关键的理论。它指出，分布式数据存储不可能同时满足以下三个条件。一致性（Consistency）：每次读取要么获得最近写入的数据，要么获得一个错误。可用性（Availability）：每次请求都能获得一个（非错误）响应，但不保证返回的是最新写入的数据。分区容忍（Partition tolerance）：尽管任意数量的消息被节点间的网络丢失（或延迟），系统仍继续运行。也就是说，CAP 定理表明，在存在网络分区的情况下，一致性和可用性必须二选一。而在没有发生网络故障时，即分布式系统正常运行时，一致性和可用性是可以同时被满足的。这里需要注意的是，CAP 定理中的一致性与 ACID 数据库事务中的一致性截然不同。

对于大多数互联网应用来说（如门户网站），因为机器数量庞大，部署节点分散，网络故障是常态，可用性是必须要保证的，所以只有舍弃一致性来保证服务的 AP。而对于银行等，需要确保一致性的场景，通常会权衡 CA 和 CP 模型，CA 模型网络故障时完全不可用，CP 模型具备部分可用性。

CA (consistency + availability)，这样的系统关注一致性和可用性，它需要非常严格的全体一致的协议，比如“两阶段提交”（2PC）。CA 系统不能容忍网络错误或节点错误，一旦出现这样的问题，整个系统就会拒绝写请求，因为它并不知道对面的那个结点是否挂掉了，还是只是网络问题。唯一安全的做法就是把自己变成只读的。
CP (consistency + partition tolerance)，这样的系统关注一致性和分区容忍性。它关注的是系统里大多数人的一致性协议，比如：Paxos 算法 (Quorum 类的算法)。这样的系统只需要保证大多数结点数据一致，而少数的结点会在没有同步到最新版本的数据时变成不可用的状态。这样能够提供一部分的可用性。
AP (availability + partition tolerance)，这样的系统关心可用性和分区容忍性。因此，这样的系统不能达成一致性，需要给出数据冲突，给出数据冲突就需要维护数据版本。Dynamo 就是这样的系统。

# 数据一致性

## 一致性分类

## 一致性协议

### Paxos

### Raft

## 多阶段提交

## MVCC

# 分布式应用（微服务）架构模式

# 分布式计算

## 批计算

## 流计算