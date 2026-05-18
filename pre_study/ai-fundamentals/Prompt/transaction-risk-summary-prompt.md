# Transaction Risk Summary Prompt ｜ 交易风险摘要

> 关联章节：[Prompt](./README.md) · 状态：⚪ 未完成

## 练习目标

用 Structured Output 强制模型按固定字段返回，再用边界 case 测试模型的判断稳定性。重点不是 prompt 写得多好，而是模型能否稳定区分风险等级和不确定性。

## 任务描述

写一个"交易风险摘要"prompt。

输入包括：交易目标地址、函数名、参数、资产变化、simulation 结果、用户原始意图。

## 输出要求

要求模型输出固定 JSON：

```json
{
  "summary": "",
  "asset_changes": [],
  "permissions_changed": [],
  "risk_level": "low / medium / high",
  "requires_human_approval": true,
  "uncertainties": [],
  "recommended_user_checks": []
}
```

## 测试用例

准备三组测试：

1. **普通转账** — 验证基础解析能力
2. **无限授权** — 验证权限风险识别
3. **目标地址与用户意图不匹配** — 验证异常检测能力

## 验收标准

- [ ] Prompt 输出为固定 JSON schema
- [ ] 三组测试用例均能稳定运行
- [ ] 模型能区分 risk_level 等级
- [ ] uncertainties 字段能正确标记不可验证信息

## 完成记录

> 完成后在此处填写日期、测试结果、关键收获。

-
