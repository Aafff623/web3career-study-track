# Git Commit 规范

> 针对 AI Web3 School BootCamp 4 周共学营的提交节奏设计的 个性化的 commit Agent参考的git提交规范

## Commit 格式

```
<type>(<scope>): <subject>
```

- `type`：提交类型（见下方）
- `scope`：可选，影响范围（日期/模块名）
- `subject`：简短描述，中英文均可

## Type 类型

| type | 用途 | 频率 |
|------|------|------|
| `log` | 每日学习笔记、Co-Learning 记录 | 每天 |
| `task` | 任务完成、打卡提交、交付证明 | 每天 |
| `study` | 预习资料同步、知识笔记补充 | 按需 |
| `feat` | Hackathon 项目新功能 | Week 3-4 |
| `fix` | 项目 bug 修复 | Week 3-4 |
| `contract` | 智能合约相关（部署、测试、验证） | Week 3-4 |
| `docs` | README、规范文件、文档更新 | 按需 |
| `chore` | 仓库结构调整、配置变更 | 按需 |

## 示例

### 每日打卡（最高频）

```
log(05-18): AI Agent 入门课程笔记
log(05-20): Web3 运行原理 + Co-Learning 讨论
task(05-18): 完成 Day2 打卡任务
task(05-22): Week 1 优秀笔记提交
```

### 预习资料

```
study: 同步 AI 基础模块笔记
study(RAG): 补充检索增强生成笔记
```

### Hackathon 项目

```
feat: 初始化 Agent Wallet 项目结构
contract: 部署 SessionKey 合约到 Sepolia
contract: 添加测试用例 - Session Key 过期验证
fix: 修复 Gas 估算逻辑
feat: 完成 Demo 页面
```

### 文档与维护

```
docs: 更新 README 进度
docs: 添加 Hackathon proposal
chore: 调整目录结构
```

## 规则

1. **一天可以多次提交**，按内容类型分开（笔记一次、任务一次）
2. **scope 用日期**时写 `MM-DD` 格式（如 `05-18`），不用写年份
3. **subject 保持一行**，不超过 50 字
4. **有 Tx Hash 时**在 commit body 里附上：
   ```
   task(06-10): 提交最终项目合约
   
   Tx Hash: 0x1234...abcd
   Network: Sepolia
   Contract: 0xabcd...1234
   ```
5. **不要把多天的内容合成一个 commit**——git log 就是你的学习时间线

## 快速参考

```bash
# 每日笔记
git add daily-log/2026-05-18/
git commit -m "log(05-18): AI Agent 入门课程笔记"

# 任务打卡
git commit -m "task(05-18): 完成 Day2 打卡"

# 项目代码
git add hackathon/
git commit -m "feat: Agent Wallet MVP 完成"

# 推送
git push
```
