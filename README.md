# gs-research

空间智能 / 具身实验日志仓。本仓记录实验约定、环境指纹、阶段清单与结论，不存放模型权重、全量数据集或仿真资产。

## E5 目录约定

每项实验一个目录，E5 使用：

```
experiments/E5-real2sim-smoke/
  README.md                 # 任务摘要、状态、主栈、门禁、派工、本轮锁定
  checklist.md              # S0–S8 清单与状态
  S0_env_fingerprint.md     # 开跑时已核实的环境指纹
```

约定：

- 目录名：`experiments/<实验ID>-<短名>/`。
- 状态取值：`pending`、`in_progress`、`done`、`skip`、`blocked`。
- 后续阶段按 `S1_*.md` … `S8_*.md` 追加日志与报告。
- `S0_env_fingerprint.md` 中的硬件事实（尤其 GPU 有无）不得事后改写。无 GPU 就保持无 GPU。
- 本轮范围锁定写在该实验的 `README.md` 与 `checklist.md`，不靠口头覆盖。

## 实验索引

| ID | 目录 | 状态 | 说明 |
| --- | --- | --- | --- |
| E5 | [experiments/E5-real2sim-smoke](experiments/E5-real2sim-smoke/README.md) | closed as PASS\* | 有条件合格。降级 = proxy_bin + 运动学 P1。A1/G1 = SKIP；GPU = 无 |
