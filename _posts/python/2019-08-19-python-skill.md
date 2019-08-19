---

layout: post
title:  "py：python的一些使用技巧"
date:   2019-08-19 11:19:54
categories: python
tags: python 
excerpt: python使用上的技巧，或者说是代码的规范
---

* content
{:toc}
> 警惕自己不是程序员！
>
> <p align="right">——jabingu　　</p>



> 记录的python的一些使用上的技巧，主要是自己在使用别人的代码的时候进行一下摘抄



## main

> 规范程序主体结构的书写(日后持续的进行跟进修改)

**主要的特点：**

- 规范化程序的编写，减小日后再次阅读的困难。
- 默认增加时间计时，方便对代码的复杂度有一个时间上的概念
- 每一个函数前面增加说明，使用`'''函数说明'''` 字符串来进行字体高亮显示说明

```python
# -*- coding: utf-8 -*-
'''
Created on 时间
@author: jabingu
@function:程序模版
'''
import time
'''程序主体函数'''
...
'''主函数'''
if __name__ == '__main__':
    time_start = time.time() #开始时间
    '''程序主体函数'''
    time_end = time.time()   #结束时间
    print('---------------------:------------')
    print('Program running time ：%.4f Second '%(time_end - time_start))
```



## @staticmethod

> 在实际进行操作的时候，发现很多函数是会被反复的进行调用的，当然我们是可以使用函数来进行封装的，但是如果这样的函数很多，那么我们就可以使用类来进行再次的封装，并使用`@staticmethod`来使得其脱离正常类使用的范畴。
>
> 在这里基础上，我们也是可以把这些函数单独放在一个文件中，使用`import`来进行导入，使得我们单个文件更加的简介

python staticmethod 返回函数的静态方法。

该方法不强制要求传递参数，如下**声明**一个静态方法：

```python
class C(object):
    @staticmethod
    def f(arg1, arg2, ...):
        ...
```

以上实例声明了静态方法 **f**，从而可以实现实例化使用 **C().f()**，当然也可以不实例化调用该方法 **C.f()**。

**示例**

```python
# -*- coding: UTF-8 -*-
class C(object):
    @staticmethod
    def f():
        print('runoob');
 
C.f();          # 静态方法无需实例化
cobj = C()
cobj.f()        # 也可以实例化后调用
```

**输出**

```python
runoob
runoob
```



## 参考文献

[Python staticmethod() 函数](https://www.runoob.com/python/python-func-staticmethod.html)