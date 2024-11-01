## 相似度度量（Similatiry Scoring）

相似度度量的原理是利用一个函数来判断两个音频嵌入码是否具有一致性。

输入：分别是运行时录入得到的和训练时用户录入的声纹档案，可以分别表征为两个向量，分别是：

* 运行时音频特征：$\mathbf {e_1}$
* 运行前用户录入的声纹特征：$\mathbf {e_2}$

### 余弦相似度

计算两个向量在欧式空间中的夹角，分子是向量内积，分母是两个向量的 L2 范数乘积：

越大与相似。

### 欧氏距离

对两向量的差再取 L2 范数得到：

然后再对其取倒数。

越小越相似。

> 注意：
>
> 余弦相似度与向量长度无关，因为分母中有 L2 范数，相当于是单位向量。但欧氏距离是和限量长度相关的。



### 基于模型的相似度量

前面两种打分机制都是没有任何参数的，只和输入特征向量有关。除此之外还有另外的一种打分情况，那就是基于**可变参数**模型的相似度量。

简而言之：就是用一个带参数向量（$\boldsymbol\theta$）的函数来进行打分，输入变量还是两个向量。
$$
\boldsymbol{f}\,(\bold{e_1},\bold{e_1}\,|\,\boldsymbol{\theta})
$$
这里的 $\boldsymbol{f}(\bold{\cdot})$一般指的就是 AI 模型。可能是 ML ，也可能是一个 ANN 。注意，此处的神经网络一般称为**决策网络**（**Decision Network**）。

> 怎样理解参数向量 $\boldsymbol\theta$ ？

例如此处的 $\boldsymbol{f}(\bold{\cdot})$ 是一个简单的多项式，那么这个多项式的系数就组成了参数向量 $\boldsymbol\theta$ 。如果模型比较复杂，例如一个神经网络，那么 $\boldsymbol\theta$ 就是一个神经网络的参数（权重weights、偏差bias等）。

$\boldsymbol\theta$ 是由训练数据得到的参数向量。



> 基于模型的相似度量的变种——**Dr-Vectors**

融合了余弦相似度和神经网络两种相似度度量方式，然后将二者的分数相加。

* 余弦相似度使用了整个声纹嵌入码
* 决策网络只使用了声纹嵌入码的一部分维度

这种变种相似度度量方法保留了两种方式的优势。



## 决策（Thresholding）

设定阈值 T ，当相似性度量不小于 T 认为声纹时匹配的。可以分为三种应用情况：

* low threshold：直接冻结
* medium threshold：拒绝后，允许充重试
* high threshold：直接接受



## 评价

> 如何评价一个声纹识别系统的好坏？

例如有两个声纹识别系统 A 和 B，需要保证一些评价变量的一致性：

1. 测试集
2. 指标
3. 测试流程

总的来说有两种评价方式：

1. 基于语音对——Pair-Based
2. 基于集合——Set-Based



### 构建测试集

构建测试集需要保证以下几点要求：

1. 出现在训练集中的数据都不能再出现在测试集中；
2. 出现在训练集中的说话人都不能再出现在测试集中



### Pair-Based

由多组 trial pair 组成的一个 list 。每一个 trial pair 包含：

1. 两段音频（two utterances）：可能来自于同一说话人，也可能来自不同说话人。用一个标志位（0表示来自不同说话人，1表示来自相同说话人）来标记。

参考 **VoxCeleb** 数据集中 standard trial pairs 。

相当于一段音频是提前录入的 enrollment ，另一段是运行时录入的实时音频。

### Set-Based

实际情况中，可能有多个 enrollment （录入语音）。所以有时候需要基于集合的评价指标。实际做法是：

1. 将数据集划分为两个子集（录入数据集enrollment set 和验证数据集 verification set）



> 评价指标

一般来说有两个指标：

1. **TPR，True Positive Rate**
2. **FPR，False Positive Rate**

但有时候这两个指标对于两个系统是矛盾的，例如 A 系统 TPR 高，另一个系统 FPR 高，很难用这两个指标来评判系统好坏，这时候就引入了 **ROC**（**Receiver Operating Characteristic Curve，ROC**） 曲线 。该曲线 X 轴是 FPR，y 轴是 TPR（值域均为0~1），对于一个声纹识别系统，每一个阈值都对应 ROC 系统上的一个点。

如何通过 ROC曲线来量化说明一个系统的好坏程度呢？答案是：**AUC**，**Area Understand Curve**。AUC 越大，说明该系统的表现越好（AUC 值域为0-1）。



## 高斯混合模型-GMM

哪些变量可能符合高斯分布：

1. 基频：Fundamental Frequency
2. 共振峰：Formants
3. 声强：Intensity
4. 信噪比：Signal-to-Noise Rate
5. 音节长度：length of word/phoneme

那用很多个高斯分布是否可以来研究一个复杂问题？这就是 GMM 的目标。

GMM 基本***思想***：用很多简单函数（多变量高斯分布）通过线性组合（乘以权重）来拟合一个复杂函数。

当参数量达到一个比较大的规模后，会出现***过拟合***问题。解决方法有两种：

1. 共享协方差矩阵；
2. 简化协方差矩阵



## 深度学习

相对于 GMM 和 SVM ；

大量***并行计算***操作使得 Neural Network 在之前提出的时候无法实现，算力不够。目前使其优势突出的优势有以下几点：

1. 硬件：支持大量并行计算，例如 CUDA
2. 数据量：海量数据集的产生
3. 软件：开源 DL 框架使相关算法的使用门槛降低



神经网络的仿生学启发，神经元结构：

1. 树突（dendrite）：接受电信号
2. 轴突（axon）：传递电信号
3. 突触（synapse）：发送电信号

有一个生物学事实（**全有全无率**）是：神经元要么不被激活，被激活了就一定会有完整信号响应。

根据这个事实，可以用一个数学模型来描述激活过程，也就是***激活函数***。



> 基本神经元模型组成的常见神经网络

1. 前馈（**Feed-Froward** NN）
2. 卷积（**Convolutional** NN）
3. 循环（**Recurrent** NN）
4. 注意力机制（**Attention**）



> 损失函数

衡量预测值与实际值差异的一个函数，对于不同问题我们有多种定义损失函数的方法：

![image-20241030170521771](C:\Users\zdy\AppData\Roaming\Typora\typora-user-images\image-20241030170521771.png)

要让损失函数尽量小，就是以参数向量 $\Theta$ 为变量的优化问题，且是一个标准的无约束优化问题。如果**可微**，可以使用**梯度下降法**（**Gradient Descent**）。

在计算梯度下降法的时候会用到一种计算方法叫反向**传播算法**（**back-propagation**）。

随着参数规模增大，传统梯度下降计算效率降低（计算成本高昂），这时提出了一种改进，就是**随机梯度下降**法（**Stochastic Gradient Descent，SGD**）。也就是在计算过程中不是每一步都要计算损失函数，只对数据集的一个子集计算损失函数 L 和它的偏微分。

在计算 SGD 的过程中又涉及到另一个问题：**学习率**（Learning Rate）应该怎样选取。

1. 在训练初期，我们希望 LR 大一点，这样能尽快接近最优解；
2. 在训练后期，我们希望 LR 小一点，这样不会轻易远离最优解

一种常见做法是为 LR 设定一个**半衰期**（**helf-life**）。例如设定其为 K 步，那么每过 K 步，就将 LR 减半。

另外一种做法是自适应做法：

1. **Adagrad**
2. **AdaDelta**
3. **Adam**（业界最常用也是最成熟的做法，同时用到了自适应和动量）



> 小结：神经网络建模步骤

1. 弄清楚输入空间和输出空间，需要建立从 x 到 y 的映射；
2. 定义神经网络
3. 定义损失函数
4. 建立训练集
5. 选取优化算法：如 SGD 法
6. 优化 $\boldsymbol{\theta}$ 来使损失函数最小，例如：Adam 算法
7. 使用神经网络模型来预测实时数据

## 其他工作亮点

>  ADSP新算法落地以及性能问题处理

### ADSP crash 问题

1. 踩内存：stack overflow

   打印内存栈的起始基址地址（pxStack）以及当前指针位置（pxTopOfStack），当前指针向下移动来申请内存，当top>px时，说明内存还未分配完。踩内存时（pxStack会被写坏）不会触发Crash，只有被踩地址被后续访问才会触发。需要打debug patch 才能精准检查地址是否被写坏，打印 Exception。

   最终实验和讨论得出结论：给算法的Stack太小导致，集成新算法时需要重新考虑stack大小，最终增加了10KB。

2. 空间分配失败：malloc failed

   集成新算法需要考虑heap size，否则会出现 malloc failed。需要用到的内存在初始化时就要申请好，最好不要在算法的process过程中进行申请内存操作；及时查看算法需要的DRAM。

3. ADSP 性能问题

   抓取 cpu 占用率：

   ```shell
   #铃声响起时
   adb shell "echo runtime_status_start > sys/kernel/debug/audiodsp0"
   #复现卡顿后
   adb shell "echo runtime_status_start > sys/kernel/debug/audiodsp0,cat sys/kernel/debug/audiodsp0" > d:\cpu.txt
   ```

   通过抓取ADSP中各个人物的CPU占用率，可以看出 IDLE 卡顿时剩余很少，一般低于 5% 就会卡顿，PA 所在task占用达到 45%，a2dp 占用 35%，因此蓝牙以及pa场景容易卡顿。做了以下优化：

   * 艾为增加响铃场景，去除大部分效果类模块
   * 针对特定场景 AURISYS_SCENARIO 不挂载音效算法
   * offload 通路以前会挂载两个算法，因此将其从playback移动到music，因此只需要在music挂在算法即可

