## 线性回归

```python
# 导入简单的 wave 数据集
import mglearn
X, y = mglearn.datasets.make_wave(n_samples=60)

# 划分数据集
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y,random_state=42)

# 训练 lr 线性回归模型
from sklearn.linear_model import LinearRegression
lr = LinearRegression().fit(X_train, y_train)

# “斜率”（或者说权重向量） [w] 保存在 coef_ 属性中，偏移 b 保存在 intercept_ 属性中
print("lr.coef_: {}".format(lr.coef_))               # [0.39]
print("lr.intercept_: {}".format(lr.intercept_))     # -0.032

# 分别测试训练性能和泛化性能
print("Training set score: {: .2f}".format(lr.score(X_train, y_train)))
print("Test set score: {: .2f}".format(lr.score(X_test, y_test)))
```

性能测试结果：

Training set score:  0.67
Test set score:  0.66

> 标准线性回归的 $R^2$ 值较低（约为 0.66），训练集和测试集的分数非常接近，说明可能存在**欠拟合**。不过此处只是一维数据集，对于高维（有大量特征）复杂数据集，过拟合可能性变高。



```python
# 导入Boston 房价数据集
import mglearn
X, y = mglearn.datasets.load_extended_boston()

# 划分数据集
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y,random_state=0)

# 训练 lr 线性回归模型
from sklearn.linear_model import LinearRegression
lr = LinearRegression().fit(X_train, y_train)

# 分别测试训练性能和泛化性能
print("Training set score: {: .2f}".format(ridge.score(X_train, y_train)))
print("Test set score: {: .2f}".format(ridge.score(X_test, y_test)))
```

性能测试结果：

Training set score:  0.95
Test set score:  0.61

> 训练集和测试集之间的性能差异是**过拟合**的明显标志，因此需要找一个可以控制复杂度的模型。

## 岭回归

* 一种类似标准线性回归的线性模型（作为标准线性回归的替代方法）
* 对系数（***w***）要求：除了得到较好的预测结果，还有对模型附加显性约束（来避免过拟合），希望 ***w*** 尽量小（都接近 0）
* 这种显性约束是一种 **L2** 正则化
* 目的是避免过拟合
* 在`linear_model.Ridge`中实现



```python
# 导入Boston 房价数据集
import mglearn
X, y = mglearn.datasets.load_extended_boston()

# 划分数据集
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y,random_state=0)

# 训练集拟合 Ridge 线性回归模型
from sklearn.linear_model import Ridge
ridge = Ridge().fit(X_train, y_train)

# 对训练集和测试集性能分别进行评估，评估标准是 R^2 值
print("Training set score: {: .2f}".format(ridge.score(X_train, y_train)))
print("Test set score: {: .2f}".format(ridge.score(X_test, y_test)))
```

处理结果；

Training set score:  0.89
Test set score:  0.75



Ridge 模型在简单性（系数都接近0）和训练集性能之间做权衡，通过 alpha （默认是 0）参数来调整二者关系。关于 alpha 有以下事实：

* alpha 越大，系数约趋于 0，降低训练集性能，可能会提高泛化性能

```python
# alpha = 10
ridge01 = Ridge(alpha=10).fit(X_train, y_train)
print("Training set score: {: .2f}".format(ridge01.score(X_train, y_train)))
print("Test set score: {: .2f}".format(ridge01.score(X_test, y_test)))
```

测试结果：

Training set score:  0.79
Test set score:  0.64

```python
# alpha = 0.1
ridge02 = Ridge(alpha=0.1).fit(X_train, y_train)
print("Training set score: {: .2f}".format(ridge02.score(X_train, y_train)))
print("Test set score: {: .2f}".format(ridge02.score(X_test, y_test)))
```

测试结果：

Training set score:  0.93
Test set score:  0.77