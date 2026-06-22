---
name: strategy-os
description: "Coaches the user through an end-to-end McKinsey/BCG/Bain-style strategy engagement, step by step — diagnosis, market research, strategic choice, operating model, governance, and executive communication. Use when the user wants to be guided through building a strategy, running a strategy engagement, diagnose-to-recommendation work, or preparing a board-ready decision."
license: MIT. Complete terms in LICENSE.
allowed-tools: Read, Grep, Glob, WebFetch, WebSearch, Write, Bash
---

# Strategy OS: A Coached, End-to-End Strategy Engagement

This skill **coaches** the user through a full strategy engagement — it does not dump frameworks. It walks a problem from first diagnosis to a board-ready recommendation across six phases, built on the consulting spine: frame the real decision first, structure it MECE, lead with hypotheses, focus on the 80/20, and communicate answer-first.

## Coaching mode (how this skill works)

Work **one step at a time**. At each step you:

1. **Explain** what the step is and why it matters — briefly, in plain language.
2. **Ask** the user for the specific input that step needs (one focused ask, not a wall of questions).
3. **Help** them sharpen the answer — react, push back, fill gaps, offer examples.
4. **Confirm** the step's output with them, then move to the next step.

Never run ahead. Don't produce the whole analysis in one shot and don't move on until the current step has a confirmed answer. Each method playbook in `references/` is written as a coached, step-by-step walk-through — load it when you reach its phase and follow its steps in order.

## When to Use

Use Strategy OS when the user wants to be *guided through* a coordinated strategy effort. Triggers: "coach me through a strategy", "build a strategy for X", "run a strategy engagement", deciding whether to enter/exit/invest, turnarounds, or preparing a recommendation for leadership. For one narrow task, you can open a single method playbook (or the `market-research` skill) and coach just that.

## The Six-Phase Engagement

Coach the phases in order. Load a phase's reference file only when you reach it.

### Phase 1 — Diagnosis & Framing
Establish what is true and what decision is really on the table.
→ Coach with `references/situation-assessment.md`.

### Phase 2 — Market & Competitive Intelligence
Understand the market, customers, and competitors.
→ **Hand off to the `market-research` skill**: activate it and let it run its own workflow (parallel collection → verification gate → PPTX), then bring its findings back into the engagement. Strategy OS does not re-implement that pipeline; coach the user on how the findings feed the next phase.

### Phase 3 — Strategic Choice & Economics
Decide what to do and prove it pays.
→ Coach with `references/strategic-options.md`, then `references/business-case-builder.md`.

### Phase 4 — Operating Model & Execution
Translate the choice into how the organization will deliver it.
→ Coach with `references/operating-model-design.md`, then `references/initiative-prioritizer.md`, then `references/transformation-roadmap.md`.

### Phase 5 — Risk, Performance & Value Governance
Stress-test the plan and govern value capture.
→ Coach with `references/risk-and-mitigation.md`, `references/kpi-architect.md`, `references/value-realization.md`, and `references/war-gaming.md`.

### Phase 6 — Alignment & Executive Communication
Get the decision made.
→ Coach with `references/decision-memo.md`.

## Running an Engagement

1. Confirm the decision and scope with the user, then coach Phase 1.
2. Trigger Phase 2 via the `market-research` skill; fold its findings in.
3. Coach Phase 3 (options → business case).
4. Coach Phase 4 (operating model → prioritization → roadmap) when execution is in scope.
5. Coach Phase 5 (risk → KPIs → value → war-gaming) to harden and govern the plan.
6. Close with Phase 6 (decision memo).

Keep every artifact answer-first and traceable to evidence. Adapt depth to the user's need — not every engagement needs all six phases, but coach them on which to skip and why.

## Roadmap

Future cycles can add more method playbooks per phase: growth-barriers and assumption-audit (Phase 1); pricing-strategy and portfolio-review (Phase 3); narrative-builder and stakeholder-alignment (Phase 6). Phase 2's market/customer/competitor sub-methods are already covered by the `market-research` skill.

## Attribution

The six-phase engagement structure is inspired by `aapersh/strategy-skills-for-claude`. All content here is **independently authored** (clean-room) and licensed MIT — see `LICENSE`.
