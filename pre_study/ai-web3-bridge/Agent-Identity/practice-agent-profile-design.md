# Practice: 设计一个 Agent Profile

> 模块：AI × Web3 交叉 · Agent-Identity

## 目标

设计一个完整的 Agent Profile，覆盖身份、能力、服务入口、控制权和更新机制。

## 场景

设计一个"合约风险分析 Agent"的公开 profile。

## 流程

1. 基础信息：名称、描述、owner（多签地址）、版本号
2. 服务入口：HTTPS endpoint + 支持协议（MCP / REST）
3. 3 个 capability：
   - 只读分析（低风险）：输入合约地址 → 输出风险摘要
   - 生成审计报告（中风险）：输入合约地址 + 范围 → 输出 PDF 报告
   - 生成交易草稿（高风险）：输入风险结论 + 修复建议 → 输出 calldata
4. 每个 capability 写：输入 schema、输出 schema、价格、限制、风险等级
5. Profile URI：IPFS 地址
6. 更新机制：owner 多签签名 → 更新 profile → 事件通知用户

## 验收标准

- [ ] 基础信息完整（名称 / owner / endpoint / 版本）
- [ ] 3 个 capability 各有输入 / 输出 / 价格 / 限制 / 风险等级
- [ ] Profile URI 可访问（或设计为可访问）
- [ ] 更新机制需要 owner 签名
- [ ] 能说明 endpoint 如何证明属于该 Agent
