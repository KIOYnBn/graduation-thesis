# Hierarchical progressive learning of cell identities in single-cell data

> Lieke Michielsen · nature communcations · 2021

[打开 PDF](origin.pdf)

## 收获
1. 双重拒绝与未知细胞识别机制
  1. . 两级过滤机制：
    1. 第一级（全局过滤）：PCA 重构误差.重构误差会超过阈值，直接被判定为未知细胞
    2. 第二级（局部过滤）：分类器判别
     1. Linear SVM（线性 SVM）：分类准确率极高。若在某细分节点无法确定，则回退并标注为中间节点
5. 渐进式学习
  1. 底层的分类器换成神经网络，利用深度学习中的知识蒸馏或弹性权重固化
## 创新点
分层渐进式学习方法，通过利用多个数据集中的不同分辨率的注释来学习和持续更新分类树，从而实现从单细胞数据中进行持续学习。
## 研究问题

## 背景

## 方法

## 关键结论

## 待办

- [ ] 
