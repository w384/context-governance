# 新项目初始化（一次性同步）

在初始化项目、安装 Agent 模板、或复制 project-agent 脚手架时执行。同步一次，之后项目保持自包含。

## 步骤
1. 确认当前目录是项目根。
2. 把整个模板 `$CODEX_HOME/agent-templates/project-agent/` 复制到项目根——不要手写一个删减版 AGENTS.md。
3. 模板包含：`AGENTS.md`、`README.md`、`.learnings/LEARNINGS.md`、`.learnings/ERRORS.md`、`docs/agent/workflows.md`、`docs/agent/memory-and-decisions.md`。
4. 若文件已存在，判断是否替换；「重新安装」请求意味着模板覆盖。
5. 填写项目 AGENTS.md 的占位：一句话定位、目标用户、当前阶段、成功标准、「当前不做」、权威来源、约束（必须保留 / 禁止改变 / 需确认）、工具路由、验证命令。
6. 让项目 AGENTS.md 指向全局 AGENTS.md 与记忆（模板默认已如此）。
7. 过程文件放 `work/`，交付物放 `outputs/`。
8. 在 `memories/memory_summary.md` 登记该项目的记忆位置。
9. 把每次创建 / 覆盖 / 复制写进项目变更日志（按路径与日志工作流）。
10. 若只要求初始化单个文件，就缩小范围；否则不要省略模板里的配套文件。