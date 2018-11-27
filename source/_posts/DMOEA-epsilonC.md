---
title: DMOEA-epsilonC
date: 2018-11-27 18:06:47
tags: Cloud Workflow Scheduling
categories: Cloud Workflow Scheduling
---

## 主要贡献

* 首次将$\epsilon$约束法和分解的方法合并起来，
* 在优化的过程中，使用了主函数变化的策略，
* 由于不同问题的计算复杂度不同，则需要对计算资源进行动态分配
* 并且使用了解和子问题的匹配，子问题和解的匹配等方法来平衡解的多样性和收敛性之间的关系

## 基本概念

### 多目标进化算法(MOEA)

* 分类:基于他们的选择策略，我们可以将他们分为三类:
  * (1)基于Parero支配
  * (2)基于performance indicator
  * (3)基于分解策略的
* 一般处理多目标问题的两个基本方法: 权重法和$\epsilon$约束法
* **$\epsilon$约束法**：选择一个目标作为主函数，其他的目标作为约束来处理，并且为每一个约束来添加一个**上界**

## 基本框架介绍

### Problem Formulation under $\epsilon$ constraint

![1](DMOEA-epsilonC\1.png)

那么Fig1中多目标优问题可以转化为:
$$
minimize~~~f_{main} = f_s(x) +\rho \sum^{m}_{i=1}f_i(x)\\
subject~~~to~~ 
\begin{equation}
\left\{
\begin{array}{**rc1**}
\frac{f_i(x)-z_i}{z^{nad}_{i}-z_{i}}\leq \epsilon_i, \forall i \in \{i,1,...,m\}/\{s\}\\
x = (x_1,x_2,...,x_n)\in \Omega
\end{array}
\right.
\end{equation}\\
其中， 0\leq \epsilon = (\epsilon_1,...,\epsilon_{s-1},\epsilon_{s+1},...,\epsilon_{m})\leq 1\\
s是从m中任意选的，\rho >0 是一个很小的正数\\
z = (z_1,...,z_m)和z^{nad} = (z^{nad}_1,...,z^{nad}_m)分别是理想点和最低点
$$

* **理想点(ideal point $z\in R^m$)**：是通过独立地最小化每一个目标函数得到的，即满足
  $$
  minimize~~f_i(x)\\
  subject~to~x\in \Omega~~~for~i=1,...,m.
  $$


* **最低点(nadir point $z^{nad}$)**:最低点是PF(Pareto Front)的上界，$z^{nad}$的每个元素定义为
  $$
  z^{nad}_{i} = max\{f_i|F = (f_1,f_2,...,f_m)\in PF\}\\
  where~ i=1,2,...,m
  $$
  **算法框架**

  ![2](DMOEA-epsilonC\2.png)


* 对两个解进行比较的基本规则：

  * (1)可行解优于不可行解
  * (2)对于两个可行解，对应目标函数值更好的更优
  * (3)对于两不可行解，选择对约束破坏更小的解

* 基本参数介绍：

  * **N**: 上界向量的个数，和种群大小相同
  * **T**: 邻居的个数**neighborhood size**
  * **$\delta$**：选择 mate solutions的概率
  * **$n_r$**: 替换的最大数量(Maximum number of replacement)
  * **$IN_m$**: 在迭代中采用更换主函数策略的代数间隔
  * **$DRA\_interval$**：在迭代中采用动态资源分配策略的代数间隔
  * **S**: 外部存档种群（EP）的最大规模
  * **NFE**: 函数评价值的最大值


### 算法

![3](DMOEA-epsilonC\3.png)

* After the main objective alternation strategy is utilized, a solution which is good for the current subproblem will no longer perform well since the objective function of this subproblem has been changed.  

![4](DMOEA-epsilonC\4.png)

* Different subproblems have different computational difficulties, therefore, it is reasonable to assign different amounts of computational effort to them based on their utility values which are defined in the line 3 of Algorithm 3 

![5](DMOEA-epsilonC\5.png)

* When a new solution is generated, it may perform badly for the current subproblem but perform well for another subproblem. 

![6](DMOEA-epsilonC\6.png)

* An EP is maintained in addition to the evolving population. Thus when a new solution is generated, the EP should be updated. And if the number of individuals in EP exceeds S, EP is pruned until its size equals to S. 
* 首先选择bounded points(有最小或最大目标值的解)，然后从剩余解中迭代选择距离已选择点最远的点