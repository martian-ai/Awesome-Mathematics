# 拉格朗日对偶
任何一个约束优化问题都存在一个对偶问题${\color{Red}(问题1：什么是对偶问题，对偶问题存在几种)}$与其对应，一般情况下原问题的最优值都大于或等于对偶问题的最优值（对偶性质）${\color{Red} (问题2：为什么对偶性质成立呢)}$,因此当原问题很难求解时，可以通过求解对偶问题得到原问题的近似解或者判定原问题是否有解（利用对偶性质可得）。

$e.g.$

令$f(x^{*})$是原问题的最优解，$f^{*}(\lambda^{*})$是对偶问题的最优解，他们满足对偶性质：

$f(x^{*})\ge f^{*}(\lambda^{*})$

其中$\Delta =f(x^{*})-f^{*}(\lambda^{*})$定义为对偶间隔，当$\Delta =0$为零时，说明原问题的最优解和对偶问题的最优解相同，这时我们称对偶是强对偶问题，这是我们希望得到${\color{Red} (问题3：在什么条件下强对偶成立)}$

**为了回答上述问题，我们先介绍原优化问题的拉格朗日对偶问题，至于原问题的其它对偶问题可以作为扩展另做介绍**

## 大纲
1、介绍该问题涉及到的一些基本概念以及前提假设
2、给出拉格朗日乘子存在性定理
3、给出拉格朗日对偶问题存在性的几何解释
4、给出强对偶成立的条件
## 1，基本概念
给定**凸优化**问题，称作**原问题**
$$ \begin{matrix} \underset{x\in \Re}{min} f(x) \\c_{i}(x)\le 0; \forall i \in I  \end{matrix}$$
给定原问题的**扰动问题**：
$$ \begin{matrix} \underset{x\in \Re}{min} f(x) \\c_{i}(x)\le z; \forall i \in I  \end{matrix}$$
其中$z$是扰动量
定义函数$w(z)=\underset {c(x)\le z}{inf} f(x)$
**易知扰动问题关于扰动变量**z**是单调不增的**
定义扰动的问题的上方集$L(\Gamma,Z)=\{(r,z)|inf(x)\le r,\forall x, st, c(x)\le z \}$
**易知扰动问题的上方集是凸集**

 


## 2、拉格朗日乘子的存在性
（拉格朗日乘子的存在性的证明中能够得到拉格朗日对偶的几何解释的原形）
#### 2.1 约束问题的拉格朗日函数

原问题：$$ \begin{matrix} \underset{x\in \Re}{min} f(x) \\c_{i}(x)\le 0; \forall i \in I  \end{matrix}$$
其拉格朗日函数为$f(x)+\sum \lambda c(x)$,其中$\lambda $称作**朗格朗日乘子**

#### 2.2 拉格朗日乘子的存在性
 **2.2.1拉格朗日乘子存在性问题：**
假设约束原问题存在最优解$p^{*}$,则是否存在$\lambda\ge 0 $使得 $p^{*}=\underset{x\in \Re}{min}(f(x)+\lambda c(x)$,该问题称为拉格朗日乘子存在性问题
**2.2.2 朗格朗日乘子存在性定理**
给定凸优化约束问题:$ \begin{matrix} \underset{x\in \Re}{min} f(x) \\c_{i}(x)\le 0; \forall i \in I  \end{matrix}$,如果该约束问题在$x^{*}$取得最优值$p^{*}$,且存在$x\in \Re,st. c(x)<0 $,则存在$\lambda\ge 0,st.p^{*}=\underset{x\in \Re}{min}(f(x)+\lambda c(x))$且$p^{*}=f(x^{*})+\lambda c(x^{*})$(也就是最优值在同一个点上得到)

**2.2.3 ${\color{red}拉个朗日乘子存在性定理的证明}$**

![拉格朗日对偶](C:\Users\hanmushuying\Desktop\拉格朗日对偶.jpg)



**f.1，构建可分离的凸集**

给定约束扰动问题$w(z)$的上方集$L_{1}(\Gamma,Z)$和集合$L_{2}(|\Gamma,Z)={(r,z)|r\le 0,z\le p^{*}}$如图1所示（红色代表$L_{1}$,绿色代表$L_{2}$),可以其定义易知，两个集合是只有交点$(0,p^{*}$)的凸集合
由凸集分离定理，存在过$(0,p^{*})$的超平面将集合$L_{1}$和集合$L_{2}\setminus (0,p^{*})$分离，即存在超平面$Hp(\lambda,\mu)$使得满足$ \forall (z_{1},r_{1})\in L_{1},(z_{2},r_{2})\in L_{2} ,\lambda z_{1}+\mu r_{1}\ge \lambda z_{2}+\mu r_{2}$

**f.2 构建分离超平面法向量**

由不等式$\lambda z_{1}+\mu r_{1}\ge \lambda z_{2}+\mu r_{2}$可知，当$z_{1}\rightarrow 0,z_{2}\rightarrow 0$,存在 $r_{1}\ge r_{2}$,可知$\mu \ge 0$

同时，当$r_{1}\rightarrow p^{*},r_{2}\rightarrow p^{*}$,存在$z_{2}\ge z_{1}$,可知$\lambda \ge 0$

由于$(0,p^{*})\in L_{2}$,$\lambda z_{1}+\mu r_{1}\ge \lambda z_{2}+\mu r_{2}$，可得$\lambda z_{1}+\mu r_{1}\ge \mu p^{*}$,当$\mu=0$,存在$\lambda>0$(超平面法向量不为零)使得$\lambda z_{1} \ge 0$,由于拉格朗日存在性定理条件"存在$x\in \Re, st.c(x)=z_{1}\le0$"，故$\lambda z_{1} < 0$这和$\lambda z_{1} \ge 0$是自相矛盾的，故$\mu>0$;

**f.3 利用凸集不等式证明乘子的存在性**

由于$\mu>0$，超平面的法向量可表示为$Hp(\lambda,1)$,故$\forall (z_{1},r_{1})\in L_{1},(z_{2},r_{2})\in L_{2},\lambda z_{1}+ r_{1}\ge \lambda z_{2}+ r_{2}$ 成立，由于$(0,p^{*})\in L_{2}，故有$$p^{*}\le \lambda z_{1}+ r_{1},\forall (z_{1},r_{1})\in L_{1} $.

由于$\forall x\in \Re, \exist z_{1}=c(x)$,由于$ f(x)\ge \underset{c(x^{’})=z_{1} }{min}(f(x^{‘}))$,故$\forall x\in \Re, (c(x),f(x))\in L_{1}$,故有$p^{*}\le \lambda c(x)+f(x),\forall x\in \Re\Rightarrow p^{*}\le \underset{x\in\Re}{inf}(f(x)+\lambda c(x))$,由于$\underset{x\in \Re}{inf}(f(x)+\lambda c(x))\le\underset{x\in\Re,c(x)\le 0}{inf}(f(x)+\lambda c(x))$,由于$\lambda \ge 0$,故$\underset{x\in\Re,c(x)\le 0}{inf}(f(x)+\lambda c(x))\le \underset{x\in\Re,c(x)\le 0}{inf}(f(x))=p^{*}$,故有$p^{*}\le \underset{x\in \Re}{inf}(f(x)+\lambda c(x))\le \underset{x\in \Re,c(x)\le 0}{inf}f(x)=p^{*}\Rightarrow  \underset{x\in \Re}{inf}(f(x)+\lambda c(x))=p^{*} $

#### 2.3 拉格朗日乘子的几何意义

由于$p^{*}\le\underset{x\in\Re,c(x)\le 0}{inf}(f(x)+\lambda c(x))$可知，$w(0)\le \underset{x\in \Re,c(x)\le 0}{inf}(f(x))+\lambda c(x)=w(z)+\lambda z$,即$w(z)-w(0)\ge -\lambda(z-0)$,即$-\lambda$是扰动问题$w(z)$在0处的次梯度，当$w(z)$关于$z$可微时，$-\lambda$即为$w(z)在0处的导数。


## 3、拉格朗日对偶
#### 3.1 拉格朗日对偶的几何解释
![拉格朗日对偶几何解释](C:\Users\hanmushuying\Desktop\拉格朗日对偶几何解释.jpg)

给定约束问题的扰动问题$w(z)$,如图2 中的红色曲线所示，原问题的最优值在为$w(0)$，因此该值可以通过扰动问题各支撑平面在$R$中的截距来逼近，即扰动问题所有支撑平面在$R$上的截距的最大值，作为$w(0)$的逼近，因此原问题可以转换为求扰动问题所有支撑超平面在$R$上的截距最大的优化问题

#### 3.2 拉格朗日对偶问题的代数表示

给定扰动问题$w(z)$上的一点$(z_{0},w(z_{0}))$,取$w(z)$在该点处的支撑超平面的法向量为$(\lambda_{0},1)$,则过该点的超平面为$\lambda z+r-(\lambda_{0} z_{0}+w(z_{0}))=0$,该超平面在$R$轴上的截距为$r=\lambda_{0} z_{0}+w{(z_{0})}$;由拉格朗日乘子的性质可知，$\lambda_{0}$为拉格朗日函数​ $\underset{x\in \Re}{inf}(f(x)+\lambda (c(x)-z_{0}))$的拉格朗日乘子，故有$r=\lambda_{0}z_{0}+\underset{x\in\Re}{inf}（f(x)+\lambda_{0} (c(x)-z_{0}）=\underset{x\in\Re}{inf}(f(x)+\lambda_{0} c(x)))$。由于所有的拉格朗日乘子满足$\lambda\ge 0$ ,故截距最大的值为$\underset {\lambda\ge 0}{max}(\underset{x\in \Re}{min}(f(x)+\lambda c(x))$

称函数$d(\lambda)=\underset{x\in\Re}{f(x)+\lambda c(x)}$为原始问题的对偶函数，可以肯定的是凸优化问题的对偶函数一定是凹函数，这可以通过凹函数的定义很好的证明。
称最优化问题$\underset{\lambda\ge 0}{d(\lambda)}$为原始优化问题的对偶问题。

#### 3.2 强对偶和弱对偶
如果原始问题的最优值和其对偶问题的最优值相同，则称该对偶是强对偶，否则称为弱对偶问题；
**满足拉格朗日乘子存在性的条件的凸优化问题一定是强对偶问题**

