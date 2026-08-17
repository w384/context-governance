---
name: context-governance
description: 维护 Codex 上下文架构——常驻规则最小化、项目知识项目化、专项能力按需加载、历史记录归档化，并把新项目初始化进这套结构。当需要治理 / 重构 / 优化 / 压缩 Codex 全局上下文（AGENTS.md、MEMORY.md、memory_summary.md、降低 token、上下文分层），或初始化新项目 / 安装 Agent 模板 / 同步项目知识时使用。覆盖分层模型（全局 AGENTS / MEMORY / memory_summary / 项目 AGENTS / docs / .learnings / workflows / history）与「备份 → 测量 → 迁移 → 压缩 → 验证」工作流。
---

# 上下文治理（Context Governance）

把 Codex 上下文拆成分层，让常驻上下文保持最小，同时不丢失规则、偏好、项目知识与历史。

> 本文件是 SKILL.md 的中文译本，仅用于阅读交流；Codex 实际自动加载的是 SKILL.md。

## 分层模型

每一层只放一类内容：

| 层 | 位置 | 承载内容 |
|---|---|---|
| 常驻规则 | `$CODEX_HOME/AGENTS.md` | 每轮都必须遵守的最小规则 |
| 长期偏好 | `$CODEX_HOME/memories/MEMORY.md` | 关于用户、长期值得记住什么 |
| 记忆索引 | `$CODEX_HOME/memories/memory_summary.md` | 极短导航摘要 |
| 项目规则 | 项目 `AGENTS.md` | 在该项目必须遵守什么 |
| 项目知识 | 项目 `README.md`、`docs/` | 项目知道什么 |
| 项目经验 | 项目 `.learnings/` | 项目学到了什么 |
| 专项能力 | `$CODEX_HOME/skills/`、`$CODEX_HOME/workflows/` | 某类任务怎么做 |
| 历史归档 | `$CODEX_HOME/memories/raw_memories.md`、`$CODEX_HOME/memories/rollout_summaries/`、项目 `devlog/` | 过去发生过什么 |

`$CODEX_HOME` 指 Codex 主目录（未设置时默认 `~/.codex`）。

**判据**：放进常驻层之前先问一句——它值得每一轮都被重新阅读吗？不值得，就不要放进常驻层。

## 工作流

### 1. 治理（重构现有上下文）

当需要降低固定输入 token 或重新分层时使用。按 [references/governance-procedure.zh-CN.md](references/governance-procedure.zh-CN.md) 执行。顺序不可跳过：先备份 → 测量 → 迁移（A/B/C）→ 压缩 → 验证。

### 2. 初始化新项目（一次性同步）

当初始化项目或安装 Agent 模板时使用。按 [references/project-init-sync.zh-CN.md](references/project-init-sync.zh-CN.md) 执行。

## 禁止事项（永远不要做）

- 不要删除所有规则；目标是分层，不是清空。
- 不要把一切重新塞回一个超长文件。
- 不要为了省 token 而删除安全边界。
- 不要让 MEMORY 保存项目 Wiki。
- 不要通过删除插件缓存来「优化上下文」。
- 不要只凭文件大小推断 token；要在新线程上实测。

## 关键路径

- 常驻：`$CODEX_HOME/AGENTS.md`、`$CODEX_HOME/memories/MEMORY.md`、`$CODEX_HOME/memories/memory_summary.md`
- 项目模板：`$CODEX_HOME/agent-templates/project-agent/`
- 专项能力：`$CODEX_HOME/skills/`、`$CODEX_HOME/workflows/`
- 历史归档：`$CODEX_HOME/memories/raw_memories.md`、`$CODEX_HOME/memories/rollout_summaries/`