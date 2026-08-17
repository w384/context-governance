# New-project initialization (one-time sync)

Run when initializing a project, installing an agent template, or copying the project-agent scaffolding. Sync once, then keep the project self-contained.

## Steps
1. Confirm the current directory is the project root.
2. Copy the whole template `$CODEX_HOME/agent-templates/project-agent/` into the project root — do not hand-write a stripped AGENTS.md.
3. The template contains: `AGENTS.md`, `README.md`, `.learnings/LEARNINGS.md`, `.learnings/ERRORS.md`, `docs/agent/workflows.md`, `docs/agent/memory-and-decisions.md`.
4. If files already exist, decide whether to replace; a "reinstall" request means the template overwrites.
5. Fill the project AGENTS.md placeholders: one-line positioning, target users, current phase, success criteria, "currently not doing", authority sources, constraints (must-keep / must-not-change / needs-confirmation), tool routing, verification commands.
6. Point the project AGENTS.md at the global AGENTS.md and memory (the template already does this by default).
7. Use `work/` for process files and `outputs/` for deliverables.
8. Register the project's memory location in `memories/memory_summary.md`.
9. Log every create/overwrite/copy to the project change log (per the paths-and-logs workflow).
10. If asked to init only a single file, narrow the scope; otherwise do not omit the template's companion files.