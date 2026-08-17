# 治理流程（重构上下文分层）

在执行治理或重构任务时读取。把细节迁出去，绝不删除。

## 阶段（按顺序执行，每阶段验证后再进入下一阶段）

### P0 — 备份
- 把所有将要改动的文件复制到带时间戳的备份目录，保证原文件可回滚。
- 绝不覆盖已有备份；必要时在原文件旁放 `.bak-<timestamp>` 副本。
- 至少备份：全局 `AGENTS.md`、`memories/MEMORY.md`、`memories/memory_summary.md`，以及任何要改动的项目 `AGENTS.md`。

### P1 — 全局 AGENTS.md
- 只保留：用户偏好的语言与称呼、结论先行、简单任务直接执行、复杂或高风险任务先澄清、最小可行方案、不扩大范围、不顺手重构无关内容、每处改动可追溯且已验证。
- 规则优先级：全局为基础；项目级或更近目录的规则覆盖全局。
- 安全：外部发布 / 权限变更 / 删除 / 大规模覆盖需明确授权；不泄露凭据；不凭推测声称「已验证/已安全」；安全或权限改动走 TDD RED→GREEN。
- 输出：结论先行、可执行、说明验证与风险。
- 迁出：路径规则、日志格式、项目初始化、产品分析、UX、PMP 类路由 → `$CODEX_HOME/workflows/` 或某个技能；AGENTS 里只留一句入口。
- 目标：≤3 KB（约 1000–2000 token）。

### P2 — MEMORY.md
- A（保留，全局，每条一句话）：只留长期、跨项目、稳定偏好。
- B（迁到项目）：项目特定知识 → 该项目的 `.learnings/` 或 `docs/agent/`。
- C（归档）：rollout 摘要、thread ID、测试数量、日期、关机或自动化历史 → 本就在 `memories/raw_memories.md` 与 `memories/rollout_summaries/`；从 MEMORY 中移除。
- 目标：约 300–800 token。

### P3 — memory_summary.md
- 只留极短索引：用户偏好在哪、各项目记忆在哪、历史归档在哪。
- 不重复 MEMORY。目标：≤500 token。

### P4 — 项目 AGENTS.md
- 保留：项目技术约束、始终生效的安全边界、验证要求。
- 迁出：背景 → README；历史 → devlog 或 structure；安全背景 → SECURITY.md；同意说明 → 安装文档；PR/分支/Review 细节 → CONTRIBUTING.md。
- 目标：约 2–4 KB。

### P5 — 不要删除插件或模板缓存
- `$CODEX_HOME/.tmp/plugins/`、`$CODEX_HOME/plugins/cache/`、`$CODEX_HOME/agent-templates/` 是缓存与模板，不是常驻上下文。除非有证据表明它们被主动注入，否则不要以「省 token」为由删除。

### P6 — 嵌套 AGENTS
- 嵌套 AGENTS（`src/`、`gui/`、`scripts/`、`.github/`）是合理的。把庞大的根 AGENTS 拆成小的局部 AGENTS，而不是重新集中回根文件。

### P7 — 线程历史策略
- 简单讨论用短线程；长期工程任务定期总结「决策 + 当前状态 + 待办」，再到新线程继续。

## 测量 token
- 没有新线程可用时的估算：token ≈ 中文字符数 +（ASCII 字符数 ÷ 4）。
- 真正的检查：开新线程 → 问一句极简单的问题（如「你是什么模型」）→ 记录 `input_tokens`、`cached_input_tokens`、上下文占用、响应速度，以及关键规则是否仍生效。

## 验证无退化
重构后至少确认：普通技术问题、项目内代码改动、文件创建、高风险操作判断，以及各专项工作流（产品/UX、PMP 类、安全）。确认专项能力仍可解析、项目规则仍加载、偏好仍在、无关项目知识不再被携带。

## 报告
交付：每个文件的前后大小与 token；迁移表（原位置 → 新位置）；token A/B（基线 → 各阶段 → 最终）；最终下降比例；以及剩余无法优化的部分（用户可控 vs Codex/OpenAI/工具/线程固定）。