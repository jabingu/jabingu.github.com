---
layout: post
title:  "Tensorflow ：Saver 保存读取"
date:   2019-08-08 6:30:00
categories: ML
tags: ML Tensorflow 
thumbnail: "assets/img/post/tensorflow.jpg"
feature-img: "assets/img/post/tensorflow.jpg"
excerpt: 使用Saver来保存读取
---

* content
{:toc}
> 使用机器学习来学习人类，人类再去学习机器学习的结果。
>
> <p align="right">—-jabingu　　</p>



## 前言

> Saver 保存读取

## 保存

主要是使用`saver.save`来保存数据，后面的参数是`地址+文件名`，比如是我是要保证在`D:\doc\spyder\时间序列预测` 下面，那么我的语句应该这样写`save_path = saver.save(sess, "D:\doc\spyder\时间序列预测\save_net.ckpt")`

```python
import tensorflow as tf
import numpy as np
tf.reset_default_graph()

saver = tf.train.Saver()
sess = tf.Session()
sess.run(init)
save_path = saver.save(sess, "地址\save_net.ckpt")
print("Save to path: ", save_path)
```



## 提取

```python
import tensorflow as tf
import numpy as np
tf.reset_default_graph()

# 先建立 W, b 的容器
W = tf.Variable(np.arange(6).reshape((2, 3)), dtype=tf.float32, name="weights")
b = tf.Variable(np.arange(3).reshape((1, 3)), dtype=tf.float32, name="biases")

# 这里不需要初始化步骤 init= tf.initialize_all_variables()
saver = tf.train.Saver()
with tf.Session() as sess:
    # 提取变量
    saver.restore(sess, "地址\save_net.ckpt")
    print("weights:", sess.run(W))
    print("biases:", sess.run(b))
```



## 注意

在生成Session时候，我使用了两种不同的方式，其中方式而使用了`with`语句，会在结束时候自动的关闭session，而一般我们在提取变量的时候，后续还会用到session，所以不是用`with`语句

```python
sess = tf.Session()
```

和

```python
with tf.Session() as sess:
```



## 参考文献

[Saver 保存读取](https://morvanzhou.github.io/tutorials/machine-learning/tensorflow/5-06-save/)





