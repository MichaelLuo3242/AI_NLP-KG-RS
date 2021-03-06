[[校招-基础算法]GBDT/XGBoost常见问题](https://zhuanlan.zhihu.com/p/81368182) 

[面试官如何判断面试者的机器学习水平？](https://www.zhihu.com/question/62482926/answer/210531386) ⭐️

https://zhuanlan.zhihu.com/p/31743196

作业的特征工程通过建模给Age赋值，可以参考





## AdaBoost

### 简介

Boosting，也称为增强学习或提升法，是一种重要的集成学习技术，能够将预测精度仅比随机猜度略高的**弱学习器增强为预测精度高的强学习器**，这在直接构造强学习器非常困难的情况下，为学习算法的设计提供了一种有效的新思路和新方法。

出的AdaBoost算法。AdaBoost是英文“Adaptive Boosting“（自适应增强）的缩写。

它的自适应在于前一个基本分类器**被错误分类的样本的权值会增大，而正确分类的样本的权值会减小**，并再次用来训练下一个基本分类器。

**同时，在每一轮迭代中，加入一个新的弱分类器**，直到达到某个预定的足够小的错误率或达到预先指定的最大迭代次数才确定最终的强分类器。

Adaboost的两个主要特性。

1. 训练的错误率上界， 随着迭代次数的增加会逐渐下降；
2. Adaboost算法即使训练次数很多，也不会出现过拟合的问题。

Adaboost算法可以简述为三个步骤：

1. 首先，是初始化训练数据的权值分布D1。假设有N个训练样本数据，则每一个训练样本最开始时，都被赋予相同的权值：`w1=1/N`。

2. 然后，训练弱分类器`hⅰ`。具体训练过程中是：

   如果某个训练样本点，被弱分类器`i`准确地分类，那么在构造下一个训练集中，它对应的权值要减小；相反，如果某个训练样本点被错误分类，那么它的权值就应该增大。

   权值更新过的样本集被用于训练下一个分类器，整个训练过程如此迭代地进行下去。

3. 最后，将各个训练得到的弱分类器组合成一个强分类器。各个弱分类器的训练过程结束后，**加大分类误差率小的弱分类器的权重**，使其在最终的分类函数中起着较大的决定作用，而降低分类误差率大的弱分类器的权重，使其在最终的分类函数中起着较小的决定作用。

   换而言之，误差率低的弱分类器在最终分类器中占的权重较大，否则较小。

### AdaBoost的优点和缺点

**优点** 

- Adaboost提供一种框架，在框架内可以使用各种方法构建子分类器。**可以使用简单的弱分类器**，**不用对特征进行筛选**，**也不存在过拟合的现象**。
- Adaboost算法不需要弱分类器的先验知识，最后得到的强分类器的分类精度依赖于所有弱分类器。 无论是应用于人造数据还是真实数据，Adaboost都能显著的提高学习精度。**不需要先验知识，不在意数据人造还是真实的**。
- Adaboost算法不需要预先知道弱分类器的错误率上限，且最后得到的强分类器的分类精度依赖于所有弱分类器的分类精度，可以深挖分类器的能力。Adaboost**可以根据弱分类器的反馈，自适应地调整假定的错误率**，执行的效率高。
- Adaboost对同一个训练样本集训练不同的弱分类器，按照一定的方法把这些弱分类器集合起来，构造一个分类能力很强的强分类器，即“三个臭皮匠赛过一个诸葛亮”。

**缺点** 

- 在Adaboost训练过程中，Adaboost会使得**难于分类样本的权值呈指数增长**，训练将会过于向这类困难的样本，导致Adaboost算法**易受噪声干扰**。此外，Adaboost依赖于弱分类器，而**弱分类器的训练时间往往很长**。

Adaboost迭代算法有三步

1. 初始化训练样本的权值分布，每个样本具有相同权重；
2. 训练弱分类器，如果样本分类正确，则在构造下一个训练集中，它的权值就会被降低；反之提高。用更新过的样本集去训练下一个分类器；
3. 将所有弱分类组合成强分类器，各个弱分类器的训练过程结束后，加大分类误差率小的弱分类器的权重，降低分类误差率大的弱分类器的权重。

## 梯度提升树

AdaBoost 学习的是错误数据，GBDT学习的是上一个结果的残差值。



## GBDT、XGBoost和LightGBM辨析

### XGBoost

XGBoost是基于GBDT的一种算法或者说工程实现。

GBDT是一种基于boosting集成思想的加法模型，训练时采用前向分布算法进行贪婪的学习，每次迭代都学习一棵CART树来拟合之前 t-1 棵树的预测结果与训练样本真实值的残差。

XGBoost的基本思想和GBDT相同，但是做了一些优化，如默认的缺失值处理，加入了二阶导数信息、正则项、列抽样，并且可以并行计算等。

数学原理

- 目标函数
- 基于决策树的目标函数
- 最优切分点划分算法
- 加权分位数缩略图
- 稀疏感知算法 

工程实现

- 块结构设计
- 缓存访问优化算法
- “核外”块计算

### LightGBM

LightGBM由微软提出，主要用于解决GDBT在海量数据中遇到的问题，以便其可以更好更快地用于工业 实践中。从LightGBM名字我们可以看出其是轻量级(Light)的梯度提升机(GBM)，其相对XGBoost具有训 练速度快、内存占用低的特点。

我们刚刚分析了XGBoost的缺点，LightGBM为了解决这些问题提出了以下几点解决方案：

- 单边梯度抽样算法；
- 直方图算法；
- 互斥特征捆绑算法；
- 基于最大深度的Leaf-wise的垂直生长算法；
- 类别特征最优分割；
- 特征并行和数据并行；
- 缓存优化。

数学原理

- 单边梯度抽样算法
- 直方图算法
- 互斥特征捆绑算法
- 带深度限制的Leaf-wise算法
- 类别特征最优分割

工程实现

- 特征并行/数据并行/投票并行 
- 缓存优化

## XGBoost和GBDT的不同点

- GBDT是机器学习算法，XGBoost是该算法的**工程实现**。
- 在使用CART作为基分类器时，XGBoost显式地加入了**正则项**来控制模型的复杂度，有利于防止过拟合，从而提高模型的泛化能力。
- GBDT在模型训练时只是用了代价函数的一阶导数信息，XGBoost对代价函数进行**二阶泰勒展开**，可以同时使用一阶和二阶导数。（好处：相对于GBDT的一阶泰勒展开，XGBoost采用二阶泰勒展开，可以更为精准的逼近真实的损失函数。需要注意的是，损失函数需要二阶可导。）
- 传统的GBDT采用CART作为基分类器，XGBoost支持**多种类型的基分类器**，比如线性分类器。
- 传统的GBDT在每轮迭代时使用全部的数据，XGBoost则采用了与随机森林相似的策略，支持对数据进行**列采样**。
- 传统的GBDT没有涉及对缺失值进行处理，XGBoost能够自动学习出**缺失值的处理策略**。
- **特征维度上的并行化**。XGBoost预先将每个特征按特征值排好序，存储为块结构，分裂结点时可以采用多线程并行查找每个特征的最佳分割点，极大提升训练速度。



## QA

### 介绍一下GBDT

GBDT(Gradient Boosting Decision Tree) 又叫 MART（Multiple Additive Regression Tree)，是一种迭代的决策树算法，该算法由多棵决策树组成，所有树的结论累加起来做最终答案。

梯度提升决策树（Gradient Boosting Decision Tree, GBDT） 由三个概念组成：回归树（Regression Decision Tree, DT）、 梯度上升（Gradient Boosting, GB），和收缩 Shrinkage（一个重要演变）。

**回归树（Regression Decision Tree）**

GBDT 的核心在于==**累加所有树的结果作为最终结果**==，分类树的结果显然是没办法累加的，所以 GBDT 中的树**都是回归树**。回归树**在分枝时会穷举每一个特征的每个阈值以找到最好的分割点**，衡量标准是**最小化均方误差**。

**梯度迭代（Gradient Boosting）** 

GBDT的核心就在于，**每一棵树学的是之前所有树结论和的残差**，这个残差就是**一个加预测值后能得真实值的累加量**。

Gradient —— 该版本用残差作为全局最优的绝对方向，并不需要Gradient求解。其**残差其实是最小均方损失函数关于预测值的反向梯度**：
$$
-\frac{\partial\left(\frac{1}{2}\left(y-F_{k}(x)\right)^{2}\right)}{\partial F_{k}(x)}=y-F_{k}(x)
$$
也就是说，预测值和实际值的残差与损失函数的负梯度相同，本质上还是梯度下降法。

Boosting —— 最大好处在于，每一步的残差计算其实变相地增大了分错instance的权重，而已经分对的instance则都趋向于0。这样后面的树就能越来越专注那些前面被分错的instance。==**GBDT不是Adaboost Decistion Tree**，AdaBoost用**错分数据点来识别问题**，通过调整错分数据点的权重来改进模型。GBDT通过**负梯度来识别问题**，通过计算负梯度来改进模型==。

**收缩（Shrinkage）** 

Shrinkage（缩减）的思想认为，每次走一小步逐渐逼近结果的效果，要比每次迈一大步很快逼近结果的方式更容易避免过拟合。即它不完全信任每一个棵残差树，它认为每棵树只学到了真理的一小部分，累加的时候只累加一小部分，通过多学几棵树弥补不足。

Shrinkage仍然以残差作为学习目标，但对于残差学习出来的结果，只累加一小部分（step*残差）逐步逼近目标，step一般都比较小，如0.01~0.001（注意该step非gradient的step），导致各个树的残差是渐变的而不是陡变的。直觉上这也很好理解，不像直接用残差一步修复误差，而是只修复一点点，其实就是把大步切成了很多小步。**本质上，Shrinkage为每棵树设置了一个weight，累加时要乘以这个weight，但和Gradient并没有关系。**这个weight就是step。

**GBDT的适用范围** 

该版本GBDT**几乎可用于所有回归问题（线性/非线性），相对logistic regression仅能用于线性回归，GBDT的适用面非常广。亦可用于二分类问题**（设定阈值，大于阈值为正例，反之为负例）。

**GBDT哪些地方可以并行**：

1. 计算每个样本的负梯度； 
2. 分裂挑选最佳特征及其分割点时，对特征计算相应的误差及均值时； 
3. 更新每个样本的负梯度时； 
4. 最后预测过程中，每个样本将之前的所有树的结果累加的时候。



### XGBoost有哪些改进

xgboost 的全称是eXtreme Gradient  Boosting，它是Gradient Boosting Machine的一个c++实现，作者为正在华盛顿大学研究机器学习的大牛陈天奇  。XGBoost最大的特点在于它能够自动利用CPU的多线程进行并行，同时在算法上加以改进提高了精度。因此在计算速度和准确率上，较GBDT有明显的提升。

1. 在使用CART作为基分类器时，XGBoost显式地加入了正则项来控制模型的复杂度，有利于防止过拟合，从而提高模型泛化能力。
2. GBDT在模型训练过程中只使用了代价函数的一阶导信息，XGBoost对代价函数进行二阶泰勒展开，可以同时使用一阶和二阶导数。 
3. 传统的GBDT采用CART作为基分类器，XGBoost支持多种类型的基分类器，比如线性分类器。
4. 传统的GBDT在每轮迭代时使用全部的数据，XGBoost则采用了与随机森林相似的策略，支持对数据进行采样。
5. 传统的GBDT没有设计对缺失值进行处理，XGBoost能够自动学习出缺失值的处理策略。



### GBDT与随机森林的异同点

相同：GBDT与RF的基分类器均为决策树，都对决策树算法进行了优化，均属于集成算法的一种。

不同：

- GBDT属于Boosting策略。Boosting通过**降低偏差**来提升弱分类器的性能，其基本思想是根据当前模型损失函数的负梯度信息来训练新加入的弱分类器，然后将训练好的弱分类器以累加的形式结合到现有的模型中。这个过程不断地减小损失函数，使得模型偏差不断降低。但Boosting的过程不会显著降低方差，这是因为Boosting的训练过程中使得各弱分类器之间是强相关的，缺乏独立性，所以并不会对降低方差有作用。
- Random Forest（随机森林）属于Bagging策略。Bagging通过**降低方差**来提升弱分类器的性能，RF在以决策树为基学习器构建 Bagging 集成的基础上，进一步在决策树的训练过程中引入了随机特征选择，每次选取节点分裂属性时，会随机抽取一个属性子集，而不是从所以属性中选择最优属性，避免了弱分类器之间过强的相关性。**通过训练集的重采样也能够带来弱分类器之间一定的独立性，从而降低Bagging后模型的方差**。



### GBDT防止过拟合有什么方法，如何调参？

XGBoost 在目标函数中加入了正则项，用于控制模型的复杂度。

正则项里包含了树的叶子节点个数、叶子节点权重的 L2 范式。

正则项降低了模型的方差，使学习出来的模型更加简单，有助于防止过拟合。



### GBDT为什么对缺失值不敏感，如何处理缺失值的？

XGBoost 在构建树的节点过程中只考虑非缺失值的数据遍历，而为每个节点增加了一个缺省方向，当样本相应的特征值缺失时，可以被归类到缺省方向上，最优的缺省方向可以从数据中学到。

学习缺省值的分支的方法，分别枚举特征缺省的样本归为左右分支后的增益，选择增益最大的枚举项即为最优缺省方向。



### 解释一下GBDT沿着梯度下降方向提升，如何实现的？

GBDT在每一轮迭代学习回归树的时候，拟合目标就是损失函数L对当前所学模型F预测值的负梯度，所以模型的更新自然而然是沿着梯度下降方向的。







