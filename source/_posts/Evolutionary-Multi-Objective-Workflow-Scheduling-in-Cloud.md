---
title: Evolutionary Multi-Objective Workflow Scheduling in Cloud
date: 2018-11-16 18:57:43
tags: Cloud Workflow Scheduling
categories: Cloud Workflow Scheduling
---

## Main idea

* **Objective**: optimize both makespan and cost

* **Main Contributions**:

  * 突出显示直接应用于云的现有调度算法的挑战，利用真实的云特性制定云工作流调度问题。

    使用基于实例的IaaS风格方案制定定价选项，但不指定特定的定价规则

  * present the EMO(Evolutionary Multi-Objective) algorithm for the modeled workflow scheduling problem.

## Challenges for Scheduling Workflows in Cloud

### 云计算和网格计算模型的差别

* the complex pricing schemes:在云环境下一个任务的cost在调度之前很难精准地预算；

  大多数调度的启发式算法还要求知道每个任务的cost来进行优先级排序或者处理器的选择。

* the large-size resource pools：在传统异构的环境中，资源池是有限的，所以有些算法是遍历资源池来进行处理器的选择，但是对于云环境不使用。

* 有一种是把所有种类的instance(VMs)做成一个列表，但是依然太大了。

## Workflow Scheduling Problem

### 基本概念定义

* **DAG** W = (T,D), $T = \{T_0,T_1,...,T_n\}$ is the set of tasks, $D = \{(T_i,T_j)|T_i,T_j\in T\}$ is the set of data or control dependencies.
* **refertime($T_i$)**: reference execution time of $T_i$
* **data($T_i,T_j$)** data transfer size from $T_i$ to $T_j$
* **pred(T_i)=$\{T_j|(T_i,T_j)\in D\}$**
*  **T_{entry}**: the entry task;**T_{exit}**: exit task 

### 云资源管理

* 认为云端的instances是无穷的，用$I=\{I_0,I_1,...\}$来形容所有可用的instances。$P =\{P_0,P_1,...,P_m\}$代表所有的instances的类型，共m种。

* 用$cu(P_i)$来代表instance type $P_i$的计算单元（compute unit），并且假设**如果一个instacne的CU变为原来的两倍，执行时间会缩短为原来的一半**,故而任务$T_i$的实际运行时间为
  $$
  Time_{comp}(T_i)=\frac{refertime(T_i)}{cu(P_j)}
  $$

* 带宽 $bw(P_i)$代表instance type $P_i$的带宽，那么$T_i$和$T_j$之间的communication time (忽略setup delays)为
  $$
  Time_{comm}(T_i,T_j)=\begin{equation}
  \left\{
  	\begin{array}{**rc1**}
  	\frac{data(T_i,T_j)}{min\{bw(P_p),bw(P_q)\}},~~~p\neq q\\
  	0,~~~p=q
  	\end{array}
  \right.
  \end{equation}
  $$

* **定价模型**：用$M=\{M_0,M_1,...,M_k\}$来表示IaaS提供的pricing options，并且定义了函数**charge**$(M_h,P_j,I_i)$计算用定价模型$M_h$来算type为$P_j$的instance $I_i$.

### 工作流调度问题定义

* 已知$W=(T,D)$，并且有IaaS平台$S=(I,P,M)$,那么一个调度问题就是要产生一个或多个下列形式的解 $R = (Ins, Type, Order)$，其中
  $$
  Ins: T\rightarrow I, Ins(T_i) = I_j\\
  Type: I\rightarrow P, Type(I_s) = P_t
  $$
  ![1](Evolutionary-Multi-Objective-Workflow-Scheduling-in-Cloud\1.png)


## 多目标进化算法优化

* 最主要的贡献就是：present a whole set of the exploration operations, including encoding, population initialization, crossover, and mutation. These operations can work with any exploitation operation (e.g., fitness assignment, selection) in the EMO area 

![2](Evolutionary-Multi-Objective-Workflow-Scheduling-in-Cloud\2.png)

其中$avail(Ins(T_i))$为instance $I_i$可用的时间，他是通过$FT(T_i)$来更新的

### Encoding

* 由于解的形式为$R = (Ins, Type, Order)$,所以染色体分为三段。

  **order**是所有任务序列的排列，如果i在j前面，则$T_i$会比$T_j$先确定用hosting instance(VM),但是并不意味$T_i$比$T_j$先执行。

  **task2ins**:是长度为n（假设有n中类型）的映射*Ins*的向量,其中index代表一个任务，他的值代表选择哪一个instance来执行此任务。例如tak2ins[i]=j就是让$T_i$被安排到一个index为j的instance($I_j$)上。

  **ins2type**:一个从instance index映射到他们类型的映射，例如ins2type[j] = k表示instance $I_j$的类型为$P_k$

![3](Evolutionary-Multi-Objective-Workflow-Scheduling-in-Cloud\3.png)

### Crossover

![4](Evolutionary-Multi-Objective-Workflow-Scheduling-in-Cloud\4.png)

* 需要注意不能违反依赖关系；This operator will not cause any dependency conflict since the order of any two tasks should have already existed in at least one parent.  