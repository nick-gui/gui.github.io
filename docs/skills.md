# Skills 使用手册

收集各种好用的 Cursor Agent Skill，包括安装方法、核心功能介绍和使用技巧。

> **什么是 Skill？** Skill 是一种可移植的、版本化的知识包，以 `SKILL.md` 文件定义，教 AI Agent 如何执行特定领域的任务。Cursor 启动时会自动发现并加载已安装的 Skill，Agent 会根据上下文自动判断何时调用。

---

## 目录

- [Superpowers — 完整的 AI 开发工作流框架](#superpowers--完整的-ai-开发工作流框架)

---

## Superpowers — 完整的 AI 开发工作流框架

> GitHub 176k+ Stars | 作者: Jesse Vincent ([@obra](https://github.com/obra)) | [仓库地址](https://github.com/obra/superpowers)

Superpowers 不只是一个 Skill，而是一套**完整的软件开发方法论**。它通过 14 个可组合的 Skill，将 AI 编程助手从"快速打字员"变成"有纪律的工程搭档"。

### 安装

**Cursor（推荐方式）**

在 Agent 聊天窗口中输入：

```text
/plugin-add superpowers
```

Cursor 会自动下载并激活插件。

**验证安装**

开启一个新的 Agent 会话，询问：

```text
你有哪些 superpowers skills？
```

Agent 应该能列出所有可用的 Skill。

**更新**

```text
/plugin-update superpowers
```

**卸载**

```text
/plugin-remove superpowers
```

### 核心理念

Superpowers 的核心思想是：**先想清楚，再动手**。

传统方式：用户说"帮我做 X" → Agent 立即开始写代码 → 代码质量参差不齐

Superpowers 方式：用户说"帮我做 X" → 头脑风暴 → 制定计划 → TDD 实现 → 代码审查 → 验证完成

### 14 个核心 Skill 一览

#### 工作流程类

| Skill | 用途 | 何时触发 |
|---|---|---|
| `using-superpowers` | 技能系统入门介绍 | 会话开始时 |
| `brainstorming` | 苏格拉底式设计探索，将模糊想法变成具体设计 | 任何创造性工作之前（做功能、加组件、改行为） |
| `writing-plans` | 生成详细实施计划，每个任务 2-5 分钟粒度 | 设计方案获批后 |
| `executing-plans` | 按批次执行计划，设有人工检查点 | 有书面计划需要执行时 |
| `subagent-driven-development` | 每个任务派遣新 subagent，两阶段审查 | 执行计划时（替代 executing-plans） |
| `dispatching-parallel-agents` | 并发派遣多个 subagent 处理独立任务 | 面对 2+ 个可并行的独立任务时 |

#### 开发实践类

| Skill | 用途 | 何时触发 |
|---|---|---|
| `test-driven-development` | 严格的 RED-GREEN-REFACTOR 循环 | 实现任何功能或修复 bug 时 |
| `systematic-debugging` | 四阶段根因分析流程 | 调查 bug 或故障时 |
| `verification-before-completion` | 用证据证明问题确实已修复 | 宣布"完成"之前 |
| `using-git-worktrees` | 并行开发分支，隔离工作空间 | 需要隔离环境时 |

#### 协作类

| Skill | 用途 | 何时触发 |
|---|---|---|
| `requesting-code-review` | 提交审查前的自检清单 | 请求人工审查之前 |
| `receiving-code-review` | 技术严谨地回应反馈，拒绝盲目执行 | 收到审查意见后 |
| `finishing-a-development-branch` | 引导合并/PR/清理决策 | 实现完成、测试通过后 |
| `writing-skills` | 创建新的自定义 Skill | 需要编写自定义 Skill 时 |

### 典型工作流

一个完整的功能开发流程通常是这样的：

```
用户："帮我实现用户认证功能"
         │
         ▼
  ┌─ brainstorming ─┐
  │ 探索需求和意图     │
  │ 提出 2-3 个方案    │
  │ 讨论权衡取舍       │
  │ 获得用户批准       │
  └────────┬─────────┘
           ▼
  ┌─ writing-plans ──┐
  │ 拆分为 2-5 分钟任务 │
  │ 每任务含文件路径    │
  │ 包含验证步骤       │
  └────────┬─────────┘
           ▼
  ┌─ TDD + subagent ─┐
  │ 写失败测试 → 红灯   │
  │ 写最少代码 → 绿灯   │
  │ 重构 → 提交        │
  │ （每任务独立subagent）│
  └────────┬─────────┘
           ▼
  ┌─ code-reviewer ──┐
  │ 规范合规检查       │
  │ 代码质量审查       │
  └────────┬─────────┘
           ▼
  ┌─ finishing ───────┐
  │ 合并 / 提 PR / 清理 │
  └───────────────────┘
```

### 重点 Skill 详解

#### brainstorming — 先想后做

这是 Superpowers 最重要的 Skill。铁律：

> **在展示设计方案并获得用户批准之前，不要写任何代码、搭建任何项目、采取任何实现行动。**

Agent 会：
1. 先阅读项目上下文（文件、文档、最近提交）
2. 逐个提出澄清问题
3. 提出 2-3 个方案及权衡分析
4. 分段展示设计方案供审批
5. 批准后才转入实现

**使用技巧**：当 Agent 开始提问而不是直接写代码时，不要急着说"直接做就行"。回答它的问题，审批设计方案，你会发现后续实现的质量明显提升。

#### test-driven-development — 测试驱动开发

铁律：

> **没有失败的测试，就没有生产代码。先写了代码再补测试？删掉重来，没有例外。**

严格执行 RED-GREEN-REFACTOR 循环：
1. **RED** — 写一个会失败的测试，确认它确实失败了
2. **GREEN** — 写刚好够让测试通过的最少代码
3. **REFACTOR** — 在测试保持绿灯的前提下重构
4. **COMMIT** — 提交

#### systematic-debugging — 系统化调试

铁律：

> **不做根因调查就不要修 bug。越是时间紧迫越要遵守这条规则。**

四阶段流程：
1. **根因调查** — 追踪问题源头
2. **假设形成** — 提出可能的原因
3. **定向修复** — 针对根因修复，而非治标
4. **验证** — 用证据证明修复有效

### 使用技巧

1. **技能优先级**：遇到任务时，先用流程类 Skill（brainstorming、debugging），再用实现类 Skill
2. **刚性 vs 柔性**：TDD 和 debugging 是**刚性**的——严格按流程来，不要绕过纪律。brainstorming 和 planning 是**柔性**的——可以根据项目实际调整
3. **手动触发**：如果 Agent 没有自动激活某个 Skill，可以在 Agent 聊天中输入 `/skill-name` 手动触发
4. **Skill 不生效时**：
   - 开启一个新的 Agent 会话（`Cmd+L` / `Ctrl+L`）
   - 显式请求："使用 brainstorming skill"
   - 在设置中确认插件已安装
   - 运行 `/plugin-update superpowers` 更新

### 常见问题

**Q: Superpowers 只能在 Cursor 中使用吗？**

不是。Superpowers 的 Skill 本质是 Markdown 文件，支持 Claude Code、Cursor、Codex CLI、OpenCode、Gemini CLI 等多个平台。在 Cursor 中通过插件市场安装最方便。

**Q: 安装后 Agent 没有自动使用 Skill？**

确保在 Agent 聊天界面中操作（不是 Composer 或 inline chat）。Superpowers 针对 Agent 模式优化。如果仍不生效，尝试重启 Cursor 或更新插件。

**Q: 会不会让开发变慢？**

初期流程确实更多，但 brainstorming 减少了返工，TDD 减少了 bug，计划拆分让实现更聚焦。整体效率通常是提升的。

### 参考链接

- [GitHub 仓库](https://github.com/obra/superpowers)
- [Cursor 插件市场页面](https://cursor.com/marketplace/superpowers)
- [官方安装文档](https://mintlify.com/obra/superpowers/installation/cursor)
- [Cursor Agent Skills 官方文档](https://cursor.com/docs/skills)
