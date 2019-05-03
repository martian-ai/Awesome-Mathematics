# Pointwise Mutual Information

### Reference

+ http://www.shuang0420.com/2017/03/21/NLP%20%E7%AC%94%E8%AE%B0%20-%20%E5%86%8D%E8%B0%88%E8%AF%8D%E5%90%91%E9%87%8F/

### Tools

+ nltk
+ sklearn



### Term-document matrix

+ 行 - term
+ 列 - document

### Term-Term matrix

+ 考虑更小的粒度，更小的上下文，也就是不用整篇文档，而是用段落(paragraph)，或者小的窗口(window of ±4±4 words)，所以这个时候，向量就是对上下文单词的计数，大小不再是文档长度 |D|，而是窗口长度 |V| 了，所以现在 word-word matrix 是 |V|*|V|

+ 关于窗口的大小，还有一个基本知识，如果窗口很小，比如说在 ± 1-3 之间，那么这个向量是更加基于语法(syntactic)的向量，而如果窗口更长一些，比如说在 ± 4-10 之间，那么向量是更加基于语义(semantic)的

+ 共现矩阵
  主要用于发现主题，解决词向量相近关系的表示； 
  将共现矩阵行(列)作为词向量

+ 例如：语料库如下： 
  • I like deep learning. 
  • I like NLP. 
  • I enjoy flying.

+ 则共现矩阵表示如下：（使用对称的窗函数（左右window length都为1) ）

  例如：“I like”出现在第1，2句话中，一共出现2次，所以=2。 
  对称的窗口指的是，“like I”也是2次

+ 将共现矩阵行(列)作为词向量表示后，可以知道like，enjoy都是在I附近且统计数目大约相等，他们意思相近

![](https://img-blog.csdn.net/2018052519154472?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhbzUzMzUxNTY=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

+ 共现矩阵不足： 
  面临稀疏性问题、向量维数随着词典大小线性增长

+ 解决：SVD、PCA降维，但是计算量大



###  PPMI

+ 先来看看两种词共现(co-occurrence)的类型。
  + First-order co-occurrence(syntagmatic association)
    通常是临近词，比如说，wrote 是 book 或者 poem 的 first-order associate
  + Second-order co-occurrence(paradigmatic association)
    通常有相似的临近词/上下文，比如说，wrote 是 said 或者 remarked 的 second-order associate

+ 原始的词频对单词间的联系可能不是一个很好的估计，因为它非常的 skewed，一些停顿词如 the, of 非常的常见，也就没有区分度，而我们想要的是看 context word 能不能对 target word 提供有用的信息，于是就有了 PPMI。

+ 先看下 PMI，看两个事件 x,y 同时出现的概率是不是比单独出现的概率高呢？

+ PMI 的范围是负无穷到正无穷，但是负值会带来各种各样的问题，所以我们通常会把负的 PMI 替换成 0，也就是有了 Positive PMI(PPMI)

### PMI 有 bias，rare words 会有很高的 PMI 值，有两个解决办法

- Give rare words slightly higher probabilites
- Add-one smoothing