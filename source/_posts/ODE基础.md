---
title: ODE基础
date: 2020-09-23 00:23:00
tags: 
- math
- ODE
categories:
- math
- ODE
---

## 一、基本概念

在学习常微分方程之前，我们先了解一些基本的概念；我们在中学的时候都学过解方程（如： ![[公式]](https://www.zhihu.com/equation?tex=x%5E2%2B5%3D0) ），不过那都是函数方程（ ![[公式]](https://www.zhihu.com/equation?tex=f%28x%29%3D0) ，即含有未知数x的方程）。

因此，我们就引出了一个新的概念，什么是微分方程？

（1）微分方程：未知函数及其**导数或微分**的关系式，如： ![[公式]](https://www.zhihu.com/equation?tex=y%27%2B5y%3D3x+%28y%3Df%28x%29%29) ）。

由此，我们便可知道函数方程是关于未知数x的，而微分方程是关于x的导数或微分的；微分方程的英文名叫differential equation，简称D.E.。

我们这一章复习的是常微分方程，什么是常微分方程呢，这个“常”又代表什么呢？

（2）常微分方程：**一个**未知函数及其导数或微分的关系式， 如： ![[公式]](https://www.zhihu.com/equation?tex=f%27%28x%29-7f%28x%29%3D0) 。

这个“常”（Ordinary）表示平常，也就是在一般情况（**理想情况**）下的微分方程，即只有一个未知函数；正是因为如此，所以我们在尚未进行特殊说明的情况下，默认D.E.表示常微分方程。

既然我们已经知道了什么是常微分方程了，那么它的解又是什么呢？（有问题，就应该有答案啊）

（3）解：能使D.E的关系式恒成立的函数，形如 ![[公式]](https://www.zhihu.com/equation?tex=y%3Df%28x%29) 。

先回顾一下我们熟悉的函数方程，它的解是什么？是满足函数关系式的未知数，也就是 ![[公式]](https://www.zhihu.com/equation?tex=x%3DC) （C一般为常数）；不难推出D.E.的解也是要满足关系式，是长成 ![[公式]](https://www.zhihu.com/equation?tex=y%3Df%28x%29) 这个样子。

（4）通解：带有常数C的解，如 ：![[公式]](https://www.zhihu.com/equation?tex=y%3DC_1x%5E2%2BC_2e%5Ex) （有两项）。

（5）通积分：隐函数形式的通解，如： ![[公式]](https://www.zhihu.com/equation?tex=f%28y%29+%3D+C_1x%5E2+%2B+C_2e%5Ex) 。

注：某D.E.通解的项和该D.E.的阶相同，即二阶D.E.的通解就有两项，下文会介绍什么是阶。

① ![[公式]](https://www.zhihu.com/equation?tex=%28y%27%29%5E2+%2B+p%28x%29y+%3D+0) 和② ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+f%28x%29) 有什么区别呢？ 

（5）阶：D.E.中的**最高阶导数**或微分称为这个D.E的阶，如：①是1阶，②是2阶。

（6）齐次：D.E.中不含未知函数和常量，如：①是齐次，②是非齐。

（7）线性：D.E中的导数或微分**只有一次**，如：①是二次，②是一次。

注：“线性”这个概念在代数上一般都是指一次，如： ![[公式]](https://www.zhihu.com/equation?tex=y%3D3x) 就是线性的，而 ![[公式]](https://www.zhihu.com/equation?tex=y%3Dx%5E2) 是非线性的；从几何上看也很好理解， ![[公式]](https://www.zhihu.com/equation?tex=y%3D3x) 是一条直线，而 ![[公式]](https://www.zhihu.com/equation?tex=y%3Dx%5E2) 是一条曲线。

（8）定解条件：其实就是一些已知信息，能用来确定解中的常数C。

（9）初始条件：定解条件中最常见的一种，给出初始条件的问题称为初值问题，也叫**柯西问题**。

（10）特解：常数C确定后的通解，称为特解，比如由定解条件确定常数C。

最后，我们来看一下D.E.的两种表现形式。

（11）显函数形式： ![[公式]](https://www.zhihu.com/equation?tex=y%5E%7B%28n%29%7D+%3D+f%28x%2Cy%2Cy%27%2Cy%27%27%2C...%2Cy%5E%7B%28n-1%29%7D%29) 

（12）隐函数形式： ![[公式]](https://www.zhihu.com/equation?tex=f%28x%2Cy%2Cy%27%2Cy%27%27%2C...%2Cy%5E%7B%28n%29%7D%29+%3D+0) 

## 二、求解D.E.

好，我们现在已经了解了有关常微分方程的基本概念，那么我们应该如何去求一个常微分方程的解呢？（一般是求通解，在特定条件下会是求特解）

为了能快速的求解D.E.，通常把D.E分为以下几个类型。

（1）**可分离变量型**：形如 ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7Bdy%7D%7Bdx%7D+%3D+p%28y%29q%28x%29) 

首先，分离变量： ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7B1%7D%7Bp%28y%29%7Ddy+%3D+q%28x%29dx) 

然后，两边积分： ![[公式]](https://www.zhihu.com/equation?tex=%5Cint%5Cfrac%7B1%7D%7Bp%28y%29%7Ddy+%3D+%5Cint+q%28x%29dx+%2BC) （**注意**：自变量一端加常数C，而不定积分的结果就不要加C了）

最后，计算结果。

（2）**齐次型**：形如 ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7Bdy%7D%7Bdx%7D+%3D+f%28%5Cfrac+yx%29) 

首先，换元法：设 ![[公式]](https://www.zhihu.com/equation?tex=u%3D%5Cfrac+yx) ，则 ![[公式]](https://www.zhihu.com/equation?tex=y%3Dxu%2C+%5Cfrac%7Bdy%7D%7Bdx%7D+%3D+%28xu%29%27+%3D+u%2Bx%5Cfrac%7Bdu%7D%7Bdx%7D) 

然后，原式就变成： ![[公式]](https://www.zhihu.com/equation?tex=u%2Bx%5Cfrac%7Bdu%7D%7Bdx%7D+%3D+f%28u%29) 

现在就和分离变量型一样了，如法炮制。

就先，分离变量： ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7B1%7D%7Bf%28u%29-u%7Ddu+%3D+%5Cfrac+1x+dx) 

接着，两边积分： ![[公式]](https://www.zhihu.com/equation?tex=%5Cint%5Cfrac%7B1%7D%7Bf%28u%29-u%7Ddu+%3D+%5Cint%5Cfrac+1x+dx+%2B+C) 

最后，计算结果。

（3）**一阶齐次线性型**：形如 ![[公式]](https://www.zhihu.com/equation?tex=y%27+%2B+p%28x%29y+%3D+0) 

直接套用公式： ![[公式]](https://www.zhihu.com/equation?tex=y%3DCe%5E%7B-%5Cint+p%28x%29dx%7D) 

下面我们来推导这个公式：

![[公式]](https://www.zhihu.com/equation?tex=y%27+%2B+p%28x%29y+%3D+0%5CRightarrow+%5Cfrac%7Bdy%7D%7Bdx%7D%3D-p%28x%29y%5CRightarrow+%5Cfrac+1ydy+%3D+-p%28x%29dx%5CRightarrow+%5Cint%5Cfrac+1ydy+%3D+%5Cint+-p%28x%29dx%2BC_1) 

![[公式]](https://www.zhihu.com/equation?tex=%5CRightarrow+ln%7Cy%7C+%3D+%5Cint+-p%28x%29dx%2BC_1%5CRightarrow+%7Cy%7C+%3D+e%5E%7BC_1%7De%5E%5Cint+-p%28x%29dx%5CRightarrow+y+%3D+%5Cpm+e%5E%7BC_1%7De%5E%5Cint+-p%28x%29dx) 

![[公式]](https://www.zhihu.com/equation?tex=%5CRightarrow+y+%3D+Ce%5E%5Cint+-p%28x%29dx) 

（4）**一阶非齐线性型**：形如 ![[公式]](https://www.zhihu.com/equation?tex=y%27+%2B+p%28x%29y+%3D+q%28x%29) 

直接套用公式： ![[公式]](https://www.zhihu.com/equation?tex=y%3D%28%5Cint+q%28x%29e%5E%7B%5Cint+p%28x%29dx%7D%2BC%29e%5E%7B-%5Cint+p%28x%29dx%7D) 

这里就不推导了，麻烦。

上面我们求解的都是一阶D.E.，下面我们来看看高阶D.E如何求解（主要以二阶为例）。

（5）**可降阶型（双缺）**：形如 ![[公式]](https://www.zhihu.com/equation?tex=y%5E%7B%28n%29%7D+%3D+f%28x%29) 

由基本概念中“某D.E.通解的项和该D.E.的阶相同”可知， ![[公式]](https://www.zhihu.com/equation?tex=y%5E%7B%28n%29%7D+%3D+f%28x%29) 的解为：

![[公式]](https://www.zhihu.com/equation?tex=y%27+%3D+f%28x%29%5CRightarrow+y+%3D+%5Cint+f%28x%29dx+%2BC) 

![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%3D+f%28x%29%5CRightarrow+y%27%3D+%5Cint+f%28x%29dx+%2B+C_1%5CRightarrow+y+%3D+%5Ciint+f%28x%29dx%5E2+%2BC_1x+%2B+C_2%5C) 

![[公式]](https://www.zhihu.com/equation?tex=y%27%27%27+%3D+f%28x%29%5CRightarrow+y%27%27%3D+%5Cint+f%28x%29dx+%2B+C_1%5CRightarrow+y%27+%3D+%5Ciint+f%28x%29dx%5E2+%2BC_1x+%2B+C_2%5CRightarrow+y+%3D+%5Ciiint+f%28x%29dx%5E3+%2BC_1x%5E2+%2B+C_2x+%2B+C_3) 

以此类推：

![[公式]](https://www.zhihu.com/equation?tex=y%5E%7B%28n%29%7D+%3D+f%28x%29%5CRightarrow+y+%3D+%5Ciiint...%5Cint+f%28x%29dx%5En+%2BC_1x%5E%7Bn-1%7D+%2B+C_2x%5E%7Bn-2%7D+%2B+...+%2BC_%7Bn-3%7Dx%5E2+%2B+C_%7Bn-2%7Dx+%2B+C_%7Bn-1%7D) 

（6）**二阶可降阶型（缺y）**：形如 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%3D+f%28x%2Cy%27%29) 

首先，换元法：设 ![[公式]](https://www.zhihu.com/equation?tex=p+%3D+y%27) ，则 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%3D+p%27+%3D+%5Cfrac%7Bdp%7D%7Bdx%7D) 

然后，原式就变成： ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7Bdp%7D%7Bdx%7D+%3D+f%28x%2Cp%29) 

这就化成了一阶线性D.E，最后直接套公式计算结果就好了。

（7）**二阶可降阶型（缺x）**：形如 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%3D+f%28y%2Cy%27%29) 

首先，换元法：设 ![[公式]](https://www.zhihu.com/equation?tex=p+%3D+y%27) ，则 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%3D+p%27+%3D+%5Cfrac%7Bdp%7D%7Bdx%7D) 

然后，原式就变成： ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7Bdp%7D%7Bdx%7D+%3D+f%28y%2Cp%29) 

但是这样就出现了三个字母（p，y，x），我们不希望有三个字母，因为只有两个字母的话，我们就可以如法炮制，变成一阶线性D.E.，然后直接套公式计算了。

所以，我们把 ![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7Bdp%7D%7Bdx%7D+%3D+%5Cfrac%7Bdp%7D%7Bdy%7D+%5Cfrac%7Bdy%7D%7Bdx%7D+%3D+p%5Cfrac%7Bdp%7D%7Bdy%7D) 

于是，原式就变成： ![[公式]](https://www.zhihu.com/equation?tex=p%5Cfrac%7Bdp%7D%7Bdy%7D+%3D+f%28y%2Cp%29) 

这样就只有两个字母了，哈哈可以套公式直接算了。

（8）**二阶常系数齐次线性型**：形如 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+py%27+%2Bqy+%3D+0) 

首先，写出特征方程： ![[公式]](https://www.zhihu.com/equation?tex=%5Clambda+%5E2+%2B+p%5Clambda+%2B+q+%3D+0) 

然后，看有几个根（用求根公式）： ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta+%3D+b%5E2+-+4ac+%3D+p%5E2+-+4q) 

当Δ>0，即 ![[公式]](https://www.zhihu.com/equation?tex=%5Clambda+_1+%5Cne+%5Clambda+_2) ,则： ![[公式]](https://www.zhihu.com/equation?tex=y+%3D+C_1e%5E%7B%5Clambda+_1+x%7D+%2B+C_2e%5E%7B%5Clambda+_2+x%7D) 

当Δ=0，即 ![[公式]](https://www.zhihu.com/equation?tex=%5Clambda+_1+%3D+%5Clambda+_2) ,则： ![[公式]](https://www.zhihu.com/equation?tex=y+%3D+%28C_1%2BC_2x%29e%5E%7B%5Clambda+_1+x%7D) 

当Δ<0，存在共轭复根 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha+%5Cpm+i%5Cbeta) ，则： ![[公式]](https://www.zhihu.com/equation?tex=y+%3D+e%5E%7B%5Calpha+x%7D%28C_1+cos+%5Cbeta+x+%2B+C_2+sin+%5Cbeta+x%29) 

（在中学的时候啊，对于Δ<0的情况，我们就直接说该方程无解，但如果引入虚数的概念，则有一对共轭复根为解）

拓展：这个特征方程是怎么来的呢？（特征方程的来源）

由方程的结构可知， ![[公式]](https://www.zhihu.com/equation?tex=y%27%27%2Cy%27%2Cy) 必须是同类函数，才能满足![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+py%27+%2Bqy+%3D+0) 

不难猜出， ![[公式]](https://www.zhihu.com/equation?tex=y) 是指数函数，即 ![[公式]](https://www.zhihu.com/equation?tex=y+%3D+e%5E%7Brx%7D%2C+y%27+%3D+re%5E%7Brx%7D%2C+y%27%27+%3D+r%5E2e%5E%7Brx%7D) 

于是，原式等于 ![[公式]](https://www.zhihu.com/equation?tex=r%5E2e%5E%7Brx%7D%2B+pre%5E%7Brx%7D+%2Bqe%5E%7Brx%7D+%3D+0%5CRightarrow+e%5E%7Brx%7D%28r%5E2%2B+pr+%2Bq%29+%3D+0) 

![[公式]](https://www.zhihu.com/equation?tex=%E2%88%B5e%5E%7Brx%7D%5Cne0+%E2%88%B4+r%5E2%2B+pr+%2Bq+%3D+0) 

故可设，特征方程 ![[公式]](https://www.zhihu.com/equation?tex=%5Clambda%5E2%2B+p%5Clambda+%2Bq+%3D+0) （其实就是把 ![[公式]](https://www.zhihu.com/equation?tex=r) 写成 ![[公式]](https://www.zhihu.com/equation?tex=%5Clambda) ，因为习惯上用![[公式]](https://www.zhihu.com/equation?tex=%5Clambda)来描述特征方程）。

那么特征方程后面所对应的用来求出D..通解的公式又是怎么来的呢？

由于，这个特征方程![[公式]](https://www.zhihu.com/equation?tex=%5Clambda%5E2%2B+p%5Clambda+%2Bq+%3D+0)是一个一元二次方程（![[公式]](https://www.zhihu.com/equation?tex=%5Clambda)为未知数）。

根据求根公式 ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta+%3D+b%5E2-4ac) 可知，这个特征方程的解有三种情况。

我就以第一种情况为例（因为后两种情况推导起来很麻烦）：

当 ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta+%3E0) ，有两个不同根 ![[公式]](https://www.zhihu.com/equation?tex=%5Clambda_1%5Cne+%5Clambda_2) ，将其分别代入![[公式]](https://www.zhihu.com/equation?tex=y+%3D+e%5E%7Brx%7D) 

得： ![[公式]](https://www.zhihu.com/equation?tex=y_1+%3D+e%5E%7B%5Clambda_1x+%7D) 和![[公式]](https://www.zhihu.com/equation?tex=y_2+%3D+e%5E%7B%5Clambda_2x+%7D)（两个特解）

由基本概念中“某D.E.通解的项和该D.E.的阶相同”可知， ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+py%27+%2Bqy+%3D+0) 的通解应有两项，不妨设为 ![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2) 。

再根据下文“解的性质中线性无关那块的概念”可知，如果 ![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2) 要是 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+py%27+%2Bqy+%3D+0) 的解，则必须满足 ![[公式]](https://www.zhihu.com/equation?tex=Cy_1+%5Cne+y_2) （即二者线性无关）。

![[公式]](https://www.zhihu.com/equation?tex=%E2%88%B5%5Clambda_1+%5Cne+%5Clambda_2+%E2%88%B4%5Cfrac%7By_1%7D%7By_2%7D+%3D+%5Cfrac%7Be%5E%7B%5Clambda_1x+%7D%7D%7Be%5E%7B%5Clambda_2x+%7D%7D+%5Cne+C) （C为常数）则二者线性无关。

故，![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2+%3D+C_1e%5E%7B%5Clambda_2x+%7D+%2B+C_1e%5E%7B%5Clambda_2x+%7D) 

第二种情况：当 ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta+%3D0) ，有一个二重根 ![[公式]](https://www.zhihu.com/equation?tex=%5Clambda_1%3D+%5Clambda_2)，可以通过设一个线性无关的另一个特解来推导。

第三种情况：当 ![[公式]](https://www.zhihu.com/equation?tex=%5CDelta+%3C0) ，存在共轭复根 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha+%5Cpm+i%5Cbeta)，要注意复数的运算规则。

（9）**二阶常系数非齐线性型①**：形如 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+py%27+%2Bqy+%3D+P_n%28x%29e%5E%7Bkx%7D) 

（ ![[公式]](https://www.zhihu.com/equation?tex=+P_n) 是多项式的意思，洋屁名polynomial）

它的解其实就是：二阶常系数齐次线性型的通解 + 一个自己的特解。

例题： ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+-+3y%27+%2B+2y+%3D+%282x%2B1%29e%5E%7Bx%7D) 

第一步，求齐次的通解：

![[公式]](https://www.zhihu.com/equation?tex=%5Clambda+%5E2+-3%5Clambda+%2B2+%3D+0+%5CRightarrow%5CDelta+%3D+1+%3E+0%2C+%5Clambda+_1+%3D+1%2C+%5Clambda+_2+%3D+2%5CRightarrow+y+%3D+C_1e%5E%7Bx%7D+%2B+C_2e%5E%7B2x%7D) 

第二步，找一个非齐的特解（按通解的模样，假设一个特解）：

![[公式]](https://www.zhihu.com/equation?tex=y_0%28x%29+%3D+%28ax+%2B+b%29e%5E%7B%28x%29%7D) 

![[公式]](https://www.zhihu.com/equation?tex=%E2%88%B5k+%3D+1+%3D+%5Clambda+_1+%5Cne+%5Clambda+_2+%E2%88%B4) 特解乘以x，是![[公式]](https://www.zhihu.com/equation?tex=y_0+%3D+x%28ax+%2B+b%29e%5E%7Bx%7D+%3D+%28ax%5E2+%2B+bx%29e%5E%7Bx%7D) 

如果![[公式]](https://www.zhihu.com/equation?tex=k+%5Cne+%5Clambda+_1+%5Cne+%5Clambda+_2+)则特解是 ![[公式]](https://www.zhihu.com/equation?tex=%28ax+%2B+b%29e%5E%7Bx%7D+) 

如果![[公式]](https://www.zhihu.com/equation?tex=k+%3D+%5Clambda+_1+%3D+%5Clambda+_2) 则特解乘以 ![[公式]](https://www.zhihu.com/equation?tex=x%5E2) 

 由于![[公式]](https://www.zhihu.com/equation?tex=y_0+%3D+%28ax%5E2+%2B+bx%29e%5E%7Bx%7D) 则：

![[公式]](https://www.zhihu.com/equation?tex=y%27_0+%3D+%28ax%5E2+%2B+bx%29e%5E%7Bx%7D+%2B+%282ax%2B+b%29e%5E%7Bx%7D+%3D+%5Bax%5E2+%2B+%282a%2Bb%29x+%2B+b%5De%5E%7Bx%7D) 

![[公式]](https://www.zhihu.com/equation?tex=y%27%27_0+%3D+2ae%5Ex+%2B+%28ax%5E2+%2B+bx%29e%5E%7Bx%7D+%2B+2%282ax%2B+b%29e%5E%7Bx%7D+%3D+%5Bax%5E2+%2B+%284a%2Bb%29x+%2B+2a%2Bb%5De%5Ex) 

代入原式，得 ![[公式]](https://www.zhihu.com/equation?tex=+%5B3ax%5E2+%2B+%286a%2B3b%29x+%2B+2a%2B2b%5De%5Ex+%3D+%282x-1%29e%5Ex) 

求出： ![[公式]](https://www.zhihu.com/equation?tex=a+%3D+-1%2C+b%3D-1) 

则原式的解就是： ![[公式]](https://www.zhihu.com/equation?tex=y+%3D+C_1e%5E%7Bx%7D+%2B+C_2e%5E%7B2x%7D+%2B+%28-x%5E2+%2B+-x%29e%5E%7Bx%7D) 

拓展：这里代入原式，是有一定技巧的（ ![[公式]](https://www.zhihu.com/equation?tex=Q) 为特解里的 ![[公式]](https://www.zhihu.com/equation?tex=P_n%28x%29) ）

如果![[公式]](https://www.zhihu.com/equation?tex=k+%3D+%5Clambda+_1+%3D+%5Clambda+_2+)则公式为 ![[公式]](https://www.zhihu.com/equation?tex=Q%27%27+%3D+P_n%28x%29) 

如果![[公式]](https://www.zhihu.com/equation?tex=k+%3D+%5Clambda+_1+%5Cne+%5Clambda+_2+)则公式为 ![[公式]](https://www.zhihu.com/equation?tex=Q%27%27+%2B+%282k-p%29Q%27+%3D+P_n%28x%29) 

如果![[公式]](https://www.zhihu.com/equation?tex=k+%5Cne+%5Clambda+_1+%5Cne+%5Clambda+_2+)，那就没有技巧了。

以上题为例：

由于![[公式]](https://www.zhihu.com/equation?tex=k+%3D+1+%3D+%5Clambda+_1+%5Cne+%5Clambda+_2+) ，得到![[公式]](https://www.zhihu.com/equation?tex=y_0+%3D+x%28ax+%2B+b%29e%5E%7Bx%7D+%3D+%28ax%5E2+%2B+bx%29e%5E%7Bx%7D)这个特解

代入公式： ![[公式]](https://www.zhihu.com/equation?tex=2a+%2B+%282-3%29%282ax%2Bb%29+%3D+%282x-1%29%5CRightarrow+-2ax+%2B+2a-b+%3D+%282x-1%29) 

解得： ![[公式]](https://www.zhihu.com/equation?tex=a+%3D+-1%2C+b+%3D+-1) （是不是快很多）

## 三、解的性质

（1）**线性组成**： ![[公式]](https://www.zhihu.com/equation?tex=y_1) 和 ![[公式]](https://www.zhihu.com/equation?tex=y_2) 是 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+0) 的解，则 ![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2) 也是它的解。

证：把 ![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2) 代入 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29+) 得：

![[公式]](https://www.zhihu.com/equation?tex=C_1+y%27%27_1+%2B+C_2+y%27%27_2+%2B+p%28x%29%28C_1+y%27_1+%2B+C_2+y%27_2+%29+%2B+q%28x%29%28C_1+y_1+%2B+C_2+y_2+%29) 

![[公式]](https://www.zhihu.com/equation?tex=%5CRightarrow+C_1+%28y%27%27_1+%2B+p%28x%29y%27_1+%2B+q%28x%29y_1%29+%2B+C_2+%28y%27%27_2+%2B+p%28x%29y%27_2+%2B+q%28x%29y_2%29+) 

![[公式]](https://www.zhihu.com/equation?tex=%E2%88%B5y_1%2C+y_2) 是 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29+%3D+0)的解

![[公式]](https://www.zhihu.com/equation?tex=%E2%88%B4y%27%27_1+%2B+p%28x%29y%27_1+%2B+q%28x%29y_1+%3D+y%27%27_2+%2B+p%28x%29y%27_2+%2B+q%28x%29y_2+%3D+0) 

则 ![[公式]](https://www.zhihu.com/equation?tex=C_1+%28y%27%27_1+%2B+p%28x%29y%27_1+%2B+q%28x%29y_1%29+%2B+C_2+%28y%27%27_2+%2B+p%28x%29y%27_2+%2B+q%28x%29y_2%29+%3D+0) 

Q.E.D.嘻嘻

同理其实我们可以推出，在 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+f%28x%29) 的情况。

![[公式]](https://www.zhihu.com/equation?tex=%E2%88%B5y_1%2C+y_2) 是 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29+%3D+f%28x%29)的解

![[公式]](https://www.zhihu.com/equation?tex=%E2%88%B4y%27%27_1+%2B+p%28x%29y%27_1+%2B+q%28x%29y_1+%3D+y%27%27_2+%2B+p%28x%29y%27_2+%2B+q%28x%29y_2+%3D+f%28x%29) 

则![[公式]](https://www.zhihu.com/equation?tex=C_1+%28y%27%27_1+%2B+p%28x%29y%27_1+%2B+q%28x%29y_1%29+%2B+C_2+%28y%27%27_2+%2B+p%28x%29y%27_2+%2B+q%28x%29y_2%29+%3D+%28C_1+%2B+C_2%29f%28x%29) 

当 ![[公式]](https://www.zhihu.com/equation?tex=C_1+%2B+C_2+%3D1) 时， ![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2) 是![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+f%28x%29)的解

当 ![[公式]](https://www.zhihu.com/equation?tex=C_1+%2B+C_2+%3D0) 时， ![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2) 是![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+0)的解、

否则， ![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2) 是![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+%28C_1+%2B+C_2%29f%28x%29)的解

（2）**线性无关**：![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2)是![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29+%3D+0) 的解，充要条件是![[公式]](https://www.zhihu.com/equation?tex=y_1) 和 ![[公式]](https://www.zhihu.com/equation?tex=y_2)是线性无关的。

（所谓线性无关，就是指 ![[公式]](https://www.zhihu.com/equation?tex=y_1) 和 ![[公式]](https://www.zhihu.com/equation?tex=y_2) 谁都不能表示谁，即![[公式]](https://www.zhihu.com/equation?tex=Cy_1+%5Cne+y_2) （C为任意常数））

证：

充分性：因为![[公式]](https://www.zhihu.com/equation?tex=y_1) 和 ![[公式]](https://www.zhihu.com/equation?tex=y_2)线性无关的，根据基本概念中关于通解的定义，不难看出![[公式]](https://www.zhihu.com/equation?tex=C_1+y_1+%2B+C_2+y_2)是![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29+%3D+0) 的解

必要性（反证法）：设![[公式]](https://www.zhihu.com/equation?tex=y_1) 和 ![[公式]](https://www.zhihu.com/equation?tex=y_2)线性相关，则

![[公式]](https://www.zhihu.com/equation?tex=Cy_1+%3D+y_2%5CRightarrow+C_1+y_1+%3D+C_2+y_2%5CRightarrow+y+%3D+C_1+y_1+%2B+C_2+y_2+%3D+C_1+y_1) 

这与基本概念中“某D.E.通解的项和该D.E.的阶相同”矛盾，则![[公式]](https://www.zhihu.com/equation?tex=y_1) 和 ![[公式]](https://www.zhihu.com/equation?tex=y_2)线性无关。

Q.E.D.O(∩_∩)O哈哈~

（3）**叠加原理**：如果 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+f%28x%29+%3D+f_1%28x%29+%2B+f_2%28x%29) 

![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+f_1%28x%29) 的解为 ![[公式]](https://www.zhihu.com/equation?tex=y_1) 

![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+f_2%28x%29) 的解为 ![[公式]](https://www.zhihu.com/equation?tex=y_2) 

则 ![[公式]](https://www.zhihu.com/equation?tex=y_1%2B2+y_1) 便是 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+%3D+f%28x%29) 的通解

证：把 ![[公式]](https://www.zhihu.com/equation?tex=y_1%2By_1) 代入 ![[公式]](https://www.zhihu.com/equation?tex=y%27%27+%2B+p%28x%29y%27+%2B+q%28x%29y+) ，得出

![[公式]](https://www.zhihu.com/equation?tex=%28y%27%27_1%2B+y%27%27_1%29+%2B+p%28x%29%28y%27_1%2B+y%27_1%29+%2B+q%28x%29%28y_1%2B+y_1%29) 

![[公式]](https://www.zhihu.com/equation?tex=%5CRightarrow+y%27%27_1%2B+p%28x%29y%27_1+%2B+q%28x%29y_1+%2B+y%27%27_2%2B+p%28x%29y%27_2+%2B+q%28x%29y_2) 

![[公式]](https://www.zhihu.com/equation?tex=%E2%88%B5y%27%27_1%2B+p%28x%29y%27_1+%2B+q%28x%29y_1+%3D+f_1%28x%29%2C+y%27%27_2%2B+p%28x%29y%27_2+%2B+q%28x%29y_2+%3D+f_2%28x%29) 

![[公式]](https://www.zhihu.com/equation?tex=%E2%88%B4+y%27%27_1%2B+p%28x%29y%27_1+%2B+q%28x%29y_1+%2B+y%27%27_2%2B+p%28x%29y%27_2+%2B+q%28x%29y_2+%3D+f_1%28x%29+%2B+f_2%28x%29+%3D+f%28x%29)

> **本文转载自[（回忆大学所学）常微分方程](https://zhuanlan.zhihu.com/p/38573924)**