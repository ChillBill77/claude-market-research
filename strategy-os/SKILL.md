---
name: strategy-os
description: "Runs an end-to-end McKinsey/BCG/Bain-style strategy engagement, coordinating diagnosis, market research, strategic choice, and executive communication. Use when the user wants a full strategy workup rather than a single analysis — e.g. 'build a strategy', 'run a strategy engagement', diagnose-to-recommendation work, or preparing a board-ready strategic decision."
license: MIT. Complete terms in LICENSE.
allowed-tools: Read, Grep, Glob, WebFetch, WebSearch, Write, Bash
---

# Strategy OS: End-to-End Strategy Engagement

This skill is the **orchestrator** for a full strategy engagement. It walks a problem from first diagnosis through a board-ready recommendation, applying the consulting spine that runs through every step: frame the real decision first, structure it MECE, lead with hypotheses, focus on the 80/20, and communicate answer-first.

It does not do all the work itself. It sequences the engagement and, at each phase, points to the method to apply — a focused playbook in `references/`, or, for market work, the dedicated `market-research` skill.

## When to Use

Use Strategy OS when the user wants a *coordinated* strategy effort, not just one analysis. Typical triggers: "build a strategy for X", "run a strategy engagement", "we need to decide whether to enter/exit/invest", turnaround framing, or preparing a recommendation for leadership.

For a single narrow task (just a market sizing, just a competitor map), invoke that one method or the `market-research` skill directly instead.

## The Six-Phase Engagement

Work the phases in order. Read a phase's reference file only when you reach that phase (keep context lean).

### Phase 1 — Diagnosis & Framing
**Goal:** establish what is actually true and what decision is really on the table, before debating answers.
**Do:** apply `references/situation-assessment.md` to build a defensible current-state read and sharpen the decision question.

### Phase 2 — Market & Competitive Intelligence
**Goal:** understand the market, customers, and competitors well enough to choose.
**Do:** **hand off to the `market-research` skill.** Activate it and let it run its own workflow — parallel collection across market/customer/competitive levels, an independent verification gate, and a presentation-ready deck — then bring its pyramid analysis and findings back into the engagement. Strategy OS does not re-implement that pipeline.

### Phase 3 — Strategic Choice & Economics
**Goal:** decide what to do and prove it pays.
**Do:** apply `references/strategic-options.md` to generate and judge distinct paths, then `references/business-case-builder.md` to turn the chosen path into an economic case.

### Phase 4 — Operating Model & Execution
**Goal:** translate the choice into how the organization will actually deliver it.
**Status:** *Roadmap — not built this cycle.* Will cover operating-model design, initiative prioritization, and a transformation roadmap.

### Phase 5 — Risk, Performance & Value Governance
**Goal:** stress-test the plan and govern value capture.
**Status:** *Roadmap — not built this cycle.* Will cover risk and mitigation, KPI design, value realization, and war-gaming.

### Phase 6 — Alignment & Executive Communication
**Goal:** get the decision made.
**Do:** apply `references/decision-memo.md` to produce a board-ready, answer-first recommendation.

## Running an Engagement

1. Confirm the decision and scope with the user; do Phase 1.
2. Trigger Phase 2 via the `market-research` skill; fold its findings in.
3. Work Phase 3 (options → business case).
4. Close with Phase 6 (decision memo). Note Phases 4–5 as next steps if execution/governance is in scope.
5. Keep every artifact answer-first and traceable to evidence.

## Roadmap

Later cycles will add the deferred phases (4 Operating Model & Execution, 5 Risk/Performance/Governance) and more method playbooks per phase (e.g. growth-barriers and assumption-audit for diagnosis; pricing-strategy and portfolio-review for strategic choice; narrative-builder and stakeholder-alignment for communication).

## Attribution

The six-phase engagement structure is inspired by `aapersh/strategy-skills-for-claude`. All content here is **independently authored** (clean-room) and licensed MIT — see `LICENSE`.
