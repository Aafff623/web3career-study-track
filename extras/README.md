# extras / 加餐学习

> 课程外自己吸收的学习资料 —— B 站视频、技术博客、Twitter、Podcast、官方文档。
> 与 `pre_study/`（课程内预习）和 `daily-log/`（课程内打卡）形成互补，专门沉淀"溢出"的内容。

## 主题

| 目录 | 范围 |
|---|---|
| [`web3/`](./web3/) | Web3 基础、协议、DeFi、NFT、钱包、L2、隐私 |
| [`ai/`](./ai/) | AI 基础、Agent、LLM、训练/推理、Workflow、Prompt |
| [`crossover/`](./crossover/) | AI × Web3 交叉点：Agentic Commerce、链上 AI、Smart Account、AI Wallet |

## 笔记规范

### 展开笔记

值得深入消化的资料独立成 `.md`，文件名英文 slug（如 `vitalik-rollup-centric-roadmap.md`），顶部填元数据：

```yaml
---
source: <URL>
type: video | blog | thread | podcast | doc | repo
author: <作者 / UP 主 / 频道>
length: <时长 / 字数 / 推数>
tags: [tag1, tag2]
read_at: YYYY-MM-DD
rating: ⭐⭐⭐⭐ / 5
---
```

正文按"概要 → 关键观点 → 我的思考 → 延伸链接"组织。

### 简短收藏

不值得展开的，直接挂在对应主题的 `README.md` 的「简短收藏」清单：

- `[资料标题](URL) — 一句话说明 · YYYY-MM-DD`

## 与 hackathon 的关系

如果某条资料启发了 hackathon 方向，加 `tag: hackathon-input`，并在 `hackathon/` 对应文档里反向引用。
