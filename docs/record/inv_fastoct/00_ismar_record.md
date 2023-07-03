## 投稿日期

> [Call for Conference Papers - ISMAR 2023 (ismar23.org)](https://ismar23.org/call-for-conference-papers/)；[AAAI-24 - AAAI](https://aaai.org/aaai-conference/)

| ![image-20230524212858501](https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202305251747762.png) | <img src="https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202305251748303.png" alt="image-20230525174857268" style="zoom: 67%;" /> |
| ------------------------------------------------------------ | ------------------------------------------------------------ |



## 标题

Real-time (Learn-based) <u>Adaptive</u> Lighting Estimation <u>for AR</u> via Differentiable Octree Cone Tracing

## 动机

#### 存在的问题

- 目前AR/MR领域中主要是 *基于二维表示的光照估计算法*，估计结果与真值在三维空间尺度上具有较大差异，在虚实融合渲染时也存在缺陷。
- 图像编辑（CV）领域中 *基于三维表示的光照估计算法*，无论是在二维图像尺度还是在三维空间尺度上，在精度上均有显著提升。
- 但三维空间操作相比二维图像操作，网络预测、逆渲染与虚实融合渲染等过程的存储和运算等开销显著增加，使得已有的基于三维表示的光照估计算法不能很好地在AR/MR领域得到应用。

#### 观察的现象

- 若使用均匀划分的三维结构表示光照，会引入大量的存储与计算，复杂度为 $O(n^3)$。

- 稀疏性：如果将场景中的表面视为次级光源，仅考虑场景中的直接光源与次级光源，其在三维尺度上是稀疏的，复杂度为 $O(n^2)$。

#### 提出的方法

- 引入八叉树作为场景与光照的压缩表示，提出了自适应的光照估计与虚实融合算法：

  - 基于八叉树的图卷积神经网络（Octree-based GCNN）
  - 基于八叉树的可微体素锥追踪渲染（Differentiable Octree/Voxel Cone Tracing）
- 基于八叉树的虚实融合绘制（）

## 思路

### 动机
在保证估计精度的前提下，引入稀疏体素八叉树结构以及相应的设计，同时提高网络学习与虚实融合渲染两个过程的效率，自适应地减少不必要的存储与计算开销。更好地支持增强现实等应用场景。

## 算法
### 基于SVO的网络

### 基于SVO的虚实融合渲染

## 实验