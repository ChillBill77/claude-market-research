# Strategy OS (Cycle 1) Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a `strategy-os` umbrella skill that orchestrates a 6-phase MBB strategy engagement — handing off to the existing `market-research` skill for Phase 2 and providing four clean-room method playbooks — plus a root `LICENSE` and a rewritten root `README`.

**Architecture:** A standard directory-skill `strategy-os/` with `SKILL.md` (the 6-phase orchestrator) and `references/` holding four clean-room method playbooks. Phase 2 hands off to `market-research` (unchanged). Phases 4 & 5 are documented as roadmap. All content is independently authored (clean-room); no upstream file is copied.

**Tech Stack:** Markdown (Claude Code skill format). No test runner — verification via `grep`, `git diff`, and the packaging validator `quick_validate.py`.

**Spec:** `docs/superpowers/specs/2026-06-22-strategy-os-design.md`

**Constraints:**
- Repo is git (`origin/main`, `github.com/ChillBill77/claude-market-research`). Per-task commits are real. A push-only `/loop` is active and will push commits; do not force-push.
- **Clean-room is mandatory.** Author every `strategy-os/` file from the intent in this plan + general consulting knowledge, with the upstream repo (`/tmp/strategy-skills-inspect`) CLOSED. Do not transcribe or paraphrase upstream prose, headings, or tables. Use this repo's heading shape: `## Use it when` / `## How to think about it` / `## Steps` / `## Deliverable`.
- All paths relative to repo root `/Users/gillesvanheijst/GIT/claude-skills`.

---

## File Structure

| File | Responsibility | Action |
|------|----------------|--------|
| `LICENSE` (root) | MIT license for the repo | Create |
| `strategy-os/SKILL.md` | 6-phase engagement orchestrator | Create |
| `strategy-os/references/situation-assessment.md` | Phase 1 method playbook | Create |
| `strategy-os/references/strategic-options.md` | Phase 3 method playbook | Create |
| `strategy-os/references/business-case-builder.md` | Phase 3 method playbook | Create |
| `strategy-os/references/decision-memo.md` | Phase 6 method playbook | Create |
| `README.md` (root) | Strategy-OS landing page | Rewrite |

---

## Chunk 1: Strategy OS skill

### Task 1: Root LICENSE

**Files:** Create `LICENSE`

- [ ] **Step 1:** Write a standard MIT License with `Copyright (c) 2026 Gilles van Heijst and YaWorks` (same text/holder as `market-research/LICENSE.txt`).
- [ ] **Step 2: Verify** — `head -3 LICENSE` shows `MIT License` and the 2026 copyright line.
- [ ] **Step 3: Commit** — `git add LICENSE && git commit -m "Add root MIT LICENSE"`

---

### Task 2: strategy-os/SKILL.md (orchestrator)

**Files:** Create `strategy-os/SKILL.md`

- [ ] **Step 1: Write the frontmatter**

```yaml
---
name: strategy-os
description: "Runs an end-to-end McKinsey/BCG/Bain-style strategy engagement, coordinating diagnosis, market research, strategic choice, and executive communication. Use when the user wants a full strategy workup — not just one analysis — e.g. 'build a strategy', 'run a strategy engagement', diagnose-to-recommendation work, or board-ready strategic decisions."
license: MIT. Complete terms in LICENSE.
allowed-tools: Read, Grep, Glob, WebFetch, WebSearch, Write, Bash
---
```

- [ ] **Step 2: Write the body** covering, in order:
  - A short intro: this skill is the orchestrator for a six-phase engagement built on the MBB spine (crisp framing, MECE, hypothesis-led, 80/20, answer-first).
  - **The six phases**, each with: objective (1-2 lines) + what to do:
    1. **Diagnosis & Framing** → load `references/situation-assessment.md`.
    2. **Market & Competitive Intelligence** → hand off to the **`market-research` skill** (it runs its own parallel-collection → verification → PPTX workflow and returns the pyramid analysis + deck). strategy-os does not re-implement that.
    3. **Strategic Choice & Economics** → load `references/strategic-options.md`, then `references/business-case-builder.md`.
    4. **Operating Model & Execution** → *Roadmap — not built this cycle.* One line on what it will cover.
    5. **Risk, Performance & Value Governance** → *Roadmap — not built this cycle.*
    6. **Alignment & Executive Communication** → load `references/decision-memo.md`.
  - **Progressive disclosure note:** read a phase's reference file only when that phase is active.
  - **Roadmap section:** list the deferred phases (4, 5) and the other upstream-inspired methods to add in later cycles.
  - **Attribution line:** inspired by `aapersh/strategy-skills-for-claude`; independently authored (clean-room) under MIT.

- [ ] **Step 3: Verify**
  - `grep -nE "^name: strategy-os|^license: MIT|^allowed-tools:" strategy-os/SKILL.md` shows all three; the allowed-tools line does NOT contain `Task`.
  - `grep -c "market-research" strategy-os/SKILL.md` ≥ 1 (Phase 2 hand-off).
  - `grep -ciE "roadmap|not built this cycle" strategy-os/SKILL.md` ≥ 1.

- [ ] **Step 4: Commit** — `git add strategy-os/SKILL.md && git commit -m "Add strategy-os orchestrator SKILL.md"`

---

### Task 3: references/situation-assessment.md (clean-room)

**Files:** Create `strategy-os/references/situation-assessment.md`

- [ ] **Step 1: Author from intent** (upstream closed). Use the four headings `## Use it when`, `## How to think about it`, `## Steps`, `## Deliverable`. Intent: produce a defensible current-state read before any strategy debate — what is true now, what is inference, what is still unknown, across the dimensions that matter to the decision (performance, market, customers, operations, organization). The `## Deliverable` is an original markdown template (e.g., an executive read + a facts/inferences/unknowns split + the few facts that matter + next diagnostic questions). Original wording throughout.
- [ ] **Step 2: Verify** — file has all four headings; `grep -ri "McKinsey-Style Approach\|When To Use" strategy-os/references/situation-assessment.md` returns nothing.
- [ ] **Step 3: Commit** — `git add strategy-os/references/situation-assessment.md && git commit -m "Add situation-assessment playbook"`

---

### Task 4: references/strategic-options.md (clean-room)

**Files:** Create `strategy-os/references/strategic-options.md`

- [ ] **Step 1: Author from intent** (upstream closed). Same four headings. Intent: develop a small set of genuinely distinct, mutually-exclusive strategic paths; define decision-relevant evaluation criteria; judge each path against them; recommend one with trade-offs and key risks. `## Deliverable` = original template (options table, criteria/scoring, recommendation + rationale + risks).
- [ ] **Step 2: Verify** — four headings present; no upstream heading strings.
- [ ] **Step 3: Commit** — `git add strategy-os/references/strategic-options.md && git commit -m "Add strategic-options playbook"`

---

### Task 5: references/business-case-builder.md (clean-room)

**Files:** Create `strategy-os/references/business-case-builder.md`

- [ ] **Step 1: Author from intent** (upstream closed). Same four headings. Intent: turn a chosen path into an economic argument — where value comes from (value drivers), what it costs, the assumptions it rides on, behavior under base/upside/downside scenarios, and whether it clears the hurdle (go/no-go). `## Deliverable` = original template (value drivers, cost lines, assumptions, scenario table, recommendation).
- [ ] **Step 2: Verify** — four headings present; no upstream heading strings.
- [ ] **Step 3: Commit** — `git add strategy-os/references/business-case-builder.md && git commit -m "Add business-case-builder playbook"`

---

### Task 6: references/decision-memo.md (clean-room)

**Files:** Create `strategy-os/references/decision-memo.md`

- [ ] **Step 1: Author from intent** (upstream closed). Same four headings. Intent: a board-ready, answer-first memo — recommendation first, the few reasons it holds, cost and risk, and the explicit decision being requested. The `## Deliverable` template must include an explicit "Decision requested" line so the memo is genuinely board-ready. Original wording.
- [ ] **Step 2: Verify** — four headings present; `grep -c "Decision requested" strategy-os/references/decision-memo.md` ≥ 1; no upstream heading strings.
- [ ] **Step 3: Commit** — `git add strategy-os/references/decision-memo.md && git commit -m "Add decision-memo playbook"`

---

### Task 7: Rewrite root README.md

**Files:** Modify `README.md` (root)

- [ ] **Step 1: Rewrite** as the strategy-OS landing page:
  - Title + one-line description (a strategy OS: orchestrator + market-research engine).
  - **The 6-phase map** (Diagnose → Map → Choose → Operate → Govern → Communicate), marking phases 4 & 5 as roadmap.
  - **The two skills:** `strategy-os` (umbrella orchestrator + the 4 method playbooks) and `market-research` (Phase-2 engine).
  - **Install** (copy each skill dir into a `.claude/skills/` directory; restart).
  - **Roadmap** (deferred phases + methods).
  - **License:** MIT — Copyright (c) 2026 Gilles van Heijst and YaWorks (see `LICENSE`).
  - **Credit:** inspired by `aapersh/strategy-skills-for-claude`, **independently authored**; note upstream has no license, so this clean-room reimplementation is what makes the work distributable under MIT.

- [ ] **Step 2: Verify** — `grep -ciE "strategy-os|market-research|roadmap|aapersh|MIT" README.md` ≥ 1 each; `grep -ci "independently authored" README.md` ≥ 1.
- [ ] **Step 3: Commit** — `git add README.md && git commit -m "Rewrite root README as strategy-OS landing page"`

---

### Task 8: Verification & validation

- [ ] **Step 1: Pre-flight the validator path**

Run: `test -f ~/.claude/commands/skills/scripts/quick_validate.py && echo HAVE_VALIDATOR || echo NO_VALIDATOR`
If `NO_VALIDATOR`, fall back to a manual frontmatter check (name + description present, valid YAML).

- [ ] **Step 2: Validate the skill**

Run (if validator present): `PYTHONPATH=~/.claude/commands/skills/scripts python3 ~/.claude/commands/skills/scripts/quick_validate.py strategy-os`
Expected: validation passes.

- [ ] **Step 3: Clean-room spot-check (no upstream heading set anywhere)**

Run: `grep -riE "McKinsey-Style Approach|^## When To Use|^## Output Format|^## Quality Bar" strategy-os/ || echo CLEAN`
Expected: `CLEAN` (these are the distinctive upstream heading sentinels — none should appear).
Then manually skim each playbook to confirm prose is independent, not reworded upstream.

- [ ] **Step 4: market-research untouched**

Run: `git diff --quiet HEAD -- market-research && echo MR_UNCHANGED || echo MR_CHANGED`
Expected: `MR_UNCHANGED` (no commits in this plan touched `market-research/`).

- [ ] **Step 5: Structure present**

Run:
```bash
test -f strategy-os/SKILL.md && ls strategy-os/references/*.md | wc -l && test -f LICENSE && echo OK
```
Expected: `4` reference files and `OK`.

- [ ] **Step 6: Final commit if any verification fixups were made.**

---

## Success Criteria (from spec)

1. `strategy-os/SKILL.md` valid frontmatter (no `Task`), six phases, Phase 2 hand-off, phases 4/5 roadmap. ✓ Task 2
2. Four playbooks with this repo's heading shape (not upstream's). ✓ Tasks 3-6
3. Clean-room verified (no upstream headings/layouts; independent prose). ✓ Tasks 3-6, 8
4. `market-research/` unchanged. ✓ Task 8
5. Root README = 6-phase OS, roadmap, install, MIT, inspired-by/independent credit. ✓ Task 7
6. Root `LICENSE` exists; frontmatter consistent. ✓ Tasks 1, 2
7. `strategy-os` passes `quick_validate.py`. ✓ Task 8
