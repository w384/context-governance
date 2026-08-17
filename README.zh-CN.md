# context-governance

一个用于维持精简、分层式 Codex 上下文架构，并把新项目初始化进该结构的 Codex 技能。

## 它能做什么

- 让常驻上下文保持最小：精简的全局 `AGENTS.md`、简短的 `MEMORY.md`、只做导航的 `memory_summary.md`。
- 让各类知识各归其位：项目知识留在项目里，专项能力放在技能/工作流里，历史放进归档。
- 提供可复用的治理流程：备份 → 测量 → 迁移 → 压缩 → 验证。
- 提供新项目初始化的一次性同步清单。

对放进常驻上下文的一切内容，先问一句：

> 它值得每一轮都被重新阅读吗？不值得，就不要放进常驻层。

## 目录结构

- `SKILL.md` — 英文说明（正式版；Codex 自动发现的是这个文件）。
- `SKILL.zh-CN.md` — 中文译本。
- `references/governance-procedure.md` — 详细治理流程（英文）。
- `references/governance-procedure.zh-CN.md` — 中文译本。
- `references/project-init-sync.md` — 新项目同步清单（英文）。
- `references/project-init-sync.zh-CN.md` — 中文译本。
- `agents/openai.yaml` — 技能列表与标签的 UI 元数据。

所有路径统一使用 `$CODEX_HOME`（Codex 主目录，未设置时默认 `~/.codex`），因此该技能可跨机器移植。

## 安装

把本目录复制到你的 Codex 技能目录：

```bash
mkdir -p "$CODEX_HOME/skills"      # 未设置 CODEX_HOME 时为 ~/.codex/skills
cp -r context-governance "$CODEX_HOME/skills/"
```

Codex 会在下次运行时自动发现 `SKILL.md`。

## 触发场景

当需要以下操作时，Codex 会加载该技能：

- 治理、重构、优化或压缩 Codex 全局上下文（AGENTS.md、MEMORY.md、memory_summary.md、降低 token、上下文分层）；
- 初始化新项目或安装 Agent 模板。

## 许可证

MIT — 见 [LICENSE](LICENSE)。