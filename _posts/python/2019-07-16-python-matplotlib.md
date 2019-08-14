---

layout: post
title:  "py：画图通用模版"
date:   2019-07-16 07:14:54
categories: python
tags: python matplotlib
excerpt: python使用matplotlib来进行画图的通用模版，方便日后的使用
---

* content
{:toc}
> 记录的python的使用matplotlib来进行画图
>
> matplotlib和matlab画图的思想类似



## 最简单的模版

单纯的把数据显示出来。

```python
import matplotlib.pyplot as plt#导入库

date_x=list(range(0,10))#x坐标
date_y=list(range(0,10))#y坐标
plt.plot(date_x, date_y)#添加曲线
plt.show()#显示图片
```

<center><img src="https://s2.ax1x.com/2019/07/17/Zq21qU.png" alt="Zq21qU.png" border="0"></center>
## 复杂的模版

在一个画布上显示两条曲线，并添加标题，x坐标名字，y坐标名字，曲线名字

其中第2-4行代码是为了显示中文

```python
import matplotlib.pyplot as plt#导入库
from pylab import mpl
mpl.rcParams['font.sans-serif'] = ['SimHei'] #指定默认字体
mpl.rcParams['axes.unicode_minus'] = False   #解决保存图像是负号'-'显示为方块的问题

date_x=list(range(0,10)) #x坐标
date_y1=list(range(0,10))#y坐标
date_y2=list(range(1,11))#y坐标

plt.figure()#生成第一个画布
plt.grid()   #生成网格
plt.title("复杂的模版")  #添加标题
plt.xlabel('this is x')#x坐标名字
plt.ylabel('this is y')#y坐标名字
plt.plot(date_x,date_y1,'-',label='date_y1')#label为图例
plt.plot(date_x,date_y2,'-',label='date_y2')
plt.legend() # 显示图例
plt.show()
```



<center><img src="https://s2.ax1x.com/2019/07/17/Zq28ZF.png" alt="Zq28ZF.png" border="0"></center>

## 函数封装

为了更加方便的使用画图函数，对画图函数进行了封装。其中

**输入：**

- **fugure_name**：标题
- **y_name**：纵坐标名字
- **data_x**：横坐标数据
- **data_y**：纵坐标数据
- **curve**：曲线式样，默认为直线

```python
import matplotlib.pyplot as plt#导入库
from pylab import mpl
mpl.rcParams['font.sans-serif'] = ['SimHei'] #指定默认字体
mpl.rcParams['axes.unicode_minus'] = False   #解决保存图像是负号'-'显示为方块的问题

'''个人的画图函数'''
def guFigure(fugure_name,y_name,data_x,data_y,curve='-'):
    plt.figure()            #新建图纸
    plt.title(fugure_name)  #添加标题
    plt.plot(data_x,data_y,curve,label=y_name)
    plt.grid()              #显示网格
    plt.legend()            #显示图例
    plt.show()  
```





## 参数说明

> plt.plot(date_x,date_y1,'-',label='date_y1') #label为图例

这里的`‘-’`表示线条是直线，当然默认也是直线，我们还可以选择其他的线条或者是点来显示数据。也可以自己设置颜色比如`‘-b’`表示蓝色的直线

### 线条标记

|     标记      | **描述** | **标记** |     **描述**     |
| :-----------: | :------: | :------: | :--------------: |
|      ‘o’      |   圆圈   |   ‘.’    |        点        |
|      ‘D’      |   菱形   |   ‘s’    |      正方形      |
|      ‘h’      | 六边形1  |   ‘*’    |       星号       |
|      ‘H’      | 六边形2  |   ‘d’    |      小菱形      |
|      ‘_’      |  水平线  |   ‘v’    | 一角朝下的三角形 |
|      ‘8’      |  八边形  |   ‘<’    | 一角朝左的三角形 |
|      ‘p’      |  五边形  |   ‘>’    | 一角朝右的三角形 |
|      ‘,’      |   像素   |   ‘^’    | 一角朝上的三角形 |
|      ‘+’      |   加号   |   ‘\\'   |       竖线       |
| ‘None’,’’,’ ‘ |    无    |   ‘x’    |        X         |

### 颜色

| 别名 | **颜色** | 别名 | **颜色** |
| :--: | :------: | :--: | :------: |
|  b   |   蓝色   |  g   |   绿色   |
|  r   |   红色   |  y   |   黄色   |
|  c   |   青色   |  k   |   黑色   |
|  m   |  洋红色  |  w   |   白色   |



## 参考文献



[matplotlib](https://matplotlib.org/users/screenshots.html)

[matplotlib新手教程](http://azaleasays.com/2010/04/27/matplotlib-beginner-guide/)

[Python--matplotlib绘图可视化知识点整理](https://www.cnblogs.com/zhizhan/p/5615947.html)