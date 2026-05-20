# Practice: 设计一个链上 Agent Swap 工作流

> 模块：AI × Web3 交叉 · Agent-Workflow

## 目标

为一笔小额 ERC-20 swap 设计完整的 Agent 工作流，练习 task graph、状态机、human-in-the-loop 和 regression case 的设计。

## 流程

1. 画出 task graph（至少 7 步）：
   - 读取用户目标和限制
   - 获取余额和 allowance
   - 查询价格和流动性
   - 生成候选交易
   - 模拟交易
   - 展示风险（给用户看）
   - 用户确认
   - 发送交易
   - 追踪结果
2. 为每一步定义：输入、输出、可用工具、失败处理
3. 标出 human-in-the-loop 节点（至少 1 个必须确认点）
4. 定义状态机状态（至少 6 个：draft / plan_ready / simulation_failed / waiting_confirmation / submitted / confirmed）
5. 写 5 个 regression case

## 验收标准

- [ ] Task graph ≥ 7 步，每步有输入 / 输出 / 工具 / 失败处理
- [ ] 至少 1 个步骤标记为"必须人工确认"
- [ ] 状态机 ≥ 6 个状态，覆盖正常 + 异常路径
- [ ] 5 个 regression case 覆盖：正常、错误链、滑点过大、余额不足、用户拒绝
