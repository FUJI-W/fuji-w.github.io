```mermaid
graph TD
A[基于体素化表示的室内光照估计方法]--> | 优化宏观组织形式 - 稀疏体素八叉树 | B[基于神经自适应模型的室内光照估计方法]
A--> |优化微观单元表示 - 线性变换球面分布| C[基于线性变换球面分布的室内光照估计方法]
B--> |输出| G[基于稀疏混合体素化表示的虚实融合渲染方法]
C--> |输出| G
G--> |系统集成| H[基于体素化表示的室内场景混合现实展示系统]
```

```mermaid
graph LR
A[论文工作计划]-->B[论文研究背景]
A-->C[论文研究目标]
D[已完成的工作]-->E[主要研究内容]
D-->F[基于神经自适应模型的室内光照估计方法]
F-->F1[稀疏场景组织结构]
F-->F2[八叉树结点细分的分类模型]
F-->F3[八叉树结点值预测的回归模型]
F-->F4[基于体素化表示的可微渲染器]
F4-->F5[可微体渲染]
F4-->F6[可微重渲染]
D-->G[基于线性变换球面分布的室内光照估计方法]
G-->G1[PRT实验]
D-->H[基于稀疏混合体素化表示的虚实融合渲染方法与系统]
H-->H1[基于cone tracing的虚实融合渲染]
H-->H2[对照实验-基于差分渲染的方法实现]
```





#### lighthouse 网络权重

```
  | Name         | Type     | Params
------------------------------------------
0 | mpi_model    | MPINet   | 2.2 M 
1 | mcube0_model | MCubeNet | 2.2 M 
2 | mcube1_model | MCubeNet | 2.2 M 
3 | mcube2_model | MCubeNet | 2.2 M 
4 | mcube3_model | MCubeNet | 2.2 M 
5 | mcube4_model | MCubeNet | 2.2 M 
6 | vgg_lossfn   | VGGLoss  | 12.9 M
------------------------------------------
13.2 M    Trainable params
12.9 M    Non-trainable params
26.2 M    Total params
104.761   Total estimated model params size (MB)
```

