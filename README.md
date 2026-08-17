# Context Governance

Keep long-lived Codex and AI-agent context lean by putting each kind of knowledge in the right lifecycle layer.

[中文 README](README.zh-CN.md)

## Why does context get heavier over time?

Long-running Codex and agent projects accumulate useful rules, preferences, project notes, specialist instructions, and history. The failure mode is not that the knowledge is useless. It is that everything gradually gets copied into files that are treated as if they must be read on every turn.

That creates a context that is expensive to reread, difficult to navigate, and more likely to produce unstable behavior as unrelated details compete for attention.

Context Governance keeps the knowledge while separating its lifecycles:

```text
Global Rules
    ↓
Memory
    ↓
Project Knowledge
    ↓
Skills
    ↓
History
```

The governing question is simple:

> Is this worth re-reading every single turn?

If not, it does not belong in resident context.

This is not about knowing less. It is about keeping knowledge available while placing it where it belongs.

## Before and after

| Before | After |
|---|---|
| AGENTS.md, MEMORY.md, project rules, specialist instructions, and history grow together. | Resident context keeps only rules and preferences that must apply every turn. |
| Project details are repeated in global memory. | Project knowledge stays with the project. |
| Capabilities and workflows are always described up front. | Skills and workflows are loaded when the task needs them. |
| Old decisions remain mixed with current guidance. | History is archived and retrieved when it is relevant. |

## Features

- A layered model for resident rules, memory, project knowledge, skills, and history.
- A repeatable **backup → measure → migrate → compress → verify** governance procedure.
- A one-time project initialization checklist.
- Guardrails against deleting safety rules, moving project wikis into memory, or inferring tokens from file size alone.
- A Codex-discoverable SKILL.md with no runtime dependencies.

## Why this exists

Most context advice focuses on adding memory, retrieving more information, or compressing prompts. Context Governance starts earlier: decide what deserves a permanent seat in the context and what should remain available on demand.

It is a documentation method and Codex Skill for people who maintain long-lived agent workspaces and want a stable way to review context architecture before adding more content.

## Architecture

```text
Codex
  │
  ├── Resident Context
  │   ├── Global Rules
  │   └── Long-term Preferences
  │
  ├── Project Context
  │   ├── Project Rules
  │   ├── Project Knowledge
  │   └── Project Learnings
  │
  ├── Skills and Workflows
  │
  └── Archive
      └── History and past decisions
```

See the copyable Before/After diagram and layer explanations in [docs/context-architecture.md](docs/context-architecture.md).

## Installation

Copy this repository into the Codex skills directory:

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

Codex discovers SKILL.md on the next run.

## Usage

Ask Codex to govern an existing context:

```text
Use context-governance to review my current Codex context.
Identify what belongs in resident context, project knowledge, skills, and archive.
Back up files first, measure the baseline, then propose a minimal migration.
```

Or initialize a project:

```text
Use context-governance to initialize this project into the layered context structure.
```

The Skill covers two workflows:

- [Govern an existing context](references/governance-procedure.md)
- [Initialize a new project](references/project-init-sync.md)

## Example

Read the full migration walkthrough in [examples/context-cleanup-case.md](examples/context-cleanup-case.md). It shows how a mixed AGENTS.md, MEMORY.md, project rules, skills, and history can be separated without deleting useful knowledge.

## Comparison with alternatives

| Approach | Primary question | How Context Governance differs |
|---|---|---|
| Memory systems | What facts should be saved or retrieved? | Defines which information is allowed to remain resident before retrieval is considered. |
| RAG systems | Which external passages should be retrieved? | Does not retrieve documents or build an index; it governs the agent's context layers. |
| Prompt compression | How can the same input be represented more compactly? | Does not compress content; it decides whether content belongs in the fixed input at all. |
| Project templates | What files should a project start with? | Adds lifecycle governance so the template does not become another permanent catch-all. |

These approaches can complement each other. Context Governance is the architecture and review method around them, not a replacement for them.

## Measurement note

This repository does not publish a universal token-saving number. Context size depends on the model, client, enabled skills, project, and thread history.

For a useful baseline, compare a fresh thread before and after migration and record the actual input tokens, cached input tokens, context occupancy, latency, and whether key rules still hold. Do not infer token usage from file size alone.

## Roadmap

- **v0.1** — Core Codex Skill, layered model, governance procedure, and project initialization checklist.
- **Next** — Publish a small, reproducible measurement worksheet with example baseline data from a documented workspace.
- **Later** — Add more migration examples for different agent setups while keeping the project documentation-only and model-agnostic.

## License

MIT. See [LICENSE](LICENSE).

## Repository metadata

Suggested GitHub description:

> Keep Codex context lean by managing rules, memory, project knowledge, skills, and history with a layered governance model.

Suggested topics:

codex · openai-codex · ai-agent · agent-context · context-engineering · context-management · llm-agent · developer-tools · prompt-engineering

See [CHANGELOG.md](CHANGELOG.md) for the v0.1.0 release notes.
