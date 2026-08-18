# Governance procedure (restructure the context layers)

Read when running a governance or restructure task. Move detail out; never delete it.

## Phases (run in order, verify each before the next)

### P0 — Back up
- Copy every file you will change into a timestamped backup directory; keep originals restorable.
- Never overwrite an existing backup; co-locate `.bak-<timestamp>` next to originals when helpful.
- Minimum: global `AGENTS.md`, `memories/MEMORY.md`, `memories/memory_summary.md`, plus any project `AGENTS.md` touched.

### P1 — Global AGENTS.md
- Keep only: the user's preferred language and salutation, conclusion-first output, execute simple tasks directly, clarify complex or high-risk tasks first, minimal viable solution, no scope creep, no unrelated refactors, every change traced and verified.
- Keep the tool-availability guard as an always-on rule: before claiming a tool is missing, runtime-enumerate or directly probe it. This prevents prompt/runtime drift from becoming a repeated false conclusion.
- Rule precedence: global = base; project or nearer rules override.
- Safety: external publish / permission change / delete / bulk overwrite need explicit authorization; never leak credentials; never claim "verified/safe" without evidence; security or permission changes use TDD RED→GREEN.
- Output: conclusion-first, executable, state verification and risk.
- Move out: path rules, log format, project init, product analysis, UX, PMP-style routing → `$CODEX_HOME/workflows/` or a skill; keep only a one-line entry in AGENTS.
- Target: ≤3 KB (~1000–2000 tokens).

### P2 — MEMORY.md
- A (keep, global, one line each): long-term cross-project stable preferences only.
- B (move to project): project-specific knowledge → that project's `.learnings/` or `docs/agent/`.
- C (archive): rollout summaries, thread IDs, test counts, dates, shutdown or automation history → already live in `memories/raw_memories.md` and `memories/rollout_summaries/`; remove from MEMORY.
- Target: ~300–800 tokens.

### P3 — memory_summary.md
- A very short index only: where user preferences live, where each project's memory lives, where history and archive live.
- Do not duplicate MEMORY. Target: ≤500 tokens.

### P4 — Project AGENTS.md
- Keep: project tech constraints, always-on safety boundaries, verification requirements.
- Keep the project/template tool-routing guard when the project depends on Codex desktop tools, especially codex_app__ thread tools and runtime Object.keys(tools) / typeof tools.<name> verification.
- Move out: background → README; history → devlog or structure; security background → SECURITY.md; consent explainers → install doc; PR/branch/review detail → CONTRIBUTING.md.
- Target: ~2–4 KB.

### P5 — Do not delete plugin or template caches
- `$CODEX_HOME/.tmp/plugins/`, `$CODEX_HOME/plugins/cache/`, `$CODEX_HOME/agent-templates/` are caches and templates, not resident context. Do not delete them to "save tokens" unless there is proof they are injected.

### P6 — Nested AGENTS
- Nested AGENTS (`src/`, `gui/`, `scripts/`, `.github/`) are correct. Split a big root AGENTS into small local ones rather than re-centralizing.

### P7 — Thread history strategy
- Short threads for simple discussion; for long engineering tasks, periodically summarize decisions, current state, and todos, then continue in a fresh thread.

## Measure tokens
- Estimate when no fresh thread is available: tokens ≈ CJK chars + (ASCII chars ÷ 4).
- The real check: open a fresh thread → ask a trivial question ("what model are you") → record `input_tokens`, `cached_input_tokens`, context occupancy, latency, and whether key rules still hold.

## Verify no regression
After restructuring, confirm at least: a normal tech question; an in-project code change; file creation; high-risk action judgment; and each specialist workflow (product/UX, PMP-style, security). Confirm capabilities still resolve, project rules still load, preferences remain, and unrelated project knowledge no longer rides along.

## Report
Deliver: before/after size and tokens per file; a migration table (original → new location); token A/B (baseline → each phase → final); final reduction percentage; and the remaining non-optimizable parts (user-controllable vs Codex/OpenAI/tool/thread fixed).