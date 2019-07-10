[TOC]



# Summary of Unconstrained Optimization



# Outline

+ 极小点条件

+ 无约束优化方法：线搜索法
  + 最速下降法
  + 牛顿法
  + 共轭梯度法
  + 拟牛顿法
  + DFP和BFGS法
  + 最小二乘
+ 无约束优化方法：信赖域法



# Linear Search Methods

## Gradient Descent

+ Batch Gradient Descent

- 计算所有样本的误差,然后根据总误差来更新权值

- Stochastic Gradient Descent
  - 抽取一个样本来计算误差, 然后更新权值
- Mini-Batch Gradient Descent
  - 从总样本中选取一个批次, 然后计算这个批次的总误差, 然后根据总误差更新权值



### Mini-Batch Gradient Descent

- 对于训练数据集，我们首先将其分成n个batch，每个batch包含m个样本。我们每次更新都利用一个batch的数据，而非整个训练集。即：

![](https://images2017.cnblogs.com/blog/1218582/201801/1218582-20180116222037021-1729097658.jpg)

- 其中，x 表示自变量， $\Delta x$  表示导数,  η为学习率，$g_t$为x在t时刻的梯度。 
- 这么做的好处在于：
  - 当训练数据太多时，利用整个数据集更新往往时间上不现实。
  - batch的方法可以减少机器的压力，并且可以更快地收敛。
  - 当训练集有很多冗余时（类似的样本出现多次），batch方法收敛更快。
    - 以一个极端情况为例，若训练集前一半和后一半梯度相同。那么如果前一半作为一个batch，后一半作为另一个batch，那么在一次遍历训练集时，batch的方法向最优解前进两个step，而整体的方法只前进一个step。(速度会更快)
- 有待讨论的点：
  - mini-batch 过大时会产生泛化误差

### Momentum

- SGD方法的一个缺点是，**其更新方向完全依赖于当前的batch，因而其更新十分不稳定**
- 解决这一问题的一个简单的做法便是引入momentum
- momentum即动量，它模拟的是物体运动时的惯性，即更新的时候在一定程度上保留之前更新的方向，同时利用当前batch的梯度微调最终的更新方向。这样一来，**可以在一定程度上增加稳定性，从而学习地更快，并且还有一定摆脱局部最优的能力**：

![](https://images2017.cnblogs.com/blog/1218582/201801/1218582-20180116222155974-1758841902.jpg)

- 其中，ρ 即momentum，表示要在多大程度上保留原来的更新方向，这个值在0-1之间

- 在训练开始时，由于梯度可能会很大，所以初始值一般选为0.5；

- 当梯度不那么大时，改为0.9

- η 是学习率，即当前batch的梯度多大程度上影响最终更新方向，跟普通的SGD含义相同

- ρ 与 η 之和不一定为1

  ![](http://ww4.sinaimg.cn/large/006tNc79ly1g4b72eouc9j30be04uglp.jpg)



![](http://ww3.sinaimg.cn/large/006tNc79ly1g4b72h3k9tj30be04udfx.jpg)

### Nesterov Momentum / Nesterov Accelerated Gradient(NAG)

### Adagrad （对学习率进行自适应约束，但依赖全局学习率）

- Adagrad其实是对学习率进行了一个约束。即：

![](https://images2017.cnblogs.com/blog/1218582/201801/1218582-20180116222331021-786003572.jpg)

- 此处，对$g_t$从1到t进行一个递推形成一个约束项regularizer，$-\frac{1}{\sqrt{\sum_{r=1}^t(g_r)^2+\epsilon}},\epsilon$用来保证分母非0
- 特点：
  - 前期$g_t$较小的时候， regularizer较大，能够放大梯度
  - 后期$g_t$较大的时候，regularizer较小，能够约束梯度
  - 适合处理稀疏梯度
- 缺点：
  - 由公式可以看出，仍依赖于人工设置一个全局学习率 
  - $\eta$设置过大的话，会使regularizer过于敏感，对梯度的调节太大
  - 中后期，分母上梯度平方的累加将会越来越大，使$gradient\to0$，使得训练提前结束

### Adadelta (不依赖全局学习率)

- Adadelta是对Adagrad的扩展，最初方案依然是对学习率进行自适应约束，但是进行了计算上的简化。Adagrad会累加之前所有的梯度平方，而Adadelta只累加固定大小的项，并且也不直接存储这些项，仅仅是近似计算对应的平均值。即：

$$
n_t=\nu*n_{t-1}+(1-\nu)*g_t^2
$$

$$
\Delta{\theta_t} = -\frac{\eta}{\sqrt{n_t+\epsilon}}*g_t
$$

- 在此处Adadelta其实还是依赖于全局学习率的，但是作者做了一定处理，经过近似牛顿迭代法（求根点）之后：

$$
E|g^2|_t=\rho*E|g^2|_{t-1}+(1-\rho)*g_t^2
$$

$$
\Delta{x_t}=-\frac{\sqrt{\sum_{r=1}^{t-1}\Delta{x_r}}}{\sqrt{E|g^2|_t+\epsilon}}
$$

- 其中，E代表求期望。 此时，可以看出Adadelta已经不用依赖于全局学习率了。 
- 特点：
  - 训练初中期，加速效果不错，很快 
  - 训练后期，反复在局部最小值附近抖动

### RMSprop

- 未理解https://www.cnblogs.com/callyblog/p/8299074.html

- AdaGrad算法的改进。鉴于神经网络都是非凸条件下的，**RMSProp在非凸条件下结果更好**，改变梯度累积为指数衰减的移动平均以丢弃遥远的过去历史

- 经验上，RMSProp被证明有效且实用的深度学习网络优化算法。

- 相比于AdaGrad的历史梯度, RMSProp增加了一个衰减系数来控制历史信息的获取多少
  $$
  Adagrad:n_t = n_{t-1} + {g_t}^2
  $$

  $$
  RMSprop : n_t = v*n_{t-1} + (1-v)* {g_t}^2
  $$

  

- 特点：

  - 其实RMSprop依然依赖于全局学习率 
  - RMSprop算是Adagrad的一种发展，和Adadelta的变体，效果趋于二者之间
  - 适合处理非平稳目标
    - 对于RNN效果很好

### Adam

- Adam(Adaptive Moment Estimation)本质上是带有动量项的RMSprop，它利用梯度的**一阶矩估计**和**二阶矩估计**动态调整每个参数的学习率
- Adam的优点主要在于经过偏置校正后，每一次迭代学习率都有个确定范围，使得参数比较平稳。公式如下：

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

- 其中，m_t，n_t分别是对梯度的一阶矩估计和二阶矩估计，u和v为衰减率，u通常为0.9，v通常为0.999,可以看作对期望$E|g_t|$，$E|g_t^2|$的估计；$\hat{m_t}$，$\hat{n_t}$是对m_t，n_t的校正，这样可以近似为对期望的无偏估计。可以看出，直接对梯度的矩估计对内存没有额外的要求，而且可以根据梯度进行动态调整，而$-\frac{\hat{m_t}}{\sqrt{\hat{n_t}}+\epsilon}$对学习率形成一个动态约束，而且有明确的范围。
- 特点：
  - 结合了Adagrad善于处理稀疏梯度和RMSprop善于处理非平稳目标的优点 
  - 对内存需求较小 
  - 为不同的参数计算不同的自适应学习率 
  - 也适用于大多非凸优化
  - 适用于大数据集和高维空间

### Others

- AdaShift(ICLR 2019)
- NosAdam(IJCAI2019) https://arxiv.org/abs/1805.07557
- Adabound https://github.com/Luolc/AdaBound

### 对比

![](http://ww3.sinaimg.cn/large/006tNc79ly1g4b755auj7g30h80dc7k9.gif)

- 从上图可以看出， Adagrad、Adadelta与RMSprop在损失曲面上能够立即转移到正确的移动方向上达到快速的收敛。而Momentum 与NAG会导致偏离(off-track)。同时NAG能够在偏离之后快速修正其路线，因为其根据梯度修正来提高响应性

![](http://ww3.sinaimg.cn/large/006tNc79ly1g4b75z8wjbg30h80dc4b1.gif)

- 从上图可以看出，在鞍点（saddle points）处(即某些维度上梯度为零，某些维度上梯度不为零)，SGD、Momentum与NAG一直在鞍点梯度为零的方向上振荡，很难打破鞍点位置的对称性；Adagrad、RMSprop与Adadelta能够很快地向梯度不为零的方向上转移
- 选择
  - 如果你的数据特征是稀疏的，那么你最好使用自适应学习速率SGD优化方法(Adagrad、Adadelta、RMSprop与Adam)，因为你不需要在迭代过程中对学习速率进行人工调整
  - RMSprop是Adagrad的一种扩展，与Adadelta类似，但是改进版的Adadelta使用RMS去自动更新学习速率，并且不需要设置初始学习速率。而Adam是在RMSprop基础上使用动量与偏差修正。RMSprop、Adadelta与Adam在类似的情形下的表现差不多。Kingma[15]指出收益于偏差修正，Adam略优于RMSprop，因为其在接近收敛时梯度变得更加稀疏。因此，Adam可能是目前最好的SGD优化方法。
  - 有趣的是，最近很多论文都是使用原始的SGD梯度下降算法，并且使用简单的学习速率退火调整（无动量项）。现有的已经表明：SGD能够收敛于最小值点，但是相对于其他的SGD，它可能花费的时间更长，并且依赖于鲁棒的初始值以及学习速率退火调整策略，并且容易陷入局部极小值点，甚至鞍点。因此，如果你在意收敛速度或者训练一个深度或者复杂的网络，你应该选择一个自适应学习速率的SGD优化方法。

### 并行与分布式SGD

#### Hogwild

#### Downpour SGD

#### **Delay-tolerant Algorithms for SGD**

#### **Elastic Averaging SGD**

#### Tensorflow



### 基于SGD的进一步优化

- shuffling and curriculum learing
- batch normaliztion
- early stopping
- gradient noise

### Reference

- https://www.cnblogs.com/callyblog/p/8299074.html
- https://blog.csdn.net/bvl10101111/article/details/72616378

## 牛顿法

### 求根

+ 并不是所有方程都有求根公式，或者求根公式很复杂，导致求解很困难，利用牛顿法，可以迭代求解
+ 原理：
  + 利用泰勒公式展开，在$x_0$ 处展开一阶形式，$f(x) = f(x_0) + f^{`}(x_0)(x-x_0)$ , 并不是完全相等
  + 令$f(x) = 0$, 得到$x_1$, $x_1$ 相对 $x_0$ 更接近正确结果，逐步递推
  + $x_{n+1} = x_n  - f(x_n)/f^{`}(x_n)$
  + 迭代之后，在 $f(x^*) = 0$ 收敛

![](http://ww4.sinaimg.cn/large/006tNc79ly1g3qlcv7uj6j30es0ck3yp.jpg)

### 最优化

+ 优化目标如下, 并设 $x^*$ 为目标函数的极小点

  $$ min_{x \in R^n}  f(x) $$ 

+ 设f(x) 具有二阶偏导数， 若第k次的迭代值为 $x^{(k)}$, 则 $x^{(k)}$附近的二阶泰勒展开为

  $$ f(x) = f(x^{(k)}) + g^T_k(x-x^{(k)}) + \frac{1}{2}(x - x^{(k)})^T H(x^{(k)})(x-x^{(k)} ）$$

+ 其中

  + $g_k = g(x^{(k)}) = \nabla f(x(k))$ 是该点的梯度值
  + $H(x^{(k)}) = [\frac{\partial^2 f}{\partial x_i \partial x_j}]_{n*n}$  是 $f(x)$ 的海森矩阵 

+ f(x) 有极值必要条件，一阶导为零，当$H(x^{(k)}) $ 为正定阵时，取得极小值

+ 利用牛顿法求解所有一节导数为0的点,   求解过程如下:

	+ Step 1 : 取初始点 $x^{(0)}$,  k = 0
	+ Step 2 : 根据二阶泰勒展开,将 $ \nabla f(x)$ 在 $x^{(k)}$ 进行展开, 求得$g_k$,  若$g_k < \epsilon$ , 则终止迭代，得到近似解　$x^\star$ , 否则继续进行Step 3
	+ Step 3:  计算 $H_k$,  并获得下一个跌点的坐标 $x^{k+1}$
		+  $\nabla f(x^{(k)}) = g_k + H_k(x - x^{(k)}) ,  H_k = H(x^{(k)})$
		+ $ g_k + H_k(x^{k+1} - x^{k}) = 0 $
		+ $x^{k+1}  = x^k - H_k^{-1} g_k$
		+ 继续进行 Step 2



## 梯度下降法 v.s. 牛顿法

+ 两者都是迭代求解, 梯度下降法是梯度求解,  而牛顿法是二阶的海森矩阵的逆矩阵求解
+ 相对而言, 牛顿法收敛更快(迭代次数更少), 但每次迭代的时间会更长
	+ $x^{( k+1 )} = x^{(k)} - \lambda \nabla f(x^{(k)})$
	+ $x^{(k+1)} = x^{(k)} - \lambda  H_k^{-1}\nabla f(x^{(k)})$
+ 至于为什么牛顿法收敛更快，通俗来说梯度下降法每次只从你当前所处位置选一个坡度最大的方向走一步，牛顿法在选择方向时，不仅会考虑坡度是否够大，还会考虑你走了一步之后，坡度是否会变得更大。所以，可以说牛顿法比梯度下降法看得更远一点，能更快地走到最底部



## 拟牛顿法

+ 牛顿法中, 需要计算 $H^{-1}_k$ , 计算较为复杂, 考虑用另外一个n阶矩阵 $G_k = G(x^{(k)})$ 来代替

+ $H_k$ 满足的条件（拟牛顿条件）

	+ $g_{k+1} - g_k = H_k(x^{(k+1)} - x^{(x) })$

+ 在公式 (*) 中

	+ $f(x) = f(x^{(k)}) - \lambda g_k^T H_k^{-1} g_k^T$

	+ 因为　$H_k$ 正定, 所以　$H_k^{-1} $ 正定，当$\lambda$ 为一个充分小的正数时, 总有$f(x) < f(x^{(k)})$

+ 拟牛顿将$G_k$ 当做 $H_k$ 的近似,  近似条件如下

	+ $G_k$ 是正定的
	+ 满足拟牛顿条件

+ 表示 

	+ $G_{k+1} = G_{k} + \Delta G_k$

## DFP(Davidon-Fletcher-Powell)

+  $G_0$ 正定的
+  $G_{k+1} $ 由　$G_k$ 加上两个附加项构成
+ $G_{k+1} = G_{k} + P_k + Q_k$
+ 令 $y_k = g_{k+1} - g_{k}$,   $\delta_k = x^{(k+1)} - x^{(k)}$
+ $G_{k+1}y_k　= G_{k}  y_k+ P_k y_k + Q_k y_k$
+ 为了使$G_{k+1}$ 满足拟牛顿条件, 可使得$P_k$ 和 $Q_k$ 满足
	+ $P_k y_k = \delta_k$ 
	+ $Q_k y_k = -G_k y_k$
	+ 即  $G_{k+1}y_k =  x^{(k+1)} - x^{(k)}$
+ 求解得
	+ $P_k = \frac{\delta_k \delta_k^T}{\delta_k^T y_k}$
	+ $Q_k = - \frac{G_k y_k y_k^T G_k}{y_k^TG_ky_k}$
+ 则有
	+ $G_{k+1} = G_{k} + \frac{\delta_k \delta_k^T}{\delta_k^T y_k}   - \frac{G_k y_k y_k^T G_k}{y_k^TG_ky_k}$
+  $P_k$ $Q_k$ 的求解过程？
+  正定？

## BFGS

+ 与 DFP 类似, 唯一的区别是 使用 $B_k$ 逼近 $H_k$
+ 公式如下
	+ $B_{k+1} = B_{k} + \frac{y_k y_k^T}{y_k^T \delta_k}   - \frac{B_k \delta_k \delta_k^T B_k}{\delta_k^T B_k \delta_k}$



## Broyden

+ 在 BFGS 的公式中带入 $G_k = B_k^{-1} $, $G_{k+1} = B_{k+1}^{-1} $
+ 并使用两次 Sherman-Morrison 公式得到, BFGS 关于$G_k$ 的公式
	+ $G_{k+1} = (I - \frac{\delta_k y^T}{\delta_k^T y_k})G_{k} (I - \frac{\delta_k y^T}{\delta_k^T y_k})^{-T} + \frac{\delta_k \delta_k^T}{\delta_k^T y_k} $
+ $G_{k+1} = \alpha G^{DFP} + (1-\alpha) G^{BFGS}$





# 信赖域法



# Usage

+ 牛顿法：支持向量机 liblinear

# Reference

+ 统计学习方法第二版 附录B
+ https://zhuanlan.zhihu.com/p/37524275



1. 实用算法应该具有的典型特征就是迭代点**稳定**逼近局部极小点的**邻域**然后迅速**收敛**到局部极小点

2. 算法的理论分析比较困难而且远远匹配不上算法的实际表现

3. 大范围收敛和局部收敛

4. 局部收敛性;用于分析比较迭代点进入局部极小点邻域后的收敛行为

5. 局部收敛性会给出：二阶，线性，超线性，次线性等收敛行为

6. 收敛性和收敛阶的结论并不能保证算法在实际中一定有好的计算效果

7. 收敛性和收敛速度的证明通常根据特定算法进行非常具体的分析，它本身不能告诉我们如何更好地设计算法

8. 算法迭代停止准则

   1. 1）迭代点当前的梯度值的模值小于给定的值

      2）相邻两次迭代的距离或者对应函数的增量小于给定的值

      3）预测下降量的收敛准则

9. 对于一般函数而言，在局部极小点附近可以用一个**二次函数很好的近似**

10. 在设计无约束非线性优化问题的迭代算法时，可以借助二次模型来完成一次迭代

11. 对于一阶导数不可得的极小化方法，以证明用差商估计一阶导数，再结合拟牛顿法是目前有效的方式之一

12. 线搜索方法和信赖域法是两种基本的最优化算法格式

13. 精确线搜索方法

    1）精确线搜索方法

    a)确定搜索方向（search direction)

      各种线搜索方法的主要区别在于此

    主要区别在于构造的二次模型的方式：为什么要引入二次模型呢？

    b)寻找子问题的最优解（这是必须的吗？）

    c)更新迭代点

    精确线搜索方法一定能够保证全局收敛性吗？

14. 非精确线搜索方法

    问题：在线搜索子问题中，单纯保证增量减少的条件，无法保证算法收敛，或者收敛到目标解

    非精确线搜索方法和精确线搜索的方法主要差异在于线搜索方法的第二步，即：寻找子问题的解的问题，两者的差异性体现在一个求解最优解，一个给出近似解。

    既然子问题中给出下降方向的可行解无法保证线搜索方法收敛，或者收敛于局部最优解，子问题的近似的解的求解需要满足什么准则才能保证线搜索方法收敛并收敛域局部极小点呢：

15. **非精确线搜索收敛准则**

    

    原优化问题$f(x)$在$x_{0}$处给定下降方向$p$则精确线搜索问题的子问题为$\underset{\alpha\ge0}{min}(\phi (\alpha)),where, \phi(\alpha)=f(x_{0}+\alpha p)$

    非精确线搜索问题表示为找到$\alpha_{0}$使得$\phi(\alpha_{0})\le \phi(\alpha)$

    

    1）$armijo$准则

    满足如下条件的点$\alpha_{0}$：

    a) $\phi (\alpha_{0}) \le \phi(0)+\rho \phi^{’}(0)\alpha_{0},\rho\in(0,1)$

    b) $\exist \lambda \in(0,1).st.\phi( \alpha_{0}/\lambda)>\phi(0)+\rho \phi^{‘}(0)\alpha_{0}/\lambda$

    ------

    基于armijo准则非精确线搜索方法

    Initialization: $\alpha_{0},\lambda$

    if $\phi (\alpha_{0}) \le \phi(0)+\rho \phi^{’}(0)\alpha_{0},\rho\in(0,1)$

    do  

    ​	$\alpha_{0}=\alpha_{0}/\lambda$

    while $\phi (\alpha_{0}) > \phi(0)+\rho \phi^{’}(0)\alpha_{0},\rho\in(0,1)$

    else

    do 

    ​	$\alpha_{0}=\alpha_{0} \lambda$

    while $\phi (\alpha_{0}) \le \phi(0)+\rho \phi^{’}(0)\alpha_{0},\rho\in(0,1)$

    ------

    2）Goldstein 准则

    满足如下条件的点$\alpha_{0}$：

    a) $\phi (\alpha_{0}) \le \phi(0)+\rho \phi^{’}(0)\alpha_{0},\rho\in(0,0.5)$

    b)$\phi (\alpha_{0}) \ge \phi(0)+(1-\rho) \phi^{’}(0)\alpha_{0},\rho\in(0,0.5)$

    该准则保证二次函数的极小点满足该准则；

    但是对于非二次函数的极小点不一定能够满足该准则

    3）Wolf准则

    满足如下条件的点$\alpha_{0}$：

    $0<\rho \le\sigma<1$

    a) $\phi (\alpha_{0}) \le \phi(0)+\rho \phi^{’}(0)\alpha_{0},\rho\in(0,1 )$

    b) $\phi^{’}(\alpha_{0})\ge \sigma \phi^{‘}(0)$

    该准则能够保证所有函数的极小点满足该准则点

    4）强wolf准则

    $0<\rho<\sigma<1$

    a) $\phi (\alpha_{0}) \le \phi(0)+\rho \phi^{’}(0)\alpha_{0},\rho\in(0, 1)$

    b) $\left | \phi^{’}(\alpha_{0}) \right |\le -\sigma \phi^{‘}(0)$

    该准则具有更小的搜索范围，通过控制$\sigma$的值能够控制搜索的精度，当$\sigma=0$时，该准则退化为精确线搜索为题

    

    理论证明，线搜索中子问题中满足上述四种准则任何一个近似解都能收敛于局部最小解，当然上述准则也是有强约束的存在的，只有在这种约束满足时上述结论才成立。

    ------

16. **非精确线搜索方法**

    采用迭代方法寻找线搜索子问题的满足强wolf准则的点

    **迭代方法包括两个步骤**

    a)**划界阶段**(bracketing phase):寻找满足强wolf准则区域的一个**覆盖**

    **覆盖**：包含可接受点（满足强wolf条件的可行解）的一个**非平凡**区间$[m_{i},n_{i}]$(非平凡指的是$m_{i}\ne n_{i}$)

    b) **分割阶段**(secting phase):寻找覆盖$[m_{i},n_{i}]$的一个包含序列$[m_{j},n_{j}]$使得$[m_{j},n_{j}]\subset [m_{i},n_{i}]$, $\underset {j\rightarrow\infty}{lim}\left| m_{j}-n_{j}\right|=0$

    ------

    **恰当覆盖**

    给定迭代序列$\alpha_{0},\alpha_{1},\alpha_{2},...\alpha_{n}$

    恰当覆盖的定义：

    1）$a$是最好的测试点即$a=arg\underset{i\in [0,n]}{min} \alpha_{i}|\phi (\alpha_{i}) \le \phi(0)+\rho \phi^{’}(0)\alpha_{i},\rho\in(0,1)$

    2)	$b=\alpha_{i}|i\in[1,n]$，且满足$(b-a)\phi(a)^{‘}<0\wedge\left |(\phi(a)^{’}\right |\ge-\sigma \phi(0)^{‘}$

    3)	满足$\phi(b)>\phi(0)+\rho\phi(0)^{’}b||\phi(b)\ge\phi(a)$

    **可以证明，恰当覆盖包含满足强wolf条件点**

    可接受下界$\bar{\phi}$的定义: $\forall \alpha \ge 0,st,\phi(\alpha) \le \bar{\alpha}$,的界线为可接受下界，即任何使目标函数值小于结界的变量都是可接受点

    通过可接受点可以约束一下变量的搜索范围：

    即$\alpha\in [0,\mu]|\mu=\frac{\bar{\phi}-\phi(0)} {\rho\phi(0)^{‘}}$

    ------

    **一种基于wolf强约束准则的非精确线搜索算法流程**

    （1）**Bracketing Phase**

    ------

    **Algorithm1**

    **Initialization:**	$\alpha(0)=0;\alpha(1)\in (0,\mu);i=0;a_{0}=b_{0}=\alpha(0)；\tau_{1}=9$

    **Loop:**	$i=i+1$

    ​		**Part1:**判断当前迭代点$\alpha(i)$的值是否满足可接受下界$\bar{\phi}$，如果是则终止迭代并输出当前迭代点为目标点	

    ​				if  $\phi(\alpha(i))\le\bar{\phi}$

    ​						return $\alpha(i)$

    ​						迭代终止

    ​				else to **Part2**

    ​		**Part2:**判断当前迭代点是否能够和前循环区间$[a_{i-1},b_{i-1}]$构成恰当覆盖，如果成立则终止迭代，将当前区间作为目标输出

    ​				if $\phi(\alpha_{i})>\phi(0)+\rho\phi(0)\alpha_{i}||\phi(\alpha_{i})\ge\phi(\alpha_{i-1})$

    ​						$a_{i}=\alpha_{i-1};b_{i}=\alpha_{i}$

    ​						return $[a_{i},b_{i}]$

    ​						迭代终止

    ​				else to **Part3**

    ​		**Part3:** 判断当前迭代点是否满足强wolf准则的梯度约束条件，如果满足则终止迭代，将当前迭代点作为目标点输出

    ​				if $\left|\phi(\alpha_{i})^{’}\right |\le-\sigma\phi(0)^{‘}$

    ​						return $\alpha_ {i}$

    ​						迭代终止

    ​				else to **Part4**

    ​		**Part4:**判断当前迭代点是否能够和前循环区间$[a_{i-1},b_{i-1}]$构成恰当覆盖，如果成立则终止迭代，将当前区间作为目标输出

    ​				if $\phi(\alpha_{i})^{’}\ge 0$

    ​						$a_{i}=\alpha_{i};b_{i}=\alpha_{i-1}$

    ​						return $[a_{i},b_{i}]$

    ​						迭代终止

    ​				else to **Part5**

    ​		**Part5:**确定下次迭代的搜索区间

    ​				if $\mu\le 2\alpha_{i}-\alpha_{i-1}$

    ​						$\alpha_{i+1}=\mu$

    ​				else

    ​						$\alpha_{i}\in [2\alpha_{i}-\alpha_{i-1},min(\mu,\alpha_{i}+\tau_{1}(\alpha_{i}-\alpha_{i-1}))]$

    ​                return to **Loop**

    ------

    **算法说明**

    ​		1）Part5的搜索区间更新规则能够保证$\alpha_{0}<\alpha_{1}<...<\alpha_{n}$

    ​		2）Part2-Part4的条件保证迭代未终止时，$\alpha_{i}$满足如下条件

    ​		$(\phi(\alpha_{i})\le\phi(0)+\rho\phi(0)\alpha_{i})\wedge (\phi(\alpha_{i})^{’}< 0)\wedge(\phi(\alpha_{i})=\underset{k=1:i}{min}\phi(\alpha_{k})$

    ​		2）保证Part2和Part4的规则恒成立；同时也保证Part5区间更新规则的有效性；

    

    ------

    （2）**Sect ting Phase**

    

    **原理**： 对于bracketing phase 给出的恰当覆盖$[a_{0},b_{0}]$,sectting phase 部分是在该覆盖中找到一个新点$c$，如果$c$满足强wolf准则则迭代结束，否则产生一个新的恰当覆盖$[a_{1},b_{1}]$,其中$\left |(b_{1}-a_{1})\right|<\left |(b_{0}-a_{0})\right|$,并在其中寻找新得点，如此循环

    ------

    **Algorithm2**

    **Initialization:**	$[a_{0},b_{0}]$是一个恰当覆盖,$\tau_{2}=0.1;\tau_{3}=0.5;i=0$

    **Loop:**	$i=i+1$

    **Step1:**	在区间$（a_{i},b_{i}）$随机选择一个数$c$

    ​				$c\in[a_{i}+\tau_{2}(b_{i}-a_{i}),b_{i}-\tau_{3}(b_{i}-a_{i})]$

    **Step2:**	判断区间$[a_{i},c]$是否能够构成一个恰当覆盖

    ​				$if_{1}$ $\phi(c)>\phi(0)+\rho \phi(0)^{’}c ||\phi(c)\ge \phi(a)$

    ​						$[a_{i},c]$能够构成恰当覆盖

    ​						$a_{i+1}=a_{i};b_{i+1}=c$

    ​						return $[a_{i+1},b_{i+1}]$ to **Loop**

    ​				else 

    ​						判断点$c$是否满足强wolf准则的梯度条件

    ​						$if_{2}$ $\left|\phi(c)^{‘}\right|\le -\sigma\phi(0)^{’}$

    ​								return $c$

    ​								**迭代终止**

    ​						else

    ​								$a_{i+1}=c$

    ​								判断$[c,b_{i}]$能够构成恰当覆盖

    ​								$if_{3}$ $(b_{i}-a_{i})\phi(c)^{‘}<0$

    ​										$b_{i+1}=b$

    ​								else

    ​										$b_{i+1}=a_{i}$

    ​							    end $if_{3}$

    ​								return $[a_{i+1},b_{i+1}]$ to **Loop**

    ​						end $if_{2}$

    ​				end $if_{1}$

    **End Loop**

    ------

    **定理：**若$\sigma>\rho$且初始覆盖$[a_{0},b_{0}]$是一个恰当覆盖，则上述分割算法必定终止与满足强wolf准则条件的可接受点。

    

    ​						

    

    

    

    

    

    

    

    

    

 