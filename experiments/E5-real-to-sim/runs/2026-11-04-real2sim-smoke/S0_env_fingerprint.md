# E5 S0 环境指纹

记录时间：2026-11-04（Asia/Shanghai）

执行机：Grok Bot box

下列为开跑时**已核实**事实。GPU 为无，不得改记为有。

| 项 | 已核实值 |
| --- | --- |
| 操作系统 | Debian GNU/Linux 13 (trixie)；kernel 6.12.94+；x86_64 |
| CPU | 8 核 |
| RAM | 15Gi |
| 磁盘 | `/workspace` 约 118G 可用 |
| GPU | 无 NVIDIA（无 `nvidia-smi`，无 `/dev/nvidia*`） |
| CUDA | 无 |
| Python | 系统 3.13.5（`/usr/bin/python3`）；安装中将改用 3.11/3.12 venv |
| 开跑时依赖 | `mujoco`、`torch` 未安装 |
| 代码 | DISCOVERSE 与 DISCOVERSE-Real2Sim 已 shallow clone 到执行机 `/workspace` |

## 本轮处置

无 GPU、无 CUDA，因此完整 3DGS / 外观路径在本机不能跑。

用户已拍板接受这一事实，**本轮只做 MuJoCo 几何-物理子集**：

- A1 = SKIP（外观保真，含 3DGS / 外观）。
- G1 = SKIP（含 3DGS / 外观 / GPU 重建）。
- **勿再等待 GPU。** 不把「需要 Linux + NVIDIA GPU」留作本轮阻塞，也不停在等待 GPU 的状态。
- 安装与后续 S1–S5 以 CPU 上的 MuJoCo 几何-物理子集为准。

## 预计墙钟

- S0–S1：估 1–3h。
- S2–S5：视 CPU 上 MuJoCo 是否可过 S1 再估。
