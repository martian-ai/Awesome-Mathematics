#### 基本概念--默认函数$f\in C^{n}$

1. **$C^{n}函数$**：$n$阶导数存在切连续的函数的集合（光滑函数：无穷阶导数存在且连续的函数$:=C^{\infty}$)

2. 函数的支撑集：即函数的定义域（但是由于不是所有的函数都定义在具有域代数结构的集合上，所以一般采用支撑集而非定义域）

3. 凸集：给定集合$C$，若$\forall x,y \in C ,\theta\in \left [0,1\right], \exists ((\theta x +(1-\theta)y)\in C)$

4. 锥：给定集合$C$，若$\forall x\in C ,\theta\in \Re], \exists (\theta x\in C)$

5. 凸锥：给定集合$C$，若$\forall x,y \in C ,a,b\in \Re^{+},\exists （(ax+by)\in C）$

6. 超平面：给定$n$空间$\Re^{n}$,任意一个子集$\Re^{n-1}$叫做空间$\Re^{n}$的超平面。

7. 集合与集合的分离：对于一般的两个集合，如果能够找到一个超平面，让这两个集合(严格)位于超平面的两侧，则称这两个集合是(严格)可分离的。严格的意义就是集合不同时在这个超平面接触。

8. 闭凸集的性质：设$S\subseteq\Re^{n}$是非空的闭集合，$y\in \Re^{n}$,若$y\notin S$，则存在唯一的$\bar{x}\in S,st:\left \|\bar{x} -y\right\|=\underset{x\in S}{min}\left\|x-y\right|$

9. 点与闭凸集的分离定理：对于非空闭凸集与其外一点，一定能够找到一个超平面，使得点与凸集位于超平面的两侧，即超平面严格分离这两者：

   设$S\subseteq\Re^{n}$是非空的闭集合，$y\in \Re^{n}$,若$y\notin S$，则存在$P\in \Re^{n}\setminus \\{0\\},a \in \Re,st: \forall x\in S,P^{T}x<a<P^{T}y$

10. 点与闭凸锥分离定理：对于非空凸锥与其外一点，一定能够找到一个过原点的超平面，让点与凸锥位于超平面两侧，即超平面严格分离这两点：

    设$C\subseteq\Re^{n}$是非空的闭凸锥，$y\in \Re^{n}\wedge y \notin C $,则存在$P\in \Re^{n}\setminus \\{0\\},st: \forall x\in S,P^{T}x<0<P^{T}y$

11. 凸集与凸集的分离定理：设$S_{1},S_{2}\subset \Re^{n}$是非空的凸集。若$S_{1}\cap S_{2}=\varnothing$,则存在$P\in \Re^{n}\setminus \\{0 \\},st:P^{T}x^{1}\leq P^{T}x^{2},\forall x^{1}\in S_{1},x^{2}\in S_{2}$

12. 凸函数：给定函数$f$及其支撑凸集$C$,若$\forall x,y \in C,\theta \in \left [0,1 \right],f(\theta x+\left(1-\theta\right)y)\leq \theta f(x)+(1-\theta)f(y)$

13. 凹函数：给定函数$f$及其支撑凸集$C$,若$\forall x,y \in C,\theta \in \left [0,1 \right],f(\theta x+\left(1-\theta\right)y)\geq \theta f(x)+(1-\theta)f(y)$

14. 函数的上方集：设$f$是定义在凸集$C\in \Re^{n}$上的函数，函数的上方图定义为：$[f,C]=\\{(x,r)\in \Re^{n}\times\Re|x\in C,f(x)\leq r\\}$

15. 次梯度次微分：设$f$是定义在$\Re^{n}$上的函数，如果向量$p\in \Re^{n}$满足：$f(y)\geq f(x)+p^{T}(y-x),\forall y\in \Re^{n}$,则称$p$ 为$f$在$x$处的次梯度(subgradient)；$f$在$x$处的所有次梯度的集合记$\partial f(x)$,称为$f$在$x$处的次微分(subdifferential)

16. 次微分性质：如果$f$在$x$处可微，则$\partial f(x)=\\{\Delta f(x)\\}$

17. 正定矩阵：给定矩阵$A\in M_{\Re}^{n}$,若$\forall P\in \Re^{n},P\neq 0,\exists (P^{T}AP>0)$,则称该矩阵是正定矩阵

18. 正定矩阵的性质：

    1）正定矩阵所有的特征值都大于零

    2）对于任意的正定矩阵$A$都可以表示成$A=B^2$的形式，其中$B$也是正定矩阵

    3）矩阵$A$正定的充分必要条件是存在非退化矩$B$,使$A=B^{T}B$

    4)  矩阵$A$正定的充分必要条件是其各阶主子式都大于零

19. 半正定矩阵：给定矩阵$A\in M_{\Re}^{n}$,若$\forall P\in \Re^{n},P\neq 0,\exists (P^{T}AP\geq0)$,则称该矩阵是半正定矩阵

    

    

    

    

    

    

    

    

