# E5 S1 结果

记录时间：2026-11-04（Asia/Shanghai）

阶段 S1（DISCOVERSE 自带最小 MuJoCo demo）**PASS**。这是空场景物理步进，不是后续周次的传感器闭环门禁。

| 项 | 结果 |
| --- | --- |
| discoverse | 1.9.0 |
| mujoco | 3.17.0 |
| `MUJOCO_GL` | `egl` |
| 场景 | 空场景 |
| 步进 | 2500 step **PASS** |
| A1 外观保真 | SKIP（含 3DGS / 外观） |
| G1 几何保真 | SKIP（含 3DGS / 外观 / GPU 重建） |
| GPU | 无 NVIDIA（无 `nvidia-smi`，无 `/dev/nvidia*`）。不得改记为有 |
| CUDA | 无 |

本轮仍只做 MuJoCo 几何-物理子集，勿再等待 GPU。下一步是 S2：GraspClutter6D 单 bin（优先 `hard/000091`）。

执行机本地详细日志只作路径引用，全文未推送到本仓：

`/workspace/real2sim-research/E5_S0_env_fingerprint_2026-11-04.md`
