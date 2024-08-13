# Naive Bayes

> 朴素贝叶斯分类器是与线性模型类似的分类器，但它的训练速度往往更快，快速的带捷爱士泛化能力稍差（对比 LogisticRegression 和 LinearSVC）。

scikit-learn 实现了三种朴素贝叶斯分类器：

| 分类器           | 输入数据类型 | 典型应用     |
| ---------------- | ------------ | ------------ |
| **GaussionNB**   | 任意连续数据 |              |
| **BernoulliNB**  | 二分类数据   | 文本数据分类 |
| **MultinomiaNB** | 计数数据     | 文本数据分类 |



> 一个例子理解 **BernoulliNB** 分类器

**BernoulliNB** 分类器会计算每个类别中每个特征不为 0 的元素个数

