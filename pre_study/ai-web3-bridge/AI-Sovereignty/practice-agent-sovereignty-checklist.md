# Practice: Agent 主权检查表设计

> 模块：AI × Web3 交叉 · AI-Sovereignty

## 目标

为一个 AI DeFi Agent 设计完整的主权检查表，覆盖用户控制 → 数据可迁移 → 模型选择 → 抗审查 → 可验证性。

## 场景

用户使用 AI Agent 管理 DeFi 投资组合，Agent 具备：读取钱包、执行交易、保存偏好、调用多种模型、跨平台协作能力。

## 流程

### 1. User Control 检查

| 检查项 | 当前状态 | 改进方案 |
|--------|---------|---------|
| 用户能否查看 Agent 正在使用哪个模型？ | ❌ 不可见 | 控制面板显示当前模型 + 切换入口 |
| 用户能否查看 Agent 保存了哪些记忆？ | ❌ 不可见 | 记忆管理页面，支持查看/删除/导出 |
| 用户能否查看 session key 权限和额度？ | ⚠️ 部分可见 | 完整显示：地址/额度/有效期/方法白名单 |
| 用户能否一键撤销所有权限？ | ❌ 无 | 紧急停止按钮：撤销 session key + 暂停 Agent |
| 用户能否导出所有数据？ | ❌ 无 | 数据导出入口：记忆/历史/偏好/日志 |

### 2. Data Portability 检查

| 数据类型 | 导出格式 | 敏感等级 | 可迁移目标 |
|----------|---------|---------|-----------|
| 任务历史 | JSON | 低 | 任何 Agent |
| 用户偏好 | JSON Schema | 中 | 兼容 Agent |
| 工具日志 | 签名 JSON | 低 | 审计系统 |
| 身份凭证 | VC (Verifiable Credential) | 高 | DID 兼容系统 |
| 可公开声誉 | 签名 Attestation | 低 | 任何平台 |
| 私有记忆 | 加密 JSON + 用户密钥 | 极高 | 仅用户控制的 Agent |

### 3. Model Choice 检查

| 策略 | 触发条件 | 模型选择 | 用户可控 |
|------|---------|---------|---------|
| 隐私优先 | 涉及私钥/持仓详情 | 本地模型 | ✅ 默认开启 |
| 成本优先 | 低风险查询/总结 | 小模型/免费模型 | ✅ 可设默认 |
| 质量优先 | 复杂推理/交易决策 | 强模型 | ✅ 可设默认 |
| 可验证优先 | 需要链上证明 | ZK/TEE 支持的模型 | ⚠️ 需手动开启 |

### 4. Censorship Resistance 检查

| 组件 | 单点风险 | 去中心化方案 |
|------|---------|------------|
| 模型推理 | 依赖单一 API | 多模型 fallback（本地 + 云端 + 备选） |
| Agent 身份 | 平台锁定 | DID + 可迁移 profile |
| 数据存储 | 平台数据库 | 去中心化存储 + 本地优先 |
| 执行记录 | 平台日志 | 链上 hash 锚定 + 签名日志 |
| 工具入口 | 平台封禁 | 开源客户端 + 可自托管 |

### 5. CROPS 检查表

| 属性 | 检查问题 | 当前状态 | 改进 |
|------|---------|---------|------|
| Censorship Resistance | Agent 能否被单点下架？ | ⚠️ 依赖平台 | 开源客户端 + DID 身份 |
| Open Source | 关键合约/策略是否可检查？ | ✅ 合约开源 | 评估集和路由策略也开源 |
| Privacy | 数据是否最小化？ | ⚠️ 部分 | 本地优先 + 分层脱敏 |
| Security | session key 权限是否受限？ | ✅ 有策略 | 增加紧急停止 + 审计日志 |

### 6. 审计字段

```json
{
  "event": "sovereignty_check",
  "user_control": {
    "model_visible": true,
    "memory_manageable": true,
    "permissions_revocable": true,
    "data_exportable": true
  },
  "data_portability": {
    "formats": ["json", "vc", "signed_log"],
    "sensitivity_levels": ["public", "internal", "private", "secret"]
  },
  "censorship_resistance": {
    "fallback_models": 3,
    "identity_portable": true,
    "storage_decentralized": true
  },
  "timestamp": "2026-05-20T10:30:00Z"
}
```

## 验收标准

- [ ] User Control 五项检查全部可操作
- [ ] Data Portability 提供分层导出格式
- [ ] Model Choice 支持策略化选择
- [ ] Censorship Resistance 有 fallback 方案
- [ ] CROPS 检查表完整覆盖四个维度
