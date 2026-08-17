# context-governance

A Codex skill for keeping a lean, layered context architecture, and for initializing new projects into that structure.

## What it does

- Keeps resident context minimal: a compact global `AGENTS.md`, a short `MEMORY.md`, and a navigation-only `memory_summary.md`.
- Puts each kind of knowledge where it belongs: project knowledge in the project, capabilities in skills/workflows, history in archives.
- Provides a repeatable governance procedure: back up → measure → migrate → compress → verify.
- Provides a one-time new-project initialization sync checklist.

The guiding question for everything that goes into resident context:

> Is this worth re-reading every single turn? If not, it does not belong in resident context.

## Structure

- `SKILL.md` — English instructions (canonical; this is the file Codex auto-discovers).
- `SKILL.zh-CN.md` — Chinese translation.
- `references/governance-procedure.md` — detailed governance workflow (English).
- `references/governance-procedure.zh-CN.md` — Chinese translation.
- `references/project-init-sync.md` — new-project sync checklist (English).
- `references/project-init-sync.zh-CN.md` — Chinese translation.
- `agents/openai.yaml` — UI metadata for skill lists and chips.

All paths use `$CODEX_HOME` (the Codex home directory, defaulting to `~/.codex`) so the skill is portable across machines.

## Install

Copy this folder into your Codex skills directory:

```bash
mkdir -p "$CODEX_HOME/skills"      # ~/.codex/skills when CODEX_HOME is unset
cp -r context-governance "$CODEX_HOME/skills/"
```

Codex discovers `SKILL.md` automatically on the next run.

## Trigger

Codex loads this skill when asked to:

- govern, restructure, optimize, or compress Codex global context (AGENTS.md, MEMORY.md, memory_summary.md, token reduction, context layering);
- initialize a new project or install an agent template.

## License

MIT — see [LICENSE](LICENSE).