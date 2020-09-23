---
title: ODE数值解
date: 2020-09-24 00:20:43
tags: machine learning
categories:
- math 
- ODE
---

> 转载自  **李森科在zhihu** [链接](https://zhuanlan.zhihu.com/p/70255604) <!-- more -->

## 第一部分 常微分方程的数值解法

常微分方程数值解法主要分为两大部分，初值问题与边值问题的数值方法。本部分只讨论初值问题。

## 第一章 常微分方程初值问题

本章讨论一阶常微分方程初值问题 ![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Bcases%7D++%5Cfrac%7Bdu%28t%29%7D%7Bdt%7D%3Df%28t%2Cu%28t%29%29%5C%5C+u%28t_0%29%3Du_0%5C%5C+%5Cend%7Bcases%7D%5C+++%281.0.1%29) 的数值求解，其中 ![[公式]](https://www.zhihu.com/equation?tex=f) 为 ![[公式]](https://www.zhihu.com/equation?tex=t) 和 ![[公式]](https://www.zhihu.com/equation?tex=u) 的已知函数， ![[公式]](https://www.zhihu.com/equation?tex=u_0)为给定的初值。在基本假设下，初值问题 ![[公式]](https://www.zhihu.com/equation?tex=%281.0.1%29) 在区间 ![[公式]](https://www.zhihu.com/equation?tex=%5Bt_0%2CT%5D) 上有唯一解 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%29) ，并且 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%29) 是连续可微的。

数值解法是一种离散化方法，利用这种方法，可以在一系列离散点 ![[公式]](https://www.zhihu.com/equation?tex=t_1%2C...%2Ct_N) 上求出未知函数 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%29) 的近似值 ![[公式]](https://www.zhihu.com/equation?tex=u_1%2C...%2Cu_N) ，这个近似值称为初值问题的一个数值解。

自变量 ![[公式]](https://www.zhihu.com/equation?tex=t) 的离散值 ![[公式]](https://www.zhihu.com/equation?tex=t_1%2C...%2Ct_N) 是事先取定的，称之为节点，通常取成等距的，即 ![[公式]](https://www.zhihu.com/equation?tex=t_1%3Dt_0%2Bh%2C...%2Ct_N%3Dt_0%2BNh) ，其中 ![[公式]](https://www.zhihu.com/equation?tex=h%3E0) 称为步长。

## 1.1 基本概念 Euler法与梯形法

**1.1.1 Euler法介绍**

本节通过Euler法及梯形法的讨论，说明常微分方程数值解法中的一些基本概念与主要研究的问题。

首先得到初值问题 ![[公式]](https://www.zhihu.com/equation?tex=%281.0.1%29) 等价的积分形式 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%2Bh%29%3Du%28t%29%2B%5Cint%5E%7Bt%2Bh%7D_%7Bt%7Df%28%5Ctau%2Cu%28%5Ctau%29%29d%5Ctau+%5C+%281.1.2%29) 

设 ![[公式]](https://www.zhihu.com/equation?tex=t_1%3Dt_0%2Bh) ，使用左矩形公式计算一步 ![[公式]](https://www.zhihu.com/equation?tex=u_1%3Du_0%2Bhf%28t_0%2Cu_0%29) ，类似地利用 ![[公式]](https://www.zhihu.com/equation?tex=u_1) 和 ![[公式]](https://www.zhihu.com/equation?tex=f%28t_1%2Cu_1%29) 计算出 ![[公式]](https://www.zhihu.com/equation?tex=u%28t_2%29) 的近似值，那么可以得到Euler法的计算公式  ![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Bcases%7Du_0%3Du_0%EF%BC%8C%5C%5C+u_%7Bn%2B1%7D%3Du_n%2Bhf%28t_n%2Cu_n%29%5C+%281.1.1%29%2Cn%5Cgeq0%5C%5C+%5Cend%7Bcases%7D%5C+) 

Euler法的几何意义是十分清楚的：在这种方法中，实际上是用一条过 ![[公式]](https://www.zhihu.com/equation?tex=%28t_0%2Cu_0%29) 的折现来近似替代过 ![[公式]](https://www.zhihu.com/equation?tex=%28t_0%2Cu_0%29) 的积分曲线，因此这种方法又称为折线法。

**1.1.2 收敛性，截断误差，稳定性问题的简单介绍**

为考察由Euler法提供的数值解是否具有实用价值，首先应该知道，当步长 ![[公式]](https://www.zhihu.com/equation?tex=h) 取得充分小时，所得数值解 ![[公式]](https://www.zhihu.com/equation?tex=u_n) 能否足够精确地逼近初值问题 ![[公式]](https://www.zhihu.com/equation?tex=%281.0.1%29) 的真解 ![[公式]](https://www.zhihu.com/equation?tex=u%28t_n%29) ，这就是收敛性问题。

其次，还必须估计数值解与真解之间的误差，以便于在实际计算中根据精度要求确定计算方案。在Euler法中产生的误差称为截断误差。

其次，计算过程中还会由于数值误差的舍入产生舍入误差。由于Euler法是一种步进方法，只有当最初产生的误差在以后各步的计算中不会无限制扩大时，即只有当 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.1%29) 的解对初值具有某种连续相依性质时，方法才具有实用价值。这种性质称为稳定性问题。

**1.1.3 Euler法的截断误差估计**

首先讨论Euler法的截断误差估计及收敛性问题。初值问题 ![[公式]](https://www.zhihu.com/equation?tex=%281.0.1%29) 可以写成等价的积分形式 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%2Bh%29%3Du%28t%29%2B%5Cint%5E%7Bt%2Bh%7D_%7Bt%7Df%28%5Ctau%2Cu%28%5Ctau%29%29d%5Ctau%5C+%281.1.2%29) 

在上式中，令 ![[公式]](https://www.zhihu.com/equation?tex=t%3Dt_n) ，并用左矩形公式计算右端积分，有

![[公式]](https://www.zhihu.com/equation?tex=u%28t_%7Bn%2B1%7D%29%3Du%28t_n%29%2B%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7Df%28%5Ctau%2Cu%28%5Ctau%29%29d%5Ctau) ![[公式]](https://www.zhihu.com/equation?tex=%3Du%28t_n%29%2B%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%5Bf%28%5Ctau%2Cu%28%5Ctau%29-f%28t_n%2Cu%28t_n%29%29%5Dd%5Ctau%2B%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7Df%28t_n%2Cu%28t_n%29%29d%5Ctau) ![[公式]](https://www.zhihu.com/equation?tex=%3Du%28t_n%29%2Bhf%28t_n%2Cu%28t_n%29%29%2B%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%5Bf%28%5Ctau%2Cu%28%5Ctau%29-f%28t_n%2Cu%28t_n%29%29%5Dd%5Ctau) ![[公式]](https://www.zhihu.com/equation?tex=%3Du%28t_n%29%2Bhf%28t_n%2Cu%28t_n%29%29%2BR_n%5C+%281.1.3%29) 

![[公式]](https://www.zhihu.com/equation?tex=R_n) 称为Euler法的局部截断误差，它表示当 ![[公式]](https://www.zhihu.com/equation?tex=u_n%3Du%28t_n%29) 为精确值时，利用公式 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.1%29) 计算 ![[公式]](https://www.zhihu.com/equation?tex=u%28t_n%2Bh%29) 的误差。在逐步计算的过程中，局部截断误差会传播和积累，因此还必须对这种误差的积累与传播作出估计。

设 ![[公式]](https://www.zhihu.com/equation?tex=u_n) 是在无舍入误差情况下用 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.1%29) 计算出的数值解，而 ![[公式]](https://www.zhihu.com/equation?tex=u%28t_n%29) 是真解， ![[公式]](https://www.zhihu.com/equation?tex=%5Cepsilon_n%3Du%28t_n%29-u_n) 为Euler法 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.1%29) 的整体截断误差。

为估计 ![[公式]](https://www.zhihu.com/equation?tex=%5Cepsilon_n) ，先给出 ![[公式]](https://www.zhihu.com/equation?tex=R_n) 的上界。从式 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.3%29) 知，

![[公式]](https://www.zhihu.com/equation?tex=R_n%3D%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%5Bf%28%5Ctau%2Cu%28%5Ctau%29-f%28t_n%2Cu%28t_n%29%29%5Dd%5Ctau) ![[公式]](https://www.zhihu.com/equation?tex=%3D%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%5Bf%28%5Ctau%2Cu%28%5Ctau%29-f%28t_n%2Cu%28%5Ctau%29%29%5Dd%5Ctau%2B%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%5Bf%28t_n%2Cu%28%5Ctau%29-f%28t_n%2Cu%28t_n%29%29%5Dd%5Ctau) 

若函数 ![[公式]](https://www.zhihu.com/equation?tex=f%28t%2Cu%29) 关于 ![[公式]](https://www.zhihu.com/equation?tex=t) 也满足Lipschitz条件，以 ![[公式]](https://www.zhihu.com/equation?tex=K) 记相应的Lipschitz常数，则由上式推出 ![[公式]](https://www.zhihu.com/equation?tex=%7CR_n%7C%5Cleq%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%5CBig%7Cf%28%5Ctau%2Cu%28%5Ctau%29-f%28t_n%2Cu%28%5Ctau%29%29%5CBig%7Cd%5Ctau%2B%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%5CBig%7Cf%28t_n%2Cu%28%5Ctau%29-f%28t_n%2Cu%28t_n%29%29%5CBig%7Cd%5Ctau) ![[公式]](https://www.zhihu.com/equation?tex=%5Cleq+K%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%7C%5Ctau-t_n%7Cd%5Ctau%2BL%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%7Cu%28%5Ctau%29-u%28t_n%29%7Cd%5Ctau) ![[公式]](https://www.zhihu.com/equation?tex=%5Cleq+K%5Cint%5E%7Bh%7D_%7B0%7D%7Cu%7Cdu%2BhL%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7D%7C%5Cfrac%7Bu%28%5Ctau%29-u%28t_n%29%7D%7Bh%7D%7Cd%5Ctau) ![[公式]](https://www.zhihu.com/equation?tex=%5Cleq+K%5Cint%5E%7Bh%7D_%7B0%7Dudu%2BhL%5Cint%5E%7Bt_%7Bn%2B1%7D%7D_%7Bt_n%7DMd%5Ctau%3D%5Cfrac%7B1%7D%7B2%7Dh%5E2K%2Bh%5E2LM%5Cleq+h%5E2%28K%2BLM%29) 

其中 ![[公式]](https://www.zhihu.com/equation?tex=M%3D%5Cmax_%7Bt_0%5Cleq+t%5Cleq+T%7D%7Cu%27%28t%29%7C%3D%5Cmax_%7Bt_0%5Cleq+t%5Cleq+T%7D%7Cf%28t%2Cu%28t%29%29%7C) ，于是 ![[公式]](https://www.zhihu.com/equation?tex=%7CR_n%7C%5Cleq+R%3Dh%5E2%28K%2BLM%29) 

用式 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.3%29) 减去式 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.1%29) ，得到整体截断误差所满足的方程

![[公式]](https://www.zhihu.com/equation?tex=%5Cepsilon_%7Bn%2B1%7D%3D%5Cepsilon_%7Bn%7D%2Bh%5Bf%28t_n%2Cu%28t_n%29%29-f%28t_n%2Cu_n%29%5D%2BR_n) ，进一步可以得到

![[公式]](https://www.zhihu.com/equation?tex=%7C%5Cepsilon_%7Bn%2B1%7D%7C%5Cleq%7C%5Cepsilon_%7Bn%7D%7C%2Bh%7Cf%28t_n%2Cu%28t_n%29%29-f%28t_n%2Cu_n%29%7C%2BR+) ![[公式]](https://www.zhihu.com/equation?tex=%5Cleq%7C%5Cepsilon_n%7C%2BhL%7C%5Cepsilon_n%7C%2BR) ![[公式]](https://www.zhihu.com/equation?tex=%3D%281%2BhL%29%7C%5Cepsilon_n%7C%2BR%5Cleq%281%2B%28T-t_0%29L%29%7C%5Cxi_n%7C%2BR) 

这是一个递推公式，我们需要得到对任意 ![[公式]](https://www.zhihu.com/equation?tex=n) 均成立的上界。下面的引理能够做到这一点。

**引理1.1.1** 设数列 ![[公式]](https://www.zhihu.com/equation?tex=%5Cxi_i) 满足不等式 ![[公式]](https://www.zhihu.com/equation?tex=%7C%5Cxi_%7Bi%2B1%7D%7C%5Cleq%281%2B%5Cdelta%29%7C%5Cxi_i%7C%2BB%2C) ， 其中![[公式]](https://www.zhihu.com/equation?tex=%5C+%5Cdelta%3E0%2C%5C+B%5Cgeq0%2C%5C+i%3D0%2C1%2C2%2C...) ，则有 ![[公式]](https://www.zhihu.com/equation?tex=%7C%5Cxi_i%7C%5Cleq+e%5E%7Bi%5Cdelta%7D%7C%5Cxi_0%7C%2B%5Cfrac%7Be%5E%7Bi%5Cdelta%7D-1%7D%7B%5Cdelta%7DB%2C%5C+i%3E1) 。

由此我们可以得到整体截断误差的估计 ![[公式]](https://www.zhihu.com/equation?tex=%7C%5Cepsilon_n%7C%5Cleq+e%5E%7BL%28T-t_0%29%7D%7C%5Cepsilon_0%7C%2B%5Cfrac%7Bh%7D%7B2%7D%28e%5E%7BL%28T-t_0%29%7D-1%29%28%5Cfrac%7BLM%2BK%7D%7BL%7D%29%5C+%281.1.5%29) 

从 ![[公式]](https://www.zhihu.com/equation?tex=u_0%3Du%28t_0%29) 及式 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.5%29) ，又知 ![[公式]](https://www.zhihu.com/equation?tex=%5Cepsilon_n%3DO%28h%29%EF%BC%8Ch%5Crightarrow0) ，即Euler法的整体阶段误差与 ![[公式]](https://www.zhihu.com/equation?tex=h) 同阶，此时称Euler法为一阶方法。它的直观意义是，当 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%29) 是一次多项式时，Euler法是精确的。

**1.1.4 Euler法的稳定性**

这里考虑仅初值 ![[公式]](https://www.zhihu.com/equation?tex=u_0) 有误差，而其他计算步骤无误差的简单情况。

...

上述结论所表述的Euler法的性质，及所谓关于初值的稳定性：当初始误差充分小时，以后各步的误差也可充分小。

**1.1.5 梯形法**

由式 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.2%29) ，取 ![[公式]](https://www.zhihu.com/equation?tex=t%3Dt_n) ，并用梯形求积公式计算右端积分，舍去每一步梯形求积公式的余项，可以得到梯形法的计算公式 ![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Bcases%7D+u_0%3Du_0%5C%5C+u_%7Bn%2B1%7D%3Du_n%2B%5Cfrac%7Bh%7D%7B2%7D%5Bf_n%2Bf_%7Bn%2B1%7D%5D%2Cn%5Cgeq0%5C%5C+%5Cend%7Bcases%7D+) 

对于梯形法，可类似地建立其截断误差估计式及收敛性，且 ![[公式]](https://www.zhihu.com/equation?tex=%7Cu%28t_n%29-u_n%7C%3DO%28h%5E2%29%2Ch%5Crightarrow0) ，此时称梯形法为二阶方法。

这里要注意梯形法与Euler法的一个重要区别，即式 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.8%29) 只给出一个关于 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D) 的（非线性）方程，而Euler法给出的是 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D) 的显式表达式，因此Euler法是一个显式方法，而梯形法是隐式方法。

当梯形法求 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D) 时，可利用求解非线性方程的各种方法，最简单的是下述迭代方法： ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D%5E%7B%28m%2B1%29%7D%3Du_n%2B%5Cfrac%7Bh%7D%7B2%7D%5Bf_n%2Bf%28t_%7Bn%2B1%7D%2Cu_%7Bn%2B1%7D%5E%7B%28m%29%7D%29%5D%2Cm%5Cgeq0) 。

实际计算时，初始近似 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D%5E%7B%280%29%7D) 可用Euler法求出，然后再使用迭代法，这便是预测校正格式（又称为改进Euler法）：

![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Bcases%7D+u_%7Bn%2B1%7D%5E%7B%280%29%7D%3Du_n%2Bhf%28t_%7Bn%7D%2Cu_n%29%5C%5C+u_%7Bn%2B1%7D%5E%7B%28m%2B1%29%7D%3Du_n%2B%5Cfrac%7Bh%7D%7B2%7D%5Bf_n%2Bf%28t_%7Bn%2B1%7D%2Cu_%7Bn%2B1%7D%5E%7B%28m%29%7D%29%5D%2Cm%5Cgeq0%5C%5C+%5Cend%7Bcases%7D) 

**1.1.6 总结**

通过上述两个方法的讨论可知，数值方法的研究有如下基本问题：计算公式的构造，方法的收敛性，截断误差估计，稳定性及方法的实际应用等。

## **1.2 Runge-Kutta方法及一般单步方法**

前节介绍的两个方法精度是很低的。本节从提高局部截断误差阶入手，来构造具有较高精度的方法。

**1.2.1 Taylor级数法**

设初值问题 ![[公式]](https://www.zhihu.com/equation?tex=%281.0.1%29)  的解 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%29) 具有 ![[公式]](https://www.zhihu.com/equation?tex=q%2B1) 次连续导数。考虑 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%29) 在 ![[公式]](https://www.zhihu.com/equation?tex=t%3Dt_0) 处的Taylor展开式，可得局部截断误差 ![[公式]](https://www.zhihu.com/equation?tex=u%28t_0%2Bh%29-u_1%3DO%28h%5E%7Bq%2B1%7D%29) 。

...

这种方法称为Taylor级数法。虽然它的局部截断误差的阶可任意高，但各阶导数 ![[公式]](https://www.zhihu.com/equation?tex=u%5E%7B%28i%29%7D%28t%29) 的计算量非常大，不实用。现在介绍一类既可以达到较高精度，又可避免高阶导数计算的方法——Runge-Kutta方法。

**1.2.2 RK方法**

根据公式 ![[公式]](https://www.zhihu.com/equation?tex=%281.1.2%29) 及积分中值定理 ![[公式]](https://www.zhihu.com/equation?tex=%5Cint%5E%7Bt%2Bh%7D_%7Bt%7Df%28%5Ctau%2Cu%28%5Ctau%29%29d%5Ctau+%3Dhf%28t_n%2B%5Ctheta+h%2Cu%28t_n%2B%5Ctheta+h%29%29) ，可得 ![[公式]](https://www.zhihu.com/equation?tex=u%28t_n%2Bh%29%3Du%28t_n%29%2Bhf%28t_n%2B%5Ctheta+h%2Cu%28t_n%2B%5Ctheta+h%29%29+%5C+%281.2.3%29) 。

但 ![[公式]](https://www.zhihu.com/equation?tex=f%28t_n%2B%5Ctheta+h%2Cu%28t_n%2B%5Ctheta+h%29%29)是无法计算的。我们用 ![[公式]](https://www.zhihu.com/equation?tex=f) 在位于 ![[公式]](https://www.zhihu.com/equation?tex=%5Bt_n%2Ct_n%2Bh%5D) 上的若干个点（例如 ![[公式]](https://www.zhihu.com/equation?tex=s) 个点）值的线性组合来近似它，并使之有尽可能高的精度。具体来讲，就是用下列公式代替式 ![[公式]](https://www.zhihu.com/equation?tex=%281.2.3%29) ![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Bequation%7D+u_%7Bn%2B1%7D%3Du%28t_n%29%2Bh%5Csum%5E%7Bs%7D_%7Bi%3D1%7DW_iK_i%5C+%281.2.4%29%5C%5C+++%5Cbegin%7Bcases%7D+K_1%3Df%28t_n%2Cu%28t_n%29%29%EF%BC%8C%5C%5C+K_i%3Df%28t_n%2Bh%5Calpha_i%2Cu%28t_n%29%2Bh%5Csum%5E%7Bi-1%7D_%7Bj%3D1%7D%5Cbeta_%7Bij%7DK_i%29%5C+%5C%5C+%5Cend%7Bcases%7D%281.2.5%29%5C%5C+%5Cend%7Bequation%7D%5C+) 

现在去选定系数 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha_i%2C%5Cbeta_%7Bij%7D%28i%5Cgeq2%29) ，以及 ![[公式]](https://www.zhihu.com/equation?tex=W_i%28i%5Cgeq1%29) ，使RK方法的整体截断误差具有尽可能高的阶 ![[公式]](https://www.zhihu.com/equation?tex=q) ，这个阶数 ![[公式]](https://www.zhihu.com/equation?tex=q) 当然与级数 ![[公式]](https://www.zhihu.com/equation?tex=s) 有关，可记为 ![[公式]](https://www.zhihu.com/equation?tex=q%28s%29) 。

构造RK方法的基本步骤是，选定上述系数，使 ![[公式]](https://www.zhihu.com/equation?tex=u%28t_n%2Bh%29-u%28t_n%29) 与 ![[公式]](https://www.zhihu.com/equation?tex=h%5Csum%5E%7Bs%7D_%7Bi%3D1%7DW_iK_i) 两者的Taylor展开式中含 ![[公式]](https://www.zhihu.com/equation?tex=h%5Er%28r%3D1%2C...%2Cq%29) 的项的系数对尽可能大的 ![[公式]](https://www.zhihu.com/equation?tex=q) 相等。

书上考虑的是 ![[公式]](https://www.zhihu.com/equation?tex=s%3D4) 的情况，在这里我们只考虑 ![[公式]](https://www.zhihu.com/equation?tex=s%3D2) 的情况。

\------------------------------------------------------------------

由一元函数Taylor展开可得

![[公式]](https://www.zhihu.com/equation?tex=u%28t_n%2Bh%29-u%28t_n%29%3Du%27%28t_n%29h%2Bu%27%27%28t_n%29%5Cfrac%7Bh%5E2%7D%7B2%7D%2BO%28h%5E3%29) ![[公式]](https://www.zhihu.com/equation?tex=%3Df%28t_n%2Cu%28t_n%29%29h%2B%5CBig%5Bf_t%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%2Bf_u%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29f%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%5CBig%5D%5Cfrac%7Bh%5E2%7D%7B2%7D%2BO%28h%5E3%29) ![[公式]](https://www.zhihu.com/equation?tex=%3Dhf%28t_n%2Cu%28t_n%29%29%2B%5Cfrac%7Bh%5E2%7D%7B2%7Df_t%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%2B%5Cfrac%7Bh%5E2%7D%7B2%7Df_u%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29f%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%2BO%28h%5E3%29) 

由二元函数的Taylor展开可得

![[公式]](https://www.zhihu.com/equation?tex=K_2%3Df%28t_n%2Ba_2h%2Cu%28t_n%29%2B%5Cbeta_%7B21%7DK_1h%29) 

![[公式]](https://www.zhihu.com/equation?tex=%3Df%28t_n%2Cu%28t_n%29%29%2Bf_t%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%5Calpha_2h%2Bf_u%28t_n%2Cu%28t_n%29%29%5Cbeta_%7B21%7DK_1h) ![[公式]](https://www.zhihu.com/equation?tex=%2BO%28h%5E2%29) 

![[公式]](https://www.zhihu.com/equation?tex=%3Df%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%2Bf_t%28t_n%2Cu%28t_n%29%29%5Calpha_2h%2Bf%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29f_u%28t_n%2Cu%28t_n%29%29%5Cbeta_%7B21%7Dh) ![[公式]](https://www.zhihu.com/equation?tex=%2BO%28h%5E2%29%5C+%28RK.2%29) 

将 ![[公式]](https://www.zhihu.com/equation?tex=%28RK.2%29) 代入 ![[公式]](https://www.zhihu.com/equation?tex=%281.2.4%29) 可得 

![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D-u%28t_n%29%3Dh%28W_1K_1%2BW_2K_2%29%3DhW_1K_1%2BhW_2K_2)![[公式]](https://www.zhihu.com/equation?tex=%3DhW_1f%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%2BhW_2%5CBig%28f%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%2Bf_t%28t_n%2Cu%28t_n%29%29%5Calpha_2h) ![[公式]](https://www.zhihu.com/equation?tex=%2Bf%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29f_u%28t_n%2Cu%28t_n%29%29%5Cbeta_%7B21%7Dh%2BO%28h%5E2%29%5CBig%29)![[公式]](https://www.zhihu.com/equation?tex=%3DhW_1f%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%2BhW_2f%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%2Bh%5E2W_2%5Calpha_2f_t%28t_n%2Cu%28t_n%29%29)![[公式]](https://www.zhihu.com/equation?tex=%2Bh%5E2W_2%5Cbeta_%7B12%7Df%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29f_u%28t_n%2Cu%28t_n%29%29%2BO%28h%5E3%29%5C)

![[公式]](https://www.zhihu.com/equation?tex=%3D%28W_1%2BW_2%29hf%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29%2BW_2%5Calpha_2h%5E2f_t%28t_n%2Cu%28t_n%29%29) ![[公式]](https://www.zhihu.com/equation?tex=%2BW_2%5Cbeta_%7B12%7Dh%5E2f%5Cbig%28t_n%2Cu%28t_n%29%5Cbig%29f_u%28t_n%2Cu%28t_n%29%29%2BO%28h%5E3%29) 

比较 ![[公式]](https://www.zhihu.com/equation?tex=%28RK.1%29) 与 ![[公式]](https://www.zhihu.com/equation?tex=%28RK.3%29) ，使 ![[公式]](https://www.zhihu.com/equation?tex=h%5Er%28r%3D1%2C2%29) 的系数相等，得

![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Bcases%7D+W_1%2BW_2%3D1%5C%5C+W_2%5Calpha_2%3D%5Cfrac%7B1%7D%7B2%7D%5C%5C+W_2%5Cbeta_%7B21%7D%3D%5Cfrac%7B1%7D%7B2%7D%5C%5C+%5Cend%7Bcases%7D) ，即 ![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Bcases%7D+W_1%2BW_2%3D1%5C%5C+W_2%5Calpha_2%3D%5Cfrac%7B1%7D%7B2%7D%5C%5C+%5Cbeta_%7B21%7D%3D%5Calpha_2%5C%5C+%5Cend%7Bcases%7D) 

取不同的 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha_2) ，可以得到不同的2级RK公式。

（以上 ![[公式]](https://www.zhihu.com/equation?tex=s%3D2) 情况的推导与书本无关）

\------------------------------------------------------------------

...

含 ![[公式]](https://www.zhihu.com/equation?tex=h%5Er%28r%3D1%2C2%2C3%2C4%29) 项的系数对应相等，且一般不能再使含 ![[公式]](https://www.zhihu.com/equation?tex=h%5E5)项的系数相等，故所得方法的局部截断误差为 ![[公式]](https://www.zhihu.com/equation?tex=O%28h%5E5%29) ，即方法是四阶的。

...

从这些公式的讨论得知，当 ![[公式]](https://www.zhihu.com/equation?tex=s%5Cleq4) 时， ![[公式]](https://www.zhihu.com/equation?tex=s) 级RK方法的阶 ![[公式]](https://www.zhihu.com/equation?tex=q%28s%29%3Ds) ；当 ![[公式]](https://www.zhihu.com/equation?tex=s%3D5%2C6%2C7) ， ![[公式]](https://www.zhihu.com/equation?tex=q%28s%29%3Ds-1) ；当 ![[公式]](https://www.zhihu.com/equation?tex=s%3D8%2C9) ， ![[公式]](https://www.zhihu.com/equation?tex=q%28s%29%3Ds-2) ； ![[公式]](https://www.zhihu.com/equation?tex=q%2810%29%5Cleq8) 。可见，对于四级以上的公式，计算函数值的计算量增加较快，而精度即阶数提高较慢，因此在实际问题中比较常用的是四级RK公式。

**1.2.3 单步法的相容性与收敛性**

无论是Euler法还是各级RK法，他们都是在已知 ![[公式]](https://www.zhihu.com/equation?tex=u_n) 的条件下算出 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D) ，因此称为显式单步方法，简称为单步方法。这类方法的一般形式为 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D%3Du_n%2Bh%5Cvarphi%28t_n%2Cu_n%2Ch%29%5C+%281.2.28%29) ，其中 ![[公式]](https://www.zhihu.com/equation?tex=%5Cvarphi%28t%2Cu%2Ch%29) 称为方法 ![[公式]](https://www.zhihu.com/equation?tex=%281.2.28%29) 的增量函数，它是依赖于 ![[公式]](https://www.zhihu.com/equation?tex=u) 及 ![[公式]](https://www.zhihu.com/equation?tex=f) 的非线性函数（此处为简单计，略写了 ![[公式]](https://www.zhihu.com/equation?tex=%5Cvarphi) 对 ![[公式]](https://www.zhihu.com/equation?tex=f) 的依赖关系）。

在前面的讨论中，我们一再提到了每个具体方法的阶，现对单步方法 ![[公式]](https://www.zhihu.com/equation?tex=%281.2.8%29) 给出阶的一般定义。

定义1.2.1 单步方法 ![[公式]](https://www.zhihu.com/equation?tex=%281.2.28%29) 称为是 ![[公式]](https://www.zhihu.com/equation?tex=q) 阶的，如果对于真解 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%29) ， ![[公式]](https://www.zhihu.com/equation?tex=q) 是使关系式 ![[公式]](https://www.zhihu.com/equation?tex=u%28t%2Bh%29-u%28t%29%3Dh%5Cvarphi%28t%2Cu%28t%29%2Ch%29%2BO%28h%5E%7Bq%2B1%7D%29) 成立的最大整数。

...

## **1.3 线性多步方法**

在前面所讨论的单步方法中，为提高截断误差的阶，每个时间布必须增加计算右端 ![[公式]](https://www.zhihu.com/equation?tex=f%28t%2Cu%29) 的次数。当 ![[公式]](https://www.zhihu.com/equation?tex=f) 的结构比较复杂时，计算量会比较大。现在指出另一个提高截断误差阶的办法：构造这样的方法，在计算公式中 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D-u_%7Bn%7D) 不仅依赖于 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%7D) ，且也直接依赖于 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn-1%7D%2Cn_%7Bn-2%7D) 等已算出的值，但每进一步，只计算一次 ![[公式]](https://www.zhihu.com/equation?tex=f%28t%2Cu%29) 的值。这样的方法称为多步方法。记 ![[公式]](https://www.zhihu.com/equation?tex=f_n%3Df%28t_n%2Cu_n%29) ，若函数值 ![[公式]](https://www.zhihu.com/equation?tex=f_n%2Cf_%7Bn-1%7D) 等以线性组合的形式出现于公式中，则称方法为线性多步方法。

**1.3.1 数值积分法**

**仍然考虑初值问题** ![[公式]](https://www.zhihu.com/equation?tex=%281.0.1%29) 。易知 ![[公式]](https://www.zhihu.com/equation?tex=u%28t_%7Bn%2Bk%7D%29-u%28t_%7Bn-j%7D%29%3D%5Cint%5E%7Bt_%7Bn%2Bk%7D%7D_%7Bt_%7Bn-j%7D%7Df%28t%2Cu%28t%29%29dt%5C+%281.3.1%29)

我们用被积函数 ![[公式]](https://www.zhihu.com/equation?tex=f%28t%2Cu%28t%29%29) 的 ![[公式]](https://www.zhihu.com/equation?tex=q) 次Lagrange插值多项式 ![[公式]](https://www.zhihu.com/equation?tex=P_q%28t%29%3D%5Csum%5E%7Bq%7D_%7Bi%3D0%7Df%28t_%7Bn-i%7D%2Cu%28t_%7Bn-i%7D%29%29L_i%28t%29) 来近似替代 ![[公式]](https://www.zhihu.com/equation?tex=%281.3.1%29) 中的被积函数，其中![[公式]](https://www.zhihu.com/equation?tex=L_i%28t%29%3D%5Cprod_%7Bl%3D0%2Cl%5Cneq+i%7D%5E%7Bq%7D%5Cfrac%7Bt-t_%7Bn-l%7D%7D%7Bt_%7Bn-i%7D-t_%7Bn-l%7D%7D%3D%5Cprod_%7Bl%3D0%2Cl%5Cneq+i%7D%5E%7Bq%7D%5Cfrac%7Bt-t_n%2Bt_n-t_%7Bn-l%7D%7D%7Bt_%7Bn-i%7D-t_%7Bn-l%7D%7D) ![[公式]](https://www.zhihu.com/equation?tex=%3D%5Cprod_%7Bl%3D0%2Cl%5Cneq+i%7D%5E%7Bq%7D%5Cfrac%7Bt-t_n%2Blh%7D%7B%28-i%2Bl%29h%7D) ![[公式]](https://www.zhihu.com/equation?tex=%3D%5Cprod_%7Bl%3D0%2Cl%5Cneq+i%7D%5E%7Bq%7D%5Cfrac%7B%5Cfrac%7Bt-t_n%7D%7Bh%7D%2Bl%7D%7B%28-i%2Bl%29%7D) ，而有下面的恒等式成立![[公式]](https://www.zhihu.com/equation?tex=%5Cint%5E%7Bt_%7Bn%2Bk%7D%7D_%7Bt_%7Bn-j%7D%7DL_i%28t%29dt%3D%5Cprod_%7Bl%3D0%2Cl%5Cneq+i%7D%5E%7Bq%7D%5Cint%5E%7Bt_%7Bn%7D%2Bkh%7D_%7Bt_%7Bn%7D-jh%7D%5Cfrac%7B%5Cfrac%7Bt-t_n%7D%7Bh%7D%2Bl%7D%7B-i%2Bl%7Ddt+%3Dh%5Cprod_%7Bl%3D0%2Cl%5Cneq+i%7D%5E%7Bq%7D%5Cint%5E%7Bk%7D_%7B-j%7D%5Cfrac%7Bs%2Bl%7D%7B-i%2Bl%7Dds%2C%5C+) ![[公式]](https://www.zhihu.com/equation?tex=i%3D0%2C1%2C...%2Cq) ，插值节点是 ![[公式]](https://www.zhihu.com/equation?tex=t_%7Bn-q%7D%2C...%2Ct_n) 。

于是得到近似公式

![[公式]](https://www.zhihu.com/equation?tex=u%28t_%7Bn%2Bk%7D%29-u%28t_%7Bn-j%7D%29%5Capprox%5Csum%5E%7Bq%7D_%7Bi%3D0%7Df%5Cbig%28t_%7Bn-i%7D%2Cu%28t_%7Bn-i%7D%29%5Cbig%29%5Cint%5E%7Bt_%7Bn%2Bk%7D%7D_%7Bt_%7Bn-j%7D%7DL_i%28t%29dt) ![[公式]](https://www.zhihu.com/equation?tex=%3Dh%5Csum%5E%7Bq%7D_%7Bi%3D0%7D%5CBigg%28%5Cprod_%7Bl%3D0%2Cl%5Cneq+i%7D%5E%7Bq%7D%5Cint%5E%7Bk%7D_%7B-j%7D%5Cfrac%7Bs%2Bl%7D%7B%28-i%2Bl%29%7Dds%5CBigg%29f%5Cbig%28t_%7Bn-i%7D%2Cu%28t_%7Bn-i%7D%29%5Cbig%29) ![[公式]](https://www.zhihu.com/equation?tex=%3Dh%5Csum%5E%7Bq%7D_%7Bi%3D0%7D%5Cbeta_%7Bqi%7Df%5Cbig%28t_%7Bn-i%7D%2Cu%28t_%7Bn-i%7D%29%5Cbig%29%5C+%281.3.2%29) 

在式 ![[公式]](https://www.zhihu.com/equation?tex=%281.3.2%29) 中，用 ![[公式]](https://www.zhihu.com/equation?tex=u_n) 代替 ![[公式]](https://www.zhihu.com/equation?tex=u%28t_n%29) ，仍用 ![[公式]](https://www.zhihu.com/equation?tex=f_n) 表示 ![[公式]](https://www.zhihu.com/equation?tex=f%28t_n%2Cu_n%29) ，用等号代替 ![[公式]](https://www.zhihu.com/equation?tex=%5Capprox) ，则得到线性多步法公式 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2Bk%7D%3Du_%7Bn-j%7D%2Bh%5Csum%5E%7Bq%7D_%7Bi%3D0%7D%5Cbeta_%7Bqi%7Df_%7Bn-i%7D%5C+%281.3.4%29) 

对 ![[公式]](https://www.zhihu.com/equation?tex=k%2Cj) 和 ![[公式]](https://www.zhihu.com/equation?tex=q) 的不同选择，得到不同类型的具体公式。对 ![[公式]](https://www.zhihu.com/equation?tex=k%3D1%2Cj%3D0) 和 ![[公式]](https://www.zhihu.com/equation?tex=q%3D0%2C1%2C...) ，我们得到Adams显式方法

![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Bcases%7D+u_%7Bn%2B1%7D%3Du_n%2Bh%28%5Cbeta_%7Bq0%7Df_n%2B%5Cbeta_%7Bq1%7Df_%7Bn-1%7D%2B...%2B%5Cbeta_%7Bqq%7Df_%7Bn-q%7D%29%5C%5C+%5Cbeta_%7Bqi%7D%3D%5Cint%5E%7B1%7D_%7B0%7D%5Cprod%5E%7Bq%7D_%7Bl%3D0%2Cl%5Cneq+1%7D%5Cfrac%7Bs%2Bl%7D%7B-i%2Bl%7Dds%2C%5C+i%3D0%2C1%2C...%2Cq%5C%5C+%5Cend%7Bcases%7D%5C+%281.3.5%29) 

![[公式]](https://www.zhihu.com/equation?tex=q%2B1) 步Adams显式方法和 ![[公式]](https://www.zhihu.com/equation?tex=q) 步Admas隐式方法的局部截断误差都与 ![[公式]](https://www.zhihu.com/equation?tex=h%5E%7Bq%2B2%7D) 同阶，即他们是![[公式]](https://www.zhihu.com/equation?tex=q%2B1) 阶方法。

**1.3.2 待定系数法**

线性 ![[公式]](https://www.zhihu.com/equation?tex=k) 步方法的一般形式为 ![[公式]](https://www.zhihu.com/equation?tex=%5Csum%5E%7Bk%7D_%7Bj%3D0%7D%5Calpha_ju_%7Bn%2Bj%7D%3Dh%5Csum%5E%7Bk%7D_%7Bj%3D0%7D%5Cbeta_jf_%7Bn%2Bj%7D) ，这里 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha_j) 和 ![[公式]](https://www.zhihu.com/equation?tex=%5Cbeta_j) 为实常数（注意这个 ![[公式]](https://www.zhihu.com/equation?tex=h) 先被提了出来），且最大步长系数 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha_k%5Cneq0) ，![[公式]](https://www.zhihu.com/equation?tex=%7C%5Calpha_0%7C%2B%7C%5Cbeta_0%7C%3E0) （其他系数都有可能为0）。为讨论方便，改为以 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2Bk%7D) 为未知量， ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2Bk-1%7D%2C...%2Cu_n) 为已知量。我们用待定系数法来构造这种公式。

...

## **1.6 数值稳定性**

前面各节，对一个数值方法进行理论分析时，引进了相容性，收敛性等有关概念。此时，我们作出过共同的假设，即 ![[公式]](https://www.zhihu.com/equation?tex=h%5Crightarrow0) 。这些概念在数值分析中虽然很重要，但还没有充分考虑到实际计算过程的主要特征：步长 ![[公式]](https://www.zhihu.com/equation?tex=h) 由于计算工具等条件的限制，不可能任意取小，更不要说趋于零。另一方面，由于每计算一步，总会产生舍入误差，而且这些舍入误差还要步步传播下去，步数增多就有可能使误差累积到影响数值解的精度，甚至于淹没了所求的近似解。因此，从实际计算的角度来看，反而要求步长 ![[公式]](https://www.zhihu.com/equation?tex=h) 尽可能大些。对有限的步长 ![[公式]](https://www.zhihu.com/equation?tex=h) ，考察一个方法对舍入误差的敏感性，这就是数值稳定性问题。这不但与计算公式有关，而且与微分方程本身的性质有关。

### **1.6.1 线性多步方法的绝对稳定性**

首先考察一个数值例子。

...

从这个数值表看到，当用有限步长 ![[公式]](https://www.zhihu.com/equation?tex=h%3D0.1) 进行 ![[公式]](https://www.zhihu.com/equation?tex=40) 余步的计算之后，所得数值解与真解之值偏离相当大，已无法作为近似解提供使用。但我们知道，Milne方法 ![[公式]](https://www.zhihu.com/equation?tex=%281.6.1%29) 是收敛的二步四阶方法，在所有的二步方法中精度阶最高，应该给出较好的数值计算结果。为什么会出现这种反常的不稳定现象？一个方法具有什么性质才能避免上述不稳定现象？这正是本节要讨论的问题。

首先假设所考虑的线性多步方法是收敛的。对于一般的线性 ![[公式]](https://www.zhihu.com/equation?tex=k) 步方法 ![[公式]](https://www.zhihu.com/equation?tex=%5Csum%5E%7Bk%7D_%7Bj%3D0%7D%5Calpha_ju_%7Bn%2Bj%7D%3Dh%5Csum%5E%7Bk%7D_%7Bj%3D0%7D%5Cbeta_jf_%7Bn%2Bj%7D%5C+%281.6.2%29) 

...

为了对 ![[公式]](https://www.zhihu.com/equation?tex=e_n) 的性质进行分析，我们作两个简化问题的假设：...；二是 ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7B%5Cpartial+f%7D%7B%5Cpartial+u%7D%3D%5Cmu%3D%5Crm+const.) ，即此时所考虑的是模型方程 ![[公式]](https://www.zhihu.com/equation?tex=u%27%3D%5Cmu+u) 的求解问题。

...

记 ![[公式]](https://www.zhihu.com/equation?tex=%5Coverline%7Bh%7D%3D%5Cmu+h) ，用 ![[公式]](https://www.zhihu.com/equation?tex=%5Cxi_j%3D%5Cxi_j%28%5Coverline%7Bh%7D%29) 表示稳定多项式 ![[公式]](https://www.zhihu.com/equation?tex=%5Cpi%28%5Clambda%3B%5Coverline%7Bh%7D%29%5Cequiv%5Crho%28%5Clambda%29-%5Coverline%7Bh%7D%5Csigma%28%5Clambda%29%5C+%281.6.7%29) 的零点，其中 ![[公式]](https://www.zhihu.com/equation?tex=%5Crho%28%5Clambda%29%3D%5Clambda%5Ek%2B%5Csum%5E%7Bk-1%7D_%7Bj%3D0%7D%5Calpha_j%5Clambda%5Ej%2C%5C+%5Csigma%28%5Clambda%29%3D%5Csum%5E%7Bk%7D_%7Bj%3D0%7D%5Cbeta_j%5Clambda%5Ej) 。

...

我们感兴趣的不是对 ![[公式]](https://www.zhihu.com/equation?tex=e_n) 大小的估计，而是判定当 ![[公式]](https://www.zhihu.com/equation?tex=n) 增大时， ![[公式]](https://www.zhihu.com/equation?tex=e_n) 是随着增大还是减小或是振荡的问题。若 ![[公式]](https://www.zhihu.com/equation?tex=e_n) 是在减小，那就是说每步计算所产生的舍入误差对以后计算结果的影响在减弱，即可受到控制。据此，我们引进绝对稳定性的概念。

**定义1.6.1** 若对于给定的 ![[公式]](https://www.zhihu.com/equation?tex=%5Coverline%7Bh%7D%3D%5Cmu+h) ，稳定多项式 ![[公式]](https://www.zhihu.com/equation?tex=%5Cpi%28%5Clambda%3B%5Coverline%7Bh%7D%29) 的所有根 ![[公式]](https://www.zhihu.com/equation?tex=%5Cxi_j) 都满足 ![[公式]](https://www.zhihu.com/equation?tex=%7C%5Cxi_j%7C%3C1%2Cj%3D1%2C...%2Ck) ，则称方法 ![[公式]](https://www.zhihu.com/equation?tex=%281.6.2%29) 关于 ![[公式]](https://www.zhihu.com/equation?tex=%5Coverline%7Bh%7D) 是绝对稳定的；若对实轴上的某区间（或复平面上某区域）内的**任意** ![[公式]](https://www.zhihu.com/equation?tex=%5Coverline%7Bh%7D) ，方法都是绝对稳定的，则称此区间（或区域）为绝对稳定区间（或区域）。

**Euler法**

计算公式为 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D%3Du_n%2Bhf_n) 。对模型方程 ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7Bdu%7D%7Bdt%7D%3Df%3D%5Cmu+u) ，可化为 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D-u_n%3Dh%5Cmu+u_n) 

这是线性 ![[公式]](https://www.zhihu.com/equation?tex=1) 步方法， ![[公式]](https://www.zhihu.com/equation?tex=k%3D1)， ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha_0%3D-1%2C%5Calpha_1%3D1%2C) ![[公式]](https://www.zhihu.com/equation?tex=%5Cbeta_0%3D%5Cfrac%7B%5Cmu%7D%7Bh%7D%2C%5Cbeta_1%3D0) ，![[公式]](https://www.zhihu.com/equation?tex=%5Crho%28%5Clambda%29%3D%5Clambda%2B%5Calpha_0%3D%5Clambda-1%2C%5Csigma%28%5Clambda%29%3D%5Cfrac%7B%5Cmu%7D%7Bh%7D)

稳定多项式为 ![[公式]](https://www.zhihu.com/equation?tex=%5Cpi%28%5Clambda%3B%5Coverline%7Bh%7D%29%3D%5Crho%28%5Clambda%29-%5Coverline%7Bh%7D%5Csigma%28%5Clambda%29%3D%5Clambda-1-%5Coverline%7Bh%7D%5Cfrac%7B%5Cmu%7D%7Bh%7D%3D%5Clambda-%281%2B%5Coverline%7Bh%7D%29) 

绝对稳定区域满足 ![[公式]](https://www.zhihu.com/equation?tex=%7C1%2B%5Coverline%7Bh%7D%7C%3C1) 。当 ![[公式]](https://www.zhihu.com/equation?tex=%5Cmu) 为复常数时，上式表示复平面上以 ![[公式]](https://www.zhihu.com/equation?tex=-1) 为中心的单位圆域内部。当 ![[公式]](https://www.zhihu.com/equation?tex=%5Cmu)  为实常数时，绝对稳定区间为实轴上的线段 ![[公式]](https://www.zhihu.com/equation?tex=%28-2%2C0%29) 。

**向后Euler法**

计算公式为 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D%3Du_n%2Bhf_%7Bn%2B1%7D) 。稳定多项式 ![[公式]](https://www.zhihu.com/equation?tex=%5Cpi%28%5Clambda%3B%5Coverline%7Bh%7D%29%3D%281-%5Coverline%7Bh%7D%29%5Clambda-1) 。绝对稳定区间满足 ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7B1%7D%7B%7C1-%5Coverline%7Bh%7D%7C%7D%3C1) ， ![[公式]](https://www.zhihu.com/equation?tex=%7C1-%5Coverline%7Bh%7D%7C%3E1) ，即方法的绝对稳定区域为复平面上以 ![[公式]](https://www.zhihu.com/equation?tex=%2B1) 为中心的单位圆域外部。特别地，当 ![[公式]](https://www.zhihu.com/equation?tex=Re%5C+%5Cmu%3C0) 时，方法绝对稳定。若 ![[公式]](https://www.zhihu.com/equation?tex=%5Cmu) 为实常数，绝对稳定区间为 ![[公式]](https://www.zhihu.com/equation?tex=%28-%5Cinfty%2C0%29%5Ccup%282%2C%5Cinfty%29) 。

**梯形法**

计算公式为 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bn%2B1%7D%3Du_n%2B%5Cfrac%7B1%7D%7B2%7D%28f_n%2Bf_%7Bn%2B1%7D%29) 

稳定多项式为 ![[公式]](https://www.zhihu.com/equation?tex=%5Cpi%28%5Clambda%3B%5Coverline%7Bh%7D%29%3D%281-%5Cfrac%7B1%7D%7B2%7D%5Coverline%7Bh%7D%29%5Clambda-%281%2B%5Cfrac%7B1%7D%7B2%7D%5Coverline%7Bh%7D%29) 

绝对稳定区间满足 ![[公式]](https://www.zhihu.com/equation?tex=%7C%5Cxi_1%7C%3D%5CBigg%7C%5Cfrac%7B%281%2B%5Cfrac%7B1%7D%7B2%7D%5Coverline%7Bh%7D%29%7D%7B%281-%5Cfrac%7B1%7D%7B2%7D%5Coverline%7Bh%7D%29%7D%5CBigg%7C%3C1) 。当 ![[公式]](https://www.zhihu.com/equation?tex=Re%5C+%5Cmu%3C0) 时，总有 ![[公式]](https://www.zhihu.com/equation?tex=%7C%5Cxi_1%7C%3C1) ，故方法的绝对稳定区间为左半复平面 ![[公式]](https://www.zhihu.com/equation?tex=Re%5C+%5Cmu%3C0) ，而绝对稳定区间为 ![[公式]](https://www.zhihu.com/equation?tex=%28-%5Cinfty%2C0%29) 。

**改进Euler法**

计算公式为 ![[公式]](https://www.zhihu.com/equation?tex=%5Cbegin%7Bcases%7D+u_%7Bn%2B1%7D%5E%7B%280%29%7D%3Du_n%2Bhf%28t_%7Bn%7D%2Cu_n%29%5C%5C+u_%7Bn%2B1%7D%5E%7B%28m%2B1%29%7D%3Du_n%2B%5Cfrac%7Bh%7D%7B2%7D%5Bf_n%2Bf%28t_%7Bn%2B1%7D%2Cu_%7Bn%2B1%7D%5E%7B%28m%29%7D%29%5D%2Cm%5Cgeq0%5C%5C+%5Cend%7Bcases%7D) 

稳定多项式为 ![[公式]](https://www.zhihu.com/equation?tex=%5Cpi%28%5Clambda%3B%5Coverline%7Bh%7D%29%3D%5Clambda-%281%2B%5Coverline%7Bh%7D%2B%5Coverline%7Bh%7D%5E2%29) 

绝对稳定区间满足 ![[公式]](https://www.zhihu.com/equation?tex=%7C%5Cxi_1%7C%3D%7C1%2B%5Coverline%7Bh%7D%2B%5Cfrac%7B1%7D%7B2%7D%5Coverline%7Bh%7D%5E2%7C%3D%7C%28%5Cfrac%7B1%7D%7B%5Csqrt%7B2%7D%7D%5Coverline%7Bh%7D%2B%5Csqrt%7B2%7D%29%5E2-1%7C%3C1) ，即 ![[公式]](https://www.zhihu.com/equation?tex=%28%5Cfrac%7B1%7D%7B%5Csqrt%7B2%7D%7D%5Coverline%7Bh%7D%2B%5Csqrt%7B2%7D%29%5E2%5Cleq2%2C+%5Coverline%7Bh%7D%5Cin+C) ，这是一个复椭圆。绝对稳定区间为 ![[公式]](https://www.zhihu.com/equation?tex=%28-2%2C0%29) 。

**二级二阶RK方法**

绝对稳定区间为 ![[公式]](https://www.zhihu.com/equation?tex=%28-2%2C0%29) 。

**四级四阶RK方法**

绝对稳定区间为 ![[公式]](https://www.zhihu.com/equation?tex=%28-2.78%2C0%29) 。

通过本节的讨论可看到，从绝对稳定性的要求来看，对于 ![[公式]](https://www.zhihu.com/equation?tex=Re%5C+%5Cmu%3E0) 的方程，没有什么可靠的算法，因为误差函数随着计算步数 ![[公式]](https://www.zhihu.com/equation?tex=n) 在增长。若从另一个角度来讨论问题，由于方法的收敛性，此时数值解必然随着真解的增长而增长，但只要误差函数的增长速度低于数值解的增长速度，而不影响数值解的精度，所得的计算结果也具有使用价值，这就是所谓的相对稳定性问题。