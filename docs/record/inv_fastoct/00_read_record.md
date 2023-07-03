| 论文                                                         | 项目                                                         | 会议      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- |
| Neural Fields meet Explicit Geometric Representations for Inverse Rendering of Urban Scenes | [project](https://research.nvidia.com/labs/toronto-ai/fegr/) | CVPR 2023 |
| Learning a Diffusion Prior for NeRFs                         |                                                              |           |
| TensoIR: Tensorial Inverse Rendering                         |                                                              |           |
| Generative Novel View Synthesis with 3D-Aware Diffusion Models |                                                              |           |
| NerfDiff: Single-image View Synthesis with NeRF-guided Distillation from 3D-aware Diffusion |                                                              |           |
|                                                              |                                                              |           |
|                                                              |                                                              |           |



- 梳理逻辑
  - 光照估计是什么样的任务？
    - 生成任务：外推
  - 引入八叉树：
    - 八叉树结构的优势/劣势
    - 对生成任务的影响，在生成任务中的作用？
    - 如何提高和改进？
- 工作进度（画张图）
  - 完成标签监督，多视角监督
  - 每个结点存储预测的法向量和材质
  - 用球谐函数存储每点的光照