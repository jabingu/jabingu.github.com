---
layout: post
title:  "时间序列：自回归模型（AR）"
date:   2019-08-13 06:14:54
categories: math
tags: math timeseries
thumbnail: "assets/img/post/time.jpg"
feature-img: "assets/img/post/time.jpg"
excerpt: 利用自回归模型（AR）预测时间序列
mathjax: 1
---

* content
{:toc}
## AR 模型的引入

考虑如图所示的单摆系统。设 $x_t$ 为第 $t$ 次摆动过程中的摆幅。根据物理原理，第 $t$ 次的摆幅 $x_t$ 由前一次的摆幅 $x_{t-1}$ 决定，即有 $x_t=a_1x_{t-1}$。考虑到空气振动的影响，我们往往假设

<br/>
$$
x_t=a_1x_{t-1}+\varepsilon_t,t\geq1
\tag{1.1}
$$
<br/>

其中，随机干扰 $\varepsilon_t$ ~$N(0, \sigma^2)$。

在这里，我们称模型 $(1.1)$ 为**一阶自回归模型**。

<span style="color:SteelBlue">**由此类推**</span>，**二阶自回归模型**是这样的：

<br/>
$$
x_t=a_1x_{t-1}+a_2x_{t-2}+\varepsilon_t,t\geq1
\tag{1.2}
$$
 <br/>

**三阶自回归模型**是这样的：

<br/>
$$
x_t=a_1x_{t-1}+a_2x_{t-2}+a_3x_{t-3}+\varepsilon_t,t\geq1
\tag{1.3}
$$
<br/>

<span style="color:SteelBlue">**更一般地**</span>，可以考虑序列值 $x_t$ 可由前 $p$ 个时刻的序列值及当前的噪声表出，即 
<br/>

<br/>
$$
\color{LightSeaGreen}{
X_t=a_1X_{t-1}+a_2X_{t-2}+\cdots+a_pX_{t-p}+\varepsilon_t,t\geq1
}\tag{2}
$$
<br/>

其中，$a_j$ 为参数，$\{\varepsilon_t\}$ 为白噪声。为了显示序列值为随机变量，这里使用 $X_t$ 而不是 $x_t$。



## AR 模型的定义

### 定义1

> 如果 $\{\varepsilon_t \}$ 为白噪声，服从$N(0, \sigma^2)$分布，$a_0$,$a_1$,...,$a_p$($a_p$≠0) 为实数，就称 $p$ 阶差分方程

$$
X_t=a_0+a_1X_{t-1}+a_2X_{t-2}+\cdots+a_pX_{t-p}+\varepsilon_t,t\in\mathbb{Z}
\tag{3}
$$

> 是一个 $p$ 阶自回归模型，简称 $AR(p)$ 模型，称 $a=(a_0,a_1,...,a_p)^T$ 是 $AR(p)$ 模型中的自回归系数。满足 $AR(p)$ 模型 $(3)$ 的时间序列 $\{Xt\}$ 称为 $AR(p)$ 序列。当 $a_0=0$ 时，称为零均值 $AR(p)$ 序列，即

$$
X_t=a_1X_{t-1}+a_2X_{t-2}+\cdots+a_pX_{t-p}+\varepsilon_t,t\in\mathbb{Z}
\tag{4}
$$

<span style="color:SteelBlue">**需要指出的是**</span>，对于 $a_0\neq0$ 的情况，我们可以通过**零均值化**的手段把一般的 $AR(p)$ 序列变为零均值 $AR(p)$ 序列。



## AR 序列的建模

### AR 模型的判定

**暂时缺少**

### <span style="color:LightSeaGreen">AR 模型的参数估计</span>

> AR 模型的参数估计主要有三种方法：矩估计、**最小二乘估计**和最大似然估计。
>
> 这里仅介绍最小二乘估计。（实际上最大似然估计与最小二乘估计的结果一样）

对于样本序列$ \{x_t\}$，当$ j\geq p+1$时，记白噪声 $ε_j$ 的估计为

<br/>
$$
\hat{\varepsilon}_j=x_j-(\hat{a}_1x_{j-1}+\hat{a}_2x_{j-2}+\cdots+\hat{a}_px_{j-p})
\tag{6}
$$
<br/>

通常称 $\hat{\varepsilon}_j$为**残差**。我们的优化目标是使得残差平方和

<br/>
$$
\sum\limits_{j=p+1}^N=[x_j-(\hat{a}_1x_{j-1}+\hat{a}_2x_{j-2}+\cdots+\hat{a}_px_{j-p})]^2
\tag{7}
$$
<br/>

达到最小。我们称使上式达到最小的 $\hat{a}_1,\hat{a}_2,\cdots,\hat{a}_p $为 $AR(p)$ 模型中自回归系数 $a_1,a_2,\cdots,a_p$ 的估计。

<span style="color:SteelBlue">**记**</span>

<br/>
$$
Y=\left[\begin{array}\\x_P+1\\x_p+2\\\vdots\\x_N
    \end{array}\right]
,X=\left[\begin{array}\\x_P+1&x_P+1&\cdots&x_1\\x_p+2&x_p&\cdots&x_2\\\vdots&\vdots&\vdots&\vdots\\x_{N-1}&x_{N-2}&\cdots&x_{N-p}
    \end{array}\right]
$$
<br/>

<br/>

得到如下线性方程组

<br/>
$$
Y=Xa+\varepsilon
\tag{8}
$$
<br/>

于是式 $ (7)$的目标函数可表示为

<br/>
$$
S({a})=({Y}-{Xa})^T({Y}-{Xa})
={Y}^T{Y}-2{Y}^T{Xa}+{a}^T{X}^T{Xa}
\tag{9}
$$
<br/>

上式对参数 ${a}$求导并令其为 $0$，可得

<br/>
$$
\frac{\partial (S{a})}{\partial {a}}
=-2{Y}^{T}{Ya}+{a}^T{X}^T{Xa}
=0
\tag{10}
$$
<br/>

因此，${a}$参数的<span style="color:LightSeaGreen">**最小二乘估计**</span>为

<br/>
$$
\color{LightSeaGreen}{
\hat{a}=({X}^T{X})^{-1}{X}^T{Y}
}\tag{11}
$$
<br/>

此时，误差方差的<span style="color:LightSeaGreen">**最小二乘估计**</span>

<br/>
$$
\color{LightSeaGreen}{
\hat{\sigma}^2
=\frac{1}{N-p}({Y}-{X}{a})^{T}({Y}-{X}{a})
}\tag{12}
$$

<br/>

## 参考文献

[自回归模型（AR ）](https://www.cnblogs.com/super-zhang-828/p/7106970.html)

[第四篇 自回归模型（AR Model）](http://geodesy.blog.sohu.com/273714573.html)