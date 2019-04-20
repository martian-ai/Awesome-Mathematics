# Information Theory
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

## Joint Entropy --- H(X, Y)

$H(X,Y) = - \sum_x \sum_y P(x,y)log_2[P(x,y)]$

$$H(X, Y)  \geq max [H(X), H(Y)] $$

$$H(X, Y)  \leq H(X) + H(Y) $$

## Condition Entropy --- H(Y|X)

+  $H(Y|X) = \sum_{x \in X} p(x) H(Y|X=x) = \sum_{x \in X, y \in Y} p(x,y) log \frac{p(x)}{p(x,y)} = H(X, Y) - H(Y)$
+ 减小信息熵：使用上下文（其他条件）
	- 翻译问题中Bush 是多义的
	- 当上下文中出现 ‘美国’， ‘总统’ 等词的时候 可翻译为 ‘布什’
	- 只用当随机变量X 和 Y 有关系时 才能减小不确定性

## Mutual Information --- H(X;Y)

+ 变量之间的相关程度
+ $H(X;Y) = \sum_{y \in Y} \sum_{x \in X} p(x, y) log(\frac{p(x,y)}{p(x)p(y)}) = H(X)+ H(Y) - H(X,Y)$
+ 应用
	+ PMI

## Cross Entropy --- H(p, q)

- 两个概率分布P(x), Q(x)，其中P(x)表示真实分布，Q(x)表示非真实分布
- $$ H(P, Q) = -  \sum P(x) log \frac{1}{Q(x)} $$
- $$ H(P, Q) = -  \int P(x) log \frac{1}{Q(x)} $$

## Relative Entropy --- KL(p||q)[5]

+  Kullback-Leibler divergence or  information entropy

+ 两个概率分布间**非对称性**的度量

+ 在信息论中,相对熵等价于两个概率分布的信息熵的差值

+ $$KL(P||Q) = \sum P(x) log \frac{P(x)}{Q(x)}$$

+  $$KL(P||Q) = \int P(x) log \frac{P(x)}{Q(x)}$$

+ $$ KL(P||Q) = H(P, Q) - H(Q)$$

	+ H(P, Q) Cross Entropy

+ 推导

	+ (信息编码的解释)在同样的字符集上，假设存在另一个概率分布Q(x)，如果用概率分布的最优编码P(x)（即字符

		的编码长度等于$log \frac{1}{P(x)}$, 来为符合分布Q(x) 的字符编码，那么表示这些字符就会比理想情况多用一些比特数。相对熵就是用来衡量这种情况下平均每个字符多用的比特数，因此可以用来衡量两个分布的距离

	+ $$KL(P||Q) = - \sum P(x) log \frac{1}{P(x)} + \sum P(x) log \frac{1}{Q(x)} = \sum P(x) log \frac{P(x)}{Q(x)} $$ 

+ 性质

	+ 不对称性
		+ 尽管KL散度从直观上是个度量或距离函数，但它并不是一个真正的度量或者距离，因为它不具有对称性，即KL(P||Q)!=KL(Q||P)
	+ 非负

 ## Jensen-Shannon Divergence

+ $$ JS(P||Q) = \frac{1}{2} KL(P(x) || \frac{P(x)+Q(x)}{2} +  \frac{1}{2} KL(Q(x) || \frac{P(x)+Q(x)}{2}$$
+ 性质
	+ 值域[0,1]
	+ 对称性 JS(P||Q) = JS(Q||P)

## Entropy, Joint Entropy, Condition Entropy, Mutual Information

![](https://ws3.sinaimg.cn/large/006tNc79ly1g25go84nwnj30ko0ekwf8.jpg)



## Relative Entropy v.s. Cross Entropy

+ ML/DL
	+ 交叉熵 是 KL散度和 真实的熵的和, 所以 优化 Cross Entropy 和 KL 是一样的

## [信息增益等](<https://github.com/Apollo2Mars/Algorithms-of-Artificial-Intelligence/blob/master/2-Ensemble-Learning/0-Decision-Tree.md>)

## 最大熵模型

+　思想
	+　最大熵原理指出，需要对一个随机事件的概率分布进行预测是，我们的预测应当满足全部已知的条件，未知的部分概率应该是均匀的，这样预测的风险最小，因为这时的信息熵最大，所以称这种模型为最大熵模型。举一个例子，如果没有任何已知条件下问你投一个骰子，出现5点的概率多大，这时假定所有的点数出现的概率是相等的一定是一种最保险的方法，这就是最大熵模型。

## Reference

+ [ 1 ]: [条件熵 demo](<https://zhuanlan.zhihu.com/p/26551798>)
+ [ 2 ]:[相对熵](<https://baike.baidu.com/item/%E7%9B%B8%E5%AF%B9%E7%86%B5/4233536?fr=aladdin>)

## 不理解

+ Ｈ(X,Y) Ｈ(p,q)

