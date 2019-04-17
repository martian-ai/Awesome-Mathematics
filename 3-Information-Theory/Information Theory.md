# Information Theory
## Reference
+ 统计自然语言处理　P23
+ 交叉熵的推导
	+ https://www.cnblogs.com/baiting/p/6101969.html

## 信息的度量-自信息量

+ 描述一条信息自己的大小

+ 公式 $h(x) = -log_2 p(x)$
  + 一个事件发生的概率越大，其信息量越小， 因此概率取了负对数（保证非负）
  + 两个独立事件X， Y 的联合概率是可乘的，即$P(X,Y) = P(X)P(Y)$ ， 则有X， Y 同时发生的信息量是可以相加的 $h(XY) = h(X) + h(Y)$
+ demo
  + 英文26个字母，每个字母出现的概率是相等的，那么其中一个字母的自信息量的大小是 $h = - log_2 {\frac{1}{26}}$

## 信息不确定性的度量：熵

+ 整个系统的信息量
+ 公式 $H = \sum_{i=1}^{n} p_i h_i = -\sum_{i=1}^{n}p_i log_2 p_i$ 

## 联合熵

## 条件熵

+ 希望信息熵越小越好，可花较少的代价确定信息
+ 减小信息熵：使用上下文（其他条件）
  + Bush 是多义的
  + 当上下文中出现 ‘美国’， ‘总统’ 等词的时候 可翻译为 ‘布什’
  + 只用当随机变量X 和 Y 有关系时 才能减小不确定性
+ 公式 $H(Y|X) = \sum_{x \in X} p(x) H(Y|X=x) = \sum_{x \in X, y \in Y} p(x,y) log \frac{p(x)}{p(x,y)}$

## 互信息

+ 变量之间的相关程度
+ $I(X;Y) = \sum_{y \in Y} \sum_{x \in X} p(x, y) log(\frac{p(x,y)}{p(x)p(y)})$



## 相对熵

## 交叉熵

## 最大熵



## 信息熵，条件熵，互信息 直接的关系

![](https://ws3.sinaimg.cn/large/006tNc79ly1g25go84nwnj30ko0ekwf8.jpg)



## [信息增益等](<https://github.com/Apollo2Mars/Algorithms-of-Artificial-Intelligence/blob/master/2-Ensemble-Learning/0-Decision-Tree.md>)



## Reference

+ <https://blog.csdn.net/wwh578867817/article/details/50464922>
+ [条件熵 demo](<https://zhuanlan.zhihu.com/p/26551798>)





