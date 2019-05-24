# Summary of Constrained Optimization

# Use in Machine Learing

+ SVM
+ Maximum Entropy Model



# KKT

## Define of KKT

+ Karush-Kuhn-Tucker Conditions

## Equality optimization

+ Lagrange 乘数法

## Inequality optimization

+ 例子
  $$
  \begin{eqnarray}
  min f(x) \\
  s.t. g_1(x) = a - x \leq 0 \\
  		 g_2(x) = x - b \leq 0
  \end{eqnarray}
  $$
  

+ 主要思想

  ![](http://ww3.sinaimg.cn/large/006tNc79ly1g37pxdoa1dj30k00a8wet.jpg)

+ Step 1 **不等式约束优化** 转化 **等式约束优化**

  + 为了将不等式约束改为等式约束， 引入两个松弛变量 $a_1^2$ 和 $b_1^2$， 原来的约束变新的等式约束

    ![](https://pic4.zhimg.com/80/v2-dcf3439670719b2ac1d8878bef7d80cf_hd.jpg)

+ Step 2 **等式约束优化** 转化 **无约束优化**
  + Langrage 乘数法

# Reference

+ https://zhuanlan.zhihu.com/p/26514613
+ Convex optimization
+ https://zhuanlan.zhihu.com/p/27731819

