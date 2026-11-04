# E5 Real-to-Sim 冒烟

检查一条真实资产（或约定好的公开样例）能否走通仿真入口。这是冒烟，不是抓取成功率评测，也不是网格质量评测。网格本身归 [E3](../E3-gs-to-mesh/README.md)。

## 当前状态

尚无 run，无结论。门禁表里没有预置阈值，也没有预填的通过记录。

## 门禁 C1 / N1 / P1

这三道是本日志的检查项编号，用来把同一次冒烟对齐到三条外部依赖。公开文献没有发布同名的数值标准。每次 run 把通过条件写进自己的「假设」，跑完再填结果；没跑的格子写「未跑」。

| ID | 对齐 | 这次冒烟要回答的问题 |
| --- | --- | --- |
| C1 | [DISCOVERSE](https://github.com/discoverse-dev/DISCOVERSE) 与 [DISCOVERSE-Real2Sim](https://github.com/discoverse-dev/DISCOVERSE-Real2Sim)（论文 [arXiv:2507.21981](https://arxiv.org/abs/2507.21981)） | 资产能否作为 DISCOVERSE 的场景节点载入。该管线接受 3DGS（`.ply`）、网格（`.obj` / `.stl`）和 MJCF（`.xml`）。只记录加载，以及一帧画面或等价加载日志是否产出。 |
| N1 | [MuJoCo](https://mujoco.org/) | 对应物理模型能否步进，且状态保持有限：无 NaN、无 Inf、无立即发散。步数和判据写在当次假设里。 |
| P1 | [GraspClutter6D](https://arxiv.org/abs/2504.06866) | 约定的一条 GraspClutter6D 场景（位姿或抓取标注）能否接到上述入口，使读取或评估脚本启动并写出日志。本说明不预填抓取成功率。 |

三道都按当次假设通过，Go/No-Go 才可以写 `Go`。有一道未跑或失败，写 `No-Go` 或 `未判定`，并在失败模式里指出卡在哪一道。

依赖版本（DISCOVERSE commit、MuJoCo 版本、GraspClutter6D 划分与相机）写在该次 run 的步骤和 git commit 栏，不写在本文件里充当作固定环境。

## 一次 run 记什么

复制 [runs/_template.md](runs/_template.md)。除通用字段外，门禁表的每一行都要有结果和证据路径。证据是日志或小图，不是数据集本身。
