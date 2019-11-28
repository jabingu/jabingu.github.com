---

layout: post
title:  "py：画柱状图"
date:   2019-11-27 07:14:54
categories: python
tags: python matplotlib
thumbnail: "assets/img/post/python.jpg"
feature-img: "assets/img/post/python.jpg"
excerpt: python使用matplotlib来画出柱状图
---

* content
{:toc}
> 记录的python的使用matplotlib来进行画图
>
> matplotlib和matlab画图的思想类似



## 柱状图

### 参数说明：

- **labels**：每一个显示的柱状图的标志
- **men_means**：具体的数值
- **x**：每一个柱状图显示的中心位置
- **width**：柱状图的宽度
- **autolabel**：柱状图上显示数值的函数

```python
import matplotlib.pyplot as plt
import numpy as np

labels = ['G1', 'G2', 'G3', 'G4', 'G5']
men_means = [20, 34, 30, 35, 27]
women_means = [25, 32, 34, 20, 25]

x = np.arange(len(labels))  # the label locations
width = 0.35  # the width of the bars

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, men_means, width, label='Men')
rects2 = ax.bar(x + width/2, women_means, width, label='Women')

# Add some text for labels, title and custom x-axis tick labels, etc.
ax.set_ylabel('Scores')
ax.set_title('Scores by group and gender')
ax.set_xticks(x)
ax.set_xticklabels(labels)
ax.legend()

def autolabel(rects):
    """Attach a text label above each bar in *rects*, displaying its height."""
    for rect in rects:
        height = rect.get_height()
        ax.annotate('{}'.format(height),
                    xy=(rect.get_x() + rect.get_width() / 2, height),
                    xytext=(0, 3),  # 3 points vertical offset
                    textcoords="offset points",
                    ha='center', va='bottom')


autolabel(rects1)
autolabel(rects2)

fig.tight_layout()
plt.show()
```

###  效果图：

<center><img src="https://i.loli.net/2019/11/28/gC8TyMv4GR2sDEx.png" alt="bar.png" border="0"></center>

## 图案填充

> 使用过程中，有一些论文中会要求颜色黑白化，所以我们要在柱状图内部填充其他图案来进行区别
>
> 主要用到`bar`中的`hatch`参数

Set the hatching pattern

*hatch* 可选的**参数**有：

```python
/   - diagonal hatching
\   - back diagonal
|   - vertical
-   - horizontal
+   - crossed
x   - crossed diagonal
o   - small circle
O   - large circle
.   - dots
*   - stars
```

Letters can be combined, in which case all the specified hatchings are done. If same letter repeats, it increases the density of hatching of that pattern.

Hatching is supported in the PostScript, PDF, SVG and Agg backends only.

把原来的

```python
rects1 = ax.bar(x - width/2, men_means, width, label='Men')
rects2 = ax.bar(x + width/2, women_means, width, label='Women')
```

改成:

```python
rects1 = ax.bar(x - width/2, men_means, width, label='Men',hatch='/')
rects2 = ax.bar(x + width/2, women_means, width, label='Women',hatch='.')
```

### 效果图：

<center><img src="https://i.loli.net/2019/11/28/6UlAQBL7x1fm5YK.png" alt="bar_hatch.png" border="0"></center>

## bar常用参数

- **x** ：x轴位置
- **height**  ：高度
- **width**  ：宽度
- **color**：填充颜色
- **edgecolor**：边框颜色（使用黑色可以显示边框）
- **hatch**：图案填充



## 参考文献

[matplotlib.axes.Axes.bar](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.bar.html#matplotlib.axes.Axes.bar)

[Grouped bar chart with labels](https://matplotlib.org/gallery/lines_bars_and_markers/barchart.html#sphx-glr-gallery-lines-bars-and-markers-barchart-py)

