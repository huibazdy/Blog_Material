# Matplotlib

> 这篇文档主要介绍Matplotlib基本功能以及它在数据分析与可视化方面的应用案例。



# 一、常见实例

## 1.1 散点图



## 1.2 曲线图



## 1.3 柱状图



## 1.4 离散序列



## 1.5 台阶图



# 二、理解 figure 和 axes

* figure是一整张纸
* axes是纸上的绘制区域

如图所示：



由此引出的两种不同的绘图方式：

* `plt.plot()`
* `ax.plot()`

第一种方式：

```python
import matplotlib.pyplot as plt

plt.figure()
plt.plot([1,2,3],[4,5,6])  # 三个点：(1,4)，(2,5)，(3,6)
plt.show()
```

绘制效果：

<img src="E:\GitHub\Blog_Material\ML\Images\001.png" style="zoom: 67%;" />

第二种绘制方式：

```python
import matplotlib.pyplot as plt
fig,ax = plt.subplots()
ax.plot([1,2,3],[4,5,6])
plt.show()
```

绘制结果：

<img src="E:\GitHub\Blog_Material\ML\Images\001.png" style="zoom:67%;" />

>从绘制结果来说没有区别，但背后逻辑不一样。
>
>1. 生成了一个 Figure 画布（隐式生成了一个 Figure 对象并在此区域内画图）；
>2. 生成了一个 Figure 对象（`fig`）和一个 axes 对象（`ax`），然后用`ax`对象在`fig`绘图区域内画图。
>
>根本区别在于是否用了面向对象思维，后者用`fig`和`ax`两个对象来对画布（Figure）以及绘图区域（Axes）进行控制。如果针对复杂的图或者多个子图构成的大图，第一种就显得非常不直观。
>
>（[参考资料](https://cloud.tencent.com/developer/article/1790549)）

【例】两个子图，左边折线图，右边散点图

```python
import matplotlib.pyplot as plt
fig,ax = plt.subplots(nrows=1,ncols=2)  #子图为1行2列排列
ax[0].plot([1,2,3],[4,5,2])
ax[1].scatter([1,2,3],[4,5,2])
plt.show()
```

绘制效果：

<img src="E:\GitHub\Blog_Material\ML\Images\002.png" style="zoom: 80%;" />

在这里共有两个Axes对象，分别对应两个子图的绘制区域。

# 参考资料

1. [利用Python进行数据分析](https://wesmckinney.com/book/)