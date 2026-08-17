# Context Governance：上下文治理

通过把不同类型的知识放入正确的生命周期层，保持长期 Codex 与 AI Agent 上下文精简、稳定、可维护。

[English README](README.md)

## 为什么上下文会越来越重？

长期使用 Codex 或其他 Agent 时，规则、偏好、项目笔记、专项指令和历史记录都会不断积累。问题不是这些知识没有价值，而是它们经常被逐步复制进一些每轮都会读取的文件。

结果是：上下文重复读取成本越来越高，结构越来越难导航，不相关的细节也会互相竞争，导致 Agent 的长期行为更不稳定。

Context Governance 保留这些知识，但把它们按生命周期分开：

```text
Global Rules（全局规则）
    ↓
Memory（长期偏好）
    ↓
Project Knowledge（项目知识）
    ↓
Skills（专项能力）
    ↓
History（历史归档）
```

核心判断只有一句：

> Is this worth re-reading every single turn?
>
> 它值得每一轮都重新读取吗？

如果不值得，就不应该放在常驻上下文中。

这不是减少知识，而是让知识保持可用，并放到正确的生命周期。

## Before / After

| Before：混在一起 | After：按生命周期分层 |
|---|---|
| AGENTS.md、MEMORY.md、项目规则、专项指令和历史一起增长。 | 常驻上下文只保留每轮都必须生效的规则与偏好。 |
| 项目细节被重复写入全局记忆。 | 项目知识留在项目内。 |
| 能力和工作流被提前全部写入上下文。 | 需要某类任务时再加载对应 Skill 与工作流。 |
| 旧决策与当前指导混杂。 | 历史归档，相关时再查阅。 |

## Features

- 用分层模型管理常驻规则、长期偏好、项目知识、专项能力和历史。
- 提供可重复的 **备份 → 测量 → 迁移 → 压缩 → 验证** 治理流程。
- 提供一次性的新项目初始化清单。
- 防止为了省 token 删除安全规则、把项目 Wiki 放入 MEMORY，或仅凭文件大小推断 token。
- 提供无需运行时依赖、可被 Codex 自动发现的 SKILL.md。

## Why this exists

很多上下文方法关注于增加记忆、检索更多信息或压缩 Prompt。Context Governance 从更早的一步开始：先决定哪些信息值得永久占据上下文，哪些信息应该保持可用但按需加载。

它是一套文档化方法，也是一个 Codex Skill，适合维护长期 Agent 工作空间，并希望在继续添加内容前先审查上下文架构的开发者。

## Architecture

```text
Codex
  │
  ├── Resident Context（常驻上下文）
  │   ├── Global Rules（全局规则）
  │   └── Long-term Preferences（长期偏好）
  │
  ├── Project Context（项目上下文）
  │   ├── Project Rules（项目规则）
  │   ├── Project Knowledge（项目知识）
  │   └── Project Learnings（项目经验）
  │
  ├── Skills and Workflows（专项能力与工作流）
  │
  └── Archive（历史归档）
      └── History and past decisions（历史与过去的决策）
```

可复制的 Before / After 图和分层说明见 [docs/context-architecture.md](docs/context-architecture.md)。

## Installation

把仓库复制到 Codex 的 Skill 目录：

### macOS / Linux

```bash
mkdir -p "\${CODEX_HOME:-$HOME/.codex}/skills"
cp -R context-governance "\${CODEX_HOME:-$HOME/.codex}/skills/context-governance"
```

### Windows PowerShell

```powershell
$codexHome = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $HOME '.codex' }
New-Item -ItemType Directory -Force -Path (Join-Path $codexHome 'skills') | Out-Null
Copy-Item -Recurse -Force '.\\context-governance' (Join-Path $codexHome 'skills\\context-governance')
```

下次运行时，Codex 会自动发现 SKILL.md。

## Usage

治理已有上下文：

```text
Use context-governance to review my current Codex context.
Identify what belongs in resident context, project knowledge, skills, and archive.
Back up files first, measure the baseline, then propose a minimal migration.
```

初始化项目：

```text
Use context-governance to initialize this project into the layered context structure.
```

Skill 覆盖两类工作流：

- [治理已有上下文](references/governance-procedure.md)
- [初始化新项目](references/project-init-sync.md)

## Example

完整迁移案例见 [examples/context-cleanup-case.md](examples/context-cleanup-case.md)。它展示如何在不删除有用知识的前提下，拆分混合的 AGENTS.md、MEMORY.md、项目规则、Skills 与历史。

## Comparison with alternatives

| 方法 | 主要问题 | Context Governance 的区别 |
|---|---|---|
| Memory 系统 | 哪些事实应该保存或检索？ | 在检索之前，先定义哪些信息可以长期留在常驻层。 |
| RAG 系统 | 应该检索哪些外部资料？ | 不负责检索文档或建立索引，而是治理 Agent 上下文的生命周期。 |
| Prompt 压缩 | 如何更紧凑地表达同一批输入？ | 不压缩内容，而是先判断内容是否应该进入固定输入。 |
| 项目模板 | 项目一开始应该有哪些文件？ | 增加生命周期治理，避免模板再次变成永久的混合文件。 |

这些方法可以互相配合。Context Governance 是围绕它们的架构与审查方法，而不是替代品。

## Measurement note

本仓库不发布一个适用于所有环境的 token 节省数字。上下文大小取决于模型、客户端、启用的 Skills、项目和线程历史。

有意义的基线应在迁移前后分别开启新线程，记录实际的输入 token、缓存输入 token、上下文占用、延迟，以及关键规则是否仍然生效。不要仅凭文件大小推断 token 使用量。

## Roadmap

- **v0.1** — 核心 Codex Skill、分层模型、治理流程和项目初始化清单。
- **下一步** — 发布小型、可复现的测量工作表，并提供一个有文档记录的工作空间基线案例。
- **后续** — 在保持文档化、模型无关和范围克制的前提下，增加不同 Agent 配置的迁移案例。

## License

MIT，见 [LICENSE](LICENSE)。

## Repository metadata

建议的 GitHub description：

> Keep Codex context lean by managing rules, memory, project knowledge, skills, and history with a layered governance model.

建议 topics：

codex · openai-codex · ai-agent · agent-context · context-engineering · context-management · llm-agent · developer-tools · prompt-engineering

v0.1.0 发布说明见 [CHANGELOG.md](CHANGELOG.md)。
