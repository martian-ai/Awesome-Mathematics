

[TOC]



# Summary of Constrained Optimization

# Use in Machine Learning

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

# Basic Concept

1. **$C^{n}函数$**：$n$阶导数存在切连续的函数的集合（光滑函数：无穷阶导数存在且连续的函数$:=C^{\infty}$)

2. 函数的支撑集：即函数的定义域（但是由于不是所有的函数都定义在具有域代数结构的集合上，所以一般采用支撑集而非定义域）

3. 凸集：给定集合$C$，若$\forall x,y \in C ,\theta\in \left [0,1\right], \exist ((\theta x +(1-\theta)y)\in C)$

4. 锥：给定集合$C$，若$\forall x\in C ,\theta\in \Re], \exist (\theta x\in C)$

5. 凸锥：给定集合$C$，若$\forall x,y \in C ,a,b\in \Re^{+},\exist （(ax+by)\in C）$

6. 超平面：给定$n$空间$\Re^{n}$,任意一个子集$\Re^{n-1}$叫做空间$\Re^{n}$的超平面。

7. 集合与集合的分离：对于一般的两个集合，如果能够找到一个超平面，让这两个集合(严格)位于超平面的两侧，则称这两个集合是(严格)可分离的。严格的意义就是集合不同时在这个超平面接触。

8. 闭凸集的性质：设$S\subseteq\Re^{n}$是非空的闭集合，$y\in \Re^{n}$,若$y\notin S$，则存在唯一的$\bar{x}\in S,st:\left \|\bar{x} -y\right\|=\underset{x\in S}{min}\left\|x-y\right|$

9. 点与闭凸集的分离定理：对于非空闭凸集与其外一点，一定能够找到一个超平面，使得点与凸集位于超平面的两侧，即超平面严格分离这两者：

   设$S\subseteq\Re^{n}$是非空的闭集合，$y\in \Re^{n}$,若$y\notin S$，则存在$P\in \Re^{n}\setminus \left \{0\right\},a \in \Re,st: \forall x\in S,P^{T}x<a<P^{T}y$

10. 点与闭凸锥分离定理：对于非空凸锥与其外一点，一定能够找到一个过原点的超平面，让点与凸锥位于超平面两侧，即超平面严格分离这两点：

    设$C\subseteq\Re^{n}$是非空的闭凸锥，$y\in \Re^{n}\wedge y \notin C $,则存在$P\in \Re^{n}\setminus \left \{0\right\},st: \forall x\in S,P^{T}x<0<P^{T}y$

11. 凸集与凸集的分离定理：设$S_{1},S_{2}\subset \Re^{n}$是非空的凸集。若$S_{1}\cap S_{2}=\varnothing$,则存在$P\in \Re^{n}\setminus \left\{0\right\},st:P^{T}x^{1}\leq P^{T}x^{2},\forall x^{1}\in S_{1},x^{2}\in S_{2}$

12. 凸函数：给定函数$f$及其支撑凸集$C$,若$\forall x,y \in C,\theta \in \left [0,1 \right],f(\theta x+\left(1-\theta\right)y)\leq \theta f(x)+(1-\theta)f(y)$

13. 凹函数：给定函数$f$及其支撑凸集$C$,若$\forall x,y \in C,\theta \in \left [0,1 \right],f(\theta x+\left(1-\theta\right)y)\geq \theta f(x)+(1-\theta)f(y)$

14. 函数的上方集：设$f$是定义在凸集$C\in \Re^{n}$上的函数，函数的上方图定义为：$[f,C]=\left \{(x,r)\in \Re^{n}\times\Re|x\in C,f(x)\leq r\right\}$

15. 次梯度次微分：设$f$是定义在$\Re^{n}$上的函数，如果向量$p\in \Re^{n}$满足：$f(y)\geq f(x)+p^{T}(y-x),\forall y\in \Re^{n}$,则称$p$ 为$f$在$x$处的次梯度(subgradient)；$f$在$x$处的所有次梯度的集合记$\partial f(x)$,称为$f$在$x$处的次微分(subdifferential)

16. 次微分性质：如果$f$在$x$处可微，则$\partial f(x)=\left\{\Delta f(x)\right\}$

17. 正定矩阵：给定矩阵$A\in M_{\Re}^{n}$,若$\forall P\in \Re^{n},P\neq 0,\exist (P^{T}AP>0)$,则称该矩阵是正定矩阵

18. 正定矩阵的性质：

    1）正定矩阵所有的特征值都大于零

    2）对于任意的正定矩阵$A$都可以表示成$A=B^2$的形式，其中$B$也是正定矩阵

    3）矩阵$A$正定的充分必要条件是存在非退化矩$B$,使$A=B^{T}B$

    4)  矩阵$A$正定的充分必要条件是其各阶主子式都大于零

19. 半正定矩阵：给定矩阵$A\in M_{\Re}^{n}$,若$\forall P\in \Re^{n},P\neq 0,\exist (P^{T}AP\geq0)$,则称该矩阵是半正定矩阵

    #### KKT条件

20. 含有约束项的优化问题

    $ \begin{matrix} min f(x) \\ci(x)=0;i\in E\\cj(x) \le 0;j\in I \end{matrix}$ 

    其中$E,I$分别是等式约束和不等式约束的指标集（即约束项序号的集合）

    其中约束项给出目标函数的支撑集（目标函数自变量可取值得范围）

21. 给定优化问题的一个可行点$x^{*}$(满足约束的点)，在该点处的一个可行增量$\Delta x^{*}$（其对应的方向定义为可行方向）定义为：

    $\begin{matrix} ci(x^{*}+\Delta x^{*})=0;i\in E \\cj(x^{*}+\Delta x^{*})\le0;j\in I \end {matrix}$

    给定优化问题的一个可行点$x^{*}$(满足约束的点)，在该点处的一个下降增量$\Delta x^{*}$（其对应的方向定义为下降方向）定义为

    $f(x^{*}+\Delta x^{*})<f(x^{*})$

    可行下降增量：即是可行增量又是下降增量

    可行下降方向：即是可行方法又是下降方向

    $e.g$

    $\begin {matrix} \\min (x_{1}^{2}+x_{2}^{2})\\x_{2}-x_{1}^{2}-3\le0 \\-x_{1}-x_{2}+1\le0 \end {matrix}$

    ![fig_4](C:\Users\hanmushuying\Desktop\fig_4.jpg)

    

    

22. 积极约束和非积极约束

    1. 给定优化问题的一个可行点$x^{*}$(满足约束的点)，约束在$x^{*}$处等于零的叫做积极约束(例如上图的x2点)

       $ A^{*}=\{index|ci(x^{*})=0,i\in E ;cj(x^{*}=0,j\in I) \}$

       可行点$x^{*}$的积极约束影响目标函数的取值而非积极约束对目标函数没有影响:积极约束会限制目标函数在$x^{*}$处的可行方向，而非积极约束不会

    $e.g$

    ![fig_1](C:\Users\hanmushuying\Desktop\fig_1.jpg)

    

    

    

    

23. KKT 条件（含有约束的极小目标函数一阶必要条件）

    给定优化问题：

    $ \begin{matrix} min f(x) \\ci(x)=0;i\in E\\cj(x) \le 0;j\in I \end{matrix}$ 

    定义优化问题的拉格朗日函数$L(x,\lambda)=f(x)+\sum_{k\in E\cup I}\lambda_{k}ck(x)$

    **KKT条件为**：

    如果$x^{*}$是上述问题的局部极小点，当约束函数都是线性函数或者$[d(ci(x^{*})],d(cj(x^{*}))]$线性无关时，存在$\lambda_{i}\in \Re ,i\in E,\lambda_{j}\ge0,j\in I$使得以下条件满足：

    $\begin {matrix} d(f(x)+\sum_{i\in E \cup I} \lambda_{i}ci(x)|_{x=x^{*}}=0\\ci(x)=0;i\in E\\cj(x)\le0;j\in I\\ \lambda_{k}ck(x)=0;k\in E\cup I \end {matrix}$

    其中$\lambda$称为函数的$f(x)$的拉格朗日乘子：其反映了目标函数在$x^{*}$处对约束函数的敏感度：

    给定约束函数一个扰动如下：

    ​	$\begin {matrix} ci(x)-wi=0;i\in E\\cj(x) -wj \le 0;j\in I \end {matrix}$

    ​	其中$wi,wj$是约束函数的扰动

    ​	 如果$x^{*}$是目标函数含有扰动$w$约束的局部极小值，则其对应的朗格朗日函数$L(x{*}（w），\lambda （w),w)=f(x)+\sum_{k\in E\cup I}\lambda_{k}(ck(x)-wk)=f(x^{*})$

    $\frac {df(x)}{w}|_{w=0 }=\frac{dL(x,\lambda,w)}{dx}|_{w=0}+\frac{dL(x,\lambda,w)}{d\lambda}|_{w=0}+\frac{dL(x,\lambda,w)}{dw}|_{w=0}=-\lambda$

    

24. KKT条件推导过程

    给定最优化问题

    $ \begin{matrix} min f(x) \\ci(x)=0;i\in E\\cj(x) \le 0;j\in I \end{matrix}$ 

    约定：$a_{i}(x)，a_{j}(x)$为对应等式约束和不等式约束在点$x$处的导数

    如果$x^{*}$是上述问题的局部极小点,即$f(x)$在其局部可行增量$\Delta x $内都满足$f(x^{*}+\Delta x)\leq f(x^{*})$也就是说每个可行增量都对应目标函数的上升方向，等价于目标函数在$x^{*}$处不存在可行的下降方向

    如上所述在$x^{*}$点处，只有积极约束对目标函数有影响，非积极约束对目标函数没有约束作用，因此仅考虑积极约束集合：

    $A^{*}=\{k|c_{k}(x^{*})=0,k\in E\cup I\}=E\cup I^{*}$

    其中$I^{*}=\{k| c_{k}(x^{*})=0,k\in I\}$

    对于积极约束中的等式约束$E$，其在点$x^{*}$可行增量$\Delta x$满足如下条件：

    $a_{i}(x^{*})^{T}\Delta x=0,i\in E$

    对于积极约束中的不等式约束$I^{*}$，其在点$x^{*}$可行增量$\Delta x$满足如下条件：

    $a_{j}(x^{*})^{T}\Delta x \le 0,j\in I^{*}$

    在点$x^{*}$处使目标函数值下降的增量$\Delta x$满足如下条件：

    $f'(x^{*})^{T}\Delta x\le 0$

    因此在点$x^{*}$处不存在下降可行增量等价于下面关于增量$\Delta x$的方程组无解：

    $\left \{ \begin{matrix} a_{i}(x^{*})^{T}\Delta x=0,i\in E \\a_{j}(x^{*})^{T}\Delta x \le 0,j\in I^{*} \\f'(x^{*})^{T}\Delta x\le 0 \end {matrix} \right .$

    该方程组无解等价于下面关于$\lambda$的方程有解：

    $-f'(x^{*})=\sum_{i\in E}\lambda _{i}a_{i}(x^{*})+\sum_{j\in I^{*}}\lambda_{j}a_{j}(x^{*})$

    其中$\lambda_{i}\in \Re,\lambda_{j}\ge0$

    为了让上式能够适用于所有的约束项，上式可以等价的表述为：

    $\left \{ \begin{matrix} f'(x^{*})+\sum_{i\in E\cup I}\lambda _{i}a_{i}(x^{*}) =0 \\\lambda_{i}c_{i}(x^{*})=0,i\in E\cup I\\\lambda_{j}\ge0,j\in I^{*}  \end {matrix} \right.$

    上面的方程只给出了点$x^{*}$不存在可行下降增量的约束，但并未给出是否是可行解的约束（即是否满足约束条件），因此点$x^{*}$是局部极小点的必要条件是：

    

    当约束函数都是线性函数或者$[d(ci(x^{*})],d(cj(x^{*}))]$线性无关时

    $ \left\{ \begin {matrix} d(f(x)+\sum_{i\in E \cup I} \lambda_{i}ci(x)|_{x=x^{*}}=0\\ci(x)=0;i\in E\\cj(x)\le0;j\in I\\ \lambda_{k}ck(x)=0;k\in E\cup I \\ \lambda_{j} \ge 0,j\in I^{*}\end {matrix} \right.$

    

25. 凸优化

    函数$f$是凸函数如果一下任意一个条件满足

    $f((1-\theta)x+\theta y)=(1-\theta)f(x)+\theta f(y)$

    $f(y)-f(x)\ge f'(y)(y-x)$

    $H(f)|_{x}$is semi-positive 

    ![fig_2](C:\Users\hanmushuying\Desktop\fig_2.jpg)

    给定优化问题：

    $ \begin{matrix} min f(x) \\ci(x)=0;i\in E\\cj(x) \le 0;j\in I \end{matrix}$

    如果目标函数和约束函数都是凸函数(其中凸函数约束给出的可行解即支撑集是凸的如下图所示），那么该优化问题叫做凸优化

    ![fig_3](C:\Users\hanmushuying\Desktop\fig_3.jpg)

    由于任何非线性等式约束都是非凸约束(非线性等式约束给定的支撑集是非凸的如图所示），而任何线性等式约束都可以表示成两个不等式约束即

    $c(x)=0\leftrightarrow \left\{ \begin{matrix} c(x)\le0 \\-c(x)\le0\end {matrix}\right.$

    凸优化问题可以等效的表示成如下的形式

    $ \begin{matrix} min f(x) \\ci(x)\le0, i\in I\end{matrix}$

    **凸优化中，一阶kkt条件是全局极小点的充分条件**:

    证明：给定kkt点$x^{*}$及其对应的拉格朗日乘子$\lambda^{*}$对于任意的点$x$有：

    $f(x)\ge f(x)+\sum_{i\in I}\lambda_{i}ci(x)\ge f(x^{*})+(x-x^{*})^{T}f'(x^{*})+\sum_{i\in I}\lambda_{i}(c_{i}(x^{*})+(x-x^{*})^{T}a_{i}^{*})=f(x^{*})$

    **凸优化中，一阶kkt条件是全局极小点的充分条件,但是不是最优点一定是kkt点**（因为kkt条件是以正则化约束为前提的）

    

    # 拉格朗日对偶

    任何一个约束优化问题都存在一个对偶问题问题：什么是对偶问题，对偶问题存在几种与其对应，一般情况下原问题的最优值都大于或等于对偶问题的最优值（对偶性质）问题：为什么对偶性质成立呢,因此当原问题很难求解时，可以通过求解对偶问题得到原问题的近似解或者判定原问题是否有解（利用对偶性质可得）。

    

    令是原问题的最优解，是对偶问题的最优解，他们满足对偶性质：

    

    其中定义为对偶间隔，当为零时，说明原问题的最优解和对偶问题的最优解相同，这时我们称对偶是强对偶问题，这是我们希望得到问题：在什么条件下强对偶成立

    **为了回答上述问题，我们先介绍原优化问题的拉格朗日对偶问题，至于原问题的其它对偶问题可以作为扩展另做介绍**

    ## 大纲

    1、介绍该问题涉及到的一些基本概念以及前提假设 2、给出拉格朗日乘子存在性定理 3、给出拉格朗日对偶问题存在性的几何解释 4、给出强对偶成立的条件

    ## 1，基本概念

    给定**凸优化**问题，称作**原问题**  给定原问题的**扰动问题**：  其中是扰动量 定义函数 **易知扰动问题关于扰动变量**z**是单调不增的** 定义扰动的问题的上方集 **易知扰动问题的上方集是凸集**

     

    ## 2、拉格朗日乘子的存在性

    （拉格朗日乘子的存在性的证明中能够得到拉格朗日对偶的几何解释的原形）

    #### 2.1 约束问题的拉格朗日函数

    原问题： 其拉格朗日函数为,其中称作**朗格朗日乘子**

    #### 2.2 拉格朗日乘子的存在性

     **2.2.1拉格朗日乘子存在性问题：** 假设约束原问题存在最优解,则是否存在使得 ,该问题称为拉格朗日乘子存在性问题 **2.2.2 朗格朗日乘子存在性定理** 给定凸优化约束问题:,如果该约束问题在取得最优值,且存在,则存在且(也就是最优值在同一个点上得到)

    **2.2.3 拉个朗日乘子存在性定理的证明**

    

    

    **f.1，构建可分离的凸集**

    **给定约束扰动问题的上方集和集合如图1所示（红色代表,绿色代表),可以其定义易知，两个集合是只有交点)的凸集合 由凸集分离定理，存在过的超平面将集合和集合分离，即存在超平面使得满足**

    **f.2 构建分离超平面法向量**

    **由不等式可知，当,存在 ,可知**

    **同时，当,存在,可知**

    **由于,，可得,当,存在(超平面法向量不为零)使得,由于拉格朗日存在性定理条件"存在"，故这和是自相矛盾的，故;**

    **f.3 利用凸集不等式证明乘子的存在性**

    **由于，超平面的法向量可表示为,故 成立，由于，故有.**

    **由于,由于,故,故有,由于,由于,故,故有**

    #### **2.3 拉格朗日乘子的几何意义**

    **由于可知，,即,即是扰动问题在0处的次梯度，当关于可微时，即为$w(z)在0处的导数。**

    ## **3、拉格朗日对偶**

    #### **3.1 拉格朗日对偶的几何解释**

    

    **给定约束问题的扰动问题,如图2 中的红色曲线所示，原问题的最优值在为，因此该值可以通过扰动问题各支撑平面在中的截距来逼近，即扰动问题所有支撑平面在上的截距的最大值，作为的逼近，因此原问题可以转换为求扰动问题所有支撑超平面在上的截距最大的优化问题**

    #### **3.2 拉格朗日对偶问题的代数表示**

    **给定扰动问题上的一点,取在该点处的支撑超平面的法向量为,则过该点的超平面为,该超平面在轴上的截距为;由拉格朗日乘子的性质可知，为拉格朗日函数 的拉格朗日乘子，故有（）。由于所有的拉格朗日乘子满足 ,故截距最大的值为**

    **称函数为原始问题的对偶函数，可以肯定的是凸优化问题的对偶函数一定是凹函数，这可以通过凹函数的定义很好的证明。**

    **可以证明，任何优化问题的对偶问题都是凹函数**

    **称最优化问题为原始优化问题的对偶问题。**

    #### **3.2 强对偶和弱对偶**

    **如果原始问题的最优值和其对偶问题的最优值相同，则称该对偶是强对偶，否则称为弱对偶问题； 满足拉格朗日乘子存在性的条件的凸优化问题一定是强对偶问题**

    

