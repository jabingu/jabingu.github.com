---

layout: post
title:  "py：获取大文件的第一和最后一行数据"
date:   2019-12-11 07:14:54
categories: python
tags: python matplotlib
thumbnail: "assets/img/post/python.jpg"
feature-img: "assets/img/post/python.jpg"
excerpt: python获取文件的第一或者是最后几行的数据
---

* content
{:toc}
> 有时候我们会有对大文件读取第一行和最后一行的需求。



## 读取第一行

> 主要思想是：从第一行开始，一行一行的读取，然后判断空行。

```python
import os
def __get_first_line(filename):
    try:
        filesize = os.path.getsize(filename)
        if filesize == 0:
            return None
        else:
            with open(filename, 'r') as fp: 
                # to use seek from end, must use mode 'rb'
                while 1:
                    line = fp.readline()  # read from fp to eof
                    if len(line) >= 16:     
                        # if contains at least 16 byte
                        return line    
    except FileNotFoundError:
        print(filename + ' not found!')
        return None
```



## 读取最后一行

> 主要思想是：将读取文件的指针移动到文件尾部，然后读取指针到文件尾部之间的内容

```python
import os
def __get_last_line(filename):
    """
    get last line of a file
    :param filename: file name
    :return: last line or None for empty file
    """
    try:
        filesize = os.path.getsize(filename)
        if filesize == 0:
            return None
        else:
            with open(filename, 'rb') as fp: # seek下必须使用‘rb’
                offset = -8                 # 偏移量
                while -offset < filesize:   # 范围鉴定
                    fp.seek(offset, 2)      # 2表示尾部开始
                    lines = fp.readlines()  # 读取指针到文件尾的所有行
                    if len(lines) >= 2:     # 
                        return lines[-1].decode('ascii') #二进制解码
                    else:
                        offset *= 2         # 偏移量迭代
                fp.seek(0)
                lines = fp.readlines()
                return lines[-1]
    except FileNotFoundError:
        print(filename + ' not found!')
        return None
```





## 参考文献

[使用seek()方法报错：can't do nonzero end-relative seeks](https://blog.csdn.net/earthchinagl/article/details/80191966)

[python读取文件最后一行](https://blog.csdn.net/liuweiyuxiang/article/details/93213202)