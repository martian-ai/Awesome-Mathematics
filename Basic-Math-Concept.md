# 基本数学概念

### 1， 高斯函数

一维高斯函数是最为熟知的高斯函数形式，其形式如下：
$$
\frac{1}{\sqrt{2\pi } \sigma }e^{-\frac{\left ( x-\mu  \right )^{2}}{2\sigma^{2} }}
$$
其中$\sigma​$是方差，$\mu​$是均值，其中$\frac{1}{\sqrt{2\pi } \sigma }​$是归一化量，目的是使$\int_{-\infty}^{+\infty}\frac{1}{\sqrt{2\pi } \sigma }e^{-\frac{\left ( x-\mu  \right )^{2}}{2\sigma^{2} }}=1​$

多维高斯函数的形式如下：
$$
\frac{1}{\left(2\pi\right)^{\frac{n}{2}}\left|\sum\right|^{\frac{1}{2}}}e^{-\frac{\left(x-\mu\right)^{T}\sum^{-}\left(x-\mu\right)}{2}}
$$


其中$\mu​$是$n​$维向量，$\sum​$是变量的协方差矩阵要求是对称的和正定的，$\left|\sum\right|​$是矩阵$\sum​$的行列式，其中$\frac{1}{\left(2\pi\right)^{\frac{n}{2}}\left|\sum\right|^{\frac{1}{2}}}​$是多维高斯函数的对应的归一化量，目的使得$\int_{-\infty}^{+\infty}\frac{1}{\left(2\pi\right)^{\frac{n}{2}}\left|\sum\right|^{\frac{1}{2}}}e^{-\frac{\left(x-\mu\right)^{T}\sum^{-}\left(x-\mu\right)}{2}}=1​$,接下来推导如何将高斯函数的多维形式和一维形式统一在一起

由于$\left|\sum\right|​$是正定的，存在正交矩阵$A​$使得$A^{T}\sum A=\lambda​$

其中$\lambda​$是矩阵$\left|\sum\right|​$特征值构成的对角矩阵，则$A^{T}\sum^{-} A=\lambda^{-}​$，进而$\int_{-\infty}^{+\infty}e^{-\frac{\left(x-\mu\right)^{T}\sum^{-}\left(x-\mu\right)}{2}}dx=\int_{-\infty}^{+\infty}e^{-\frac{\left(x-\mu\right)^{T}A^{T}\lambda^{-} A\left(x-\mu\right)}{2}}dx​$

令$y=A\left(x-\mu\right)​$,则

$\int_{-\infty}^{+\infty}e^{-\frac{\left(x-\mu\right)^{T}A^{T}\lambda^{-} A\left(x-\mu\right)}{2}}dx=\int_{-\infty}^{+\infty}e^{-\frac{y^{T}\lambda^{-}y}{2}}dx​$

由于$dy=\left|A\right|dx$

则$\int_{-\infty}^{+\infty}e^{-\frac{y^{T}\lambda^{-}y}{2}}dx=\int_{-\infty}^{+\infty}e^{-\frac{y^{T}\lambda^{-}y}{2}}\left|A\right|dy=\left|A\right|\int_{-\infty}^{+\infty}e^{\sum_{1}^{n}\frac{-y_{i}^{2}}{2\lambda _{i}}}dy=\left|A\right|\prod_{i=1}^{n}\int_{-\infty}^{+\infty}e^{-\frac{y_{i}^{2}}{2\lambda_{i}}}dy_{i}​$

其中$\left|A\right|\prod_{i=1}^{n}\int_{-\infty}^{+\infty}e^{-\frac{y_{i}^{2}}{2\lambda_{i}}}dy_{i}=\left(2\pi\right)^{\frac{n}{2}}\left|A\right|^{\frac{1}{2}}$，故$\int_{-\infty}^{+\infty}\frac{1}{\left(2\pi\right)^{\frac{n}{2}}\left|\sum\right|^{\frac{1}{2}}}e^{-\frac{\left(x-\mu\right)^{T}\sum^{-}\left(x-\mu\right)}{2}}=1$

从上面的推导可以看出，协方差矩阵决定了高斯分布的形状，关于高斯函数时域和频域的特性可查看链接

[1]: https://en.wikipedia.org/wiki/Gaussian_function

