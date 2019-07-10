[TOC]



# Summary of Optimization

# Define

+ 是以数学的方式来刻画或找出问题最优解的一门学科
+ 在数学领域称为数学规划
+ 在管理领域称为运筹学
+ 解决大量实际应用问题有力的工具。

# Taxonomy

+ 根据目标函数和约束函数的性质（线性、非线性、是否凸），变量数目（多或少）和函数的光滑性（是否可微）等均可对优化问题分类
+ 无约束优化：目标函数中的可变分量没有任何约束的优化问题；

+ 约束优化：目标函数中的可变分量具有某些约束；

+ 连续优化：目标函数和约束函数都是连续的；

+ 离散优化：约束给定的可行解是离散的优化；

+ 线性优化：目标函数和约束函数都是线性的优化问题；

+ 非线性优化：目标函数和约束函数含有非线性的优化问题。

## Linear Programming

1.1  线性规划问题的基本形式

1.2  线性规划的单纯形法

1.3 线性规划的对偶问题

## Unconstrained Optimization

+ 极小点条件

+ 无约束优化方法：线搜索法
  + 最速下降法
  + 牛顿法
  + 共轭梯度法
  + 拟牛顿法
  + DFP
  + BFGS法
  + 最小二乘

+ 无约束优化方法：信赖域法

## Constrained Optimization

3.1 拉格朗日乘子

3.2 局部解一阶条件

3.2 局部解二阶条件

3.3 凸优化问题

3.4 凸优化和拉格朗日乘子

3.5 对偶问题

## Linear Constrained Optimization

4.1 等式约束二次规划

4.2 积极集法

4.3 线性等式约束规划

4.4 线性不等式约束规划

4.5 锯齿现象

## Unlinear Contrained Optimization

5.1 惩罚和障碍函数

5.2 乘子罚函数

5.3 $l_{1}$精确罚函数

5.4 逐步二次规划法



## Problem

+ 协同优化
+ 组合优化
+ 单纯行



# Reference

+ https://nlopt.readthedocs.io/en/latest/NLopt_Python_Reference/
+ https://item.jd.com/17985044812.html