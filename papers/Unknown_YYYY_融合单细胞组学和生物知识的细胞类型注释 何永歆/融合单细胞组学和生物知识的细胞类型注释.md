# 融合单细胞组学和生物知识的细胞类型注释

> 何永歆 ·  · 

[打开 PDF](origin.pdf)

## 收获
1. 细胞类型注释的自校正方法——ScoRR
## 创新点
1. 细胞类型注释自校正
2. 细胞类型文本描述作为特征输入
## 研究问题
1. 针对细胞类型注释的标签不可信问题， 提出一种自校正方法
2. 针对细胞无法注释新细胞类型， 提出根据文本描述作为特征输入
## 背景
### 1. 细胞注释
1. 标记基因的数据库： 数据库中含有描述细胞类型特异性的标记基因
2. 常见的细胞类型注释方法
  1. scPred: 基于SVM, 主成分
  2. ACTINN： 神经网络
  3. OnClass: 基于细胞本理论的词汇分类
  4. GraphCS: 图神经网路， 将标注和未标注数据的细胞进行构图
  5. scAnnotatR: 层次化SVM
  6. scDeepInsight: 卷积神经网络
  7. scSwinFormer: 注意力机制
  8. scGraphformer: Transformer的图神经网络
3. 常用的评估指标： ACC, AUCPR, AUCROC
### 2. 细胞聚类
#### 2.1 基于相似性度量
Lovain， Leiden， SIMLR
#### 2.2 基于深度学习
1. scDeepCluster： 基于零膨胀二项分布去除数据dropout
3. scNAME： 预测被掩盖的基因的表达情况去噪声， 结合领域对比学习
4. graph-sc： 图神经网络
5. DeepScena： 自监督， 负二项分布的卷积自编码器
6. scDFC： 设计两个自编码器， 分别处理基因表达， 细胞间结构
7. scDCCA： 基于零膨胀二项分布， 对比学习
8. scLEGA： 图自编码器， 充分考虑低表达基因
9. scMAE: (重构误差)给基因表达数据添加噪音， 掩码， 重新构建基因表达信息
#### 2.3 细胞聚类的评估函数
##### 2.3.1 ARI
调整兰德指数: 
<p style="color:red">衡量聚类结果与金标签的一致性</p>
设真实划分为$U=\{U_1,U_2,\dots,U_r\}$
聚类划分为$V=\{V_1,V_2,\dots,V_s\}.$
令$n_{ij}=|U_i\cap V_j|$, 即真实第 \(i\) 类且聚类第 \(j\) 类的样本数。
$$
a_i=\sum_{j=1}^{s} n_{ij},
\qquad
b_j=\sum_{i=1}^{r} n_{ij},
\qquad
n=\sum_{i=1}^{r}a_i=\sum_{j=1}^{s}b_j.
$$

ARI 的列联表计算公式为

$$
\mathrm{ARI}
=
\frac{
\displaystyle
\sum_{i=1}^{r}\sum_{j=1}^{s}\binom{n_{ij}}{2}
-
\frac{
\left(\displaystyle\sum_{i=1}^{r}\binom{a_i}{2}\right)
\left(\displaystyle\sum_{j=1}^{s}\binom{b_j}{2}\right)
}{
\binom{n}{2}
}
}{
\displaystyle
\frac{1}{2}
\left[
\sum_{i=1}^{r}\binom{a_i}{2}
+
\sum_{j=1}^{s}\binom{b_j}{2}
\right]
-
\frac{
\left(\displaystyle\sum_{i=1}^{r}\binom{a_i}{2}\right)
\left(\displaystyle\sum_{j=1}^{s}\binom{b_j}{2}\right)
}{
\binom{n}{2}}}$$
其中$\binom{x}{2}=\frac{x(x-1)}{2}.$
```
ARI解读： 
	ARI = 1：两种划分完全一致；
	ARI = 0：一致性等于随机划分的期望水平；
	ARI < 0：比随机划分还差；
	理论上 ARI 最大为 1，最小值可低于 0，常见下界约为 -0.5，具体取决于簇结构。
```
##### 3.2 NMI： 归一化互信息
<p style="color:red">衡量金标签与预测标签的信息共享程度</p>
1. 互信息为$I(U;V)=\sum_{i=1}^{r}\sum_{j=1}^{s}\frac{n_{ij}}{n}\log\frac{n\,n_{ij}}{a_i b_j}.$
2. 两个划分的熵分别为
$$
H(U)
=
-\sum_{i=1}^{r}
\frac{a_i}{n}
\log\frac{a_i}{n},
\qquad
H(V)
=
-\sum_{j=1}^{s}
\frac{b_j}{n}
\log\frac{b_j}{n}.
$$
常见的 NMI 归一化方式包括

$$
\begin{align}
\mathrm{NMI}_{\mathrm{sqrt}}&=
\frac{I(U;V)}{\sqrt{H(U)H(V)}} \tag{3.2.1} \\
\mathrm{NMI}_{\mathrm{sum}}&=
\frac{2I(U;V)}{H(U)+H(V)} \tag{3.2.2} \\
\mathrm{NMI}_{\mathrm{max}}&=
\frac{I(U;V)}{\max\{H(U),H(V)\}} \tag{3.2.3} \\
\mathrm{NMI}_{\mathrm{min}}&=
\frac{I(U;V)}{\min\{H(U),H(V)\}} \tag{3.2.4}
\end{align}
$$

- NMI=1：两种划分完全一致；
- NMI=0：两种划分相互独立

## 方法
### 1. scCoRR
1. 可信锚点识别： 全局挑选策略和近邻净化策略筛选高可靠性锚点细胞， 作为训练集。其他数据认为存在注释错误可能性，作为数据集
2. 神经网络——监督对比学习
## 关键结论
## 待办

- [ ] 
