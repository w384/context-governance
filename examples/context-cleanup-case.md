# Context cleanup case

This example shows a common long-lived workspace problem: useful information is present, but its lifecycle has been lost.

## Before: one growing context bucket

A workspace has accumulated the following material:

- Global AGENTS.md contains user preferences, shell safety rules, a web-app project's framework constraints, an old release checklist, and a detailed UX-review procedure.
- MEMORY.md contains stable communication preferences, the current project's architecture, names of closed tasks, and several dated progress updates.
- A project README contains only product-facing information, while the actual architecture decisions are duplicated in global files.
- Specialist instructions for security review and product analysis are copied into AGENTS.md even though they apply only to some requests.
- Thread summaries and rollout notes are still next to current project rules.

The result is a large always-read surface. The agent sees current rules alongside historical context and task-specific instructions, even when the request is unrelated.

## Cleanup decision

Apply the resident-context test to every item:

> Is this worth re-reading every single turn?

If the answer is no, move it instead of deleting it.

| Mixed source | Destination | Reason |
|---|---|---|
| Language preference, conclusion-first response style, and durable safety boundaries | Resident Context: global AGENTS.md | They are required across projects and turns. |
| Stable cross-project preferences | Resident Context: memories/MEMORY.md | They remain useful without tying the agent to one project. |
| Framework constraints, architecture decisions, and local verification commands | Project: project AGENTS.md and docs/ | They matter only while working in that project. |
| Product background, design decisions, and operating knowledge | Project: README.md, docs/, and .learnings/ | They should travel with the project rather than with every future task. |
| Security-review and UX-review procedures | Skills or workflows | They should be loaded when the task calls for those capabilities. |
| Closed-task summaries, rollout notes, and dated status updates | Archive: history or rollout-summary location | They are evidence and reference material, not current instructions. |

## After: information in the correct lifecycle

```text
Resident Context
  - Minimal global rules
  - Stable long-term preferences

Project
  - Project rules and constraints
  - Architecture and product knowledge
  - Project-specific learnings

Skills
  - Security review procedure
  - Product and UX workflows

Archive
  - Closed-task summaries
  - Rollout notes
  - Historical decisions
```

No knowledge is discarded merely because it is not resident. The work is a relocation: each item remains findable, but it no longer competes with the rules that must shape every response.

## Why this improves long-running-agent stability

A smaller resident layer makes the decision boundary clearer. The agent has less unrelated material to reconcile before applying global rules, while project knowledge remains close to the project that owns it and specialist procedures remain available when invoked.

The actual token and latency effect varies by client, model, enabled skills, project structure, and thread history. Measure it instead of assuming it from document size.

## Validation checklist

1. Back up every file that will change.
2. Record a baseline from a fresh thread: input tokens, cached input tokens, context occupancy, latency, and whether key rules hold.
3. Move one category at a time and confirm the destination is discoverable.
4. Open a fresh thread after migration and repeat the same checks.
5. Test a normal technical question, a project change, a file-creation request, a high-risk-action judgment, and each specialist workflow.
6. Confirm that project knowledge is still available in its project and that unrelated history no longer behaves like a standing instruction.
