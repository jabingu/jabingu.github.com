---
layout: post
title:  "Tensorflow ：动态图显示结果"
date:   2019-08-08 6:30:00
categories: ML
tags: ML Tensorflow 
excerpt: 使用动态图片来对TensorFlow 的数据进行可视化
---

* content
{:toc}
> 使用机器学习来学习人类，人类再去学习机器学习的结果。
>
> <p align="right">—-jabingu　　</p>



## 前言

> 一个简单的神经网络的模型，并且使用动态图片来显示训练的过程
>
> 使用的是Tensorflow 来进行实现的



## 代码

### 伪代码

1. 定义了**add_layer()** 
3. 创建数据，
4. 定义tf参数
4. 训练
5. 显示动态的图片



### 总代码

```python
import tensorflow as tf
import numpy as np

import matplotlib.pyplot as plt
from pylab import mpl
mpl.rcParams['font.sans-serif'] = ['SimHei'] # 指定默认字体
mpl.rcParams['axes.unicode_minus'] = False # 解决保存图像是负号'-'显示为方块的问题

def add_layer(inputs, in_size, out_size, activation_function=None):    
    Weights = tf.Variable(tf.random_normal([in_size, out_size]))
    biases = tf.Variable(tf.zeros([1, out_size]) + 0.1)
    Wx_plus_b = tf.matmul(inputs, Weights) + biases#tf.matmul()是矩阵的乘法
    if activation_function is None:
        outputs = Wx_plus_b
    else:
        outputs = activation_function(Wx_plus_b)
    return outputs

# create data
x_data = np.linspace(-1,1,300, dtype=np.float32)[:, np.newaxis]
noise = np.random.normal(0, 0.05, x_data.shape).astype(np.float32)
y_data = np.square(x_data) - 0.5 + noise

xs = tf.placeholder(tf.float32, [None, 1])             #tf.placeholder导入数据
ys = tf.placeholder(tf.float32, [None, 1])

# add hidden layer
l1 = add_layer(xs, 1, 10, activation_function=tf.nn.relu)           #神经网络层
# add output  layer
prediction = add_layer(l1, 10, 1, activation_function=None)

loss = tf.reduce_mean(tf.reduce_sum(tf.square(ys - prediction),
                     reduction_indices=[1]))                        #损失函数
train_step = tf.train.GradientDescentOptimizer(0.1).minimize(loss)  #梯度下降

#训练
init = tf.global_variables_initializer()                            # 初始化
sess = tf.Session()
sess.run(init)          # Very important

# plot the real data
fig = plt.figure()
ax = fig.add_subplot(1,1,1)
ax.scatter(x_data, y_data,marker='.')
plt.title('机器学习动态图') 
plt.grid()   #生成网格
plt.ion()#本次运行请注释，全局运行不要注释
plt.show()

for i in range(1000):
    # training
    sess.run(train_step, feed_dict={xs: x_data, ys: y_data})      #训练
    if i % 50 == 0:
        # to visualize the result and improvement
        #print(sess.run(loss, feed_dict={xs: x_data, ys: y_data}))#输出误差
        try:
            ax.lines.remove(lines[0])
        except Exception:
            pass
        prediction_value = sess.run(prediction, feed_dict={xs: x_data})
        # plot the prediction
        lines = ax.plot(x_data, prediction_value, 'r-')
        plt.pause(0.1)
```





## 参考文献

[例子3 结果可视化](https://morvanzhou.github.io/tutorials/machine-learning/tensorflow/3-3-visualize-result/)





