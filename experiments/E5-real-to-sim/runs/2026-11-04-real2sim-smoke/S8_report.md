# E5 冒烟报告（S8）

日期：2026-11-04（Asia/Shanghai）

本轮冒烟完成。范围是 MuJoCo 几何-物理子集。

| 项 | 值 |
| --- | --- |
| 场景 ID | 000091（GraspClutter6D flat `scenes/000091`；请求过 `hard/000091`） |
| 栈 | DISCOVERSE 1.9.0 + MuJoCo 3.17.0；`MUJOCO_GL=egl` |
| GPU | **无** |
| A1 | **SKIP**（外观 / 3DGS） |
| G1 | **SKIP**（几何保真门禁；含 3DGS / GPU 重建） |
| 位姿 | **proxy_bin_layout**（无官方 scene_gt） |
| 数据 | 约 796MB：`split_info` + `models_obj_eval`。物体 `[1, 3, 6, 7, 8, 9]`。未下 `scenes.7z`（约 203GB） |
| C1 | **PASS 10/10** |
| N1 | **PASS**（终态穿透约 0.053mm；高度漂移约 0；过程最大穿透约 39mm，未纳入通过口径；无官方 GT） |
| P1 | **PASS 10/10**（mocap + 运动学附着；**非接触力**） |
| J1 | N/A |
| S6 | skip |
| S7 | skip（本轮未强制，未执行） |

## 限定

本轮通过的是一条可加载、可静置、可脚本搬运的代理场景，不是官方抓取场景的接触力复现。

- 位姿是 proxy 布局。`scenes.7z` 多分卷约 203GB，不能按路径只取 `scenes/000091` 的 scene_gt。
- P1 把物体运动学地粘到 mocap 夹爪上再松开。10 次记录的是同一条脚本轨迹。接触/摩擦夹爪没有调通。
- 网格是 `models_obj_eval` 的真实 mesh；`mesh2mjcf` 只记录了 `obj_000006` 一件 PASS。

## 若继续

1. 要官方布局：需要能按路径抽出 `scenes/000091` 的 scene_gt，或有足够磁盘解开分卷后只留该场景。
2. 要接触抓取 P1：需要另调夹爪接触与摩擦。本轮运动学协议不能代替那一项。
3. A1 / G1 / 3DGS 仍要 Linux + NVIDIA GPU。本机没有，本轮也不再等待。

## 日志

仓内摘要：[S0_env_fingerprint.md](S0_env_fingerprint.md)、[S1_result.md](S1_result.md)、[S2_S5_result.md](S2_S5_result.md)、[checklist.md](checklist.md)。

执行机全文未入库，只引用路径：

- `/workspace/real2sim-research/E5_S0_env_fingerprint_2026-11-04.md`
- `/workspace/real2sim-research/E5_S2_S5_smoke_2026-11-04.md`
- `/workspace/real2sim-research/E5_S8_smoke_report_2026-11-04.md`

本地产物目录（未入库）：`E5_mjcf/`、`E5_artifacts/`、`scripts/build_and_run_e5_gates.py`。
