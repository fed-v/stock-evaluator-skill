# Stock Evaluator — Pre-Purchase Analysis Skill

**A professional-grade Claude skill that turns any stock ticker into a structured investor memo — grounded in private equity due-diligence practices.**

[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Skill spec](https://img.shields.io/badge/spec-SKILL.md-black?style=flat-square)](SKILL.md)
[![Compatible with](https://img.shields.io/badge/works%20with-Claude%20Code%20%7C%20Cowork%20%7C%20Claude.ai-orange?style=flat-square)](https://docs.anthropic.com/en/docs/claude-code)

---

**→ [See a live example: Shopify (SHOP) full analysis](demo/SHOP-analysis.md)**

---

## What It Does

Ask Claude to evaluate a stock, and this skill activates a 22-section investor memo covering everything from forensic accounting red flags to entry-price margin-of-safety math. It doesn't give you a stock tip — it gives you the structured thinking you'd want before making any investment decision.

**Example triggers:**
- *"Should I buy NVDA?"*
- *"Evaluate AAPL for me"*
- *"Is PayPal a good investment right now?"*
- *"Run your checklist on Tesla"*
- *"Analyze this stock: $MSFT"*

---

## Why This Skill Exists

Most AI stock "analysis" produces confident-sounding summaries stitched from whatever Google surfaces first. This skill is different: it enforces a rigid quality-control layer before any output is generated — demanding primary sources (SEC filings, 10-K/10-Q), correct period labels, proper SBC treatment, and explicit sourcing for every material claim.

The goal is to make Claude a more disciplined analyst, not a faster one.

---

## Output: 22-Section Investor Memo

Every evaluation follows this fixed structure, always in this order:

| # | Section | What it covers |
|---|---------|---------------|
| 1 | **Disclaimer** | Educational-use notice |
| 2 | **Company Snapshot** | Ticker, price, market cap, EV, TTM revenue, business model, archetype |
| 3 | **Hard Stop Scan** | Auditor resignations, fraud allegations, SEC investigations, material weaknesses — defaults to AVOID if triggered |
| 4 | **Data Integrity Check** | Source validation before analysis begins |
| 5 | **Dominant-Risk Weighting** | Identifies the single biggest risk to thesis |
| 6 | **Business-Model-Specific Risk** | KPIs and risks calibrated to archetype (SaaS, marketplace, bank, etc.) |
| 7 | **P&L Health** | Revenue trends, margin trajectory, operating leverage |
| 8 | **Cash-Flow Quality & Owner Earnings** | FCF, SBC adjustment, owner earnings calculation |
| 9 | **Balance Sheet & Liquidity** | Debt structure, coverage ratios, liquidity |
| 10 | **Growth Durability** | Revenue growth quality, cohort signals, TAM ceiling |
| 11 | **Competitive Position / Moat** | Pricing power, switching costs, market share trends |
| 12 | **Management, Governance & Capital Allocation** | Insider activity, buyback quality, compensation structure |
| 13 | **Earnings Quality & Forensic Accounting** | Accrual ratios, Beneish M-Score, CAMs, auditor opinion |
| 14 | **Macro, Sector & External Risks** | Rate sensitivity, regulatory exposure, cyclicality |
| 15 | **Historical Price & Volatility** | Beta, drawdown history, 52-week context |
| 16 | **Valuation vs. Expected Return** | P/E, EV/EBITDA, DCF check, implied IRR |
| 17 | **Quantitative Overlays** | Piotroski F-Score, Altman Z-Score (when inputs available) |
| 18 | **Summary Weighted Scorecard** | Aggregated rating across all dimensions |
| 19 | **Entry Price / Margin of Safety** | Fair value range, downside protection math |
| 20 | **Thesis Breakers / Kill Criteria** | Pre-defined conditions that would invalidate the investment case |
| 21 | **Final Verdict** | Buy / Hold / Avoid with explicit reasoning |
| 22 | **Sources** | Every data point linked to its filing, period, and tier |

---

## Design Decisions

This skill was built by working backward from failure modes — specific ways AI financial analysis produces confident-sounding but unreliable output. Each design decision below addresses a problem that was discovered and verified during development.

### Rules over judgment for quality control

The most important decision was replacing soft guidance ("be accurate", "use reliable sources") with explicit, non-negotiable rules. LLM behavior drifts across long outputs — a model that starts disciplined can quietly lapse by section 14. Rules lock in behavior regardless of output length.

Each rule targets a specific observed failure:

- **TTM confusion** — AI routinely labels full-year revenue as "TTM." The correct calculation is hard-wired: latest FY + current-year interim − prior-year comparable interim. No estimation, no shortcuts.
- **Debt vs. liabilities conflation** — Treating total liabilities as financial debt makes companies look far more leveraged than they are. The skill requires explicit separation across six line items: cash / short-term debt / long-term debt / finance leases / operating leases / operating liabilities.
- **SBC misdirection** — AI tends to describe SBC as "declining" when only the percentage fell while the absolute dollar amount grew. The skill requires three simultaneous views (absolute $, % of revenue, % of FCF) before any directional statement is permitted.
- **Buyback theater** — Board authorizations make headlines; actual repurchases are what move the share count. The skill requires five specific data points: shares repurchased, dollars spent, average price, remaining authorization, and whether the buyback was value-accretive at that price.
- **Take rate assertion** — Marketplace analysis often states that take rate is "rising" or "stable" without showing the math. The skill requires an explicit calculation (revenue ÷ GMV/TPV/GTV) for the current and prior periods before any directional claim is made.

### Analysis gate before narrative

The Hard Stop Scan (Section 3) runs before any other analysis. If it surfaces a qualified auditor opinion, SEC investigation, material weakness in internal controls, or credible fraud allegation, the default verdict is AVOID — and no downstream financial strength can override it. This prevents the model from building a compelling analysis on top of a disqualified company.

### Valuation as a structural override

In a naive scoring system, a cluster of green qualitative checks can outvote a red valuation flag. This skill explicitly disables that behavior: for high-growth or high-multiple names, valuation and expected return is locked at 30–40% of the weighted scorecard, and the framework prohibits qualitative business-quality scores from masking a pricing problem. The most common failure mode in AI bull-market analysis is rationalizing expensive valuations through operational flattery. This rule prevents it structurally.

### Expected-return math, not just multiples

Valuation analysis stops too early when it only reports P/E and EV/EBITDA. Section 16 adds a reverse-DCF table with bear, base, and bull scenarios answering one question: *what has to be true about this business for the stock to beat the market from current prices?* This forces the analysis to take a position rather than describe a range.

### Kill criteria tied to the entry thesis

Generic exit signals ("if growth slows, reconsider") are not actionable. The kill criteria in Section 20 are derived directly from the reverse-DCF assumptions in Section 16. If the thesis requires 25% revenue growth to justify the current multiple, the kill criterion is calibrated to that number — and it is designed to trigger before the business visibly collapses, not after. For expensive growth stocks, a visible collapse means the multiple has already re-rated violently downward.

### Per-share economics alongside totals

Total FCF can grow while per-share FCF quietly falls through dilution. Many investors track the wrong number. The skill requires showing diluted share count trends, SBC-driven dilution rate, and FCF per share alongside absolute FCF — so the picture is complete even for companies running aggressive equity compensation programs.

### Confidence tagging on every claim

Every material data point carries a tag: `[Verified]`, `[Market Data]`, `[Estimate]`, `[Qualitative judgment]`, or `[Unverified]`. A hard rule prohibits any `[Unverified]` claim from driving the scorecard verdict. This makes the epistemic status of the analysis visible rather than buried in prose confidence.

### Memo format over checklist format

Early versions produced a checklist — fine for coverage but easy to skim past. The final structure produces a 22-section investor memo with a fixed output order, a structured Final Verdict field, and prose reasoning rather than bullet ratings. The format change mattered: a memo forces synthesis; a checklist permits avoidance.

### Business-model-aware KPI layer

A single universal metric set produces shallow analysis across sectors. NRR is meaningless for a bank; combined ratio is irrelevant for a SaaS company; credit losses as a percentage of revenue matter for a BNPL lender but not for an industrial. The skill classifies each company into one of 15 archetypes and loads the appropriate KPI library from `references/business-model-kpis.md`. One framework, calibrated per sector.

### Source hierarchy with explicit tier labels

Every data point must be labeled with its source and tier. The hierarchy is enforced top-down: SEC filings first, then company releases and regulatory filings, then reputable financial data providers. News is acceptable for context only. Blogs and SEO content are explicitly prohibited for market-share claims, moat assessments, or any figure that feeds the scorecard. If two sources conflict on the same data point, the conflict must be flagged openly — never silently resolved. A standing rule makes it explicit: if a filing is cited anywhere in the analysis, it cannot later be declared unavailable.

---

## Evolution

This skill started as a 9-item checklist adapted from a YouTube video and was rebuilt through five distinct rounds of iteration. The driving question at each round was the same: *what can still produce a falsely confident output, and how do we close that gap?*

**Round 1 — From checklist to framework.** Added forensic accounting as a standalone check, ROIC analysis to separate valuable growth from value-destroying growth, per-share economics to catch dilution, and three quantitative overlays (Piotroski, Beneish, Altman). Added Hard Stop conditions that bypass the scorecard entirely.

**Round 2 — Source discipline and weighted scoring.** All checks had been treated as equally important. Added dominant-risk weighting by company archetype, kill criteria tied to the thesis, reverse-DCF expected-return math, and confidence tags on every claim. Added a Data Integrity Check that runs before scoring begins.

**Round 3 — Professional-grade rebuild.** Output still read like a checklist, not an investor memo. Rebuilt as a 22-section structured memo. Added business-model-specific risk checks backed by a 300-line sector KPI reference file. Added mandatory SBC-adjusted owner earnings, full balance sheet debt separation, and a structured Final Verdict format.

**Round 4 — Closing specific accuracy gaps.** Eleven targeted fixes: buyback analysis required five specific data points; SBC required both absolute and percentage trends; take rates required explicit calculation rather than assertion; credit losses gained hard-red thresholds; kill criteria for expensive growth stocks were calibrated to fire before visible distress.

**Round 5 — Filing-data extraction discipline.** EV calculation was corrected to deduct marketable securities and short-term investments, not just cash. Data Integrity Check expanded from 26 to 49 rows. "Needs Review" was restricted to data genuinely absent from all reviewed filings — it can no longer be applied to items present in a 10-Q or 10-K that was cited. Entry-price table now shows the formula for each column.

The skill grew from 9 checks to a 931-line framework with a 312-line sector KPI library. Each round made it harder for bad inputs to produce confident outputs, and harder for a strong operational story to paper over a broken valuation.

---

## Installation

### Option A — Copy into your Claude config (recommended for personal use)

```bash
# Claude Code / Cowork / Claude.ai Desktop
git clone https://github.com/fed-v/stock-evaluator-skill \
  ~/.claude/skills/stock-evaluator
```

Or manually:

```bash
cp -r stock-evaluator/  ~/.claude/skills/stock-evaluator/
```

Claude will discover the skill automatically on the next session.

### Option B — Project-level install

Drop the folder into your project's `.claude/skills/` directory to scope it to a specific workspace:

```bash
cp -r stock-evaluator/  your-project/.claude/skills/stock-evaluator/
```

### Option C — Other agents

For agents that follow the `SKILL.md` convention (Cursor, Codex CLI, OpenCode):

```bash
# Cursor
cp -r stock-evaluator/  your-project/.agents/skills/stock-evaluator/

# Codex CLI
cp -r stock-evaluator/  your-project/.codex/skills/stock-evaluator/
```

---

## Compatibility

| Agent / Runtime | Skill path | Status |
|----------------|-----------|--------|
| **Claude Code** | `.claude/skills/stock-evaluator/` | ✅ Verified |
| **Cowork (Claude Desktop)** | `.claude/skills/stock-evaluator/` | ✅ Verified |
| **Claude.ai** (web) | Settings → Capabilities → Skills | ✅ Verified |
| **Cursor** | `.agents/skills/stock-evaluator/` | ✅ Compatible |
| **Codex CLI** | `.codex/skills/stock-evaluator/` | ✅ Compatible |

---

## Disclaimer

This skill is for educational purposes only. It is not financial advice, investment advice, or a recommendation to buy or sell any security. Always do your own research and consult a qualified financial advisor before making investment decisions.

---

## License

MIT
