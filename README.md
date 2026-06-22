# claude-market-research

A collection of [Claude Code](https://claude.com/claude-code) **Skills**. Each top-level directory is a self-contained skill with its own `SKILL.md`.

## Skills

### `market-research/`

MBB-grade (McKinsey/BCG/Bain) market research that produces a presentation-ready PPTX. It runs a hypothesis-driven, four-level pyramid analysis (Market → Customers → Competitors → Company) via a three-phase workflow:

1. **Foundation** — research brief + MECE hypothesis tree.
2. **Parallel Collection** — three subagents research the Market, Customer, and Competitive levels concurrently; the main thread adds Company. An **independent adversarial verification gate** then re-checks every Key Finding (Confirmed / Refuted / Unverifiable–insufficient data) before synthesis — refuted findings are dropped, unverifiable ones flagged.
3. **Synthesis & Deck** — synthesize the analysis and generate the PPTX via the native `pptx` skill.

See [`market-research/README.md`](market-research/README.md) for full documentation.

## Install

Import a skill by extracting it into a Claude Code skills directory:

```bash
# Personal (all projects)
cp -r market-research ~/.claude/skills/

# OR project-local
cp -r market-research /path/to/project/.claude/skills/
```

Then restart Claude Code. A packaged `market-research.zip` (unzip into a skills directory) can also be produced for distribution.

## License

MIT License — Copyright (c) 2026 Gilles van Heijst and YaWorks. See [`market-research/LICENSE.txt`](market-research/LICENSE.txt).
