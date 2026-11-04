# E5 S2–S5 结果

记录时间：2026-11-04 11:23:56 CST（Asia/Shanghai）

执行机：Grok Bot box（实验员-E5仿真）

**GPU = 无**。A1 = SKIP。G1 = SKIP。本轮是 MuJoCo 几何-物理子集，不是官方 scene_gt，也不是接触力抓取。

## 场景与数据

| 项 | 值 |
| --- | --- |
| 场景 | **000091**。请求的是 `hard/000091`；GraspClutter6D 实际是 flat `scenes/000091`，没有 `hard/` 前缀 |
| 位姿 | **proxy_bin_layout**。官方 scene_gt 在 `scenes.7z` 多分卷（约 203GB）里，本机无法按路径只抽该场景 |
| 已下载 | `split_info.7z` + `models_obj_eval.7z`。占用约 **796MB**（`/workspace/data/GraspClutter6D`） |
| 未下载 | `scenes.7z.001–005` |
| 冒烟物体 | `[1, 3, 6, 7, 8, 9]`。全场景 20 个物体见本地 `meta.json`，本轮没有用全场景 |
| 网格 | 真实 `models_obj_eval` mesh，不是程序化方块代替物体外形 |

## S3

场景 MJCF 在执行机本地：`/workspace/real2sim-research/E5_mjcf/gc6d_000091_proxy_bin.xml`。

- L1 构建墙钟：0.084s。
- `mesh2mjcf`（`DISCOVERSE/scripts/mesh2mjcf.py`）对 `obj_000006`：**PASS**，return code 0，墙钟 0.062s。日志只记录了这一件的转换，不把单件转换写成全场景重建。
- 没有走多视前景分割，也没有 3DGS / 外观路径。

## 门禁

### C1 PASS 10/10

加载成功 10/10，errors 为空，墙钟 0.411s。

### N1 PASS

静置 12.0s（原计划 5–10s，实际 12s）。判定按实验记录的口径，不是「全程穿透为零」：

- 终态窗口穿透 `pen_final_m` = 5.30e-5 m（约 0.053mm），阈值 0.003m，终态通过。
- 过程最大穿透 `pen_max_during_m` = 0.03916m（约 39mm），高于 3mm 阈值。PASS 只用了终态窗口。
- 1s 高度漂移 `max_height_drift_m` ≈ 0（2.6e-14 m），阈值 0.02m。
- 底面误差最大 5.44e-5 m。
- 无官方 GT。

### P1 PASS 10/10

阈值 ≥ 8/10。成功 10/10，墙钟 5.35s。目标物体 `obj_000006`。

协议：**mocap 夹爪 + 运动学 freejoint 附着/释放（脚本）**。这不是接触力闭环夹爪，接触抓取没有在本机调通。

成功判据：抬升 ≥ 4cm，且放置后 XY 距目标 < 6cm、z < 0.15m。记录中 10 次的抬升与落点数值相同（`obj_z0` ≈ 0.0293m，`obj_z_lift` ≈ 0.158m，落点 z ≈ 0.0298m）。10/10 说明这条脚本搬运链路可重复，不能读成 10 次独立接触抓取。

本地只有成功帧 `P1_success.png`。因为 10 次都成功，没有失败帧。短视频不在本次产物里。

## 限定

1. **proxy 布局**：物体网格来自 `models_obj_eval`，位姿不是官方 `scene_gt`。
2. **运动学 P1**：验证的是加载、静置、脚本附着搬运，不是摩擦/接触抓取。
3. GPU = 无，A1/G1 保持 SKIP。

## 本地路径

下列全文未推送到本仓，只作引用：

- `/workspace/real2sim-research/E5_S2_S5_smoke_2026-11-04.md`
- `/workspace/real2sim-research/E5_mjcf/gc6d_000091_proxy_bin.xml`
- `/workspace/real2sim-research/E5_mjcf/layout.json`
- `/workspace/real2sim-research/E5_mjcf/gates_result.json`
- `/workspace/real2sim-research/E5_artifacts/`
- `/workspace/real2sim-research/scripts/build_and_run_e5_gates.py`
