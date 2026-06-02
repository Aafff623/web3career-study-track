# Week 3 ｜ Hackathon 启动 + 实践深化

> **周期**：2026-05-31 — 2026-06-06
> **主题**：黑客松正式启动、项目搭建、初步实现

## 本周学习目标

- 黑客松赛道确认、组队完成、项目启动
- 搭建 Smart Account + Session Key 项目基础结构
- 合约层初步实现（Foundry / ZeroDev SDK）
- 每日打卡不断档

## 黑客松时间线

| 日期 | 事项 |
|------|------|
| 6月1日 | 正式赛道细则公布 |
| 6月2日（周二） | **Open Day** — 开发周期正式启动 |
| 6月12日（周四） | 建议提交日 |
| 6月13日（周五）12:00 | 截止提交 |
| 6月14日（周六） | Demo Day |
| 约6月17日 | 获奖公布 |

## 黑客松赛道

| 赛道 | 方向 | 奖金 |
|------|------|------|
| Cobo 赛道 | Agentic Wallet / Agentic Commerce / Agentic Economic | 3500U |
| Z.ai 赛道 | Web Coding / 大模型应用 | 3500U |

**已确定方向**：Smart Account + Session Key（属于 Cobo 赛道 Agentic Wallet 方向）
详见 [`hackathon/DIRECTION.md`](../../hackathon/DIRECTION.md)

## 实践任务

- [x] 确认黑客松方向：Smart Account + Session Key
- [ ] 确认赛道细则（Cobo 赛道要求）
- [ ] 组队状态确认
- [ ] 搭建项目结构（Foundry / ZeroDev SDK）
- [ ] 合约层 MVP：部署支持 Session Key 的 Smart Account
- [ ] 策略层 MVP：金额上限 + 有效期两维限制
- [ ] 执行层 MVP：Agent 使用 Session Key 执行一笔转账
- [ ] 测试网部署 + Tx Hash 记录

## 推荐材料

- [ZeroDev Session Key 文档](https://docs.zerodev.app/sdk/permissions/session-keys)
- [ERC-4337 官方规范](https://eips.ethereum.org/EIPS/eip-4337)
- [Biconomy Session Keys](https://docs.biconomy.io/Account/signingMethods/sessionKeys)
- 预习笔记：[`Agent-Wallet`](../../pre_study/ai-web3-bridge/Agent-Wallet/README.md) · [`Account-Abstraction`](../../pre_study/web3-fundamentals/Account-Abstraction/README.md)

## 本周交付

- [ ] Hackathon 项目代码 commit / repo 结构
- [ ] 合约部署到测试网（Sepolia / Base Sepolia）
- [ ] 至少一笔 Tx Hash 证明
- [ ] Demo 材料（演示视频 / 截图 / 说明文档）

---

## 备注

- 上承：[`../week-2/WEEK.md`](../week-2/WEEK.md) 的交叉方向深入。
- 下启：Week 4 的集中开发与 Demo 提交。
