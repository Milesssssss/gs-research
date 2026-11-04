# E5 Real-to-Sim 冒烟清单

as of 2026-11-04（Asia/Shanghai）

状态取值：`pending`、`in_progress`、`done`、`skip`、`blocked`。

## 归档

本轮 **closed as PASS\***（有条件合格）。降级 = proxy_bin + 运动学 P1。见 [PASS_star_conclusion.md](PASS_star_conclusion.md)。不再扩 scope。

## 本轮锁定

- 只做 **MuJoCo 几何-物理子集**。
- **A1 = SKIP**，**G1 = SKIP**（含 3DGS / 外观 / GPU 重建）。S6 因此为 `skip`，不是待补项。
- **勿再等待 GPU。** 无 NVIDIA 不阻塞 S0–S5 与 S8。
- 必过：C1、N1、P1，本轮均为 PASS。J1 = N/A。
- 位姿为 proxy 布局；P1 为运动学附着，不是接触力抓取。

## 阶段

| 阶段 | 状态 | 内容 | 完成判据 |
| --- | --- | --- | --- |
| S0 | `done` | 环境指纹（见 [S0_env_fingerprint.md](S0_env_fingerprint.md)）；DISCOVERSE 安装到可跑 MuJoCo 子集 | 指纹已落盘。GPU 保持无。不等待 GPU |
| S1 | `done` / PASS | 官方最小 MuJoCo demo：空场景 2500 step。discoverse 1.9.0 + mujoco 3.17.0；`MUJOCO_GL=egl`。见 [S1_result.md](S1_result.md) | PASS。A1 = SKIP，G1 = SKIP，GPU = 无 |
| S2 | `done` | 场景 000091。约 796MB：`split_info` + `models_obj_eval`；物体 `[1, 3, 6, 7, 8, 9]`。未下 `scenes.7z` | 子集到位。官方 scene_gt 未抽取，改用 proxy 布局 |
| S3 | `done` | proxy bin MJCF + `models_obj_eval` mesh。`mesh2mjcf` 记录了 `obj_000006` PASS。不含 3DGS / 外观，也不是官方 scene_gt 重建 | L1 构建约 0.084s。见 [S2_S5_result.md](S2_S5_result.md) |
| S4 | `done` / PASS | 加载 + 静置。C1 10/10；N1 按终态窗口 PASS（静置 12s） | C1、N1 均 PASS 后才进入 S5 |
| S5 | `done` / PASS | 脚本搬运 ×10，目标 `obj_000006` | P1 10/10。协议是 mocap + 运动学附着，非接触力 |
| S6 | `skip` | G1 几何保真 / A1 外观保真（含 3DGS / 外观 / GPU 重建） | 本轮锁定 SKIP。勿再等待 GPU，不测 F1@1cm 与外观对比 |
| S7 | `skip` | sceneagent.dev 公开 splat 试传 | 本轮未强制，也未执行。不阻塞收口，不为它等待 GPU |
| S8 | `done` | 一页冒烟报告：[S8_report.md](S8_report.md) | 已写明 C1/N1/P1 PASS、A1/G1 SKIP、GPU = 无，以及 proxy / 运动学限定 |

## 门禁对照

| 门禁 | 本轮 | 挂在 |
| --- | --- | --- |
| C1 导出完整 | PASS 10/10 | S4 |
| N1 可碰撞 | PASS（终态窗口） | S4 |
| P1 物理冒烟 | PASS 10/10（运动学附着） | S5 |
| J1 关节 | N/A | 单 bin 无关节 |
| G1 几何保真 | SKIP | S6 |
| A1 外观保真 | SKIP | S6 |
