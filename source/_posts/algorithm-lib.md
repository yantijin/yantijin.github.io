---
title: algorithm-lib
date: 2018-11-18 23:31:57
tags: algorithm
categories: Algorithm Library
---

# 聚类算法

## Partitional Clustering Algorithm

### k均值聚类

### PAM(Partitioning Around Medoids)

### CLARA(Clustering Large Applications)

### CLARANS(Clustering Large Applications based on Randomlized Search)

## Hierarchical Clustering Algorithm

### BIRCH(balanced iterative reducing and clustering using hierachies)

### CURE(Clustering Using Representatives)

### ROCKS(A Robust Clustering Algorithm for Categorial Attributes)

## Grid-based Clustering Algorithm

### STING

### WaveCluster

## Model-based Clustering Algorithm

### Gaussian model

### Latent Dirichlet Allocation

## Density-based Clustering Algorithm

### DBSCAN聚类

* [参考博客](https://www.cnblogs.com/pinard/p/6208966.html)
* 关键概念：核心对象，密度直达，密度可达，密度相连
* 缺点：需要自己确定eps，Minpts

#### AE-DBSCAN(可以自己决定radius，Eps,parameters)

* **k-dist list**:对于给定数据集D，k-dist list是数据集中对于每个点来说距离最近的k个点
* **slope of a point with respect to another point**:对于一个给定的$k-list=(k_1,k_2,...,k_n)$,$k_i$到$k_{i+1}$的斜率就是$k_ik_{i+1}$的斜率

![1](algorithm-lib\1.png)

### OPTICS

* [参考博客](https://www.cnblogs.com/zhangruilin/p/5817784.html)
* 关键概念：核心距离，可达距离

### DENCLUE

### CLIQUE

# 关联规则

### APriori算法

* [参考博客](https://blog.csdn.net/qq_36219266/article/details/82707708)
* [代码](https://github.com/yantijin/Lean_DataMining)

### FP_Tree算法

* [参考博客](https://blog.csdn.net/qq_36219266/article/details/82784299)
* [代码](https://github.com/yantijin/Lean_DataMining)

# 决策树

### ID3+C4.5

* [参考博客](https://yantijin.github.io/2018/11/17/决策树/)

* [代码](https://github.com/yantijin/Lean_DataMining)

### CART算法

* [参考博客](https://blog.csdn.net/xiaqunfeng123/article/details/34820095)
* [代码](https://github.com/yantijin/Lean_DataMining)
# 启发式算法
### GA

* 基本构成：编码，种群初始化，选择，交叉，变异，局部搜索等

### 多目标进化算法

* NSGA，NSGA-II，SPEA，SPEA-II，MOEA/D,DMOEA-$\epsilon C$

### 差分进化算法

### 粒子群算法

### 分布估计算法

### local search

* tabu search
* 爬山法

### 蚁群算法

### 小生境

# 分类算法

### BP神经网络

### 决策树(见上)

### KNN

### 贝叶斯分类器

### AdaBoost提升装袋算法

* [参考博客](https://blog.csdn.net/qq_36219266/article/details/82799071)
* [代码](https://github.com/yantijin/Lean_DataMining)



