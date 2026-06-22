# Strategy OS for Claude

A collection of [Claude Code](https://claude.com/claude-code) **Skills** that run McKinsey/BCG/Bain-style strategy work — from first diagnosis to a board-ready recommendation. Built on the MBB spine: crisp framing, MECE structure, hypothesis-led analysis, 80/20 focus, answer-first communication.

## The engagement (6 phases)

```
1. Diagnose & Frame  →  2. Map Markets & Competition  →  3. Choose Strategy & Economics
        →  4. Operating Model & Execution  →  5. Govern Risk & Value  →  6. Align & Communicate
```

Phases 4–5 are on the roadmap (see below).

## Skills

### `strategy-os/` — the orchestrator
Runs the full six-phase engagement and, at each phase, applies the right method or hands off to the right skill. Ships with four clean-room method playbooks in `strategy-os/references/`:

- **situation-assessment** (Phase 1) — a defensible current-state read; facts vs. inferences vs. unknowns.
- **strategic-options** (Phase 3) — develop distinct paths, judge them, recommend with trade-offs.
- **business-case-builder** (Phase 3) — turn the choice into an economic case (value, cost, scenarios, go/no-go).
- **decision-memo** (Phase 6) — an answer-first, board-ready memo that asks for a specific decision.

### `market-research/` — the Phase-2 engine
MBB-grade market, customer, and competitive research with an independent adversarial verification gate and a presentation-ready PPTX. `strategy-os` hands off to it for Phase 2. See [`market-research/README.md`](market-research/README.md).

## Install

Each skill is a standard Claude Code skill directory. Copy the ones you want into a skills directory:

```bash
# Personal (all projects)
cp -r strategy-os market-research ~/.claude/skills/

# OR project-local
cp -r strategy-os market-research /path/to/project/.claude/skills/
```

Then restart Claude Code. `strategy-os` references `market-research`, so install both for the full engagement.

## Roadmap

- **Phase 4 — Operating Model & Execution:** operating-model design, initiative prioritization, transformation roadmap.
- **Phase 5 — Risk, Performance & Value Governance:** risk & mitigation, KPI design, value realization, war-gaming.
- **More per-phase methods:** growth-barriers, assumption-audit, pricing-strategy, portfolio-review, narrative-builder, stakeholder-alignment, and others.

## License

MIT License — Copyright (c) 2026 Gilles van Heijst and YaWorks. See [`LICENSE`](LICENSE).

## Credit

The six-phase engagement structure is **inspired by** [aapersh/strategy-skills-for-claude](https://github.com/aapersh/strategy-skills-for-claude). All content in this repository is **independently authored** (clean-room) — no upstream files are copied. The upstream repository carries no license; this independent reimplementation is what makes the work here distributable under MIT.
