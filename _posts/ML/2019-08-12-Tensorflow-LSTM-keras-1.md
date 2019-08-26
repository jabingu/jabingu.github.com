---
layout: post
title:  "Tensorflow ：使用keras实现LSTM进行时间序列预测"
date:   2019-08-12 7:31:00
categories: ML
tags: ML Tensorflow timeseries
thumbnail: "assets/img/post/tensorflow.jpg"
feature-img: "assets/img/post/tensorflow.jpg"
excerpt: Tensorflow ：使用keras来实现LSTM进行时间序列的预测
mathjax: 1
---

* content
{:toc}
> 使用机器学习来学习人类，人类再去学习机器学习的结果。
>
> <p align="right">—-jabingu　　</p>



## 前言

> keras和Estimators相比，更加的简洁
>
> 这里我要要利用keras来实现简单（代码简洁）的LSTM来进行时间序列的预测

## 基本使用

Keras 是一个用于构建和训练深度学习模型的高阶 API。它可用于快速设计原型、高级研究和生产，具有以下三个主要优势：

- ***方便用户使用***    
  Keras 具有针对常见用例做出优化的简单而一致的界面。它可针对用户错误提供切实可行的清晰反馈。
- ***模块化和可组合***    
  将可配置的构造块连接在一起就可以构建 Keras 模型，并且几乎不受限制。
- ***易于扩展***   
  可以编写自定义构造块以表达新的研究创意，并且可以创建新层、损失函数并开发先进的模型。



## 代码

### 伪代码：

> 1. 数据的预处理
> 2. 定义模型
> 3. 确定训练



### 数据处理

输入数据，这里的data为**（xx,）**大小。

```python
'''读入原始数据并转为list'''
f=open('dataset_1.csv')   
df=pd.read_csv(f)     #读入股票数据
data=np.array(df['最高价'])   #获取最高价序列
data=data[::-1]      #反转，使数据按照日期先后顺序排
```

**正则化函数**

```python
'''自定义数据尺度缩放函数'''
def data_processing(raw_data,scale=True):
    if scale == True:
        return (raw_data-np.mean(raw_data))/np.std(raw_data)#标准化
    else:
        return (raw_data-np.min(raw_data))/(np.max(raw_data)-np.min(raw_data))#极差规格化
```

将原始数据进行处理：输出的X大小为**(xx-TIMESTEPS-1,1,TIMESTEPS)**大小，其中**TIMESTEPS**是折叠的递归步数。所以数据中最后的**(TIMESTEPS-1)**个数据是不进行训练的。

```python
'''样本数据生成函数'''
def generate_data(seq):
    X = []#初始化输入序列X
    Y= []#初始化输出序列Y
    '''生成连贯的时间序列类型样本集，
    每一个X内的一行对应指定步长的输入序列，
    Y内的每一行对应比X滞后一期的目标数值'''
    for i in range(len(seq) - TIMESTEPS - 1):
        X.append([seq[i:i + TIMESTEPS]])#从输入序列第一期出发，等步长连续不间断采样
        Y.append([seq[i + TIMESTEPS]])#对应每个X序列的滞后一期序列值
    return np.array(X, dtype=np.float32), np.array(Y, dtype=np.float32)

```

### 模型定义

**模型参数**

```python
'''设置隐层层数'''
NUM_LAYERS = 5
'''设置一个时间步中折叠的递归步数'''
TIMESTEPS = 12
'''设置训练轮数'''
TRAINING_STEPS = 100
'''设置训练批尺寸'''
BATCH_SIZE = 20
```

**模型定义**

```python
#定义模型
model = keras.Sequential()
#lstm模型,第一个表示单元
model.add(layers.LSTM(NUM_LAYERS, input_shape=(train_X.shape[1], train_X.shape[2])))
#输出层
model.add(layers.Dense(train_y.shape[1]))
#设定损失函数，优化器。
model.compile(
        loss='mse',
#        loss='categorical_crossentropy',
        optimizer='adam',
        metrics=['accuracy'])

```

**模型训练**

```python
#训练
model.fit(train_X, train_y, epochs=TRAINING_STEPS,
          batch_size=BATCH_SIZE,
#          batch_size=len(train_X),
#          batch_size=1,
          verbose=2, shuffle=False)
result = model.predict(test_X, verbose=0)
```

### 结果比较

输出结果一个是通过图像来进行直观的查看，另外一个是通过计算MAPE(平均绝对百分比误差)来进行数值上量化查看。

计算公式是：


$$
\begin{align}
MAPE =\frac{\sum_{i=1}^n({(Y_i-F_i)}/{Y_i}\times 100)}{n}\\
\end{align}
\tag{1}
$$


```python
#输出MAPE的测试指标
print('MAPE')
print(sum(abs(np.true_divide((result-test_y),test_y)))/len(test_y)*100)
#目前是[12.373663]
```





### 总代码

```python
# -*- coding: utf-8 -*-

import spandas as pd
import numpy as np
from tensorflow import keras
from tensorflow.keras import layers

import matplotlib.pyplot as plt
from pylab import mpl
mpl.rcParams['font.sans-serif'] = ['SimHei'] #指定默认字体
mpl.rcParams['axes.unicode_minus'] = False   #解决保存图像是负号'-'显示为方块的问题

#optimizer
#tf.train.AdamOptimizer、
#tf.train.RMSPropOptimizer 或 
#tf.train.GradientDescentOptimizer。
#loss
#均方误差 (mse)、categorical_crossentropy 和 binary_crossentropy。

'''读入原始数据并转为list'''
f=open('dataset_1.csv')   
df=pd.read_csv(f)     #读入股票数据
data=np.array(df['最高价'])   #获取最高价序列
data=data[::-1]      #反转，使数据按照日期先后顺序排

'''自定义数据尺度缩放函数'''
def data_processing(raw_data,scale=True):
    if scale == True:
        return (raw_data-np.mean(raw_data))/np.std(raw_data)#标准化
    else:
        return (raw_data-np.min(raw_data))/(np.max(raw_data)-np.min(raw_data))#极差规格化
'''样本数据生成函数'''
def generate_data(seq):
    X = []#初始化输入序列X
    Y= []#初始化输出序列Y
    '''生成连贯的时间序列类型样本集，
    每一个X内的一行对应指定步长的输入序列，
    Y内的每一行对应比X滞后一期的目标数值'''
    for i in range(len(seq) - TIMESTEPS - 1):
        X.append([seq[i:i + TIMESTEPS]])#从输入序列第一期出发，等步长连续不间断采样
        Y.append([seq[i + TIMESTEPS]])#对应每个X序列的滞后一期序列值
    return np.array(X, dtype=np.float32), np.array(Y, dtype=np.float32)

#'''设置隐层神经元个数'''
#HIDDEN_SIZE = 40
'''设置隐层层数'''
NUM_LAYERS = 5
'''设置一个时间步中折叠的递归步数'''
TIMESTEPS = 12
'''设置训练轮数'''
TRAINING_STEPS = 100
'''设置训练批尺寸'''
BATCH_SIZE = 20

'''模型定义'''

'''对原数据进行尺度缩放'''
data = data_processing(data)

'''将所有样本来作为训练样本'''
train_X, train_y = generate_data(data[0:5500])

'''将所有样本作为测试样本,查看拟合的效果好不好
把后续的样本作为测试样本，查看预测的效果好不好
'''
test_X, test_y = generate_data(data[100:2000])
test_X, test_y = generate_data(data[5500-1-TIMESTEPS:-1])
test_X, test_y = generate_data(data)

#定义模型
model = keras.Sequential()
#lstm模型,第一个表示单元
model.add(layers.LSTM(NUM_LAYERS, input_shape=(train_X.shape[1], train_X.shape[2])))
#输出层
model.add(layers.Dense(train_y.shape[1]))
#设定损失函数，优化器。
model.compile(
        loss='mse',
#        loss='categorical_crossentropy',
        optimizer='adam',
        metrics=['accuracy'])
#训练
model.fit(train_X, train_y, epochs=TRAINING_STEPS,
          batch_size=BATCH_SIZE,#len(train_X),
#          batch_size=1,
          verbose=2, shuffle=False)

result = model.predict(test_X, verbose=0)
                       
'''自定义反标准化函数'''
def scale_inv(raw_data,scale=True):
    data1 = df.iloc[:, 1].tolist()
    if scale == True:
        return raw_data*np.std(data1)+np.mean(data1)
    else:
        return raw_data*(np.max(data1)-np.min(data1))+np.min(data1)                     
                       
'''绘制反标准化之前的真实值与预测值对比图'''
plt.figure()
plt.plot(scale_inv(result), '.',label='predict data')
plt.plot(scale_inv(test_y), label='true data')
plt.title('none-normalized')
plt.legend()
plt.show()  
#输出MAPE的测试指标
print('MAPE')
print(sum(abs(np.true_divide((result-test_y),test_y)))/len(test_y)*100)
#目前是[12.373663]
                                  
```



## 参考文献

[官方教程](https://tensorflow.google.cn/guide/keras#save_and_restore)

[时间序列分析和预测](https://blog.csdn.net/mengjizhiyou/article/details/82683448)