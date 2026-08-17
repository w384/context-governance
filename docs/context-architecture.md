# Context architecture

Context Governance separates information by lifecycle. The question is not whether knowledge is useful; it is whether the agent must reread it on every turn.

## Before: everything mixed

```text
Codex
  |
  +-- AGENTS.md
  |     global rules + project rules + old decisions
  |
  +-- MEMORY.md
  |     long-term preferences + project notes + status updates
  |
  +-- docs/
  |     project knowledge + instructions copied into global files
  |
  +-- history/
  |     past work mixed with current guidance
  |
  +-- skills/
  |     specialist procedures described whether needed or not
  |
  \-- everything is treated as always relevant
```

When all layers are mixed, the stable rules that must apply every turn compete with details that are useful only for one project, task type, or past decision.

## After: lifecycle layers

```text
Codex
  |
  +-- Resident Context (re-read every turn)
  |     +-- Rules
  |     \-- Memory
  |
  +-- Project
  |     +-- Project rules
  |     +-- Project knowledge
  |     \-- Project learnings
  |
  +-- Skills
  |     \-- Task-specific capabilities and workflows
  |
  \-- Archive
        \-- History and past decisions
```

A compact version for the README:

```text
Codex
 |
 Resident Context
 |
 + Rules
 + Memory
 + Project
 + Skills
 + Archive
```

The compact diagram is a lifecycle map, not a claim that every layer is injected on every turn. Only resident rules and long-term preferences are intentionally kept in the always-read layer. Project knowledge, skills, and archived history remain available through their own locations when the current task needs them.

## Layer responsibilities

| Layer | Purpose | Typical location | Read frequency |
|---|---|---|---|
| Resident rules | Minimal constraints that must always apply | global AGENTS.md | Every turn |
| Memory | Stable, cross-project preferences | memories/MEMORY.md | Every turn only when deliberately resident |
| Project | Project rules, knowledge, and learnings | project AGENTS.md, README.md, docs/, .learnings/ | In project work |
| Skills | Specialist instructions and workflows | skills/, workflows/ | On demand |
| Archive | Past decisions, raw notes, and rollout records | archive or history directories | When relevant |

The architecture preserves access to knowledge while reducing the chance that unrelated material becomes permanent context.
