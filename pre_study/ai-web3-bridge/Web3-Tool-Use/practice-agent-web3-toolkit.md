# Practice: 设计一组 Agent Web3 工具

> 模块：AI × Web3 交叉 · Web3-Tool-Use

## 目标

设计并定义一组 Agent 可调用的 Web3 工具，重点练习"读 / 写 / 签名 / 确认 / 记录"的职责分离。

## 流程

1. 定义一个只读工具：读取某地址在某链上的 ETH 余额
   - 输入 schema：{ chain_id, address }
   - 输出字段：{ balance, block_number, chain_id, timestamp }
2. 定义一个合约读取工具：读取 ERC-20 allowance(owner, spender)
   - 输入 schema：{ chain_id, token_address, owner, spender }
   - 输出字段：{ allowance, block_number, chain_id }
3. 定义一个交易草稿工具：生成 ERC-20 approve calldata（不发送）
   - 输入 schema：{ chain_id, token_address, spender, amount }
   - 输出字段：{ calldata, to, value, estimated_gas }
4. 定义写交易工具的权限规则：只允许特定 token、特定 spender、最大额度
5. 为每个工具定义错误类型（网络错误 / ABI 不匹配 / 额度超限 / 模拟失败）

## 验收标准

- [ ] 每个工具有明确的输入 schema 和输出字段
- [ ] 读 / 写工具分离，无"万能 RPC"
- [ ] 写交易工具附带权限规则（白名单 + 额度上限）
- [ ] 每个工具有至少 2 种错误类型定义
- [ ] 所有工具定义了日志字段（输入、输出、时间、错误）
