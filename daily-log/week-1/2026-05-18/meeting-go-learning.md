# Go Learning 任务推进与答疑

> 类型：线上直播 · 日期：2026-05-18 · Week 1

## 核心内容

### OpenClaw / Hermes / Claude Code / Codex 对比

| 工具 | 定位 | 垂直领域 |
|------|------|---------|
| Claude Code | Anthropic 官方 CLI，对话式编码 | 通用编码、代码审查、项目理解 |
| Codex CLI | OpenAI 官方 CLI，异步任务执行 | 通用编码、批量任务、代码生成 |
| OpenClaw | Agent 执行框架，进入执行层 | Agent 工作流、工具调用、链上交互 |
| Hermes | 长期学习 Agent，跨 session 状态管理 | 学习流程、知识沉淀、持续追踪 |

关键区别：
- Claude Code / Codex 是"编码 CLI"——你给指令，它生成代码，人在回路中审查
- OpenClaw / Hermes 是"Agent 框架"——模型自主规划、调用工具、管理状态，人设置边界后让出执行权

### 安装与配置要点

- OpenClaw / Hermes 需要 API Key（OpenAI 或 Anthropic）
- WSL 环境下 Claude Code 可直接运行
- 接入 Telegram 需要 Bot Token + Webhook 配置

## 行动项

- [ ] 使用 WSL 里的 Claude Code，喂给足够的 context 去安装属于自己的 OpenClaw / Hermes
- [ ] 对接到自己的 Telegram
- [ ] 测试成功后记录 Tx Hash 和配置过程
