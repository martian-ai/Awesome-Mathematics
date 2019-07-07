[TOC]



# Optimization for Gradient Descent

# Gradient Descent

+ Batch Gradient Descent 
	+ 计算所有样本的误差,然后根据总误差来更新权值
+ Stochastic Gradient Descent
	+ 抽取一个样本来计算误差, 然后更新权值
+ Mini-Batch Gradient Descent
	+ 从总样本中选取一个批次, 然后计算这个批次的总误差, 然后根据总误差更新权值



# Mini-Batch Gradient Descent

+ 对于训练数据集，我们首先将其分成n个batch，每个batch包含m个样本。我们每次更新都利用一个batch的数据，而非整个训练集。即：

![](https://images2017.cnblogs.com/blog/1218582/201801/1218582-20180116222037021-1729097658.jpg)

+ 其中，x 表示自变量， $\Delta x$  表示导数,  η为学习率，$g_t$为x在t时刻的梯度。 
+ 这么做的好处在于：
	+ 当训练数据太多时，利用整个数据集更新往往时间上不现实。
	+ batch的方法可以减少机器的压力，并且可以更快地收敛。
	+ 当训练集有很多冗余时（类似的样本出现多次），batch方法收敛更快。
	  + 以一个极端情况为例，若训练集前一半和后一半梯度相同。那么如果前一半作为一个batch，后一半作为另一个batch，那么在一次遍历训练集时，batch的方法向最优解前进两个step，而整体的方法只前进一个step。(速度会更快)
+ 有待讨论的点：
  + mini-batch 过大时会产生泛化误差

# Momentum

+ SGD方法的一个缺点是，**其更新方向完全依赖于当前的batch，因而其更新十分不稳定**
+ 解决这一问题的一个简单的做法便是引入momentum
+ momentum即动量，它模拟的是物体运动时的惯性，即更新的时候在一定程度上保留之前更新的方向，同时利用当前batch的梯度微调最终的更新方向。这样一来，**可以在一定程度上增加稳定性，从而学习地更快，并且还有一定摆脱局部最优的能力**：

![](https://images2017.cnblogs.com/blog/1218582/201801/1218582-20180116222155974-1758841902.jpg)

+ 其中，ρ 即momentum，表示要在多大程度上保留原来的更新方向，这个值在0-1之间

+ 在训练开始时，由于梯度可能会很大，所以初始值一般选为0.5；

+ 当梯度不那么大时，改为0.9

+ η 是学习率，即当前batch的梯度多大程度上影响最终更新方向，跟普通的SGD含义相同

+ ρ 与 η 之和不一定为1

  ![](http://ww4.sinaimg.cn/large/006tNc79ly1g4b72eouc9j30be04uglp.jpg)



![](http://ww3.sinaimg.cn/large/006tNc79ly1g4b72h3k9tj30be04udfx.jpg)

# Nesterov Momentum / Nesterov Accelerated Gradient(NAG)

# Adagrad （对学习率进行自适应约束，但依赖全局学习率）

+ Adagrad其实是对学习率进行了一个约束。即：

![](https://images2017.cnblogs.com/blog/1218582/201801/1218582-20180116222331021-786003572.jpg)

+ 此处，对$g_t$从1到t进行一个递推形成一个约束项regularizer，$-\frac{1}{\sqrt{\sum_{r=1}^t(g_r)^2+\epsilon}},\epsilon$用来保证分母非0
+ 特点：
	+ 前期$g_t$较小的时候， regularizer较大，能够放大梯度
	+ 后期$g_t$较大的时候，regularizer较小，能够约束梯度
	+ 适合处理稀疏梯度
+ 缺点：
	+ 由公式可以看出，仍依赖于人工设置一个全局学习率 
	+ $\eta$设置过大的话，会使regularizer过于敏感，对梯度的调节太大
	+ 中后期，分母上梯度平方的累加将会越来越大，使$gradient\to0$，使得训练提前结束

# Adadelta (不依赖全局学习率)

+ Adadelta是对Adagrad的扩展，最初方案依然是对学习率进行自适应约束，但是进行了计算上的简化。Adagrad会累加之前所有的梯度平方，而Adadelta只累加固定大小的项，并且也不直接存储这些项，仅仅是近似计算对应的平均值。即：
$$
n_t=\nu*n_{t-1}+(1-\nu)*g_t^2
$$
$$
\Delta{\theta_t} = -\frac{\eta}{\sqrt{n_t+\epsilon}}*g_t
$$
+ 在此处Adadelta其实还是依赖于全局学习率的，但是作者做了一定处理，经过近似牛顿迭代法（求根点）之后：
$$
E|g^2|_t=\rho*E|g^2|_{t-1}+(1-\rho)*g_t^2
$$
$$
\Delta{x_t}=-\frac{\sqrt{\sum_{r=1}^{t-1}\Delta{x_r}}}{\sqrt{E|g^2|_t+\epsilon}}
$$

+ 其中，E代表求期望。 此时，可以看出Adadelta已经不用依赖于全局学习率了。 
+ 特点：
	+ 训练初中期，加速效果不错，很快 
	+ 训练后期，反复在局部最小值附近抖动

# RMSprop

+ 未理解https://www.cnblogs.com/callyblog/p/8299074.html

+ AdaGrad算法的改进。鉴于神经网络都是非凸条件下的，**RMSProp在非凸条件下结果更好**，改变梯度累积为指数衰减的移动平均以丢弃遥远的过去历史

+ 经验上，RMSProp被证明有效且实用的深度学习网络优化算法。

+ 相比于AdaGrad的历史梯度, RMSProp增加了一个衰减系数来控制历史信息的获取多少
  $$
  Adagrad:n_t = n_{t-1} + {g_t}^2
  $$

  $$
  RMSprop : n_t = v*n_{t-1} + (1-v)* {g_t}^2
  $$

  

+ 特点：
	
	+ 其实RMSprop依然依赖于全局学习率 
	+ RMSprop算是Adagrad的一种发展，和Adadelta的变体，效果趋于二者之间
	+ 适合处理非平稳目标
	  + 对于RNN效果很好

# Adam

+ Adam(Adaptive Moment Estimation)本质上是带有动量项的RMSprop，它利用梯度的**一阶矩估计**和**二阶矩估计**动态调整每个参数的学习率
+ Adam的优点主要在于经过偏置校正后，每一次迭代学习率都有个确定范围，使得参数比较平稳。公式如下：

$$
m_t=\mu*m_{t-1}+(1-\mu)*g_t
$$
$$
n_t=\nu*n_{t-1}+(1-\nu)*g_t^2
$$
$$
\hat{m_t}=\frac{m_t}{1-\mu^t}
$$
$$
\hat{n_t}=\frac{n_t}{1-\nu^t}
$$
$$
\Delta{\theta_t}=-\frac{\hat{m_t}}{\sqrt{\hat{n_t}}+\epsilon}*\eta
$$

+ 其中，m_t，n_t分别是对梯度的一阶矩估计和二阶矩估计，u和v为衰减率，u通常为0.9，v通常为0.999,可以看作对期望$E|g_t|$，$E|g_t^2|$的估计；$\hat{m_t}$，$\hat{n_t}$是对m_t，n_t的校正，这样可以近似为对期望的无偏估计。可以看出，直接对梯度的矩估计对内存没有额外的要求，而且可以根据梯度进行动态调整，而$-\frac{\hat{m_t}}{\sqrt{\hat{n_t}}+\epsilon}$对学习率形成一个动态约束，而且有明确的范围。
+ 特点：
	+ 结合了Adagrad善于处理稀疏梯度和RMSprop善于处理非平稳目标的优点 
	+ 对内存需求较小 
	+ 为不同的参数计算不同的自适应学习率 
	+ 也适用于大多非凸优化
	+ 适用于大数据集和高维空间

# Others

+ AdaShift(ICLR 2019)
+ NosAdam(IJCAI2019) https://arxiv.org/abs/1805.07557

+ Adabound https://github.com/Luolc/AdaBound

# 对比

![](http://ww3.sinaimg.cn/large/006tNc79ly1g4b755auj7g30h80dc7k9.gif)

+ 从上图可以看出， Adagrad、Adadelta与RMSprop在损失曲面上能够立即转移到正确的移动方向上达到快速的收敛。而Momentum 与NAG会导致偏离(off-track)。同时NAG能够在偏离之后快速修正其路线，因为其根据梯度修正来提高响应性

![](http://ww3.sinaimg.cn/large/006tNc79ly1g4b75z8wjbg30h80dc4b1.gif)

+ 从上图可以看出，在鞍点（saddle points）处(即某些维度上梯度为零，某些维度上梯度不为零)，SGD、Momentum与NAG一直在鞍点梯度为零的方向上振荡，很难打破鞍点位置的对称性；Adagrad、RMSprop与Adadelta能够很快地向梯度不为零的方向上转移
+ 选择
  + 如果你的数据特征是稀疏的，那么你最好使用自适应学习速率SGD优化方法(Adagrad、Adadelta、RMSprop与Adam)，因为你不需要在迭代过程中对学习速率进行人工调整
  + RMSprop是Adagrad的一种扩展，与Adadelta类似，但是改进版的Adadelta使用RMS去自动更新学习速率，并且不需要设置初始学习速率。而Adam是在RMSprop基础上使用动量与偏差修正。RMSprop、Adadelta与Adam在类似的情形下的表现差不多。Kingma[15]指出收益于偏差修正，Adam略优于RMSprop，因为其在接近收敛时梯度变得更加稀疏。因此，Adam可能是目前最好的SGD优化方法。
  + 有趣的是，最近很多论文都是使用原始的SGD梯度下降算法，并且使用简单的学习速率退火调整（无动量项）。现有的已经表明：SGD能够收敛于最小值点，但是相对于其他的SGD，它可能花费的时间更长，并且依赖于鲁棒的初始值以及学习速率退火调整策略，并且容易陷入局部极小值点，甚至鞍点。因此，如果你在意收敛速度或者训练一个深度或者复杂的网络，你应该选择一个自适应学习速率的SGD优化方法。

# 并行与分布式SGD

## Hogwild

## Downpour SGD

## **Delay-tolerant Algorithms for SGD**

## **Elastic Averaging SGD**

## Tensorflow



# 基于SGD的进一步优化

+ shuffling and curriculum learing
+ batch normaliztion
+ early stopping
+ gradient noise

# Reference

- https://www.cnblogs.com/callyblog/p/8299074.html
- https://blog.csdn.net/bvl10101111/article/details/72616378