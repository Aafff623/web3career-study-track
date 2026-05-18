# hackathon ｜ 项目工作区

> 这里是 4 周共学营最终输出的地方——黑客松项目代码、合约、Demo 都在这里。

## 目前状态

⚪ **未开工**——Week 1-2 还在学习和选方向阶段，这块要等 **Week 3（2026-05-31 起）** 才动手。

## 候选方向

具体看根目录的 [`steering.md`](../steering.md) 里 "Hackathon 候选方向" 这一节，目前桌上四个选项：

1. **Smart Account + Session Key** — 让 Agent 安全干活
2. **Agentic Commerce 闭环** — 决策→执行→DeFi→恢复
3. **AI-native Wallet** — 重新设计钱包确认 UX
4. **链上数据分析 Agent** — 把"看 Etherscan 看到累"自动化

Week 2 结束前必须收敛到 1 个。

## 子目录

| 路径 | 内容 | 启用时机 |
|------|------|---------|
| [`contracts/`](./contracts/) | 智能合约源码（Hardhat / Foundry 工程） | Week 3 立项后 |
| [`demo/`](./demo/) | Demo 演示材料：截图、视频、slides、前端代码 | Week 4 集中开发 |

## 提交硬性要求

最终提交日：**2026-06-14（周日）**。

- ✅ 必须有**测试网 Tx Hash + 合约地址**——证明代码真的跑过
- ✅ Demo 演示材料齐全（视频 / 截图 / Slides 至少一种能展示的）
- ✅ 项目 README 与 proposal 完整
- ✅ 完整的项目复盘记录

## Commit 约定

进入这个目录后 commit 类型变化：

| 阶段 | type | 例子 |
|------|------|------|
| 立项 / 结构搭建 | `feat` | `feat: 初始化 Agent Wallet 项目结构` |
| 合约开发与部署 | `contract` | `contract: 部署 SessionKey 合约到 Sepolia` |
| 修 bug | `fix` | `fix: 修复 Gas 估算逻辑` |
| Demo 准备 | `feat` | `feat: 完成 Demo 页面` |

部署后在对应 `daily-log/.../TASK.md` 里记录 Tx Hash + 合约地址，并在 commit body 附上：

```
contract: 部署 SessionKey 合约到 Sepolia

Tx Hash: 0x...
Network: Sepolia
Contract: 0x...
```

详见 [`reference/git-commit-reference.md`](../reference/git-commit-reference.md)。

## 上承

- [`pre_study/`](../pre_study/) — 42 节预习笔记的弹药库
- [`daily-log/`](../daily-log/) — 每天的过程记录（特别是 Week 3-4 的 TASK.md）

> 等 Week 3 真正开工时，这个文件会被一份"项目说明 + 架构图 + 进度表"的真 README 取代。现在它只是一个占位入口。
