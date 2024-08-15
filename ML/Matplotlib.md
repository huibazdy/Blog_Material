# Matplotlib

> 这篇文档主要介绍Matplotlib基本功能以及它在数据分析与可视化方面的应用案例。



# 一、常见实例

## 1.1 散点图



## 1.2 曲线图



## 1.3 柱状图



## 1.4 离散序列



## 1.5 台阶图



# 二、理解 figure 和 axes

## 2.1 Figure 和 Axes

我们首先了解一下 **Matplotlib** 中对一张图的基本定义：

* **Figure** 是一整张纸（画布）
* **Axes** 是整张纸上的指定的绘制区域（画框）

## 2.2 pyplot 和 ax

**Matplotlib** 中存在两种不同的绘图方式：

1. `plt.plot()`：隐式（implicit）

2. `ax.plot()`：显式（explicit）

### 2.2.1 基本使用

第一种方式：

```python
import matplotlib.pyplot as plt
plt.figure()
plt.plot([1,2,3],[4,5,6])  # 三个点：(1,4)，(2,5)，(3,6)
plt.show()
```

第二种方式：
```python
import matplotlib.pyplot as plt
fig,ax = plt.subplots()
ax.plot([1,2,3],[4,5,6])
plt.show()
```

两种方式的绘制结果（如下）相同：

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

>两种绘制方式的逻辑区别：
>
>1. 隐式生成了一个 Figure 对象并在此区域内画图；
>2. 显式生成了一个 Figure 对象（`fig`）和一个 Axes 对象（`ax`），然后用`ax`对象在`fig`内画图。
>
>后者使用了面向对象思维，用`fig`和`ax`两个对象来对画布（Figure）以及绘图区域（Axes）进行控制。如果针对复杂的图或多个子图构成的大图，第一种就会显得非常不直观。
>
>（[参考资料](https://cloud.tencent.com/developer/article/1790549)）



### 2.2.2 子图绘制

【例】绘制两个子图，左边为折线图，右边为散点图

* **`pyplot`** 方法

  ```python
  import matplotlib.pyplot as plt
  plt.subplot(1, 2, 1)             #指定子图
  plt.plot([1,2,3],[4,5,2])        #绘制左子图
  plt.subplot(1, 2, 2)             #指定子图
  plt.scatter([1,2,3],[4,5,2])     #绘制右子图
  plt.show()

* **`Axes`** 方法

  ```python
  import matplotlib.pyplot as plt
  fig = plt.figure()
  ax = fig.subplots(nrows=1,ncols=2)
  ax[0].plot([1,2,3],[4,5,2])        #绘制左子图
  ax[1].scatter([1,2,3],[4,5,2])     #绘制右子图
  plt.show()

绘制效果：

<img src="E:\GitHub\Blog_Material\ML\Images\002.png"  />

在这里共有两个Axes对象，分别对应两个子图的绘制区域。

## 2.3 Axes 元素

### 2.3.1 轴

#### Matplotlib 中的轴

---

1. top
2. bottom
3. left
4. right

#### **获取轴**

---

* `ax = plt.gca()`
* `ax = plt.axes()`

#### **设置边框**

---

以设置 bottom 为例：

* 线形：`ax.spines['bottom'].set_linestyle("--")`
* 线宽：`ax.spines['bottom'].set_linewidth(2.0)`
* 颜色：`ax.spines['bottom'].set_color('red')`
* 显示：`ax.spines['bottom'].set_visible(False)`

#### 坐标轴

# 参考资料

1. [利用Python进行数据分析](https://wesmckinney.com/book/)