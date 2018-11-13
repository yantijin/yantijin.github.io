---
title: Basic Conceptions
date: 2018-11-13 22:15:59
tags: machine learning
categories: 
- machine learning
- basic conception
---

## Basic conception

* **特征向量(feature vector)**: 每一个分量对应一种**属性**(attribute)/**特征**(feature)的值，构成的空间为**属性空间**

* 一般地，令$D = \{x_1,x_2,...x_m\}$表示包含m个示例的**数据集**，每个示例由d个属性描述，则每个示例$x_i = (x_{i1};x_{i2};...;x_{id})$是d维样本空间$\chi$中的一个向量，$x_i\in \chi$,d为样本$x_i$的**维数**

* 训练样本的结果称为**标记(label)**；拥有了标记信息的示例，称为**样例(example)**,一般用$(x_i,y_i)$表示

* 学习任务大致可分为两类：**监督学习(supervised learning)**和**无监督学习(unsupervised learning)**，分类(classification)和回归(regression)是前者的代表，而聚类则是后者的代表。

* **泛化(generalization)能力**:所学的模型适用于新样本的能力；

* 通常假设样本空间全体样本服从一个未知的**分布(distribution)**,获得的每个样本都是**独立同分布的(independent and identically distributed),i.i.d**

* **归纳(induction)**:从特殊到一般的泛化过程；**演绎(deduction)**:从一般到特化.

* **演绎空间**：样本x每一个属性的可能取值所构成的空间，其中有可能是*,代表此属性取什么都行，也有可能整个空间为空集。

  **版本空间(version space)**:如果假设空间中有多个与训练集一致的假设，即存在一个与训练集一致的“假设集合”

* **归纳偏好(inductive bias)**:算法在学习过程中对某种类型假设的偏好

  “奥卡姆剃刀”原则：若有多个假设与观察一致，则选择最简单的那个。

* **No Free Lunch Theorem**: 所有算法的期望性能是相同的，**前提**是所有“问题”出现的机会相同、或者所有问题同等重要，但是实际情况不是这样