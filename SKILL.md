---
name: context-governance
description: Maintain a Codex context architecture — keep resident rules minimal, project knowledge project-local, capabilities on-demand, and history archived — and initialize new projects into that structure. Use when asked to govern, restructure, optimize, or compress Codex global context (AGENTS.md, MEMORY.md, memory_summary.md, token reduction, context layering), or to initialize a new project, install an agent template, or sync project knowledge. Covers the layered model (global AGENTS / MEMORY / memory_summary / project AGENTS / docs / .learnings / workflows / history) and the backup → measure → migrate → compress → verify workflow.
---

# Context Governance

Keep a Codex context in layers so resident context stays minimal without losing rules, preferences, project knowledge, or history.

## Layer model

Each layer holds exactly one kind of content:

| Layer | Location | Holds |
|---|---|---|
| Resident rules | `$CODEX_HOME/AGENTS.md` | Minimal rules every turn must obey |
| Long-term preferences | `$CODEX_HOME/memories/MEMORY.md` | What to remember about the user long-term |
| Memory index | `$CODEX_HOME/memories/memory_summary.md` | Very short navigation summary |
| Project rules | project `AGENTS.md` | What to obey in that project |
| Project knowledge | project `README.md`, `docs/` | What the project knows |
| Project learnings | project `.learnings/` | What the project learned |
| Capabilities | `$CODEX_HOME/skills/`, `$CODEX_HOME/workflows/` | How to do a class of task |
| History | `$CODEX_HOME/memories/raw_memories.md`, `$CODEX_HOME/memories/rollout_summaries/`, project `devlog/` | What happened |

`$CODEX_HOME` is the Codex home directory (defaults to `~/.codex` when unset).

**Litmus test** before putting anything in a resident layer: is this worth re-reading every single turn? If not, it does not belong in resident context.

## Workflows

### 1. Govern (restructure existing context)

Use when asked to lower fixed-input tokens or re-layer context. Follow [references/governance-procedure.md](references/governance-procedure.md). Never skip: back up first → measure → migrate (A/B/C) → compress → verify.

### 2. Initialize a new project (one-time sync)

Use when initializing a project or installing an agent template. Follow [references/project-init-sync.md](references/project-init-sync.md).

## Hard constraints (never do)

- Do not delete all rules; the goal is layering, not emptying.
- Do not consolidate everything back into one oversized file.
- Do not remove safety boundaries to save tokens.
- Do not store project wikis in MEMORY.
- Do not delete plugin caches to "optimize" context.
- Do not conclude a tool is missing from the outer tool list alone; runtime-enumerate or probe first when the environment exposes nested tools.
- Keep the tool-availability guard in the resident/project layers when contexts are re-layered or initialized.
- Do not infer tokens from file size alone; measure on a fresh thread.

## Key paths

- Resident: `$CODEX_HOME/AGENTS.md`, `$CODEX_HOME/memories/MEMORY.md`, `$CODEX_HOME/memories/memory_summary.md`
- Project template: `$CODEX_HOME/agent-templates/project-agent/`
- Capabilities: `$CODEX_HOME/skills/`, `$CODEX_HOME/workflows/`
- History: `$CODEX_HOME/memories/raw_memories.md`, `$CODEX_HOME/memories/rollout_summaries/`
