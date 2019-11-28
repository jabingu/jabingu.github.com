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

### **参数说明：**

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


## 参考文献

[Grouped bar chart with labels](https://matplotlib.org/gallery/lines_bars_and_markers/barchart.html#sphx-glr-gallery-lines-bars-and-markers-barchart-py)

