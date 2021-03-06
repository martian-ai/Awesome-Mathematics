# 代数中的基本概念

1. **二元关系** ： 设任意非空集合X,Y，$ \forall k \in X \times Y​$, $k​$ 叫做X与Y之间的一个二元关系；给定任意一个二元关系$\left(x,y\right) \in \omega ​$, 用记号$x \omega y ​$表示，并称 $x​$ 与$y​$有关系$\omega​$；例如实数域$\Re​$上的关系$\leq​$就是一个二元关系。

2. **等价关系** ：集合$X$上的一个二元关系$\sim $叫做等价关系 若$\forall x,y,z \in X $ 满足如下关系：

   1）$x \sim x​$ （反身性）；2) $x \sim y \rightarrow y\sim x​$ （对称性）； 3) $x \sim y, y\sim z \rightarrow x\sim z​$ (传递性)

   例如实数域$\Re$上的二元关系$=$就是一个等价关系；而定义在其上的二元关系$\leq$就是等价关系了

3. **偏序关系** ： 集合$X$上的一个二元关系$\leq$叫做偏序关系，若$\forall x,y,z \in X$ 满足如下关系：

   1）$x \sim x$ （反身性）； 2）$x\leq y, y\leq x \rightarrow x=y$ （反对称性); 3) $x \leq y, y\leq z \rightarrow x\leq z$ (传递性)

4. **全序集**：给定一个偏序关系$\leq$ 的集合$X$ ,如果$\forall \left(x,y\right) \in X \times X, \exists x\leq y ,or, y\leq x$,则该集合 $\left(X,\leq \right)​$称为全续集或者线性序集；

5. **偏序集**： 给定一个偏序关系$\leq$ 的集合$X$ ，如果$\exists （x,y) \in X \times X, st: x\leq y ,or, y\leq x$,则该集合$\left(X,\leq \right)$称为偏序集；

6. **公理化集合论**

   1）容积公理：集合$A$ 与集合$B$ 相等，当且仅当它们有共同的元素

   2）分出公理：对于任何集合$A$和性质$P$,有这样的集合$B$，它所包含的元素，是且仅是$A$ 中的那些具有性质$P$的元素

   3）并公理：对于由集合构成的任何集合$M$，存在集合$\cup M$,称为集合$M$的并，它的元素恰好是$M$中所包含元素的元素

   4）对公理：对于任意集合$X,Y$,存在一个集合$Z$，使$X,Y$是它仅有的元素

   5）子集之集的公理：对于任意集合$X$，存在集合$P\left(X\right)$，它的元素恰好为集合$X$的一切子集

   6）无穷公理：归纳集存在

   7）置换公理论：设$f\left(x,y\right)​$是这样一个命题，使得对于集合$X​$中任意$x_{0}​$存在唯一的对象$y_{0}​$使得$f\left(x_{0},y_{0}\right)​$成立。这时存在$x\in X st: f(x,y)​$成立的那些y能组成集合

   8）选择公理：对于任意非空集合的族，存在一个集合$C​$，使得对所给族中的每个集合$X​$ ,集合$X\cap C​$恰好只含有一个元素

7. **任何抽象公里系统的两个问题**

   1）这组公理是否相容，即是否存在满足列出的所有条件的集合，这是公理系统的无矛盾性问题；

   2）这组公理所确定的数学对象是否是唯一的，即如逻辑学所说，这组公里是不是范畴的，这里的唯一指的是同构意义上的唯一性

8. **实数集 $\Re$公里系统**

   1）给定加法运算+（加法阿贝尔群代数结构)：运算封闭性，结合性，交换性，零元和逆元的存在性

   2)  给定乘法运算$\times$ (乘法阿贝尔群代数学结构)：运算封闭性，结合性，交换性，单位元存在性，非零元素逆元存在性

   3）乘法和加法结合运算（乘法对加法满足分配律）

   4）给定集合上的线性续集二元关系$\leq$

   5)  给定加法运算与二元关系的关系

   6）给定乘法运算与二元关系的关系

   7）完备（连续）公理：如何集合$X,Y$是实数集 $\Re$上的非空子集，且具有性质：$\forall \left(x,y\right) \in X\times Y, x\leq y $恒成立，则存在$c\in \Re, st: x\leq c \leq y$

9. **归纳集**：$\forall X \subseteq \Re, \forall x \in X,\exists (x+1)\in X$,满足这种关系的集合称为归纳集，比如实数是归纳集，整数的集合是归纳集

10. **自然数集$\mathbb{N}$** ：包含数1 $\left(1 \in \Re \right)$ 的一切归纳集合之交叫做自然数集

11. **数学归纳原理** ：如何$E$是自然数集$\mathbb{N}$的子集，$1\in E$,并且当$x\in E \rightarrow x+1 \in E$,那么$E=\mathbb{N}$

    $(E\subseteq \mathbb{N} )\wedge(1\in E)\wedge(\forall x\in E(x\in E \rightarrow x+1 \in E))\rightarrow E=\mathbb{N}$

12. **归纳法原理**：假设对于每一个$n \in \mathbb{N}$,我们有某一个命题$M(n)$. 又假设我们有一个法则，对于任意给定的$l$，只要$M(k)$对所有的$k< l$ 真就可以证明$M(l)$真，则$\forall n \in \mathbb{N}, M(n)$成立

13. **素数**：设$P\in \mathbb{N},P\neq 1$, 如果在$\mathbb{N}$中除了1和其本身外，不再有因数，$P$为素数

14. **算数基本定理**：每个自然数能够唯一（不计因数顺序的区别）表成乘积的形式：$ n=\prod_{i=1}^{k} P_{i}$,其中$P_{i}$为素数

15. **阿基米德原理**: 如何$h$是任意一个固定的正数，那么，对于任何实数$x$，必能找到**唯一**的整数$k$，使得$(k-1)h\leq x\ <kh$

## 代数基本结构：群，环，域

## 群

1. **二元运算**： 设$X​$是任意集合，从$X\times X​$到$X​$的任意映射$\tau : X\times X \rightarrow X​$叫做集合$X​$上的二元代数运算。这样取元素$a,b \in X​$，有序对$(a,b)​$ 对应于$X​$中唯一确定的元素$\tau (a,b)​$,有时将$\tau (a,b)​$写成$a\tau b​$的形式。

2. **代数结构**：对于任意的集合$X$，给定在其上的一个运算$\tau$，就得到了一种代数结构$(X,\tau)$

3. **运算的结核性**：定义在集合$X$上的二元运算$\tau$是结合的，如果$\forall a,b,c \in X,(a\tau b)\tau c=a\tau (b\tau c)$

4. **运算的交换性**: 定义在集合$X$上的二元运算$\tau$是交换的，如果$\forall a,b \in X,a\tau b=b\tau a$

5. **运算的单位元**: 定义在集合$X$上的二元运算$\tau $存在单位元 $e$，如果$\forall a \in X,st:e\tau a=a\tau e=a$

6. **半群**： 集合$X$连同其上给定的满足结合律的二元运算称为一个半群

7. **幺半裙**：含有单位元的半群叫做幺半群

8. **可逆元素**：幺半群$(X,\tau )$中的元素$a$是可逆的 如果存在元素$a^{'}$使得，$a\tau a^{'}=a^{''}\tau a=e$,其中$e$是幺半群$X$的单位元

9. **群**：所有元素都可逆的幺半群称为群，其总体定义如下：

   对于集合$X$，及在其上定义的运算$\tau$,如果满足如下性质，称代数结构$(X,\tau)$是群：

   1）$\forall a,b \in X, \exists c \in X, st: a\tau b=c$(运算封闭性)；

   2）$\forall a,b,c \in X,(a\tau b)\tau c=a\tau (b\tau c)$(运算结合性)‘

   3）$\forall a\in X, \exists e\in X,st :a\tau e=e\tau a=a$(单位元存在性)

   4）$\forall a\in X,\exists a^{i}\in X,st: a\tau a^{i}=a^{i}\tau a=e$ (逆元的存在性)

10. **阿贝尔群**：运算具有交换性的群叫做阿贝尔群

11. **群同构**：两个分别具有运算$\tau_{1},\tau_{2}​$的群$(G_{1},\tau_{1})​$与$(G_{2},\tau_{2})​$称为是同构的，若存在一个映射$f:G_{1}\rightarrow G_{2}​$使得：

    1）$\forall a,b\in G_{1},\exists f(a\tau_{1} b)=f(a)\tau_{2}f(b)​$

    2) $f​$是双射

12. **同构群的性质**

    1）群$(G_{1},\tau_{1})​$的单位元$e_{1}​$与群$(G_{2},\tau_{2})​$的单位元$e_{2}​$是对应的，即$f(e_{1})=e_{2}​$

    2)  $\forall x \in G_{1},\exists f(x_{'})=f(x)^{'}$

    3) 逆映射$f^{'}:G_{2}\rightarrow G_{1}$存在，且也是一个同构

    

13. **同态**：两个分别具有运算$\tau_{1},\tau_{2}$的群$(G_{1},\tau_{1})$与$(G_{2},\tau_{2})$称为是同态的，若存在一个映射$f:G_{1}\rightarrow G_{2}$使得：

    1） $\forall a,b\in G_{1},\exists f(a\tau_{1} b)=f(a)\tau_{2}f(b)$

14. **同态群的性质**

    在同态的定义中不要求映射是单射，也不要求映射是满射，给出同态映射$f$核的定义

    $ ker f= \\{ x\in G_{1} | f(x)=e_{2} \\} $

    同构和同态的主要区别在于非平凡核$ker f$的存在性（其中的平凡指的是只有含有一个元素的集合）

## 环

1. **环**：设$X​$是一个非空集合，在$X​$上定了两种运算$\tau_{1},\tau_{2}​$,满足如下条件：则称代数结构$(X,\tau_{1},\tau_{2})​$是环：

   1）$(X,\tau_{1})​$是阿贝尔群；

   2）$(X,\tau_{2})​$是半群；

   3）运算$\tau_{1},\tau_{2}$以分配律相联系，即：

   ​	$\forall a,b,c \in X,\exists (a\tau_{1} b)\tau_{2}c=(a\tau_{2} c)\tau_{1}(b\tau_{2}c)$

   一般称$(X,\tau_{1})$是环$(X,\tau_{1},\tau_{2})$的加法群，称$(X,\tau_{2})$是环$(X,\tau_{1},\tau_{2})$的乘法群

2. **含有单位元的环**：如果$(X,\tau_{2})​$是一个幺半群（即含有单位元的群）则称环$(X,\tau_{1},\tau_{2})​$是含有单位元的环

3. **交换环**：如果$(X,\tau_{2})$是可交换的，则称环$(X,\tau_{1},\tau_{2})$是交换的

4. **环的同态**： 设$(X,\tau_{1},\tau_{2}),(Y,\phi_{1},\phi_{2} )​$是两个环，映射$f:X\rightarrow Y​$称为同态，若$f​$保持环的两种运算即：

   1）$\forall x_{1},x_{2}\in X，\exists f(x_{1}\tau_{1}x_{2})=f(x_{1})\phi_{1}f(x_{2})​$

   2)  $\forall x_{1},x_{2}\in X，\exists f(x_{1}\tau_{2}x_{2})=f(x_{1})\phi_{2}f(x_{2})$

   或者：

   $\forall x_{1} ,x_{2},x_{3}\in X ,\exists f((x_{1}\tau_{1}x_{2})\tau_{2}x_{3})=(f(x_{1})\phi_{2}f(x_{3}))\phi_{1}(f(x_{2})\phi_{1}f(x_{3}))​$

5. **同态映射的核**：定义为$ker f=\\{x\in X| f(x)=e,e\in Y \\}$,其中$e$为环$(Y,\phi_{1},\phi_{2} )$中加法群$(Y,\phi_{1})$的单位元（也称为零元）

6. **环的同构**，映射满足双射的两个同态环叫做同构

   







































