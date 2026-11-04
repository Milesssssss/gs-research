# E5 Real-to-Sim 冒烟

结论：**PASS\***（有条件合格）。主研究员评估，Real到Sim 归档。本轮 closed。as of 2026-11-04 Asia/Shanghai。

降级 = **proxy_bin** + **运动学 P1**。C1 / N1 / P1 数值达标；这不是完整官方接触抓取闭环。A1 = SKIP，G1 = SKIP，GPU = 无。

归档：[PASS_star_conclusion.md](PASS_star_conclusion.md)。本轮不再扩 scope。

任务页：<https://cursor.com/canvas/store-eb11796c-54ba-44fb-bb2f-0396f82f2c6b/aba3665d-b93c-4f8d-8b0d-030b76a9cbab>

## 本轮锁定

用户已拍板，本轮**只接受 MuJoCo 几何-物理子集**。

- **A1 = SKIP**（外观保真，含 3DGS / 外观）。
- **G1 = SKIP**（几何保真门禁；含 3DGS / 外观 / GPU 重建）。
- **勿再等待 GPU。** 执行机无 NVIDIA、无 CUDA 是已核实事实，不构成继续等待的理由，也不把 3DGS / 外观路径留作本轮阻塞项。
- 必过门禁仍是 **C1 / N1 / P1**。**J1 = N/A**（单 bin 无关节）。

完整 3DGS、外观对比与 GPU 重建不在本轮范围。若以后另开 GPU 轮次，另写指纹与清单，不回改本目录里「GPU = 无」的记录。

## 任务摘要

在仿真内走通一条 Real-to-Sim 冒烟：公开单 bin 场景导入 MuJoCo，加载、静置、脚本抓取放置，用 pass/fail 门禁收口。

- 主栈：DISCOVERSE + MuJoCo + GraspClutter6D 单 bin（优先 `hard/000091`，若可定位）。
- 主路径：DISCOVERSE（含 Real2Sim 工具）→ MuJoCo。不依赖 SceneAgent 闭源 skills，不强制 Isaac。
- 对照口径：对齐 SceneAgent 的 F1@1cm 与脚本抓取成功率；其中 F1@1cm 属于 G1，本轮 SKIP。
- 闭环：仅仿真内，观测 → 脚本策略 → 物理 → 成功判据。
- 本轮不做：真机、Isaac Lab、VLA 全量微调、4D 流体、digital sisters 规模扩增，以及任何 3DGS / 外观 / GPU 重建。
- 数据：只下 GraspClutter6D 单 bin 及对应 YCB/models mesh，禁止下全量（约 220GB）。

## 门禁

| 门禁 | 本轮 | PASS | FAIL 处置 |
| --- | --- | --- | --- |
| C1 导出完整 | 必过 | MJCF/场景加载成功率 100% | 修资产/碰撞导出后重测 |
| N1 可碰撞 | 必过 | 静置 5–10s；穿透率 = 0；高度误差 < 2cm | 修碰撞体/质量；禁止带飞出资产进 P1 |
| P1 物理冒烟 | 必过 | 脚本 pick-and-place ×10，≥ 8/10 | 记失败模式；最多调参 1 轮再重测 |
| J1 关节 | N/A | 单 bin 无关节，记 N/A | — |
| G1 几何保真 | SKIP | 用户拍板跳过（含 3DGS / GPU 重建） | 本轮不测，勿等 GPU |
| A1 外观保真 | SKIP | 用户拍板跳过（含 3DGS / 外观） | 本轮不测，勿等 GPU |

上表是开跑前的门禁定义。实际 N1 按终态窗口判过，过程最大穿透约 39mm；实际 P1 是运动学附着，不是接触力。实测见下方「本轮结果」。

任务页里的传感器闭环门禁（亦编号 S1）与 T1 吞吐属后续周次，与本目录阶段 S1（官方空场景 demo，已 PASS）不是同一项。L1 耗时全程记录：捕获到首条成功 demo 的人机时目标 ≤ 8h，超时写阻塞原因。

## 派工

- 用户终审通过。
- Real到Sim 派给实验员-E5仿真。
- 接受研究员与 Real到Sim 审核。

## 本轮结果

场景 **000091**（GraspClutter6D 为 flat `scenes/000091`，没有 `hard/` 前缀）。官方 `scenes.7z` 多分卷约 203GB，无法按路径抽出 scene_gt，因此位姿用 **proxy_bin_layout**，网格用已下载的 `models_obj_eval`。数据约 **796MB**（`split_info` + `models_obj_eval`），冒烟物体 `[1, 3, 6, 7, 8, 9]`。

| 门禁 | 结果 | 限定 |
| --- | --- | --- |
| C1 | PASS 10/10 | MJCF 可重复加载 |
| N1 | PASS | 按终态窗口判穿透；静置 12s；无官方 GT |
| P1 | PASS 10/10 | mocap + 运动学 freejoint 附着/释放，非接触力 |
| J1 | N/A | 单 bin 无关节 |
| G1 | SKIP | 含 3DGS / GPU 重建 |
| A1 | SKIP | 含 3DGS / 外观 |

## 日志

- 归档结论：[PASS_star_conclusion.md](PASS_star_conclusion.md)（PASS\*）
- 环境指纹：[S0_env_fingerprint.md](S0_env_fingerprint.md)
- S1 结果：[S1_result.md](S1_result.md)（空场景 2500 step PASS；GPU = 无）
- S2–S5 结果：[S2_S5_result.md](S2_S5_result.md)
- S8 报告：[S8_report.md](S8_report.md)
- 阶段清单：[checklist.md](checklist.md)
- 执行机本地详细日志只引用路径，全文未推送到本仓：
  - `/workspace/real2sim-research/E5_S0_env_fingerprint_2026-11-04.md`
  - `/workspace/real2sim-research/E5_S2_S5_smoke_2026-11-04.md`
  - `/workspace/real2sim-research/E5_S8_smoke_report_2026-11-04.md`
