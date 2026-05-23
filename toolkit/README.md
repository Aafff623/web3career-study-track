# toolkit / 工具箱

> 配合学习和项目使用的辅助工具与方法论沉淀。
> 与 `extras/`（学习内容）互补 —— extras 记录"学了什么"，toolkit 记录"怎么做"。

## 模块

| 目录 | 范围 |
|---|---|
| [`tools/`](./tools/) | AI 工具 · 提效工具 · 开发辅助 |
| [`workflows/`](./workflows/) | 工作流 · 方法论 · 经验分享 |

## 记录规范

### 工具条目

值得展开介绍的工具独立成 `.md`，文件名英文 slug（如 `claude-code-tips.md`），顶部元数据：

```yaml
---
name: <工具名>
url: <官网 / 文档 URL>
type: ai-tool | productivity | dev-tool | research
added: YYYY-MM-DD
tags: [tag1, tag2]
rating: ⭐⭐⭐⭐ / 5
---
```

正文按"是什么 → 怎么用 → 实际体验 → 适合场景"组织。

### 工作流条目

值得展开的工作流 / 方法论独立成 `.md`，顶部元数据：

```yaml
---
name: <工作流名称>
type: workflow | methodology | template
added: YYYY-MM-DD
tags: [tag1, tag2]
---
```

正文按"背景 → 流程步骤 → 注意事项 → 适用场景"组织。

### 简短收藏

不值得展开的，直接挂在对应子目录的 `README.md` 简短收藏清单：

- `[工具/方法名](URL) — 一句话说明 · YYYY-MM-DD`
