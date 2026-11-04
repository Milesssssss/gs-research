# E1 最小方案

本目录是 E1 最小开跑记录。产出只保留覆盖率、语义命中、墙钟与显存；密钥不入库。

本轮图像是 **interim Isaac**，非官方 Replica office0。

## 分工

| 环节 | 配置 | 边界 |
|---|---|---|
| 分割 | SAM 2.1 @ `172.16.89.51:7861`（`POST /api/v1/segment`） | 只 segment；不跑 SAM3D reconstruct；不动 7861 进程 |
| 语义 | DeepSeek 兼容网关 `https://vibeg.seer-robotics.cn/openai`，模型 `deepseek/deepseek-flash` | 模型名带 provider 前缀 |
| 几何 | `seer@172.16.88.170` RTX 5080 缩配冒烟 | 假位姿 + 随机高斯；不杀 Isaac |

## 数据

- 本轮：interim Isaac `frame000000.png`（1280×720）。
- 缺口：官方 NICE-SLAM Replica office0 RGB。到位后再重跑分割、语义、几何。

实测表见 [`2026-11-04-min-run.md`](2026-11-04-min-run.md)。
