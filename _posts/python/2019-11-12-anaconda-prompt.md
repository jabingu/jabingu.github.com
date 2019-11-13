---

layout: post
title:  "Anaconda Prompt使用说明"
date:   2019-11-12 07:19:54
categories: python
tags: python 
thumbnail: "assets/img/post/python.jpg"
feature-img: "assets/img/post/python.jpg"
excerpt: Anaconda Prompt使用说明
---

* content
{:toc}
> 警惕自己不是程序员！
>
> <p align="right">——jabingu　　</p>



> Anaconda Prompt中对python的包进行管理



## 创建虚拟环境

```python
 conda create -n your_env_name python=X.X（2.7、3.6等)
```



## 查看虚拟环境

```python
conda env list
```



## 激活虚拟环境

  **Linux:** 

```python
source activate your_env_name(虚拟环境名称)
```

  **Windows:** 

```python
activate your_env_name(虚拟环境名称)
```



## 查看已经安装的包

```python
conda list
```



## 安装新包

**conda**

```python
conda install xxxx
```

**pip**

```python
pip install xxxx
```

 **whl文件的安装** 

先下载 `whl`文件

```python
 pip install 路径+whl文件名 
```



## 参考文献

[Anaconda创建新的python环境](https://blog.csdn.net/wdx1993/article/details/83660717)