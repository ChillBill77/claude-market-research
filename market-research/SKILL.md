---
name: market-research
description: "Professional market research and competitive analysis using McKinsey/BCG/Bain methodologies. Use when analyzing markets, competitive landscapes, customer insights, or strategic positioning. Runs hypothesis-driven pyramid analysis with parallel research subagents and produces a PPTX deliverable."
license: MIT. Complete terms in LICENSE.txt
allowed-tools: Read, Grep, Glob, WebFetch, WebSearch, Write, Bash, Task
---

# Market Research: MBB-Grade Analysis & PPTX Deliverables

Execute professional market research using proven methodologies from top consulting firms (McKinsey, BCG, Bain). This skill generates hypothesis-driven analysis structured as a four-level pyramid: Segment/Market → Customers → Competitors → Your Company, culminating in a presentation-ready PPTX artifact.

## When to Use This Skill

Activate this skill when the user requests:
- Market sizing and industry analysis
- Competitive landscape assessment
- Customer needs and behavioral research
- Strategic positioning evaluation
- Business intelligence gathering
- Client-ready market research presentations

## Quality Standard

Work must demonstrate **master-level execution** typical of top consulting firms:
- Every insight backed by solid numbers and cited sources
- Strategic rigor matching McKinsey/BCG/Bain standards
- Professional-grade visual design (avoid AI slop: no purple gradients, no centered-everything layouts, no generic templates)
- CRAAP-validated sources only
- Multi-source triangulation for critical findings

---

## Three-Phase Workflow

### Phase 1: Foundation

Create the strategic foundation using hypothesis-driven methodology.

**Execute these steps:**

1. **Define the problem** using SMART criteria (Specific, Measurable, Achievable, Relevant, Time-bound)
2. **Build hypothesis tree** applying MECE principle (Mutually Exclusive, Collectively Exhaustive)
   - Reference: `references/MBB_METHODOLOGY.md` for MECE framework details
3. **Identify source strategy** prioritizing free, high-credibility resources
   - Reference: `references/FREE_SOURCES_GUIDE.md` for Tier 1-3 source hierarchy
4. **Generate research brief** using template: `templates/research-brief.md`
5. **Establish success metrics** and validation criteria

**Deliverable:** Research brief document (4-6 paragraphs) articulating:
- Core research question and decision context
- Hypothesis structure (MECE-validated)
- Source identification strategy
- Success criteria and timeline

**Standard:** Brief must demonstrate "strategic clarity typical of top consulting firms" - clear problem definition, structured thinking, actionable scope.

---

### Phase 2: Parallel Collection

Collect and validate data across the four pyramid levels, building from broad market context to specific company positioning. The three outward-facing levels (Market, Customer, Competitive) are independent, so they are researched **concurrently by subagents**. Level 1 (Company) depends on the Level 2 findings and is done afterward by the main thread.

#### Dispatch three subagents in a single message

Dispatch all three Task subagents (`general-purpose`) in one message so they research concurrently. Each is given the contract prompt below and writes one file. Wait for all three to finish.

| Agent | Level | Focus | Output file |
|-------|-------|-------|-------------|
| L4 | Market & Segment | Market size (TAM/SAM/SOM), CAGR & historical trends, drivers, opportunities/threats | `analysis/level-4-market.md` |
| L3 | Customer Insights | Segments & demographics, needs/motivations/pain points, purchase barriers, decision process, behaviors | `analysis/level-3-customer.md` |
| L2 | Competitive Landscape | Top 3-5 competitors: positioning, offering, messaging, how they meet customer needs, strengths & vulnerabilities | `analysis/level-2-competitive.md` |

**Source priority (all levels):** Tier 1 first (government statistics, academic journals, public filings), then Tier 2 (industry associations, trade publications, OECD/World Bank/IMF), Tier 3 only with cross-validation. See `references/FREE_SOURCES_GUIDE.md`.

#### Subagent contract prompt

Substitute `<N>`, `<NAME>`, `<FOCUS>`, `<OUTPUT_FILE>`, and `<TOPIC>` for each level:

```
You are researching Level <N>: <NAME> for a market-research project on <TOPIC>.
Focus: <FOCUS>.

Rules:
- Tier-1 sources first (government stats, academic, public filings); Tier-2 next.
- Any critical number needs >=2 independent sources (triangulate).
- Apply the CRAAP test; use only sources scoring >=18/25 as primary evidence.
- Never fabricate figures. If data cannot be found, say so under Confidence & Gaps.

Write your findings to <OUTPUT_FILE> with EXACTLY these sections:

# Level <N>: <NAME>
## Key Findings
- 3-6 bullets; each ends with (Source: <citation>, CRAAP: <score>/25)
## Detail
<analysis body>
## Sources
<one row per source, matching the columns in templates/source-bibliography.md>
## Confidence & Gaps
<what is solid, what is thin, what still needs triangulation>

Return only a one-line confirmation of the file written.
```

#### After the three subagents return

1. **Level 1: Your Company Position** — perform this yourself, written to `analysis/level-1-company.md` using the SAME four contract sections. Assess current strategy and business model, capabilities and culture, core strengths, brand positioning potential, and strategic fit — benchmarking against the Level 2 findings (gap analysis: market needs vs. company capabilities).

2. **Verification gate** — dispatch **four verifier subagents in a single message** (one per level file: L4, L3, L2, L1), running concurrently. Each is a `general-purpose` Task agent (web access via WebSearch/WebFetch) given ONLY its own level file path plus the verifier contract below — no other levels, to keep verification independent. Wait for all four, then aggregate `analysis/verification-report.md` (template: `templates/verification-report.md`).

   **Verifier contract prompt** (substitute `<N>` and `<LEVEL_FILE>`):

   ```
   You independently verify Level <N> findings for a market-research project.
   Read ONLY this file: <LEVEL_FILE>. You did not produce it. Be adversarial:
   assume each Key Finding is WRONG until evidence holds. Use WebSearch/WebFetch
   to seek contradicting data.

   For each bullet under "## Key Findings" (reference it as L<N>-1, L<N>-2, ... in order):
   1. Check the cited source actually supports the SPECIFIC claim (not just that it exists).
   2. Search for contradicting data or alternative figures.
   3. Assign exactly one verdict:
      - Confirmed — independent evidence supports it.
      - Refuted — credible evidence contradicts it (give a counter-source).
      - Unverifiable (insufficient data) — could not corroborate OR refute.
        ABSENCE OF COUNTER-EVIDENCE IS NOT CONFIRMATION. Use this verdict whenever
        you could not independently establish the claim.

   Write results to analysis/level-<N>-verification.md, one block per finding:

   - Finding: L<N>-<i> — <short reference>
     Verdict: Confirmed | Refuted | Unverifiable (insufficient data)
     Reason: <one line>
     Counter-source: <citation — only when Refuted>
     Missing data: <what was needed — only when Unverifiable>

   Return only a one-line confirmation of the file written.
   ```

3. **Synthesize** all four level files into `analysis/pyramid-analysis.md` using `templates/pyramid-analysis.md`. This is a mechanical merge:
   - Key Findings roll up into the Executive Summary.
   - Each level's `## Sources` rows concatenate into `analysis/source-bibliography.md` (template: `templates/source-bibliography.md`), with CRAAP scores.
   - Each level's `## Confidence & Gaps` drives any final triangulation before you commit to a number.
   - Apply the verification verdicts from `analysis/verification-report.md`:
     - **Refuted** → omit the finding from `pyramid-analysis.md` (it stays in `verification-report.md` with its counter-source as the audit trail).
     - **Unverifiable (insufficient data)** → keep the finding but flag it inline with `⚠ unverified (insufficient data)`.
     - **Confirmed** → keep normally.

#### Data Collection Standards

For each pyramid level:
1. **Source tracking:** every source recorded in `source-bibliography.md`
2. **CRAAP validation:** score Currency, Relevance, Authority, Accuracy, Purpose
3. **Triangulation:** validate critical findings with 2-3 independent sources
4. **Documentation:** capture methodology, limitations, confidence levels

**McKinsey principle:** "Any solution not backed by solid numbers carries heavy burden of proof"

---

### Phase 3: Synthesis & Deck

Transform the analysis into a presentation-ready PPTX using professional design standards.

**Execute these steps:**

1. **Prepare HTML slides** using `templates/slide-deck.html`:
   - Dimensions: 720pt width × 405pt height (16:9 aspect ratio)
   - ALL text must be in `<p>`, `<h1>`-`<h6>`, `<ul>`, or `<ol>` tags (html2pptx requirement)
   - Use professional color scheme from `assets/color-scheme.json`
   - Apply pyramid visual from `assets/pyramid-diagram.svg`

2. **Generate slide content** (7-9 slides):
   - **Slide 1:** Title - Project name, client, date
   - **Slide 2:** Executive Summary - 3-5 key findings
   - **Slide 3:** Segment & Market Analysis (Pyramid Level 4)
   - **Slide 4:** Customer Insights (Pyramid Level 3)
   - **Slide 5:** Competitive Landscape (Pyramid Level 2)
   - **Slide 6:** Your Company Position (Pyramid Level 1)
   - **Slide 7:** Strategic Recommendations - Action items with ownership
   - **Slide 8:** Next Steps - Timeline and priorities
   - **Slide 9:** Appendix: Sources Bibliography + Verification Summary (counts: confirmed / refuted / unverified, plus any ⚠ unverified findings)

3. **HTML quality checklist** — before handing the HTML to the `pptx` skill, verify:
   - Slide canvas is 720pt × 405pt (16:9).
   - ALL text is inside `<p>`, `<h1>`-`<h6>`, `<ul>`, or `<ol>` — never bare `<div>`/`<span>` (bare text renders invisible in PPTX).
   - No "AI slop" palette (no Tailwind purples `#6366F1` / `#8B5CF6` / `#A855F7`).
   - Every data point carries a source citation.

4. **Generate the PPTX:** invoke the native **`pptx`** skill with `deliverables/slide-deck.html`. It parses the HTML via the html2pptx workflow and writes `deliverables/<client>-report.pptx`.

**Deliverable:** `<client>-report.pptx` - Professional presentation matching MBB standards

**Standard:** "Museum-quality execution" with "meticulous attention to craft" - every slide should appear professionally designed, every insight substantiated.

---

## Helper Scripts

### Initialize New Research Project

```bash
bash scripts/init-research.sh <client-name> <industry>
```

Creates project structure with pre-populated templates. Runs correctly from any working directory.

### Automated Source Validation

```bash
python scripts/validate-sources.py <bibliography-file>
```

Runs automated CRAAP scoring on all documented sources, outputs validation report.

---

## References

Detailed methodologies are in `references/` for deep consultation:

- **MBB_METHODOLOGY.md** - McKinsey 7-step problem-solving process, MECE principle, Pyramid Principle, Issue Trees, 80/20 rule
- **FREE_SOURCES_GUIDE.md** - Comprehensive guide to Tier 1-3 data sources with focus on free government and academic resources
- **VALIDATION_FRAMEWORKS.md** - Complete CRAAP test framework, Six Essential Questions, triangulation methods

Grep these files when needing specific framework details during analysis.

---

## Common Pitfalls to Avoid

1. **Accepting sources at face value** → Apply systematic CRAAP evaluation
2. **Cherry-picking data** → Use comprehensive search, document all relevant sources
3. **Ignoring original context** → Understand data collection purpose and limitations
4. **Over-reliance on single database** → Multi-source triangulation mandatory
5. **Outdated information** → Check publication dates, verify currency
6. **Unclear methodology** → Only use sources with transparent methodology

---

## PPTX Generation

Phase 3 uses the native **`pptx`** skill (Anthropic document-skills suite) to convert the HTML slide deck into a `.pptx`. No local installation or git submodule is required — invoke the `pptx` skill directly and provide the path to `deliverables/slide-deck.html`.

Reference: https://github.com/anthropics/skills/tree/main/document-skills/pptx

---

## Success Checklist

Before delivering research to client, verify:

✓ Research brief demonstrates clear hypothesis-driven approach
✓ All four pyramid levels analyzed with CRAAP-validated sources
✓ Critical findings triangulated with 2-3 independent sources
✓ Every quantitative claim backed by cited source
✓ Source bibliography complete with validation scores
✓ PPTX presentation follows professional design standards
✓ No AI slop patterns (generic layouts, purple gradients, etc.)
✓ Slide narrative flows logically from market to company
✓ Recommendations are specific, actionable, and prioritized
✓ Final deliverable matches McKinsey/BCG/Bain quality standards
