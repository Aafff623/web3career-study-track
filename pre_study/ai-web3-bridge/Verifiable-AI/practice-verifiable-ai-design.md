# Practice: 设计 AI 风险评分的验证方案

> 模块：AI × Web3 交叉 · Verifiable-AI

## 目标

为一个 AI 风险评分系统设计分层验证方案，按输出影响力选择不同验证强度。

## 场景

DeFi 协议使用 AI 模型对每笔交易进行风险评分（0-100），分数决定：
- 低分（0-30）：正常放行，仅记录
- 中分（31-70）：放行但触发告警，需人工复核
- 高分（71-100）：自动拦截交易，需管理员审批

## 流程

### 1. 定义输入数据来源

```yaml
input:
  source: "链上交易数据 + 协议配置"
  fields:
    - from_address: "发起方地址"
    - to_address: "目标合约地址"
    - value: "交易金额（USDC）"
    - method: "调用方法"
    - block_number: "区块号"
    - timestamp: "交易时间戳"
  freshness: "实时（当前区块）"
```

### 2. 记录模型信息

```yaml
model:
  name: "RiskScorer-v2.1"
  version: "2.1.0"
  hash: "0xabc123..."  # 模型文件 hash
  prompt_template_hash: "0xdef456..."  # prompt 模板 hash
  output_schema:
    - score: "integer 0-100"
    - risk_flags: "string[]"
    - reason: "string"
    - model_version: "string"
    - timestamp: "ISO8601"
```

### 3. 分层验证策略

| 风险等级 | 分数范围 | 验证方式 | 说明 |
|----------|---------|---------|------|
| 低 | 0-30 | Audit Trail | 记录输入 hash + 输出 + 模型版本 + 时间戳 |
| 中 | 31-70 | Audit Trail + Challenge Window | 24 小时内可提交反证 |
| 高 | 71-100 | TEE Attestation + 人工复核 | 证明模型在可信环境中执行，且需管理员审批 |

### 4. Audit Trail 设计

```json
{
  "tx_hash": "0x123...",
  "input_hash": "0xabc...",
  "output": {
    "score": 45,
    "risk_flags": ["high_value", "new_counterparty"],
    "reason": "金额超过阈值且对方地址首次交互"
  },
  "model_version": "2.1.0",
  "model_hash": "0xabc123...",
  "prompt_template_hash": "0xdef456...",
  "evaluator": "risk-scorer-agent-01",
  "timestamp": "2026-05-20T10:30:00Z",
  "environment": "tee-graphene-v1"
}
```

### 5. Challenge Window 设计

- 中风险输出：24 小时 challenge window
- 挑战者需提交反证：指出模型误判的具体依据
- 无挑战 → 输出生效
- 有挑战 → 进入复核流程

### 6. 争议流程

```
挑战提交 → 复核（3 个独立 evaluator）→ 多数投票 → 仲裁结果
                                                    ↓
                                          释放 / 拦截 / 退款
```

### 7. 升级路径

| 阶段 | 验证方式 | 成本 | 适用场景 |
|------|---------|------|---------|
| 当前 | Audit Trail + Challenge | 低 | 日常运行 |
| 中期 | TEE Attestation | 中 | 高风险交易 |
| 远期 | zkML Proof | 高 | 需要链上密码学验证 |

## 验收标准

- [ ] 输入数据来源和更新时间明确定义
- [ ] 模型版本、prompt 模板和输出 schema 已记录
- [ ] 低风险输出只记录 audit trail
- [ ] 高风险输出需要人工复核或 challenge window
- [ ] 写出未来如何升级到 TEE 或 ZK 证明
