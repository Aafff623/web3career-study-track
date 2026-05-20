# Practice: 给一笔交易做上下文包

> 模块：AI × Web3 交叉 · Chain-aware-Context

## 目标

给一笔公开交易构建完整的链感知上下文包，练习"链上事实 → 模型可读上下文 → citation 可追溯"的完整流程。

## 流程

1. 选一笔公开交易哈希（可从 Etherscan 热门交易或已知合约交互中找）
2. 通过 RPC / Explorer 收集以下字段：
   - chain id、block number、timestamp
   - from、to、method（函数名 + 参数）
   - value、token transfers（如有）
   - logs / events
3. 找到目标合约的 ABI 或 verified source
4. 整理成模型可读的上下文段落，每个关键结论附上 tx hash 或 explorer link
5. 标注哪些是链上事实（raw data），哪些是你的解释（interpretation）

## 验收标准

- [ ] 上下文包包含：chain id、block number、from/to、method、value、logs
- [ ] 每条关键结论附有 tx hash 或 explorer link（citation）
- [ ] 明确区分了"链上事实"和"解释"
- [ ] 合约 ABI 来源可追溯（verified source 或文档链接）
