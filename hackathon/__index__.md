# hackathon ｜ 项目工作区

> 这里是 4 周共学营最终输出的地方——黑客松项目代码、合约、Demo 都在这里。

## 目前状态

🟡 **方向已确定** — 2026-05-26 收敛到 **Smart Account + Session Key（#1）**，Week 3（2026-05-31 起）启动开发。

## 最终方向

**Smart Account + Session Key** — 给 AI Agent 一把 *"只能在某段时间、某个金额内、做某类事"* 的钥匙，用户随时可撤销。

> 完整选型 rationale 见 [`DIRECTION.md`](./DIRECTION.md)

四个候选的对比回顾：

| # | 方向 | 结论 |
|---|------|------|
| 1 | **Smart Account + Session Key** | ✅ **选定** — 生态成熟（ERC-4337 / ZeroDev / Biconomy），技术门槛适中，可演示性强 |
| 2 | Agentic Commerce 闭环 | ❌ 放弃 — 4 周内做不完完整闭环，状态机太复杂 |
| 3 | AI-native Wallet | ❌ 放弃 — 偏 UX 设计，非技术长板 |
| 4 | 链上数据分析 Agent | 💡 保留为扩展点 — 可与 #1 结合（链上操作日志作为 Agent 可验证记忆）|

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
