---
name: cascade-maintain
description: |
  链式维护：当一个源文件变更后，自动检测并更新所有下游关联文件。用户说"帮我维护一下"、"cascade 一下"、"同步一下目录"时触发。适用于 web3career-study-track 项目中任何可能导致多文件联动变更的场景。
---

# Cascade Maintain Skill

改了一个文件，链式更新所有下游关联文件。用户不需要记住影响范围，只需要说"帮我维护一下"。

## 触发场景

- 用户说"帮我维护一下"
- 用户说"cascade 一下"
- 用户说"同步一下目录"
- 用户说"看看有没有要更新的"

## 工作流程

### Step 1：检测变更源

用 `git diff` 和 `git status` 扫描当前状态，根据结果进入不同模式：

**模式 A：被动追踪**（git status 有变更）

识别变更属于哪个源头：

| 变更文件模式 | 归属变更源 |
|-------------|-----------|
| `pre_study/*/README.md` | 预习笔记完成 |
| `daily-log/*/YYYY-MM-DD.md` | 每日收尾 |
| `idea/skills/*/SKILL.md` | Skill 迭代 |
| `CLAUDE.md` 或 `steering.md` | 规范同步 |
| `README.md` 或 `GUIDE.md` | 结构变更 |
| 新建周目录 | 跨周切换 |

只检查对应链路的下游文件。

**模式 B：主动巡检**（git status 干净）

遍历所有 6 条链路，逐一检查一致性。重点检查：
- 周索引中的活动状态是否与实际参加情况一致
- 日索引中的任务状态是否与日志标记一致
- pre_study 状态标记是否与实际完成数一致
- CLAUDE.md 与 steering.md 是否对称

### Step 2：按链路逐一检查

根据识别到的变更源，按对应链路检查每个下游文件：

---

#### 链路 A：预习笔记完成

```
变更源: pre_study/<module>/<Topic>/README.md
↓
1. pre_study/__index__.md          → 对应行状态 ⚪→✅ + 总进度 +1
2. README.md                       → badge 进度 +1 + highlights 数字 +1
                                      + progress 表对应行 +1 + 合计 +1
3. daily-log/week-N/YYYY-MM-DD.md  → "今天做了什么"追加一条
                                      + 产出表追加 2 行（笔记 + 练习）
4. daily-log/.../__index__.md      → 状态标记更新
5. memory/project_prestudy_status.md → 进度数字 +1 + 最新主题更新
6. git commit                      → study(<scope>): ...
```

检查项：
- [ ] `__index__.md` 里该模块状态是否与实际一致？
- [ ] `README.md` 的 badge / highlights / progress 表 / 合计四处数字是否一致？
- [ ] 当日日志里是否记录了这个产出（"做了什么" + 产出表）？
- [ ] memory 里的进度数字是否准确？
- [ ] 是否需要拆分 commit（每模块一个）？

---

#### 链路 B：每日收尾

```
变更源: daily-log/week-N/YYYY-MM-DD/YYYY-MM-DD.md
↓
1. daily-log/.../__index__.md      → 标记 🟢 已完成
2. daily-log/week-N/__index__.md   → 周进度条更新
3. git commit                      → log(week-N): ...
```

检查项 — 状态同步：
- [ ] 日索引任务状态是否与日志标记一致？
- [ ] 周索引活动状态是否与实际参加情况一致？
- [ ] 周索引任务状态是否与日索引一致？

检查项 — 内容完整性（对比 git log 与日志内容）：
- [ ] 当天 git log 中的 commit 是否都在日志"今天做了什么"里有记录？
- [ ] 产出表是否覆盖了当天所有实际产出（含新增目录、skill、reference 等）？
- [ ] "收获/卡点"是否覆盖了当天的关键发现（不遗漏重要迭代）？
- [ ] "明天打算"是否包含了当天产生的新行动项？

---

#### 链路 C：规范同步

```
变更源: CLAUDE.md 或 steering.md
↓
1. 另一个文件 → 保持对称
   - CLAUDE.md 改了 → steering.md 跟着改
   - steering.md 改了 → CLAUDE.md 跟着改
   - 差异仅在于：Claude Code 行为约定 vs Kiro 行为约定
2. memory/ → 如涉及行为偏好，更新 feedback 记忆
```

检查项：
- [ ] 两个文件的核心约束是否一致？
- [ ] "行为约定"部分的差异是否仅限于工具名？
- [ ] Learning Agent Prompt 部分是否同步？

---

#### 链路 D：Skill 迭代

```
变更源: idea/skills/<name>/SKILL.md
↓
1. idea/reference/case/            → 新案例归档
2. idea/reference/eval/            → 评估规范更新
3. idea/README.md                  → 如有结构变化
4. memory/                         → 技能经验沉淀
```

检查项：
- [ ] SKILL.md 的 description 是否足够清晰（触发条件）？
- [ ] 测试案例是否归档到 case/？
- [ ] 评估标准是否更新到 eval/？

---

#### 链路 E：结构变更

```
变更源: README.md / GUIDE.md / 新增目录
↓
1. README.md                       → 目录树同步
2. memory/                         → 相关记忆更新
3. git commit                      → docs: ...
```

检查项：
- [ ] README 的目录树是否反映最新结构？
- [ ] 新目录是否有 README.md 说明？
- [ ] memory 索引是否需要更新？

---

#### 链路 F：跨周切换

```
变更源: 进入新一周
↓
1. daily-log/week-N/WEEK.md        → 新周计划
2. daily-log/week-N/__index__.md   → 新周索引
3. daily-log/week-(N-1)/__index__.md → 上周收尾检查
4. CLAUDE.md 当前阶段              → 阶段标记更新
```

检查项：
- [ ] 上周所有 daily-log 是否都标记完成？
- [ ] 新周的 WEEK.md 目标是否已定义？
- [ ] CLAUDE.md 的"当前阶段"是否更新？

---

### Step 3：执行更新

对每个需要更新的文件：
1. 先读取当前内容
2. 生成变更建议，展示给用户确认
3. 用户确认后执行 Edit

### Step 4：提交

按模块分组 commit，格式 `<type>(<scope>): <subject>`，等待用户确认后 push。

## 约束

- **不要假设**——如果检测不到变更源，问用户
- **先展示再执行**——每个文件的变更建议先给用户看
- **不要过度更新**——只动链路上的文件，不顺手改无关内容
- **保持对称**——CLAUDE.md 和 steering.md 必须同步
- **进度数字要准**——memory 里的进度必须数 actual 已完成的模块数，不靠猜
