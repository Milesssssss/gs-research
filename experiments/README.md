# 实验编号

五条线各自回答一个问题。一次 run 只归一条线；需要交叉引用时，在 run 文件里链接到另一条线的文件，不把两套指标写进同一张结论表。

E1–E4 在本目录下还没有已完成的 run。E5 有一条 2026-11-04 的归档冒烟（PASS\*，有条件合格），见 [E5-real-to-sim](E5-real-to-sim/README.md)。本页不汇总成绩。

| 编号 | 目录 | 要回答的问题 |
| --- | --- | --- |
| E1 | [E1-semantic-3dgs](E1-semantic-3dgs/README.md) | 对象中心的语义高斯是否成立。方法参照 VLSplat。 |
| E2 | [E2-quality-speed](E2-quality-speed/README.md) | 渲染质量与速度（含显存、训练时间）的帕累托取舍。覆盖 3DGS 与 2DGS。 |
| E3 | [E3-gs-to-mesh](E3-gs-to-mesh/README.md) | 从高斯得到的网格能否进入仿真（尺度、闭合、碰撞）。 |
| E4 | [E4-online-semantic](E4-online-semantic/README.md) | 语义地图能否在线更新，而不是只做离线全量优化。 |
| E5 | [E5-real-to-sim](E5-real-to-sim/README.md) | Real-to-Sim 冒烟能否通过 DISCOVERSE、MuJoCo、GraspClutter6D 三道门禁（C1 / N1 / P1）。 |

## 边界

- **E1 与 E4**：E1 关心对象中心的语义表示是否把高斯收成物体；E4 关心这张地图能否边采集边更新。离线复现 VLSplat 记在 E1。
- **E2 与 E1 / E4**：只比较画质、速度、显存时记在 E2。语义指标仍记在 E1 或 E4，不把 PSNR 当作语义结论。
- **E3 与 E5**：E3 回答「网格能否仿真」。E5 回答「真实资产进仿真的冒烟是否通过」，门禁是 C1、N1、P1。网格质量的定量比较留在 E3；E5 不代替 E3 宣布网格合格。
- **2DGS**：质量与速度归 E2。若 2DGS 被用作语义或网格的输入，语义结论归 E1 / E4，网格结论归 E3，并在步骤里写明表示是 2DGS 还是 3DGS。

## 新增 run

过程见 [docs/process.md](../docs/process.md)。E1、E5 使用各自 `runs/_template.md`。E2、E3、E4 在补模板前，按该规范的同一组字段书写。
