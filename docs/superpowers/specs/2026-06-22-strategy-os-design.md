# Strategy OS — Umbrella Orchestrator Skill (Cycle 1)

**Date:** 2026-06-22
**Status:** Approved (design)
**Scope:** New `strategy-os/` skill + repo restructure into a 6-phase strategy OS. First cycle of a larger effort.

## Problem / Goal

The repo has one skill (`market-research/`) that produces MBB-grade market analysis. The user wants to combine it with the concepts from `github.com/aapersh/strategy-skills-for-claude` — a 21-skill, 6-phase McKinsey-style "consulting OS" (Diagnose → Map Markets → Choose Strategy → Operating Model → Govern → Communicate).

The chosen direction is a **single umbrella `strategy-os` skill** (Approach 3) that orchestrates a full engagement across the six phases, with `market-research` slotting in as the Phase-2 ("Market & Competitive Intelligence") engine. The upstream content is **clean-room reimplemented** — its *ideas* and structure are rebuilt in original wording and this repo's SKILL.md format, so everything is MIT-licensable and genuinely owned here.

This first cycle delivers the orchestrator backbone plus a curated, high-value set of four method playbooks.

## Non-Goals (YAGNI)

- No verbatim copying of any upstream file. Upstream is conceptual inspiration only.
- Not reimplementing all 21 upstream skills this cycle — only 4 curated methods.
- Phases 4 (Operating Model & Execution) and 5 (Risk, Performance & Value Governance) are documented as roadmap, not built this cycle.
- No change to `market-research/` internals — it is referenced/delegated to, not modified.
- No standalone single-file skills — methods live as references under the umbrella skill.

## Design

### New skill: `strategy-os/` (umbrella orchestrator)

A standard directory-skill:

```
strategy-os/
├── SKILL.md                 # 6-phase engagement orchestration
└── references/
    ├── situation-assessment.md      # Phase 1 method (clean-room)
    ├── strategic-options.md         # Phase 3 method (clean-room)
    ├── business-case-builder.md     # Phase 3 method (clean-room)
    └── decision-memo.md             # Phase 6 method (clean-room)
```

**`strategy-os/SKILL.md`** frontmatter:
- `name: strategy-os`
- `description:` third-person, states when to use — running an end-to-end MBB-style strategy engagement (diagnosis through executive communication), coordinating market research and strategic-choice methods.
- `license: MIT. Complete terms in LICENSE.` (a root `LICENSE` file is created — see File Impact).
- `allowed-tools: Read, Grep, Glob, WebFetch, WebSearch, Write, Bash`. No `Task`: strategy-os orchestrates by activating other skills/reading reference playbooks; it does not itself fan out subagents this cycle. The Phase-2 hand-off to `market-research` lets *that* skill run its own internal subagent dispatch — strategy-os does not need `Task` for it. (Add `Task` only in a later cycle if strategy-os gains its own parallel steps.)

**`SKILL.md` body** walks the six-phase engagement. For each phase: its objective, the method(s) to apply, and where the playbook lives:
1. **Diagnosis & Framing** → `references/situation-assessment.md`
2. **Market & Competitive Intelligence** → **hand off to the `market-research` skill**: strategy-os instructs that the market-research skill be activated, which then runs its own three-phase workflow (parallel collection → verification gate → PPTX) and returns the pyramid analysis + deck. strategy-os does not re-implement that dispatch.
3. **Strategic Choice & Economics** → `references/strategic-options.md`, then `references/business-case-builder.md`.
4. **Operating Model & Execution** → *Roadmap (not built this cycle)* — stated as a planned phase.
5. **Risk, Performance & Value Governance** → *Roadmap (not built this cycle)*.
6. **Alignment & Executive Communication** → `references/decision-memo.md`.

The orchestration emphasizes the MBB spine shared with `market-research`: crisp framing, MECE structure, hypothesis-led analysis, 80/20 focus, answer-first communication. It tells Claude to load a phase's reference file only when that phase is active (progressive disclosure).

### The four clean-room method playbooks

Each `references/*.md` is authored from general consulting knowledge in original prose. To keep the structure itself independent (not a mirror of upstream's `When To Use / McKinsey-Style Approach / Workflow / Output Format` headings), the playbooks use this repo's own four-part shape with distinct headings:

- **`## Use it when`** — the trigger situations.
- **`## How to think about it`** — the MBB lens / principle for the method.
- **`## Steps`** — numbered procedure.
- **`## Deliverable`** — a markdown output template.

The four methods, described by *intent* (the implementer writes from this intent + general knowledge, without the upstream files open — see Clean-room discipline):

- **situation-assessment** — produce a defensible current-state read before any strategy debate: what is true now, what is inference, what is still unknown, across the dimensions that matter to the decision.
- **strategic-options** — develop a small set of genuinely distinct, mutually-exclusive strategic paths, judge them against decision-relevant criteria, and land a recommendation with its trade-offs.
- **business-case-builder** — turn a chosen path into an economic argument: where value comes from, what it costs, the assumptions it rides on, how it behaves under better/worse scenarios, and whether it clears the bar.
- **decision-memo** — a board-ready, answer-first write-up: the recommendation first, the few reasons it holds, cost and risk, and the explicit decision being requested.

### Clean-room discipline

This is a genuine clean-room reimplementation, not paraphrase:
- The implementer authors each playbook from the *intent* above plus general MBB/consulting knowledge, **with the upstream files closed** — never transcribing or paraphrasing upstream prose, headings, or table layouts.
- The playbook structure deliberately diverges from upstream's heading set (see above).
- Upstream is credited only as conceptual inspiration; it has no LICENSE, which is precisely why the work must be independently authored to be distributable under MIT.

### Repo / docs updates

- **Root `README.md`** rewritten as the strategy-OS landing page: the 6-phase map, the two skills (`strategy-os` orchestrator + `market-research` Phase-2 engine), the roadmap (phases/methods to come), install instructions, MIT license, and a credit noting the work is *inspired by* `aapersh/strategy-skills-for-claude` but **independently authored** — and that, because the upstream has no license, this clean-room reimplementation is what makes the work distributable under MIT.
- **Root `LICENSE`** created (MIT, Copyright (c) 2026 Gilles van Heijst and YaWorks) so the repo has a top-level license that `strategy-os` (and the repo) reference.
- `market-research/` unchanged.

## File Impact

**Created:**
- `strategy-os/SKILL.md`
- `strategy-os/references/situation-assessment.md`
- `strategy-os/references/strategic-options.md`
- `strategy-os/references/business-case-builder.md`
- `strategy-os/references/decision-memo.md`
- `LICENSE` (root, MIT, (c) 2026 Gilles van Heijst and YaWorks)

**Edited:**
- `README.md` (root) — strategy-OS landing page + credit.

**Untouched:**
- `market-research/**`.

## Success Criteria

1. `strategy-os/SKILL.md` exists with valid frontmatter (`name`, `description`, `license: MIT…`, `allowed-tools` = `Read, Grep, Glob, WebFetch, WebSearch, Write, Bash` — no `Task`) and documents all six phases, with Phase 2 handing off to the `market-research` skill and Phases 4 & 5 explicitly marked roadmap.
2. Four playbooks exist under `strategy-os/references/`, each using this repo's heading shape (`## Use it when`, `## How to think about it`, `## Steps`, `## Deliverable`) — NOT upstream's heading set.
3. Clean-room verified: no playbook shares upstream's heading set or table layouts, and wording is substantively independent (not paraphrase). Check: `grep -ri "McKinsey-Style Approach" strategy-os/` returns nothing, and a manual read confirms the prose is not a reworded upstream file. (A verbatim-only diff is insufficient.)
4. `market-research/` is unchanged (`git diff` shows no changes under `market-research/`).
5. Root `README.md` presents the 6-phase OS (both skills), the roadmap, install instructions, MIT license, and the inspired-by/independently-authored credit (noting upstream has no license).
6. Root `LICENSE` exists (MIT, (c) 2026 Gilles van Heijst and YaWorks); `strategy-os/SKILL.md` frontmatter `license` line is consistent with it.
7. `strategy-os` passes packaging validation: `python3 ~/.claude/commands/skills/scripts/quick_validate.py strategy-os` reports pass (frontmatter valid; name + third-person description present).
