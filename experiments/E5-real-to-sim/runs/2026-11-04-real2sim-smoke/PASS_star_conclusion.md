# E5 Real-to-Sim 冒烟 · 归档结论（PASS\*）

日志仓归档：`experiments/E5-real-to-sim/runs/2026-11-04-real2sim-smoke/PASS_star_conclusion.md`

- 日期：2026-11-04（Asia/Shanghai）
- 执行：实验员-E5仿真
- 评估：主研究员 → Real到Sim 归档为 **PASS\***（有条件合格）
- 任务页：https://cursor.com/canvas/store-eb11796c-54ba-44fb-bb2f-0396f82f2c6b/aba3665d-b93c-4f8d-8b0d-030b76a9cbab

## 结论

**PASS\*** — C1 / N1 / P1 数值均达标；降级项为 proxy 布局与运动学 P1，不记作完整官方接触抓取闭环。

降级 = **proxy_bin** + **运动学 P1**。

## 场景 / 栈 / GPU

| 项 | 值 |
| --- | --- |
| 场景 ID | `000091`（GraspClutter6D flat `scenes/000091`；请求名 hard/000091，仓库无 hard/ 前缀） |
| 位姿 | **proxy_bin_layout**（无官方 `scene_gt`） |
| 数据 | ≈796MB：`split_info` + `models_obj_eval`；冒烟物体 `[1, 3, 6, 7, 8, 9]` |
| 栈 | DISCOVERSE **1.9.0** + MuJoCo **3.17.0**（仅核心；`MUJOCO_GL=egl`） |
| 执行机 | Debian 13 box · 8 核 · 15Gi RAM |
| GPU / CUDA | **无** |

## 门禁表

| 门禁 | 结果 | 说明 |
| --- | --- | --- |
| C1 导出/加载 | **PASS** | 10/10 可加载 |
| N1 可碰撞 | **PASS** | 终态穿透 ≈0.05mm；高度漂移 ≈0（过程最大穿透曾 ≈39mm，按终态窗口判定） |
| P1 操作冒烟 | **PASS\*** | **10/10**；协议 = mocap 夹爪 + **运动学 freejoint 附着/释放**（非接触力闭环） |
| A1 外观 | **SKIP** | 用户拍板；无 GPU |
| G1 几何保真 | **SKIP** | 用户拍板；无官方 GT / 无 GPU 重建 |
| J1 关节 | **N/A** | 单 bin 无关节 |

## 降级与阻塞

1. **proxy_bin_layout**：官方 `scenes.7z` 多分卷 ≈203GB，无法按路径只抽 `scenes/000091` 的 `scene_gt`；本轮用真实 mesh + proxy 布局。
2. **P1 运动学附着**：验证加载 → 静置 → 脚本搬运链路；**不是**接触力/摩擦调通的夹爪抓取。
3. **无 NVIDIA GPU**：3DGS / 外观路径本轮不做（A1/G1 SKIP）。
4. 未下 GraspClutter6D 全量（禁止 / 盘不够）。

## 下一轮清单

下一轮才做，本轮不执行：

1. 补 **官方 scene_gt**（可路径抽取单 bin，或更大磁盘解压对应分卷后只取 `000091`）。
2. 将 P1 升级为 **接触力抓取**（接触/摩擦可复现；保存成功/失败短视频）。
3. 有 GPU 后再评估是否重开 A1/G1（非本轮阻塞关闭条件）。

## 产物路径与 PR

执行机路径只作引用。除本归档结论外，那些全文与产物没有推送到本仓。

| 类型 | 路径 |
| --- | --- |
| 本结论（日志仓） | `experiments/E5-real-to-sim/runs/2026-11-04-real2sim-smoke/PASS_star_conclusion.md` |
| 本结论（执行机原文） | `/workspace/real2sim-research/E5_PASS_star_conclusion_2026-11-04.md` |
| S8 报告 | `/workspace/real2sim-research/E5_S8_smoke_report_2026-11-04.md` |
| S2–S5 日志 | `/workspace/real2sim-research/E5_S2_S5_smoke_2026-11-04.md` |
| S0/S1 指纹 | `/workspace/real2sim-research/E5_S0_env_fingerprint_2026-11-04.md` |
| MJCF | `/workspace/real2sim-research/E5_mjcf/gc6d_000091_proxy_bin.xml` |
| 门禁 JSON | `/workspace/real2sim-research/E5_mjcf/gates_result.json` |
| 脚本 | `/workspace/real2sim-research/scripts/build_and_run_e5_gates.py` |
| 帧 | `/workspace/real2sim-research/E5_artifacts/N1_settle_top.png`、`P1_success.png` |
| 日志仓 PR | https://github.com/Milesssssss/gs-research/pull/1 |

本轮 **不再扩 scope**（不下 scenes 全量、不自行开接触抓取大改），待下一轮派工。
