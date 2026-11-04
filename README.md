# gs-research

空间智能实验日志。用来记录 **3DGS / 2DGS / Mesh / real-to-sim** 的实验过程与结论。

本仓库只存放说明、单次 run 的文字记录、小图和外部链接。这里没有预填的实验结果；某次 run 在实际跑完之前，指标、结论和 Go/No-Go 保持空白。

## 目的

- 把一次实验从「开跑前的假设」留到「结束后的一页结论」，避免结论只存在于聊天记录或个人机器上。
- 用固定编号区分五条实验线，避免质量、网格、语义和仿真冒烟混在同一份笔记里。
- 大文件（高斯、权重、网格、视频、数据集）不进 Git 历史，走 Git LFS 或外链。规范见 [docs/process.md](docs/process.md)。

## 如何新增一次实验 run

1. 在 [experiments/README.md](experiments/README.md) 里确认这次工作属于哪一条线（E1–E5）。跨线的比较拆成各自的 run，并在文内互相链接。
2. 复制该线的 `runs/_template.md`，保存为 `experiments/<线>/runs/YYYY-MM-DD-<短名>.md`。E1 与 E5 已提供模板。E2、E3、E4 仍是占位说明；在补上模板之前，按 [docs/process.md](docs/process.md) 的同一组字段写。
3. **开跑前**填登记信息：日期、负责人、场景、数据授权、GPU、被测代码的 git commit、假设。状态写「登记」。
4. **开跑时**把场景、GPU 和授权补全。缺授权的数据不要开跑。
5. **结束后**在同一文件里写一页结论和指标表，给出 Go 或 No-Go，并记下日志路径和失败模式。不要另开一份只含结论的文档。
6. 提交时只包含 Markdown、小图和链接。体积大的产物按 [docs/process.md](docs/process.md) 处理。

一次 run 对应一个文件。修正已结束的记录时，在原文件追加「更正」小节并注明日期，不覆盖原来的数字。

## 目录约定

```text
docs/process.md                 实验过程如何落库
experiments/README.md           E1–E5 编号含义
experiments/E1-semantic-3dgs/   对象中心语义高斯（VLSplat）
experiments/E2-quality-speed/   质量—速度帕累托
experiments/E3-gs-to-mesh/      GS→Mesh，且网格可仿真
experiments/E4-online-semantic/ 在线语义建图
experiments/E5-real-to-sim/     Real-to-Sim 冒烟（C1 / N1 / P1）
experiments/<线>/runs/          该线的单次 run；_template.md 是空模板
```

| 路径 | 放什么 | 不放什么 |
| --- | --- | --- |
| `experiments/<线>/README.md` | 这条线要回答的问题、与邻线的边界 | 某一次跑的数字 |
| `experiments/<线>/runs/*.md` | 单次 run 的登记、步骤、指标、结论 | 第二份「总结版」 |
| `docs/` | 对所有实验线都适用的过程规范 | 某条线的专有结论 |
| 仓库内图片 | 截图、曲线等小图 | 训练输出目录、原始采集 |

被测代码通常在别的仓库。run 里的 `git commit` 填那个仓库的完整提交号，并写明远程地址。本日志仓库自己的提交只表示「这份记录何时入库」。

## 实验线

编号的定义见 [experiments/README.md](experiments/README.md)。

- [E1 对象中心语义高斯（VLSplat）](experiments/E1-semantic-3dgs/README.md)
- [E2 质量—速度帕累托](experiments/E2-quality-speed/README.md)
- [E3 GS→Mesh 可仿真](experiments/E3-gs-to-mesh/README.md)
- [E4 在线语义建图](experiments/E4-online-semantic/README.md)
- [E5 Real-to-Sim 冒烟](experiments/E5-real-to-sim/README.md)
