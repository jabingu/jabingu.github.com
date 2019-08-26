---
layout: post
title:  "Tensorflow ：TensorBoard可视化学习"
date:   2019-08-08 7:30:00
categories: ML
tags: ML Tensorflow 
thumbnail: "assets/img/post/tensorflow.jpg"
feature-img: "assets/img/post/tensorflow.jpg"
excerpt: 使用TensorBoard来对TensorFlow 的数据进行可视化
---

* content
{:toc}
> 使用机器学习来学习人类，人类再去学习机器学习的结果。
>
> <p align="right">—-jabingu　　</p>



## 前言

> TensorFlow 可用于训练大规模深度神经网络所需的计算，使用该工具涉及的计算往往复杂而深奥。为了更方便 TensorFlow 程序的理解、调试与优化，我们可以使用名为 TensorBoard 的可视化工具。可以用 TensorBoard 来展现 TensorFlow 图，绘制图像生成的定量指标图以及显示附加数据（如其中传递的图像）。



## 代码

### 伪代码

1. 定义了**add_layer()** 
3. 创建其实数据，并导入到tf中
4. 定义tf参数
4. 训练



### 总代码

```python
from __future__ import print_function
import tensorflow as tf
import numpy as np

def add_layer(inputs, in_size, out_size, n_layer, activation_function=None):
    # add one more layer and return the output of this layer
    layer_name = 'layer%s' % n_layer
    with tf.name_scope(layer_name):
        with tf.name_scope('weights'):
            Weights = tf.Variable(tf.random_normal([in_size, out_size]), name='W')
            tf.summary.histogram(layer_name + '/weights', Weights)
        with tf.name_scope('biases'):
            biases = tf.Variable(tf.zeros([1, out_size]) + 0.1, name='b')
            tf.summary.histogram(layer_name + '/biases', biases)
        with tf.name_scope('Wx_plus_b'):
            Wx_plus_b = tf.add(tf.matmul(inputs, Weights), biases)
        if activation_function is None:
            outputs = Wx_plus_b
        else:
            outputs = activation_function(Wx_plus_b, )
        tf.summary.histogram(layer_name + '/outputs', outputs)
    return outputs


# Make up some real data
x_data = np.linspace(-1, 1, 300)[:, np.newaxis]
noise = np.random.normal(0, 0.05, x_data.shape)
y_data = np.square(x_data) - 0.5 + noise

# define placeholder for inputs to network
with tf.name_scope('inputs'):
    xs = tf.placeholder(tf.float32, [None, 1], name='x_input')
    ys = tf.placeholder(tf.float32, [None, 1], name='y_input')

# add hidden layer
l1 = add_layer(xs, 1, 10, n_layer=1, activation_function=tf.nn.relu)
# add output layer
prediction = add_layer(l1, 10, 1, n_layer=2, activation_function=None)

# the error between prediciton and real data
with tf.name_scope('loss'):
    loss = tf.reduce_mean(tf.reduce_sum(tf.square(ys - prediction),
                                        reduction_indices=[1]))
    tf.summary.scalar('loss', loss)

with tf.name_scope('train'):
    train_step = tf.train.GradientDescentOptimizer(0.1).minimize(loss)

sess = tf.Session()
merged = tf.summary.merge_all()
writer = tf.summary.FileWriter("logs/", sess.graph)

init = tf.global_variables_initializer()
sess.run(init)
#训练
for i in range(1000):
    sess.run(train_step, feed_dict={xs: x_data, ys: y_data})
    if i % 50 == 0:
        result = sess.run(merged,
                          feed_dict={xs: x_data, ys: y_data})
        writer.add_summary(result, i)
```



## 启动tensorboard：

### 1 运行程序

运行程序，生成`log`文件

```bash
PS D:\doc\spyder\时间序列预测> ls

    目录: D:\doc\spyder\时间序列预测

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         2019/8/9     14:14                logs
-a----         2019/8/9     14:14           3586 untitled1.py
```



### 2 打开终端

> 1、系统自带的终端，**cmd**
>
> 2、名称为：Anaconda **Prompt**的终端

选择用哪种终端打开，根据当时安装tensorflow时用的那种终端安装的，我使用的是Anaconda Prompt终端安装的tensorflow，因此用它来打开

### 3、激活环境

使用`activate tensorflow-gpu`激活自己的tensorflow安装的环境，比如我是安装在`tensorflow-gpu`中的，如果是在`base`环境中则不要激活

```bash
(base) C:\Users\Administrator>activate tensorflow-gpu
(tensorflow-gpu) C:\Users\Administrator>cd d
```

### 4 输入命令

```bash
tensorboard --logdir=具体地址
```

**比如：**

运行成功返回网址`http://USER-20190123UB:6006 `

```bash
(tensorflow-gpu) C:\Users\Administrator>tensorboard --logdir=D:\doc\spyder\时间序列预测\logs
TensorBoard 1.12.2 at http://USER-20190123UB:6006 (Press CTRL+C to quit)
```



## 可能会遇到的问题

1. 而且与 tensorboard 兼容的浏览器是 “**Google Chrome**”. 使用其他的浏览器不保证所有内容都能正常显示.

2. 同时注意, 如果使用 **http://0.0.0.0:6006** 网址打不开的朋友们, 请使用 **http://localhost:6006**, 大多数朋友都是这个问题。事实上我在使用过程中无法打开自己返回给我地址。

3. 请确保你的 tensorboard 指令是在你的 logs 文件根目录执行的. 如果在其他目录下, 比如 `Desktop` 等, 可能不会成功看到图. 比如在我之前的代码, 我们需要执行的指令中带有地址信息。



## 参考文献

[tensorboard使用详解](https://www.jianshu.com/p/d8f9b0dfacdb)

[Tensorboard 可视化好帮手 1](https://morvanzhou.github.io/tutorials/machine-learning/tensorflow/4-1-tensorboard1/)

[TensorBoard：可视化学习](https://tensorflow.google.cn/guide/summaries_and_tensorboard)





