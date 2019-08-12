---
layout: post
title:  "Tensorflow ：最基础的模版以及说明"
date:   2019-08-12 6:30:00
categories: ML
tags: ML Tensorflow 
excerpt: TensorFlow 最基础的模版以及说明
---

* content
{:toc}
> 使用机器学习来学习人类，人类再去学习机器学习的结果。
>
> <p align="right">—-jabingu　　</p>



## 前言

> Tensorflow 最简单的一个模型，主要学习如何来使用他，实际的模型和代码中的对象关系，或者说Tensorflow 自己已经实现了哪些，我们在使用的时候又是只需要关系什么呢
>

## 基本使用

使用 TensorFlow, 你必须明白 TensorFlow:

- 使用图 (**graph**) 来表示计算任务.
- 在被称之为 `会话 (Session)` 的上下文 (context) 中执行图.
- 使用 **tensor** 表示数据.
- 通过 `变量 (Variable)` 维护状态.
- 使用 **feed** 和 **fetch** 可以为任意的操作(arbitrary operation) 赋值或者从其中获取数据.



## 代码

### 伪代码：

> 1. 确定输入
> 2. 定义模型
> 3. 确定训练

### 输入：

- x_data：
- y_data：标签

### 变量：

- **权重：**    W = tf.Variable(tf.random_uniform([1], 1.0, 1.0))
- **偏置项：** b = tf.Variable(tf.zeros([1]))

### 模型训练参数

**偏置项 **

- loss = tf.reduce_mean(tf.square(y - y_data))

**偏置项** 

- optimizer = tf.train.GradientDescentOptimizer(0.5)

### 训练

- sess = tf.Session()

### 总代码

```python
import tensorflow as tf
import numpy as np

# Create 100 phony x, y data points in NumPy, y = x * 0.1 + 0.3
x_data = np.random.rand(100).astype("float32")
y_data = x_data * 0.1 + 0.3

# Try to find values for W and b that compute y_data = W * x_data + b
# (We know that W should be 0.1 and b 0.3, but Tensorflow will
# figure that out for us.)
W = tf.Variable(tf.random_uniform([1], 1.0, 1.0))
b = tf.Variable(tf.zeros([1]))
y = W * x_data + b

# Minimize the mean squared errors.
loss = tf.reduce_mean(tf.square(y - y_data))
optimizer = tf.train.GradientDescentOptimizer(0.5)
train = optimizer.minimize(loss)

# Before starting, initialize the variables. We will 'run' this first

init = tf.global_variables_initializer()

# Launch the graph.
sess = tf.Session()
sess.run(init)

# Fit the line.
for step in range(201):
    sess.run(train)
    if step % 20 == 0:
    	print(step, sess.run(W), sess.run(b))
# Learns best fit is W: [0.1], b: [0.3]
```



## 参考文献

[基本使用](http://www.tensorfly.cn/tfdoc/get_started/basic_usage.html)





