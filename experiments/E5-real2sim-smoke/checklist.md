# E5 Real-to-Sim 冒烟清单

as of 2026-11-04（Asia/Shanghai）

状态取值：`pending`、`in_progress`、`done`、`skip`、`blocked`。

## 本轮锁定

- 只做 **MuJoCo 几何-物理子集**。
- **A1 = SKIP**，**G1 = SKIP**（含 3DGS / 外观 / GPU 重建）。S6 因此为 `skip`，不是待补项。
- **勿再等待 GPU。** 无 NVIDIA 不阻塞 S0–S5 与 S8。
- 必过：C1、N1、P1。J1 = N/A。

## 阶段

| 阶段 | 状态 | 内容 | 完成判据 |
| --- | --- | --- | --- |
| S0 | `in_progress` | 环境指纹（见 [S0_env_fingerprint.md](S0_env_fingerprint.md)）；按 README 安装 DISCOVERSE，目标 Python 3.11/3.12 venv，只准备 MuJoCo 子集 | 指纹已落盘；安装日志可复述。不等待 GPU |
| S1 | `pending` | DISCOVERSE 自带最小 MuJoCo demo（空场景或官方样例） | 绿灯。不过则停，回报安装日志 |
| S2 | `pending` | GraspClutter6D 单 bin（优先 `hard/000091`）+ 对应 YCB mesh | 仅子集。禁止下全量 ~220GB |
| S3 | `pending` | DISCOVERSE-Real2Sim：多视/规定输入 → 前景分割 → mesh/碰撞 → MJCF。不含 3DGS / 外观 | 记录 L1 分段耗时。不进入 GPU 重建 |
| S4 | `pending` | 加载场景；静置 5–10s；填穿透与沉降 | C1 与 N1 均 PASS。任一项 FAIL 不得进入 S5 |
| S5 | `pending` | 脚本接近-抓取-放置 ×10；成功/失败各至少 1 段短视频 | P1：≥ 8/10 为 PASS |
| S6 | `skip` | G1 几何保真 / A1 外观保真（含 3DGS / 外观 / GPU 重建） | 本轮锁定 SKIP。勿再等待 GPU，不测 F1@1cm 与外观对比 |
| S7 | `pending` | sceneagent.dev：仅上传公开 splat，无私有数据 | 记录能否导出/可交互。失败不阻塞主路径，也不为它等待 GPU |
| S8 | `pending` | 一页冒烟报告：场景 ID、栈、各门禁 PASS/FAIL/SKIP/N/A、日志与视频路径、阻塞项 | 交回 Real到Sim / 研究员 |

## 门禁对照

| 门禁 | 本轮 | 挂在 |
| --- | --- | --- |
| C1 导出完整 | 必过 | S4 |
| N1 可碰撞 | 必过 | S4 |
| P1 物理冒烟 | 必过 | S5 |
| J1 关节 | N/A | 单 bin 无关节 |
| G1 几何保真 | SKIP | S6 |
| A1 外观保真 | SKIP | S6 |
