# Practice: Agent 购买链上数据分析 API 流程设计

> 模块：前沿探索 · Agentic-Commerce

## 目标

设计一个完整的 Agent 购买链上数据分析 API 的商业闭环，覆盖发现 → 报价 → 支付 → 验收 → 争议全流程。

## 场景

用户需要分析某地址的 DeFi 交互历史，Agent 自动寻找合适的数据分析 API 并完成购买。

## 流程

### 1. 用户目标与预算

```json
{
  "task": "分析地址 0xABC... 的 DeFi 交互历史",
  "budget": {
    "max_single": "2 USDC",
    "daily_limit": "10 USDC",
    "currency": "USDC"
  },
  "quality": {
    "data_freshness": "最近 30 天",
    "output_format": "structured_json",
    "required_fields": ["protocol", "action", "amount", "timestamp"]
  },
  "validity": "24h"
}
```

### 2. 服务发现

```
Agent 任务需求
    ↓
[服务目录查询] → 匹配 "DeFi 交互历史分析"
    ↓
返回候选服务列表：
  - ServiceA: 1.5 USDC/次, 响应 <5s, 声誉 4.8/5
  - ServiceB: 0.8 USDC/次, 响应 <10s, 声誉 4.2/5
  - ServiceC: 2.0 USDC/次, 响应 <3s, 声誉 4.9/5
    ↓
[路由决策] → 按成本/质量/声誉综合评分
    ↓
选择 ServiceA（性价比最优）
```

### 3. Payment Intent

```json
{
  "intent_id": "intent-20260520-001",
  "task": "DeFi 交互历史分析",
  "service_provider": "ServiceA",
  "budget": "1.5 USDC",
  "acceptable_providers": ["ServiceA", "ServiceB"],
  "min_reputation": 4.0,
  "quality_requirements": {
    "response_time": "<5s",
    "data_fields": ["protocol", "action", "amount", "timestamp"]
  },
  "refund_conditions": ["timeout", "invalid_format", "missing_fields"],
  "expires_at": "2026-05-21T10:30:00Z"
}
```

### 4. 报价与支付

```
Agent → ServiceA: 询价请求
ServiceA → Agent: 报价 { fee: "1.5 USDC", delivery: "<5s" }
Agent: 检查 Payment Intent → 预算内，服务方在白名单
Agent: 生成支付指令
    ↓
[Smart Account] → 签名 UserOperation
[Bundler] → 提交 EntryPoint
[Paymaster] → 代付 gas
    ↓
资金进入 Escrow 合约
```

### 5. 任务执行与验收

```
ServiceA 执行分析
    ↓
返回结果：
{
  "data": [...],
  "output_hash": "0xdef...",
  "response_time": 3.2,
  "fields_complete": true
}
    ↓
[验收检查]
  ✅ 响应时间 <5s
  ✅ 数据字段完整
  ✅ output_hash 与结果一致
  ✅ 声誉未变化
    ↓
验收通过 → 释放 Escrow → ServiceA 收款
```

### 6. 收据记录

```json
{
  "receipt_id": "receipt-20260520-001",
  "payer": "0xUser...",
  "provider": "ServiceA",
  "service": "DeFi 交互历史分析",
  "fee": "1.5 USDC",
  "chain": "ethereum",
  "tx_hash": "0xabc...",
  "output_hash": "0xdef...",
  "response_time": 3.2,
  "acceptance_status": "passed",
  "timestamp": "2026-05-20T10:30:00Z"
}
```

### 7. 争议处理

| 场景 | 触发条件 | 处理方式 |
|------|---------|---------|
| 超时 | 响应 >5s | 自动退款 |
| 格式错误 | 字段缺失 | 部分退款 |
| 数据错误 | 与链上不一致 | 争议 → 仲裁 |
| 服务不可用 | 无响应 | 全额退款 |

## 验收标准

- [ ] Payment Intent 结构化（目标/预算/服务方/质量/退款/有效期）
- [ ] 预算分层（单次/每日/总额）
- [ ] 任务完成证明明确（output_hash + 响应时间 + 字段完整性）
- [ ] 收据包含必要字段（payer/provider/fee/tx_hash/output_hash）
- [ ] 争议处理有明确路径
