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



# 梯度下降法

+ 

# 牛顿法

## 求根

+ 并不是所有方程都有求根公式，或者求根公式很复杂，导致求解很困难，利用牛顿法，可以迭代求解
+ 原理：
  + 利用泰勒公式展开，在$x_0$ 处展开一阶形式，$f(x) = f(x_0) + f^{`}(x_0)(x-x_0)$ , 并不是完全相等
  + 令$f(x) = 0$, 得到$x_1$, $x_1$ 相对 $x_0$ 更接近正确结果，逐步递推
  + $x_{n+1} = x_n  - f(x_n)/f^{`}(x_n)$
  + 迭代之后，在 $f(x^*) = 0$ 收敛

![](http://ww4.sinaimg.cn/large/006tNc79ly1g3qlcv7uj6j30es0ck3yp.jpg)

## 最优化

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



# 梯度下降法 v.s. 牛顿法

+ 两者都是迭代求解, 梯度下降法是梯度求解,  而牛顿法是二阶的海森矩阵的逆矩阵求解
+ 相对而言, 牛顿法收敛更快(迭代次数更少), 但每次迭代的时间会更长
	+ $x^{( k+1 )} = x^{(k)} - \lambda \nabla f(x^{(k)})$
	+ $x^{(k+1)} = x^{(k)} - \lambda  H_k^{-1}\nabla f(x^{(k)})$
+ 至于为什么牛顿法收敛更快，通俗来说梯度下降法每次只从你当前所处位置选一个坡度最大的方向走一步，牛顿法在选择方向时，不仅会考虑坡度是否够大，还会考虑你走了一步之后，坡度是否会变得更大。所以，可以说牛顿法比梯度下降法看得更远一点，能更快地走到最底部



# 拟牛顿法

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

# DFP(Davidon-Fletcher-Powell)

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

# BFGS

+ 与 DFP 类似, 唯一的区别是 使用 $B_k$ 逼近 $H_k$
+ 公式如下
	+ $B_{k+1} = B_{k} + \frac{y_k y_k^T}{y_k^T \delta_k}   - \frac{B_k \delta_k \delta_k^T B_k}{\delta_k^T B_k \delta_k}$



# Broyden

+ 在 BFGS 的公式中带入 $G_k = B_k^{-1} $, $G_{k+1} = B_{k+1}^{-1} $
+ 并使用两次 Sherman-Morrison 公式得到, BFGS 关于$G_k$ 的公式
	+ $G_{k+1} = (I - \frac{\delta_k y^T}{\delta_k^T y_k})G_{k} (I - \frac{\delta_k y^T}{\delta_k^T y_k})^{-T} + \frac{\delta_k \delta_k^T}{\delta_k^T y_k} $
+ $G_{k+1} = \alpha G^{DFP} + (1-\alpha) G^{BFGS}$



# Usage

+ 

# Reference

+ 统计学习方法第二版 附录B

+ https://zhuanlan.zhihu.com/p/37524275
