# Practice: Agent 购买 API 支付流程设计

> 模块：AI × Web3 交叉 · Machine-Payment

## 目标

设计一个完整的 Agent 购买付费 API 的支付流程，覆盖预算 → quote → intent → 付款 → receipt 全链路。

## 场景

用户允许 Agent 今天最多花 3 USDC 调用某个数据 API，单次调用 0.1 USDC。

## 流程

1. 定义预算层：全局 3 USDC / 天，单次 ≤ 0.1 USDC，仅限白名单 API
2. 定义 quote 格式：服务内容、价格、币种、收款地址、有效期（5 分钟）、quote id
3. 定义 Payment Intent：用户目标、服务方、最大金额、币种、链、过期时间、quote 引用
4. 定义付款流程：检查预算 → 校验 quote → 生成交易 → 钱包确认 → 发送
5. 定义 receipt 字段：quote id、payment intent id、tx hash、服务结果引用、剩余预算
6. 定义异常处理：quote 过期怎么办、余额不足怎么办、API 无响应怎么办

## 验收标准

- [ ] 预算至少 3 层（全局 / 单次 / 服务方）
- [ ] quote 包含有效期和 quote id
- [ ] Payment Intent 绑定任务 + 金额 + 服务方 + 过期时间
- [ ] receipt 关联 quote id + intent id + tx hash
- [ ] 至少 2 种异常处理路径
