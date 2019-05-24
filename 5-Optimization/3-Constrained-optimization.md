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

+ 主要思想

  ![](http://ww3.sinaimg.cn/large/006tNc79ly1g37pxdoa1dj30k00a8wet.jpg)

+ Step 1 **不等式约束优化** 转化 **等式约束优化**

  + KKT条件

  + 一般例子

    $$ min f(x)$$

    $$ st. $$

    ```
    $$
    p(x) = 
    \begin{cases}
      p, & x = 1 \\
      1 - p, & x = 0
    \end{cases}
    $$
    ```

+ Step 2 **等式约束优化** 转化 **无约束优化**
  + Langrage 乘数法

# Reference

+ https://zhuanlan.zhihu.com/p/26514613
+ Convex optimization
+ https://zhuanlan.zhihu.com/p/27731819

