# Outline of Distance

### Reference
+ https://blog.csdn.net/Kevin_cc98/article/details/73742037
### Outline
1. 欧氏距离
2. 曼哈顿距离
3. 切比雪夫距离
4. 闵可夫斯基距离
5. 标准化欧氏距离
6. 马氏距离
7. 夹角余弦
8. 汉明距离
9. 杰卡德距离& 杰卡德相似系数
10. 相关系数& 相关距离
11. 信息熵


### 马氏距离
+ 马氏距离(Mahalanobis distance)是由印度统计学家马哈拉诺比斯(P. C. Mahalanobis)提出的，表示数据的协方差距离。它是一种有效的计算两个未知样本集的相似度的方法。
+ 与欧氏距离不同的是，它考虑到各种特性之间的联系（例如：一条关于身高的信息会带来一条关于体重的信息，因为两者是有关联的），并且是尺度无关的(scale-invariant)，即独立于测量尺度
+ 对于一个均值为μ，协方差矩阵为Σ的多变量向量，其马氏距离为

![](http://upload.wikimedia.org/wikipedia/zh/math/3/3/3/3330a9a842f281df4a3a2be192ca007b.png)

![](http://upload.wikimedia.org/wikipedia/zh/math/6/8/f/68ffb7e029ac4f8c1152caf607e9d6d8.png)

+ 缺点:它将样品的不同属性（即各指标或各变量）之间的差别等同看待，这一点有时不能满足实际要求。例如，在教育研究中，经常遇到对人的分析和判别，个体的不同属性对于区分个体有着不同的重要性。因此，有时需要采用不同的距离函数