# Practice: 设计"任务完成判断" AI Oracle

> 模块：AI × Web3 交叉 · AI-Oracle

## 目标

设计一个判断"Agent 任务是否完成"的 AI Oracle，覆盖输入 → 输出 → 记录 → challenge → 争议全流程。

## 场景

Escrow 场景：用户锁定 2 USDC 委托 Agent 生成合约风险报告，需要 AI Oracle 判断报告是否合格。

## 流程

1. 定义输入：任务说明 + 交付物 hash + 验收标准（字段完整性、风险项数量、合约地址覆盖）
2. 定义输出：accepted (bool)、score (0-100)、reason (string)、modelVersion
3. 定义记录字段：输入 hash、prompt 模板 hash、模型版本、生成时间、evaluator 身份
4. 设计 challenge window：24 小时内可提交反证
5. 设计争议流程：挑战 → 复核（多 evaluator）→ 仲裁 → 资金释放或退款
6. 定义错误处理：Oracle 输出错误时，escrow 暂停释放，进入争议

## 验收标准

- [ ] 输出为结构化 JSON（非自然语言）
- [ ] 记录包含输入 hash + 模型版本 + 时间 + evaluator
- [ ] Challenge window ≥ 24 小时
- [ ] 争议流程有明确的复核和仲裁步骤
- [ ] Oracle 错误时 escrow 有暂停机制
