# Matplotlib学习笔记

## 基础图像

### 线形图

### plot(x,y)

```python
import matplotlib.pyplot as plt
import numpy as np

#set style
plt.style.use('_mpl-gallery')

#make data
x = np.linspace(0,10,100)
y = 4 + 2 * np.sin(2 * x)

#plot
fig,ax = plt.subplots() #创建只包含一个Axes对象（此处对象就是ax）的figure

ax.plot(x,y,linewidth=2.0) #在Axes对象（即：ax）上利用数据绘制图像

ax.set(xlim=(0,8),xticks=np.arange(1,8),
       ylim=(0,8),yticks=np.arange(1,8))

plt.show()
```

执行效果如下：

<img src="https://raw.githubusercontent.com/huibazdy/TyporaPicture/main/202210291551652.png" style="zoom: 50%;" />

绘制Matplotlib图形时，都需要先创建一个图形`fig`和一个坐标轴`ax`，创建图形和坐标轴最简单的方法如下：

```python
fig = plt.figure()
ax = plt.axes()
#等价于一个语句：fig,ax = subplots()
```



### 图像元素

一张matplotlib的`figure`中包含以下元素：

<img src="https://raw.githubusercontent.com/huibazdy/TyporaPicture/main/202210301449096.png" alt="image-20221030144912026" style="zoom: 80%;" />

创建`figure`的几种典型方式：

```python
fig = plt.figure()  # an empty figure with no Axes
fig, ax = plt.subplots()  # a figure with a single Axes
fig, axs = plt.subplots(2, 2)  # a figure with a 2x2 grid of Axes
```

在创建图像的同时创建Axes对象是非常方便的，但是你也可以选择之后在手动添加Axes对象。



### 两种绘图风格

* ***显式***创建`figure`与`Axes`对象，而后调用他们的方法（即面向对象编程风格）

* 依靠`pyplot`***隐式***创建和操作`figure`和`Axes`对象，然后利用`pyplot`函数绘图

    

【**显式**】

```python
import matplotlib as mlp
import matplotlib.pyplot as plt
import numpy as np

#创建数据(sampling data)
x = np.linspace(0,2,100)

#创建图像和一个Axes对象
fig, ax = plt.subplots(figsize=(5,2.7),layout='constrained')

#绘制图像
ax.plot(x,x,label='linear')
ax.plot(x,x**2,label='quadratic')
ax.plot(x,x**3,label='cubic')
ax.set_xlabel('xlabel')
ax.set_ylabel('ylabel')
ax.set_title('Simple Plot')
ax.legend()
```



【**隐式**】

```python
import matplotlib as mlp
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 2, 100)  # Sample data.

plt.figure(figsize=(5, 2.7), layout='constrained')
plt.plot(x, x, label='linear')  # Plot some data on the (implicit) axes.
plt.plot(x, x**2, label='quadratic')  # etc.
plt.plot(x, x**3, label='cubic')
plt.xlabel('x label')
plt.ylabel('y label')
plt.title("Simple Plot")
plt.legend();
```



> **注意**：在将Matplotlib嵌入GUI应用中时，会完全抛弃`pyplot`，即使是创建`figure`也不再使用。更多关于嵌入Matplotlib到GUI应用中的文档可以参考：[Embedded Matplotlib in GUI](https://matplotlib.org/stable/gallery/user_interfaces/index.html#user-interfaces)



### 辅助函数

对于同一个绘图逻辑，想针对不同输入数据多次复用，可以用定义辅助函数的方式：

```python
def my_plotter(ax,data1,data2,param_dict):
    """
    A helper function to make a graph
    """
    out = ax.plot(data1,data2,**param_dict)
    return out
```

