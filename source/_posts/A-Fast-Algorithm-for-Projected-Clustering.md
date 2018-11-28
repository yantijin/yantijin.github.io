---
title: A Fast Algorithm for Projected Clustering
date: 2018-11-28 17:07:01
tags: Clustering Algorithm
categories: 
- Algorithm Library
- Clustering Algorithm
---

## 投影聚类法

### Basic Conceprions

* **投影聚类**:考虑一些多维空间中的一组数据点。 投影聚类是数据点的子集C以及维度的子集p，使得C中的点紧密地聚集在维度V的子空间中。

### 基本符号定义

* N:数据点的数量
* $C = \{x_1,x_2,...,x_t\}$是在一个类中数据点的集合
* cluster C的**中心点**定义为: $\bar{x}_c = \sum^t_{i=1} x_i/t$
* 定义一个类的**半径radius**为 一个点到类中心点的平均距离 $\bar{x}_c = \sum^t_{i=1} d(\bar{x}_c,x_i)/t$

### 算法介绍

* 算法分为三个部分： 初始化阶段(initialization phase)；迭代阶段(iteration phase)；类别调整阶段(cluster refinement phase)

* **初始化阶段**：使用Greedy method

  ![1](A-Fast-Algorithm-for-Projected-Clustering\1.png)

  首先从数据集中随机确定一个中心点，加入M，然后计算其他每一个点到M中所有中心点中最近的距离，然后取距离最大的点作为下一个中心点加入M，重新计算剩余点到M中所有中心点中最近的距离，依次迭代下去，直到得到满足个数的集合M

* **迭代阶段**：

  (1)首先从集合M中选择k个作为初始的中心点，然后重复(2)-(6)

  (2)对于M中的每一个中心点$m_i$：

  ​	$\delta_i$是$m_i$距离$m_i$最近的中心点的距离

  ​	$L_i$是以$m_i$为圆心，$\delta_i$为半径中包含的点的集合

  $L = \{L_1,...,L_k\}$

  (3)为集合中每一个中心点找到与之相关的维度,l最少为2(D = FindDimensions(k,l,L))

  (4)通过找到的维度将所有点按照距离来进行分类，((C1,...,Ck) = AssignPoints(D1,...,Dk))

  (5)通过分类和维度来计算目标函数；如果比目前最好的目标函数还要好，就记录下中心点的分类和当前目标函数的值。

  (6)从当前中心点中找到最坏的一些中心点，然后去除掉之后，从M中重新加入一些点来构成新的集合

* **聚类改进阶段(refinement phase)**
  ![2](A-Fast-Algorithm-for-Projected-Clustering\2.png)
  ![3](A-Fast-Algorithm-for-Projected-Clustering\3.png)
  ![4](A-Fast-Algorithm-for-Projected-Clustering\4.png)
### 算法细节
* FindDimensions(k,l,L):

  ![5](A-Fast-Algorithm-for-Projected-Clustering\5.png)

  * 其中 $X_{ij}$为$L_i$中的点到中心点$m_i$在维度j上的距离

  * $Y_i$为对第i个中心点来说，对应的$L_i$到中心点$m_i$上所有维度的平均距离

  * 而后计算标准偏差$\sigma_i$,就可以得到一个为每一个维度进行一个归一化的评价

    为$Z_{ij} = (X_{ij}-Y_i)/\sigma_i$

  * 对于每一个中心点$m_i$对应的$Z_{ij}$，选择最小的l个并将这l个记录在$D_i$中，最终返回$D = \{D_1,D_2,...,D_k\}$

* AssignPoints函数：
  ![6](A-Fast-Algorithm-for-Projected-Clustering\6.png)

  注意计算的是曼哈顿距离(街区距离)

  选取距离最小的作为某分类(其规则是关于$D_i$的维度上)中的点

* evaluateClusters函数：
  ![7](A-Fast-Algorithm-for-Projected-Clustering\7.png)

  评估一组中心点的质量，从点到它们所属的cluster的质心的曼哈顿距离的平均值作为评价标准

* 丢弃：首先确定哪些是坏的中心点：

  * (1)周围有最少点的中心点是坏的中心点
  * (2)若中心点周围的点数比$\frac{N}{k}*minDeviation$少，那么他是坏的中心点，mindDeviation是一个小于1的常数(一般用0.1)

* **聚类改进阶段**：再进行(2)-(4)一次，唯一不同的是此次用C而不是用L

[此算法的Python代码](https://github.com/cmmp/pyproclus)，写的很规范，完全是根据paper的流程写的，非常清晰。