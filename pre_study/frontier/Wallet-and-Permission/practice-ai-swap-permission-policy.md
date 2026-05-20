# Practice: AI 自动小额换币助手权限策略设计

> 模块：前沿探索 · Wallet-and-Permission

## 目标

为一个 AI 自动小额换币助手设计完整的权限策略，覆盖资产范围 → 函数白名单 → session key → 模拟展示 → 确认规则 → 日志复查。

## 场景

用户授权 AI Agent 在 Uniswap 上自动执行小额 USDC↔WETH 换币，单笔不超过 50 USDC。

## 流程

### 1. 权限策略定义

```yaml
policy:
  name: "AI Swap Assistant Policy"
  version: "1.0"
  
  asset_scope:
    allowed_tokens:
      - symbol: "USDC"
        address: "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48"
      - symbol: "WETH"
        address: "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2"
    blocked_tokens:
      - "NFT"
      - "治理 token"
  
  amount_limits:
    per_transaction: 50 USDC
    daily: 200 USDC
    weekly: 1000 USDC
  
  target_contracts:
    allowed:
      - name: "Uniswap V3 Router"
        address: "0xE592427A0AEce92De3Edee1F18E0157C05861564"
    blocked:
      - "未知合约"
      - "新部署合约"
  
  function_scope:
    allowed:
      - "exactInputSingle"
      - "exactInput"
    blocked:
      - "approve" (无限授权)
      - "permit2" (批量授权)
      - "multicall" (组合调用)
  
  price_slippage:
    max_slippage: "0.5%"
    price_source: "Chainlink Oracle"
    re_confirm_threshold: "1%"
  
  time_window:
    session_key_ttl: "24 hours"
    auto_revoke_after: "7 days"
  
  frequency:
    max_per_hour: 3
    cooldown_between: "5 minutes"
```

### 2. Session Key 配置

```json
{
  "session_key": "0xSession...",
  "permissions": {
    "target": "Uniswap V3 Router",
    "functions": ["exactInputSingle", "exactInput"],
    "tokens": ["USDC", "WETH"],
    "max_per_tx": "50 USDC",
    "max_daily": "200 USDC",
    "expires_at": "2026-05-21T10:30:00Z"
  },
  "guard": {
    "slippage_check": true,
    "price_check": true,
    "frequency_check": true
  },
  "revocation": {
    "user_can_revoke": true,
    "auto_revoke_on_excess": true,
    "revoke_url": "https://app.example.com/revoke"
  }
}
```

### 3. 交易模拟展示字段

| 字段 | 来源 | 展示方式 |
|------|------|---------|
| 输入资产和数量 | UserOperation | "花费 25 USDC" |
| 输出资产和数量 | 模拟结果 | "获得 0.0072 WETH" |
| 预期价格 | Oracle | "1 WETH = 3,472 USDC" |
| 滑点 | 计算 | "0.3%" |
| Gas 费用 | 估算 | "≈ $0.12" |
| 接收地址 | Session Key policy | "你的地址 0xABC..." |
| 最大损失 | 计算 | "最多花 50 USDC" |

### 4. 确认规则

| 场景 | 是否需要确认 | 原因 |
|------|------------|------|
| 首次使用 | ✅ 必须 | 用户了解 policy |
| 单笔 <10 USDC | ❌ 自动 | 低风险 |
| 单笔 10-50 USDC | ⚠️ 简化确认 | 显示金额+接收地址 |
| 滑点 >0.5% | ✅ 必须 | 价格偏离 |
| 连续 3 笔 | ✅ 必须 | 频率异常 |
| Session Key 过期 | ✅ 必须 | 重新授权 |
| 余额不足 | ❌ 拒绝执行 | 直接报错 |

### 5. 执行日志

```json
{
  "log_id": "log-20260520-001",
  "session_key": "0xSession...",
  "action": "swap",
  "input": { "token": "USDC", "amount": "25" },
  "output": { "token": "WETH", "amount": "0.0072" },
  "slippage": "0.3%",
  "gas": "$0.12",
  "contract": "Uniswap V3 Router",
  "function": "exactInputSingle",
  "tx_hash": "0xabc...",
  "status": "success",
  "timestamp": "2026-05-20T10:30:00Z",
  "daily_spent": "75 USDC / 200 USDC"
}
```

### 6. 异常处理

| 异常 | 响应 |
|------|------|
| 滑点 >1% | 暂停 + 通知用户 |
| 连续失败 3 次 | 撤销 session key |
| 目标合约不在白名单 | 拒绝 + 记录 |
| 余额超 daily limit | 拒绝 + 提示 |
| Session Key 过期 | 拒绝 + 要求重新授权 |

## 验收标准

- [ ] 资产范围明确（USDC/WETH，排除 NFT 和治理 token）
- [ ] 函数白名单（exactInputSingle/exactInput，禁止 approve/multicall）
- [ ] 金额限制三层（单笔 50 / 日 200 / 周 1000）
- [ ] Session Key 24h 有效期 + 可撤销
- [ ] 交易模拟展示 7 个必要字段
- [ ] 确认规则按风险分级
- [ ] 执行日志可复查
