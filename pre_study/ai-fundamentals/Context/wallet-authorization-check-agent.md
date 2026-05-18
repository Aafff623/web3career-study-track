# Wallet Authorization Check Agent ｜ 钱包授权检查 Agent

> 关联章节：[Context](./README.md) · 状态：⚪ 未完成

## 练习目标

强迫你区分信息来源和时效：哪些必须实时查询、哪些可以缓存、哪些必须标记为不可信。这是 Context Engineering 在 AI×Web3 场景里的具体应用。

## 任务描述

为"钱包授权检查 Agent"设计一份 context spec。

场景：用户问"这个 dApp 要我 approve，可以签吗？"

## 需要列出的上下文

1. chain id 和当前区块
2. token 合约、spender 地址、approve 数量
3. 用户当前 allowance 和余额
4. spender 是否在可信列表
5. simulation 或静态检查结果
6. dApp 页面提供的说明，标记为不可信外部内容
7. 用户本次意图

## 输出要求

写清楚每个字段的来源分类：

| 分类 | 说明 |
|------|------|
| 实时查询 | 必须每次从链上获取 |
| 可缓存 | 可以定期刷新，但需标注过期时间 |
| 不可信外部内容 | 必须标记，不能被模型当成事实 |

## 验收标准

- [ ] 所有字段均已分类
- [ ] 链上状态（allowance、余额）标记为实时查询
- [ ] 可信列表标记为可缓存
- [ ] dApp 页面标记为不可信
- [ ] 有 context spec 文档输出

## 完成记录

> 完成后在此处填写日期、产出物链接、关键收获。

-
