---

layout: post
title:  "缓存替换（淘汰）算法"
date:   2021-08-23 7:30:00
categories: storage
tags: cache 
thumbnail: "assets/img/post/swing.jpg"
feature-img: "assets/img/post/swing.jpg"
excerpt: Cache替换（淘汰）算法的总结
---

* content
{:toc}
## Cache简介

### 背景

Cache一词来源于1967年的一篇电子工程期刊论文。其作者将[法语](https://zh.wikipedia.org/wiki/法语)词“cache”赋予“safekeeping storage”的涵义，用于电脑工程领域。[PC-AT](https://zh.wikipedia.org/wiki/PC_AT)/XT和[80286](https://zh.wikipedia.org/wiki/80286)时代,没有Cache，CPU和内存都很慢，CPU直接访问内存。[80386](https://zh.wikipedia.org/wiki/80386)的[芯片组](https://zh.wikipedia.org/wiki/芯片组)增加了对可选的Cache的支持，高级主板带有64KB，甚至高端的128KB Write-Through Cache。[80486](https://zh.wikipedia.org/wiki/80486) CPU里面加入了8KB的L1 Unified Cache，当时也叫做内部Cache，不分代码和数据，都存在一起；芯片组中的Cache，变成了L2，也被叫做外部Cache，从128KB到256KB不等；增加了Write-back的Cache属性。[Pentium](https://zh.wikipedia.org/wiki/Pentium) CPU的L1 Cache分为Code和data，各自8KB；L2还被放在主板上。[Pentium Pro](https://zh.wikipedia.org/wiki/Pentium_Pro)的L2被放入到CPU的Package上。[Pentium 3](https://zh.wikipedia.org/wiki/Pentium_3)开始，L2 Cache被放入了CPU的Die中。从[Intel Core](https://zh.wikipedia.org/wiki/Intel_Core) CPU开始，L2 Cache为多核共享。

### Cache定义

如今缓存的概念已被扩充，不仅在CPU和主内存之间有Cache，而且在内存和[硬盘](https://zh.wikipedia.org/wiki/硬盘)之间也有Cache（**[磁盘缓存](https://zh.wikipedia.org/wiki/磁盘缓存)**），乃至在硬盘与[网络](https://zh.wikipedia.org/wiki/网络)之间也有某种意义上的Cache──称为**[Internet](https://zh.wikipedia.org/wiki/Internet)临时文件夹**或**网络内容缓存**等。

> **凡是位于速度相差较大的两种[硬件](https://zh.wikipedia.org/wiki/硬件)之间，用于协调两者数据传输速度差异的结构，均可称之为Cache。**[<sup>1</sup>](#R1-wiki)



### Cache组成

缓存一般指性能更好的期间。现在，在Memory和Disk Storage之间有新的存储器件产生，叫NVM（non-volatile memory）或者是SCM（storage class memory）。它具有比HDD更大的容量以及更好的性能，但是存在写寿命的问题。

<center>
<img src="https://z3.ax1x.com/2021/09/05/hWLEcj.png" width = 50% height = 50% alt="cache1" border="0">
</center>



## 缓存替换算法

### 为什么研究缓存替换算法

<center>
<img src="https://z3.ax1x.com/2021/09/05/hWLf58.md.png"  alt="cache1" border="0">
</center>

$$
\begin{align}
& Hit Rate(HR)=\frac{\#Hit}{\#Requests}\\
& \implies Idealized Latency_{Avg}=HR\cdot L_{Hit} 
+(1-HR)\cdot L_{Miss}\\
& L_{Hit} = Latency_{Hit}
\end{align}
$$

一般我们使用**平均延时**来表征Cache的性能，从公式我们可以知道，有**3种**方式来改善它。分别是：

- 减少命中时延
- 减少缺失惩罚
- 增加命中率/减少缺失率

其中，前两者和组成Cache的器件有关，或者是和整体的架构相关。那么在这之外，我们可以做的就是去增加缓存的命中率。这就涉及到对缓存中**数据的管理**了。我们把使用**缓存替换算法**来对缓存中的数据进行管理。



### 造成缓存未命中的种类

<center>
<img src="https://z3.ax1x.com/2021/09/05/hWjYuj.png"  alt="cache1" border="0">
</center>

我分为3类，分别是：

- 强制缺失
- 容量缺失
- 替换算法缺失

**强制缺失**表示第一次访问的数据一定会是缺失的，在图中MRC曲线中体现为缺失率永远不为0。

**容量缺失**表示由于容量有限导致数据被替换掉产生的缺失，在图中，容量大的缺失率比容量小的缺失率要低。

**替换算法缺失**表示不同的替换算法对数据的不同的管理产生的缺失，在图中，相同Cache Size 下，不同的替换算法具有不同的缺失率。



### 替换算法分类

缓存替换算法有**3类**，分别是：

- 缓存淘汰算法
- 缓存准入算法
- 缓存预取算法

其中：淘汰算法，选择那个数据剔除缓存中；准入算法，选择那些数据进入缓存；预取算法选择哪些数据提前放入缓存中。

> 本文中只对缓存淘汰算法进行整理



## 经典缓存替换算法

### opt

### LRU

### LFU



## 基于机器学习的缓存替换算法



这边文章是介绍如何在 Markdown 中增加文献引用。[<sup>1</sup>](#R1-wiki)

## 参考文献

<div><a name="R1-wiki"></a>
[1] Karlgren, Jussi. An algebra for recommendations: using reader data as a basis for measuring document proximity, 1990.
</div>

