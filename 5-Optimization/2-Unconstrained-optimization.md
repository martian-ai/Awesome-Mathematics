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



# 牛顿法

+ 求根

+ 最优化

  + 优化目标 $ min_{x \in R^n}  f(x)$， 并设 $x^*$ 为目标函数的极小点

  + 设f(x) 具有二阶偏导数， 若第k次的迭代值为 $x^{(k)}$, 则 $x^{(k)}$附近的二阶泰勒展开为

    $$ f(x) = f(x^{(k)}) + g^T_k(x-x^{(k)}) + \frac{1}{2}(x - x^{(k)})^T H(x^{(k)})(x-x^{(k)} $$

  + 其中

    + $g_k = g(x^{(k)}) = \nabla f(x(k))$ 是该点的梯度值
    + $H(x^{(k)}) = [\frac{\partial^2 f}{\partial x_i \partial x_j}]_{n*n}$  是 $f(x)$ 的海森矩阵 

  + f(x) 有极值必要条件，一阶导为零，当$H(x^{(k)}) $ 为正定阵时，取得极小值
  + https://zhuanlan.zhihu.com/p/37524275