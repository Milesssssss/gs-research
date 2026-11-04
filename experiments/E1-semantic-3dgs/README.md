# E1 对象中心语义高斯（VLSplat）

考察对象中心的语义高斯：高斯上的语义是否对应物体，而不是只贴着局部二维掩码走。方法参照 [VLSplat](https://vlsplat.github.io/)（Vision-Language Guided Object-Centric 3D Gaussian Splatting via Scene Graph，[arXiv:2611.01939](https://arxiv.org/abs/2611.01939)）。

VLSplat 的公开做法是：用物体级码本把二维掩码抬到高斯上，再把码本组当成场景图节点，用视觉语言模型的描述做组内去噪和组间补全。本目录记录的是**我们自己的 run**（复现、改动或替换某一模块）。论文里的表格不是本仓库的结果，不要抄进 run 的「数值」列；若用作对照，写在「对照」或「备注」，并标明出处。

## 当前状态

尚无 run，无结论。

## 一次 run 记什么

复制 [runs/_template.md](runs/_template.md)。建议放入指标表的量（有则填，没有则留空）：

- 渲染视角的物体类（thing）与背景类（stuff）：mAcc、mIoU
- 若做了三维点上的评测：mIoU、mAcc，以及实际使用的点云协议
- 场景图或码本规模、是否启用组内 / 组间修正

场景、划分和实现 commit 每次单独写。不要用「与论文一致」代替这些字段。

## 不归本线

- 只报 PSNR、FPS、显存：记到 [E2](../E2-quality-speed/README.md)
- 在线增量建图：记到 [E4](../E4-online-semantic/README.md)
- 网格能否进仿真器：记到 [E3](../E3-gs-to-mesh/README.md)
