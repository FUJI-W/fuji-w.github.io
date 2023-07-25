## 训练记录

| dataset     | #scene | #frame | split | light |      |
| ----------- | ------ | ------ | ----- | ----- | ---- |
| futurehouse |        |        |       |       |      |
|             |        |        |       |       |      |
|             |        |        |       |       |      |













## TODO

- [ ] 添加 SSIM 损失
- [ ] 添加 LPIPS 损失
- [ ] <font color="red">split 损失有问题，收敛的过慢，需要定位问题并解决</font>
- [x] <font color="red">加入随机的pose</font>
- [ ] <font color="red">加入模型存储，test代码，性能测试代码（参考 learn3d）</font>
- [x] Tensorboard 添加显示alpha（为了显示split）
- [ ] 录制各个loss的效果图（视频）
- [x] 物体插入渲染平台开发（支持光照估计算法切换）
- [ ] hypersim数据集中包含不同的cam，如cam_00, cam_01, ...，现在只用了 cam_00
- [ ] 添加各个loss的消融实验
- [ ] 下载大型数据集到2070上
- [x] <font color="red">处理数据集的遮挡问题</font>
- [ ] <font color="red">把深度信息添加进去</font>
- [ ] <font color="red">使用预训练模型</font>
- [ ] <font color="red">使用蒸馏</font>
- [ ] 把网络结构和训练代码抽离出来，做好训练的可视化等分割
- [ ] 数据集的整理，把任务的目标梳理好，即要实现哪些参数的提高
- [ ] 多batch训练
- [ ] ‼️主要：设计对比实验，完善训练框架
  - [ ] 寻找需要对比的论文，联系相关作者
- [ ] 八叉树结构预测：【任务一：初始数据 -> 预测体素块的数量】 -> 【网络预测哪些块被占用，在梯度下降之外，还对预测的结果用策略进行优化】
  - [ ] 难点：数据集的构建
  - [ ] 如何设计结构学习部分的loss
  - [x] 申请 structure3D 数据集
  - [x] 申请 Laval Indoor 数据集
- [ ] ‼️我们的这个渲染器是不是可以很方便的改成NeRF
  - [ ] 用NeRF进行监督
  - [ ] <font color="red">顺便做一下LSTD的优化实验</font>
- [ ] 在可微体渲染的部分，实验使用 cone tracing 是否有利于精度
- [x] 下载 futurehouse 数据集
- [x] **先把log和可视化加入，验证是否可以正常训练**
- [x] 切换成大网络进行训练
- [ ] 切换数据集的图像尺寸（注意 camera pose 也要变）
- [ ] 现在 camera pos 还有一些问题
- [x] **再把新数据集进行处理，验证是否可以正常训练**





## 训练记录

```
[2023-06-12 22:25:39,989 - INFO - [log dir] .log/hypersim/hypersim_e1000_b1_od6_ofd4_1686579939.9805655
[2023-06-12 22:25:39,989 - INFO - [log txt] .log/hypersim/hypersim_e1000_b1_od6_ofd4_1686579939.9805655/log.txt
[2023-06-12 22:25:39,989 - INFO - [see log] tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od6_ofd4_1686579939.9805655
```



```
2023-06-14 00:50:15,944 - INFO - [log dir]  .log/hypersim/hypersim_e1000_b1_od7_ofd4_1686675015.9256532
2023-06-14 00:50:15,944 - INFO - [log txt]  .log/hypersim/hypersim_e1000_b1_od7_ofd4_1686675015.9256532/log.txt
2023-06-14 00:50:15,944 - INFO - [log xlsx] .log/hypersim/hypersim_e1000_b1_od7_ofd4_1686675015.9256532/history.xlsx
2023-06-14 00:50:15,944 - INFO - [see log]  tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1686675015.9256532
```

![image-20230614010624712](https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202306140106442.png)

##### 全部loss打开

```
2023-06-14 02:36:37,818 - INFO - [log dir]  .log/hypersim/hypersim_e1000_b1_od7_ofd4_1686681397.798287
2023-06-14 02:36:37,819 - INFO - [log txt]  .log/hypersim/hypersim_e1000_b1_od7_ofd4_1686681397.798287/log.txt
023-06-14 02:36:37,819 - INFO - [log xlsx] .log/hypersim/hypersim_e1000_b1_od7_ofd4_1686681397.798287/history.xlsx
2023-06-14 02:36:37,819 - INFO - [see log]  tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1686681397.798287
```

![image-20230614111419070](https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202306141114802.png)

##### 只打开 split loss

```
2023-06-14 11:35:56,367 - INFO - [log dir]  .log/hypersim/hypersim_e1000_b1_od7_ofd4_1686713756.3502996
2023-06-14 11:35:56,367 - INFO - [log txt]  .log/hypersim/hypersim_e1000_b1_od7_ofd4_1686713756.3502996/log.txt
2023-06-14 11:35:56,367 - INFO - [log xlsx] .log/hypersim/hypersim_e1000_b1_od7_ofd4_1686713756.3502996/history.xlsx
2023-06-14 11:35:56,367 - INFO - [see log]  tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1686713756.3502996
```

![image-20230614121903389](https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202306141219149.png)



## 实验记录表

|     dataset     | scene | image number | split  loss | layer loss | direct loss | self-view render loss | envmap render loss | novel-view render loss |                            detail                            |                                                              |      |
| :-------------: | :---: | :----------: | :---------: | :--------: | :---------: | :-------------------: | :----------------: | :--------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :--: |
|  hypersim_full  |       |     1696     |      V      |            |             |                       |                    |                        | [link](#hypersim_full_e1000_b1_od7_ofd4_1686919884.7577667)  |                                                              |      |
|    hypersim     |   1   |      98      |      V      |            |             |                       |                    |                        |    [link](#hypersim_e500_b1_od7_ofd4_1686921604.0434132)     |                                                              |      |
|    hypersim     |   1   |      98      |      V      |            |             |                       |                    |                        |    [link](#hypersim_e1000_b1_od7_ofd4_1687109621.2392063)    |                                                              |      |
|  hypersim_full  |       |     1696     |             |            |      V      |           V           |         V          |           V            | [link](#hypersim_full_e1000_b1_od7_ofd4_1687110580.5316365)  |                                                              |      |
|        -        |   -   |      -       |      -      |            |      -      |           -           |         -          |           -            |                              -                               |                                                              |      |
| hypersim_ai_001 |   9   |     897      |             |            |      V      |                       |                    |                        | [link](#hypersim_ai_001_e1000_b1_od7_ofd4_1687315029.2943463) |                                                              |      |
| hypersim_ai_001 |   9   |     897      |             |            |      V      |           V           |                    |                        | [link](#hypersim_ai_001_e1000_b1_od7_ofd4_1687315685.347637) |                                                              |      |
| hypersim_ai_001 |   9   |     897      |             |            |      V      |           V           |         V          |                        | [link](#hypersim_ai_001_e1000_b1_od7_ofd4_1687315822.1028512) |                                                              |      |
| hypersim_ai_001 |   9   |     897      |             |            |      V      |           V           |         V          |           V            | [link](#hypersim_ai_001_e1000_b1_od7_ofd4_1687285455.679927) |                                                              |      |
| hypersim_ai_001 |   9   |     897      |             |            |             |           V           |                    |                        | [link](hypersim_ai_001_e1000_b1_od7_ofd4_1687316475.7076201) |                                                              |      |
| hypersim_ai_001 |   9   |     897      |             |            |             |           V           |         V          |                        | [link](#hypersim_ai_001_e1000_b1_od7_ofd4_1687316705.65941)  |                                                              |      |
| hypersim_ai_001 |   9   |     897      |             |            |             |           V           |         V          |           V            | [link](#hypersim_ai_001_e1000_b1_od7_ofd4_16x87285736.0663855) |                                                              |      |
|                 |       |              |             |            |             |                       |                    |                        |                                                              |                                                              |      |
|    hypersim     |   1   |      98      |      V      |            |             |                       |                    |                        | tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1687625133.561957 |                                                              |      |
|    hypersim     |   1   |      98      |      V      |     V      |             |                       |                    |                        | tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1687631624.1652296 |                         train_010001                         |      |
|                 |       |              |             |            |      V      |                       |                    |                        | tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1687643589.358909 |                                                              |      |
|                 |       |              |             |            |      V      |           V           |                    |                        | tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1687643649.9060779 |                                                              |      |
|                 |       |              |             |            |      V      |           V           |         V          |                        | tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1687644007.4592743 | tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1687659015.5108836 |      |
|                 |       |              |             |            |      V      |           V           |         V          |           V            | tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1687644118.6105828 | tensorboard --logdir=.log/hypersim/hypersim_e1000_b1_od7_ofd4_1687656827.6366544 |      |
|                 |       |              |             |            |             |                       |                    |                        |                                                              |                                                              |      |
|                 |       |              |             |            |             |                       |                    |                        |                                                              |                                                              |      |
|                 |       |              |             |            |             |                       |                    |                        |                                                              |                                                              |      |
|                 |       |              |             |            |             |                       |                    |                        |                                                              |                                                              |      |
|                 |       |              |             |            |             |                       |                    |                        |                                                              |                                                              |      |

#### hypersim_full_e1000_b1_od7_ofd4_1686919884.7577667

> 2023-06-16 20:51:24,779 - INFO - [log dir]  .log/hypersim_full/hypersim_full_e1000_b1_od7_ofd4_1686919884.7577667



#### hypersim_e500_b1_od7_ofd4_1686921604.0434132

> 2023-06-16 21:20:04,064 - INFO - [log dir]  .log/hypersim/hypersim_e500_b1_od7_ofd4_1686921604.0434132



#### hypersim_e1000_b1_od7_ofd4_1687109621.2392063

> 2023-06-19 01:33:41,365 - INFO - [log txt]  .log/hypersim/hypersim_e1000_b1_od7_ofd4_1687109621.2392063
>
> 加载了 hypersim_e500_b1_od7_ofd4_1686921604.0434132 的参数

![image-20230625014539865](https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202306250145162.png)

#### hypersim_full_e1000_b1_od7_ofd4_1687110580.5316365

> 2023-06-19 01:49:40,635 - INFO - [log dir]  .log/hypersim_full/hypersim_full_e1000_b1_od7_ofd4_1687110580.5316365



#### hypersim_ai_001_e1000_b1_od7_ofd4_1687285455.679927

> 2023-06-21 02:24:15,783 - INFO - [log dir]  .log/hypersim_ai_001/hypersim_ai_001_e1000_b1_od7_ofd4_1687285455.679927



#### hypersim_ai_001_e1000_b1_od7_ofd4_1687285736.0663855

> .log/hypersim_ai_001/hypersim_ai_001_e1000_b1_od7_ofd4_1687285736.0663855



#### hypersim_ai_001_e1000_b1_od7_ofd4_1687315029.2943463

> 2023-06-21 10:37:09,731 - INFO - [log dir]  .log/hypersim_ai_001/hypersim_ai_001_e1000_b1_od7_ofd4_1687315029.2943463



#### hypersim_ai_001_e1000_b1_od7_ofd4_1687315685.347637

> 2023-06-21 10:48:05,547 - INFO - [log dir]  .log/hypersim_ai_001/hypersim_ai_001_e1000_b1_od7_ofd4_1687315685.347637



#### hypersim_ai_001_e1000_b1_od7_ofd4_1687315822.1028512

> 2023-06-21 10:50:22,249 - INFO - [log dir]  .log/hypersim_ai_001/hypersim_ai_001_e1000_b1_od7_ofd4_1687315822.1028512



#### hypersim_ai_001_e1000_b1_od7_ofd4_1687316475.7076201

> 2023-06-21 11:01:15,884 - INFO - [log dir]  .log/hypersim_ai_001/hypersim_ai_001_e1000_b1_od7_ofd4_1687316475.7076201



#### hypersim_ai_001_e1000_b1_od7_ofd4_1687316705.65941

> 2023-06-21 11:05:05,839 - INFO - [log dir]  .log/hypersim_ai_001/hypersim_ai_001_e1000_b1_od7_ofd4_1687316705.65941

## 损失函数的选择

#### MAE V.S. MSE

> MSE loss可以有效地约束RGB值的范围，但是对边缘和纹理的保留效果并不理想。
>
> L1 loss能够有效保留边缘和纹理信息，但是在保证颜色一致性方面效果不如MSE loss。
>
> SSIM损失结合了MSE和L1 loss的优点，并且具有更好的视觉效果。SSIM考虑了亮度、对比度和结构等因素，因此在保留图像细节信息的同时能够保证整体色彩的一致性。

#### SSIM v.s LPIPS

- [ ] 
