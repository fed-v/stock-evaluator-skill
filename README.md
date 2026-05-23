# Stock Evaluator — Pre-Purchase Analysis Skill

**A professional-grade Claude skill that turns any stock ticker into a structured investor memo — grounded in private equity due-diligence practices.**

[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Skill spec](https://img.shields.io/badge/spec-SKILL.md-black?style=flat-square)](SKILL.md)
[![Compatible with](https://img.shields.io/badge/works%20with-Claude%20Code%20%7C%20Cowork%20%7C%20Claude.ai-orange?style=flat-square)](https://docs.anthropic.com/en/docs/claude-code)

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

## Key Design Decisions

### Non-Negotiable Quality Controls

The skill ships with a strict QC ruleset that Claude cannot bypass:

- **Source consistency** — Data labeled *Verified* only when the exact filing and period are both explicit. No stale financials when a newer 10-Q or 10-K exists.
- **Period discipline** — Fiscal-year, quarterly, and TTM figures must always be labeled. TTM is calculated correctly (latest FY + current interim − prior-year comparable), never estimated.
- **SBC treatment** — Stock-based compensation is always shown three ways: absolute $, % of revenue, % of FCF. SBC > 10% of revenue is a red flag; > 25% of FCF flags owner-earnings impact explicitly.
- **Buyback rigor** — Authorization ≠ execution. If repurchases occurred, the skill shows shares repurchased, dollars spent, average price, and accretion/dilution analysis.
- **Debt separation** — Total liabilities are never confused with financial debt. Every balance-sheet section separates cash / short-term debt / long-term debt / operating leases / finance leases.
- **Valuation weighting** — For high-multiple or high-growth names, valuation/expected return carries 30–40% of the scorecard. A cluster of green qualitative checks cannot override a major valuation red flag.

### Business-Model-Aware KPIs

The skill loads a reference document (`references/business-model-kpis.md`) that maps each company archetype to its relevant performance metrics:

- **SaaS / Software** → ARR growth, NRR, Rule of 40, magic number
- **Marketplace / Platform** → GMV, take rate, liquidity metrics
- **Payments / Fintech / BNPL** → TPV, credit losses as % of revenue, charge-off trends
- **Bank / Insurance** → NIM, efficiency ratio, Tier 1 capital, combined ratio
- **Retail** → Comp-store sales, inventory turns, gross margin by channel
- *...and more*

### Source Hierarchy

Claude is instructed to use the highest available evidence tier and label everything:

1. SEC filings (10-K, 10-Q, 20-F) — *Primary*
2. Earnings releases, investor presentations — *Company releases*
3. Proxy statements (DEF 14A), Form 4 insider activity — *Regulatory filings*
4. Reputable financial data providers — labeled with provider name and date
5. News — context only, never a scorecard basis
6. Blogs / SEO content — explicitly prohibited for any material claim

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
