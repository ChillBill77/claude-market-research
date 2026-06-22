# Strategy OS for Claude

A collection of [Claude Code](https://claude.com/claude-code) **Skills** that **coach** you through McKinsey/BCG/Bain-style strategy work — from first diagnosis to a board-ready recommendation, one step at a time. Built on the MBB spine: crisp framing, MECE structure, hypothesis-led analysis, 80/20 focus, answer-first communication.

## The engagement (6 phases)

```
1. Diagnose & Frame  →  2. Map Markets & Competition  →  3. Choose Strategy & Economics
        →  4. Operating Model & Execution  →  5. Govern Risk & Value  →  6. Align & Communicate
```

All six phases are built. `strategy-os` coaches you through each — it explains a step, asks for your input, helps you sharpen it, and only then moves on (no framework dumps).

## Skills

### `strategy-os/` — the coach / orchestrator
Guides the full six-phase engagement, applying the right method or handing off to the right skill at each step. Ships with eleven clean-room, step-by-step coaching playbooks in `strategy-os/references/`:

- **Phase 1 — Diagnosis:** `situation-assessment`
- **Phase 2 — Market & Competitive Intelligence:** handled by the `market-research` skill (below)
- **Phase 3 — Strategic Choice:** `strategic-options`, `business-case-builder`
- **Phase 4 — Operating Model & Execution:** `operating-model-design`, `initiative-prioritizer`, `transformation-roadmap`
- **Phase 5 — Risk, Performance & Governance:** `risk-and-mitigation`, `kpi-architect`, `value-realization`, `war-gaming`
- **Phase 6 — Alignment & Communication:** `decision-memo`

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

Then restart Claude Code. `strategy-os` references `market-research`, so install both for the full engagement. Prebuilt packages are in [`dist/`](dist/).

## Roadmap

Future cycles can add more method playbooks per phase: growth-barriers and assumption-audit (Phase 1); pricing-strategy and portfolio-review (Phase 3); narrative-builder and stakeholder-alignment (Phase 6).

## License

MIT License — Copyright (c) 2026 Gilles van Heijst and YaWorks. See [`LICENSE`](LICENSE).

## Credit

The six-phase engagement structure is **inspired by** [aapersh/strategy-skills-for-claude](https://github.com/aapersh/strategy-skills-for-claude). All content in this repository is **independently authored** (clean-room) — no upstream files are copied. The upstream repository carries no license; this independent reimplementation is what makes the work here distributable under MIT.
