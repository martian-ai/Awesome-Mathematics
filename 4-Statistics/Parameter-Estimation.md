# Math-Parameter Estimation

### Reference
1. EM及高斯混合模型
    + http://www.cnblogs.com/zhangchaoyang/articles/2624882.html

### 参数估计
+ MLE
+ EM
- 机器学习基本理论 : 详解最大似然估计（MLE）、最大后验概率估计（MAP），以及贝叶斯公式的理解
- 似然与极大似然估计
	- https://zhuanlan.zhihu.com/p/22092462
	- 概率是在特定环境下某件事情发生的可能性
	- 而似然刚好相反，是在确定的结果下去推测产生这个结果的可能环境（参数）
	- ![](https://www.zhihu.com/equation?tex=%5Cmathcal%7BL%7D%28%5Ctheta%7Cx%29+%3DP%28x%7C%5Ctheta%29)
	- 解释了硬币问题的似然估计方法
- 入门 | 什么是最大似然估计、最大后验估计以及贝叶斯参数估计
	- 机器之心

### Maximum Likelihood Estimation
+ 要选择一个最佳参数θ*，使得从训练集中观察到和情况出现的概率最大。即模型：
    $$ \theta^{*} = arg\ \underset{\theta}{max}\ Pr(X=x;\theta)$$
+ 举例如下图
    
    ![](https://pic002.cnblogs.com/images/2012/103496/2012080420441173.png)
    
    + 一个小黑球沿着一个三角形的木桩滚入杯子a或b中，可建立一个概率模型，由于是二值的，设服从Bernoulli分布，概率密度函数为：
        $$f(k;p)=p^k(1-p)^{1-k} \  for\ k\ \epsilon \{0,1\} $$
    + 观察到的结果是X=（b,b,b,a,b,b,b,b,b,a）。小球进入a杯的概率为p，则满足10次实验的联合概率为:
        $$ Pr(X:p) = p^2(1-p)^8$$

    + 根据MLE的思想, 令上式一阶求导函数为0，得p=0.2(如果计算较为复杂可以取log)

+ 取log
    + 想要求最大值，就要求导，log后面跟的概率函数一般都是指数函数，或者是连乘的形式，取对数之后，如果是指数函数，可以直接将指数部分取出来，化掉log(log(e^x)=x),或者累加乘积变成累加和：log(a*b)=loga+logb

### Expectation Maximization
+ EM是一种迭代算法，它试图找到一系列的估计参数θ(0),θ(1),θ(2),....使得训练数据的marginal likelihood是不断增加的，即：
    $$
    \prod_{j=1}^{|x|}\ \sum_{y\epsilon\gamma} Pr)(X = x, Y=y ; \theta^{i+1})\ \geq \prod_{j=1}^{|x|}\ \sum_{y\epsilon\gamma} Pr)(X = x, Y=y ; \theta^{i})
    $$
+ 算法刚开始的时候θ(0)赋予随机的值，每次迭代经历一个E-Step和一个M-Step，迭代终止条件是θ(i+1)与θ(i)相等或十分相近。
+ E-Step
    + 是在θ(i)已知的情况下计算X=x时,Y=y的后验概率
        $$q(x,y;\theta^{i}) = f(x|X)*\prod_{j=1}^{|x|}\ \sum_{y\epsilon\gamma} Pr)(Y=y\ |\ X=x ; \theta^{i}) $$
        + f(x|X)是一个权值，它表示观测值x在所有观察结果X中出现的频率
        
+ M-Step
    $$ \theta^{i+1} = arg\ \underset{\theta}{max}\ \sum_{(x,y)\epsilon\(X,Y)}\ q(x,y;\theta^{i})\ logPr(X=x, Y=y;\theta^i) $$
    + $q(x,y;\theta^{i})$ 在E-Step已经求出来了。这时候可以用“令一阶导数等于0”的方法求出θ
+ EM算法收敛性的证明需要用到Jensen不等式，这里略去不讲

   ![](https://pic002.cnblogs.com/images/2012/103496/2012080421094245.png)

+ 举例如上图
    +  如图多了两块三角形木桩，分别标记序号为0，1，2。并且实验中我们只知道小球最终进入了哪个杯子，中间的路线轨迹无从得知
    + X取值于{a,b,c}表示小球进入哪个杯子。Y取值于{0,1,2,3}表示小球进入杯子前最后一步走的是哪条线路。小球在3个木桩处走右边侧的概率分别是p=(p0,p1,p2)
    + 跟上例中一样，X表示训练集观测到的值，p是模型参数，而这里的Y就是"隐含变量"
    + 假如我们做了N次实验，小球经过路径0,1,2,3的次数依次是N0,N1,N2,N3
        $$ p_0 = (N_2+N_3)/N$$
        $$ p_1 = N_1/(N_0 + N_1)$$
        $$ p_2 = N_3/(N_2 + N_3)$$

    + 定义公式如下
        $$ Pr(X=x) = \sum_{y\epsilon\gamma} Pr)(X = x, Y=y ; \theta)$$
    + 由于有隐变量的存在, 实现上上式很难找到一种解析求法，使用EM这种迭代方法求解
    + EM 求解过程
        +  做了N次实验，滚进3个杯子的次数依次是Na,Nb,Nc
        +  $\theta^0 = (p^{(0)}_0,p^{(0)}_1,p^{(0)}_2)$
        +  E-Step
            $$ f(x|X) = N_x/N $$
            $$ Pr(Y=0|X=a) =1 $$ 
            $$ Pr(Y=3|X=c) = 1 $$
            $$ Pr(1|b;\theta_{(i)}) = \frac{(1-p_0^{(i)}) p_1^{(i)}}  {(1-p_0^{(i)})p_1^{(i)} + p_0^{(i)}(1-p_2^{(i)})} $$
            $$ Pr(2|b;\theta_{(i)}) = \frac{(1-p_2^{(i)}) p_0^{(i)}}  {(1-p_0^{(i)})p_1^{(i)} + p_0^{(i)}(1-p_2^{(i)})} $$
            + 其它情况下Y的后验概率都为0
        + M-Step
            + 我们只需要计算非0项就可以了
            ![](https://pic002.cnblogs.com/images/2012/103496/2012080509161081.png)
            + 上面的每行第3列和第4列相乘，最后再按行相加，就得到关于θ(i+1)的函数，分别对p0,p1,p2求偏导，令导数为0，可求出p'0,p'1,p'2
            ![](https://pic002.cnblogs.com/images/2012/103496/2012080509231752.png)
+ 对于一般的模型，EM算法需要经过若干次迭代才能收敛，因为在M-Step依然是采用求导函数的方法，所以它找到的是极值点，即局部最优解，而非全局最优解。也正是因为EM算法具有局部性，所以它找到的最终解跟初始值θ(0)的选取有很大关系。

+ 在求解HMM的学习问题、确立高斯混合模型参数用的都是EM算法。