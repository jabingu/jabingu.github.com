---

layout: post
title:  "py：判断字符串是不是由数字组成"
date:   2019-12-23 07:14:54
categories: python
tags: python 
thumbnail: "assets/img/post/python.jpg"
feature-img: "assets/img/post/python.jpg"
excerpt: python判断字符串是不是由数字组成
---

* content
{:toc}
> 有时候我们提取到的数字是以字符串的形式保存的，所以是需要把它变化成数字的，然后再进行处理



## 字符串变化数字

### float()

> 这里需要注意的是在python中int是无法进行把字符串转化成整数的，需要先转化成浮点数再转化成整数类型的。

**输入**

```python
float('123')
```

**返回**

```python
123
```

### eval()

> `eval()`函数用来执行一个字符串表达式，并返回表达式的值。所以如果字符串是由数字组成的，那么就是会返回数字的值。

**输入**

```python
eval('123')
```

**返回**

```python
123
```



## 判断是否数字

> 这里我原来的想法是要先判断字符串中是不是只有数字1-9还有符号和指数表达e。再判断是什么类型的。后来发现其实是不需要这么麻烦的，调用自带的`float()`函数，如果可以执行就是数字类型的。否则就报错表示不是数字。
>

```python
def is_number(s):
    try:
        float(s)
        return True
    except ValueError:
        pass
  
    try:
        import unicodedata
        unicodedata.numeric(s)
        return True
    except (TypeError, ValueError):
        pass
    return False
```



## 参考文献

[python判断字符串是否为数字](https://www.py.cn/faq/python/12110.html)

[Python eval() 函数](https://www.runoob.com/python/python-func-eval.html)

