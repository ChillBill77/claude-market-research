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
- `license: MIT. Complete terms in repository LICENSE.`
- `allowed-tools: Read, Grep, Glob, WebFetch, WebSearch, Write, Bash, Task` (Task so it can dispatch the market-research subagent flow during Phase 2).

**`SKILL.md` body** walks the six-phase engagement. For each phase: its objective, the method(s) to apply, and where the playbook lives:
1. **Diagnosis & Framing** → `references/situation-assessment.md`
2. **Market & Competitive Intelligence** → **invoke the `market-research` skill** for the full pyramid analysis + verification + deck.
3. **Strategic Choice & Economics** → `references/strategic-options.md`, then `references/business-case-builder.md`.
4. **Operating Model & Execution** → *Roadmap (not built this cycle)* — stated as a planned phase.
5. **Risk, Performance & Value Governance** → *Roadmap (not built this cycle)*.
6. **Alignment & Executive Communication** → `references/decision-memo.md`.

The orchestration emphasizes the MBB spine shared with `market-research`: crisp framing, MECE structure, hypothesis-led analysis, 80/20 focus, answer-first communication. It tells Claude to load a phase's reference file only when that phase is active (progressive disclosure).

### The four clean-room method playbooks

Each `references/*.md` is authored in original wording (general consulting knowledge, not upstream text) and follows a consistent shape: **When to use**, **MBB-style approach**, **Workflow** (numbered steps), **Output format** (a markdown skeleton). Summaries:

- **situation-assessment.md** — fact-based current-state baseline before choosing strategy; separates facts / interpretations / open questions across performance, market, customers, operations, organization.
- **strategic-options.md** — generate MECE strategic options, define evaluation criteria, score against them, and recommend with rationale and risks.
- **business-case-builder.md** — translate a chosen option into an economic case: value drivers, costs, assumptions, scenarios (base/upside/downside), and a go/no-go view.
- **decision-memo.md** — answer-first executive memo: recommendation, the few reasons, what it costs, risks, and the decision asked for.

### Clean-room discipline

Method content is written from general MBB/consulting knowledge in original prose. No file from the upstream repo is copied. Upstream is credited as *inspiration* only. This keeps the whole repo MIT-clean.

### Repo / docs updates

- **Root `README.md`** rewritten as the strategy-OS landing page: the 6-phase map, the two skills (`strategy-os` orchestrator + `market-research` Phase-2 engine), the roadmap (phases/methods to come), install instructions, MIT license, and an "inspired by aapersh/strategy-skills-for-claude; independently authored" credit.
- `market-research/` unchanged.

## File Impact

**Created:**
- `strategy-os/SKILL.md`
- `strategy-os/references/situation-assessment.md`
- `strategy-os/references/strategic-options.md`
- `strategy-os/references/business-case-builder.md`
- `strategy-os/references/decision-memo.md`

**Edited:**
- `README.md` (root) — strategy-OS landing page + credit.

**Untouched:**
- `market-research/**`.

## Success Criteria

1. `strategy-os/SKILL.md` exists with valid frontmatter (`name`, `description`, `license: MIT`, `allowed-tools` including `Task`) and documents all six phases, with Phase 2 delegating to the `market-research` skill and Phases 4 & 5 explicitly marked roadmap.
2. Four playbooks exist under `strategy-os/references/`, each with When-to-use / MBB approach / Workflow / Output-format sections.
3. No file under `strategy-os/` is a verbatim copy of any upstream file (clean-room) — verified by spot-diff against the cloned upstream.
4. `market-research/` is unchanged (no diff).
5. Root `README.md` presents the 6-phase OS (both skills), the roadmap, install instructions, MIT license, and the inspired-by credit.
6. The `strategy-os` skill passes the skill quick-validation used for packaging (frontmatter valid; name/description present).
