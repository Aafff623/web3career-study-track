---
date: 2026-05-26
status: 已确定
---

# Hackathon 方向：Smart Account + Session Key

> 2026-05-26 · Week 2 Day 3 · 方向收敛完成

## 一句话定位

给 AI Agent 一把 *"只能在某段时间、某个金额内、做某类事"* 的钥匙——用户随时可查看、可撤销。

## 为什么选这个方向

### 1. 生态成熟度最高

| 组件 | 状态 | 参考 |
|------|------|------|
| ERC-4337 | 已主网 | 账户抽象标准，基础设施成熟 |
| ZeroDev SDK | 可用 | Session Key 即开即用 |
| Biconomy | 可用 | Paymaster + Bundler 托管方案 |
| Pimlico | 可用 | Bundler + Paymaster API |

### 2. 与课程衔接最紧

预习笔记中直接相关的章节：

- [`pre_study/ai-web3-bridge/Agent-Wallet/README.md`](../pre_study/ai-web3-bridge/Agent-Wallet/README.md) — AA 钱包、Session Key、Policy、Guard
- [`pre_study/ai-web3-bridge/Machine-Payment/README.md`](../pre_study/ai-web3-bridge/Machine-Payment/README.md) — 预算、Payment Intent、x402
- [`pre_study/web3-fundamentals/Account-Abstraction/README.md`](../pre_study/web3-fundamentals/Account-Abstraction/README.md) — ERC-4337、Bundler、Paymaster

### 3. 可演示性强

核心闭环清晰，4 周能做出完整 Demo：

```
用户创建 Smart Account
    ↓
用户给 Agent 签发 Session Key（带限制：金额上限 / 有效期 / 允许操作白名单）
    ↓
Agent 在限制内自主执行链上操作
    ↓
用户随时查看 Audit Trail 并撤销 Session Key
```

### 4. 与其他方向对比

| 维度 | #1 Smart Account | #2 Commerce | #3 Wallet UX | #4 Data Agent |
|------|------------------|-------------|--------------|---------------|
| 技术门槛 | 中 | 高 | 中 | 中 |
| 生态成熟度 | ⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| 4 周可完成 | ✅ | ❌ | ⚠️ | ✅ |
| 我的长板匹配 | ⭐⭐⭐ | ⭐⭐ | ⭐⭐ | ⭐⭐⭐ |
| 差异化 | 中等 | 高 | 低 | 低 |

**排除理由：**
- #2 Commerce 闭环：状态机太复杂，4 周做不完可演示的闭环
- #3 Wallet UX：偏前端设计，非我当前技术长板
- #4 Data Agent：虽可行，但 Smart Account + Session Key 更有"AI 代理安全执行链上操作"的叙事张力

### 5. 潜在扩展点

- **链上记忆**：把 Agent 的操作日志写到链上，作为可验证的 Audit Trail（与 #4 链上数据分析结合）
- **Payment Intent**：用 x402 标准做机器支付结算（与 #2 Commerce 的轻量版结合）

## 技术栈初步规划

| 层 | 技术 |
|----|------|
| 智能合约 | Solidity + ERC-4337（EntryPoint / Smart Account / Session Key Module） |
| 开发框架 | Foundry（测试 + 部署）或 Hardhat |
| SDK | ZeroDev / Biconomy（Session Key 管理） |
| 测试网 | Sepolia 或 Base Sepolia |
| 前端（Demo）| Next.js + viem + wagmi（可选，如果时间够） |
| AI Agent | Claude Code / 自主 Agent（演示 Agent 调用 Session Key 的场景） |

## 最小可行 Demo（MVP）

Week 3-4 的核心目标：

1. **合约层**：部署一个支持 Session Key 的 Smart Account
2. **策略层**：实现 Session Key 的签发逻辑（金额限制 + 有效期 + 操作白名单）
3. **执行层**：Agent 使用 Session Key 在限制内执行一笔转账或合约调用
4. **撤销层**：用户界面展示 Session Key 状态，支持一键撤销
5. **审计层**：链上记录每次 Agent 操作，可追踪

## 风险与应对

| 风险 | 概率 | 应对 |
|------|------|------|
| ERC-4337 合约调试耗时 | 中 | 用 ZeroDev SDK 减少自定义合约工作量 |
| Session Key 策略复杂 | 中 | 先做"金额 + 有效期"两维限制，白名单放 Phase 2 |
| 前端时间不够 | 高 | 用 CLI / 脚本演示 Agent 调用，前端可选 |
| Gas 费（测试网）| 低 | Sepolia 或 Base Sepolia，领水龙头 |

## 参考资源

- [ZeroDev Session Key 文档](https://docs.zerodev.app/sdk/permissions/session-keys)
- [ERC-4337 官方规范](https://eips.ethereum.org/EIPS/eip-4337)
- [Biconomy Session Keys](https://docs.biconomy.io/Account/signingMethods/sessionKeys)
- 预习笔记：[`Agent-Wallet`](../pre_study/ai-web3-bridge/Agent-Wallet/README.md) · [`Account-Abstraction`](../pre_study/web3-fundamentals/Account-Abstraction/README.md)

---

> *Agent 不应该拥有"钱包"，它应该只拥有 **可限制、可审计、可撤销** 的能力。*
