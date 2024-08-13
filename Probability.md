## 一、条件空间和事件

### 1. 条件空间

假定所有可能出现的情况都是给定集合 $\mathbf\Omega$ 的子集，我们将 $\mathbf\Omega$ 称为**样本空间**或**条件空间**。

### 2. 事件

把样本空间中的元素称为**事件**。

### 3. 概率函数

一旦有了样本空间，我们就想为样本空间中的具体事件来制定概率。因此我们引入**概率函数**来描述时间的概率。

### 4. 实例

我们以经典的投色子举例，一次投色子的样本空间是什么？
$$
\mathbf\Omega\,=\,\{1,\,2,\,3,\,4,\,5,\,6\}
$$

举例一些事件：

掷出数字 6 记为事件 $\mathbf{A}$ ，可以将事件 $\mathbf{A}$ 用集合表示为：
$$
\mathbf{A}\,=\,\{6\}
$$
掷出的点数不小于 4 记为事件 $\mathbf{B}$，同样用集合将事件 $\mathbf{B}$表示为：
$$
\mathbf{B}\,=\,\{4,\,5,\,6\}
$$
可以很自然的得出，事件 $\mathbf{A}$ 的概率函数为：
$$
\mathrm{P}(\mathbf{A})\,=\,\frac{1}{6}
$$

### 5.事件关系与运算

关系：

1. 包含
2. 相等
3. 互斥：积事件为空，$\mathbf{\mathit{AB}}\,=\,\phi$

运算：

1. 和事件
2. 积事件
3. 差事件



## 二、古典概型

### 概率定义

> ***统计性定义***

随着实验次数增加，出现频率趋于一个稳定值



> ***公理化定义***

todo

## 三、条件概率

> 问题：
>
> 已知某家庭有两个孩子，其中一个是女孩儿，则另一个也是女孩儿的概率是多少？

首先需要厘清条件空间，家庭中有两个孩子，则一共有 4 种可能的组合：
$$
\mathbf{\Omega}\,=\,\{(兄弟),\,(姐妹),\,(兄妹),\,(姐弟)\}
$$
假设有一个孩子是女孩儿为事件 $\mathbf{A}$，则有三种可能：
$$
\mathbf{A}\,=\,\{(姐妹),\,(兄妹),\,(姐弟)\}
$$
事件 $\mathbf{A}$ 的概率为：
$$
\mathrm{P(\mathbf{A})}\,=\,\frac{3}{4}
$$
最终发生的事件我记为事件 $\mathbf{B}$：
$$
\mathbf{B}\,=\,\{(姐妹)\}
$$
事件 $\mathbf{B}$ 的概率为：
$$
\mathrm{P(\mathbf{B})}\,=\,\frac{1}{4}
$$
问题转化为事件 $\mathbf{A}$ 发生的前提下事件 $\mathbf{B}$ 发生的概率。因为事件 $\mathbf{A}$ 发生了，所以现在的样本空间已经缩小为：
$$
\mathbf{\Omega}\,=\,\{(姐妹),\,(兄妹),\,(姐弟)\}
$$
我们将事件 $\mathbf{A}$ 发生的前提下事件 $\mathbf{B}$ 发生的概率记为 $\mathrm{P(\mathbf{B}\,|\,\mathbf{A})}$ 并称之为**条件概率**，则有：
$$
\mathrm{P(\mathbf{B}|\mathbf{A})}\,=\,\frac{1}{3}
$$

> 【**注意**】一旦有前提条件，就会将样本空间缩小，新的样本空间是之前样本空间的子集。



> 事件不是孤立的，某个事件的发生会对另一个事件发生的概率产生影响。所谓**条件概率**就是在已知其他事件发生的前提下，某个事件发生的概率。

我们希望在已知 $\mathrm{P(\mathbf{A})}$ 和  $\mathrm{P(\mathbf{B})}$ 的情况下给出一个简洁的条件概率 $\mathrm{P(\mathbf{B}|\mathbf{A})}$ 的计算公式。

设 $\mathbf{A}$ 是满足 $\mathrm{P(\mathbf{A})}>0$ 的事件，则已知 $\mathbf{A}$ 发生时 $\mathbf{B}$ 发生的条件概率为：
$$
\mathrm{P(\mathbf{B}|\mathbf{A})}\,=\,\frac{\mathrm{P(\mathbf{A\cap{B}}})}{\mathrm{P(\mathbf{A})}}
$$
 为什么要加上前提条件 $\mathrm{P(\mathbf{A})}>0$ ，因为如果前提条件发生概率为 0 ，那么讨论条件概率是没有意义的。

根据条件概率公式我们可以变形为**一般乘法法则**：
$$
\mathrm{P(\mathbf{A\cap{B}})}\,=\,\mathrm{P(\mathbf{B}|\mathbf{A})}\cdot\mathrm{P(\mathbf{A})}
$$
如果条件概率和 $\mathbf{A}$ 的概率都很容易计算，那么利用这个变式可以很容易计算出 $\mathbf{A}$ 和 $\mathbf{B}$ 同时发生的概率。 

## 四、独立性

### 4.1 两事件独立

事件的**独立性**是概率论中最重要的概念之一。独立性的含义是什么呢？指的是两个事件互不影响。那什么又是互不影响呢？其含义就是从一个事件发生无法推断出另一个事件的可能性。

例如：

抛硬币。你某次抛出结果为正面朝上的概率是不受上次影响的（保证其他因素一样的情况下）。我们可以认为连续抛硬币的结果是相互独立的事件。我们可以利用条件概率来给出独立性的**临时定义**：如果事件 $\mathbf{B}$ 和事件 $\mathbf{A}$ 满足：
$$
\mathrm{P(\mathbf{B}|\mathbf{A})}\,=\,\mathrm{P(\mathbf{B})}
$$
那么说事件 $\mathbf{B}$ 相对于事件 $\mathbf{A}$ 是独立的。公式解读：事件 $\mathbf{B}$ 发生的概率不受事件 $\mathbf{A}$  发生概率的影响。

为什么说是临时定义？因为独立应该是相互的（具有对称性），而这个公式没有体现出事件 $\mathbf{A}$ 相对于事件 $\mathbf{B}$ 的独立性。两事件独立性的正式定义如下：

> ***独立性（两事件）***：如果事件 $\mathbf{A}$ 和事件 $\mathbf{B}$ 满足：
> $$
> \mathrm{P(\mathbf{A\cap{B}})}\,=\,\mathrm{P(\mathbf{A})}\cdot\mathrm{P(\mathbf{B})}
> $$
> 那么事件 $\mathbf{A}$ 和事件 $\mathbf{B}$ 就是相互独立的。

### 4.2 三事件独立

三个或者更多事件之间的相互独立可以通过两个事件的独立来进行扩展：

> ***独立性（三事件）***：如果事件 $\mathbf{A}$ 、$\mathbf{B}$ 和 $\mathbf{C}$ 满足：
>
> 1. $\mathrm{P(\mathbf{A\cap{B}\cap{\mathbf{C}}})}\,=\,\mathrm{P(\mathbf{A})}\cdot\mathrm{P(\mathbf{B})}\cdot\mathrm{P(\mathbf{C})}$
> 2. 其中任意两事件独立
>
> 那么事件 $\mathbf{A}$ 、$\mathbf{B}$ 和 $\mathbf{C}$ 就是相互独立的。

### 4.3 多事件独立

todo



## 五、贝叶斯定理

根据一般乘法法则有：
$$
\begin{equation}
\mathrm{P(\mathbf{A\cap{B}})}\,=\,\mathrm{P(\mathbf{B}|\mathbf{A})}\cdot\mathrm{P(\mathbf{A})}\tag{5.1}
\end{equation}
$$
根据对称性有：
$$
\begin{equation}
\mathrm{P(\mathbf{A\cap{B}})}\,=\,\mathrm{P(\mathbf{A}|\mathbf{B})}\cdot\mathrm{P(\mathbf{B})}\tag{5.2}
\end{equation}
$$
根据等式 **5.1** 和 **5.2** 很容易得出以下结论：
$$
\begin{equation}
\mathrm{P(\mathbf{A}|\mathbf{B})}\cdot\mathrm{P(\mathbf{B})}\,=\,\mathrm{P(\mathbf{B}|\mathbf{A})}\cdot\mathrm{P(\mathbf{A})}\tag{5.3}
\end{equation}
$$
因此，只要满足 $\mathrm{P(\mathbf{B})}\neq0$ 的条件下，有以下结论：
$$
\begin{equation}
\mathrm{P(\mathbf{A}|\mathbf{B})}\,=\,\mathrm{P(\mathbf{B}|\mathbf{A})}\cdot\frac{\mathrm{P(\mathbf{A})}}{\mathrm{P(\mathbf{B})}}\tag{5.4}
\end{equation}
$$
等式 5.4 就是大名鼎鼎的**贝叶斯定理**。
