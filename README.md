# Stock Evaluator — Pre-Purchase Analysis Skill

![Stock Evaluator](hero.png)

**A professional-grade Claude skill that turns any stock ticker into a structured investor memo — grounded in private equity due-diligence practices.**

[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Skill spec](https://img.shields.io/badge/spec-SKILL.md-black?style=flat-square)](SKILL.md)
[![Compatible with](https://img.shields.io/badge/works%20with-Claude%20Code%20%7C%20Cowork%20%7C%20Claude.ai-orange?style=flat-square)](https://docs.anthropic.com/en/docs/claude-code)

---

**→ [See a live example: Shopify (SHOP) full analysis](demo/SHOP-analysis.md)**

---

## What It Does

Ask Claude to evaluate a stock, and this skill activates a 25-section investor memo covering everything from forensic accounting red flags to entry-price margin-of-safety math. It doesn't give you a stock tip — it gives you the structured thinking you'd want before making any investment decision.

**Example triggers:**
- *"Run your evaluator on NVDA before I add to my position"*
- *"What are the red flags on AAPL right now?"*
- *"What does PayPal's current price assume about growth?"*
- *"Build me a thesis on Tesla — what needs to stay true?"*
- *"What should I be monitoring on $MSFT after earnings?"*

---

## Why This Skill Exists

Most AI stock "analysis" produces confident-sounding summaries stitched from whatever Google surfaces first. This skill is different: it enforces a rigid quality-control layer before any output is generated — demanding primary sources (SEC filings, 10-K/10-Q), correct period labels, proper SBC treatment, and explicit sourcing for every material claim.

The goal is to make Claude a more disciplined analyst, not a faster one.

---

## How to Use It

This skill is not a stock picker. It is a thesis builder.

The question to bring is not *"Tell me whether to buy"* — it is *"Show me what can go wrong, what needs to stay true, what the current price assumes, and what I should monitor."* That shift in framing is where it becomes genuinely useful.

A productive workflow:

1. **Run the evaluator before buying or adding to a position.** Get the full memo before any capital is committed.
2. **Read the red flags first, not the verdict.** The Final Verdict is a synthesis — the red flags are the raw material. Start there.
3. **Ask follow-up questions about the red flags.** The memo surfaces concerns; you decide whether they are priced in, manageable, or disqualifying.
4. **Decide whether the risks are acceptable given the entry price.** A business can have real problems and still be a good investment at the right price. The reverse is also true.
5. **Copy the kill criteria and watch items into an earnings-review checklist.** The thesis breakers in Section 23 are designed to be tracked across quarters, not read once.
6. **Re-run after earnings to see whether the thesis improved, weakened, or broke.** The memo gives you a baseline. Subsequent runs show you drift.

The goal is not a recommendation — it is a structured basis for your own judgment.

---

## Output: 25-Section Investor Memo

Every evaluation follows this fixed structure, always in this order:

| # | Section | What it covers |
|---|---------|---------------|
| 1 | **Disclaimer** | Educational-use notice |
| 2 | **Company Snapshot** | Ticker, price, market cap, EV, TTM revenue, business model, archetype |
| 2A | **Company Archetype Classification** | Business model classification that determines which KPI library applies — prerequisite for all downstream analysis |
| 3 | **Hard Stop Scan** | Auditor resignations, fraud allegations, SEC investigations, material weaknesses — defaults to AVOID if triggered |
| 4 | **Data Integrity Check** | Source validation and confidence tagging before analysis begins |
| 5 | **Dominant-Risk Weighting** | Identifies the single biggest risk to the thesis; sets the floor for its scorecard weight |
| 6 | **Business-Model-Specific Risk Check** | KPIs and risks calibrated to the classified archetype (SaaS, marketplace, bank, REIT, etc.) |
| 7 | **P&L Health** | Revenue trends, margin trajectory, operating leverage, period-labeled comparisons |
| 8 | **Cash-Flow Quality & Owner Earnings** | FCF generation, SBC adjustment from primary filings, owner earnings calculation |
| 9 | **Balance Sheet & Liquidity** | Debt structure separated across six line items, coverage ratios, liquidity runway |
| 10 | **Growth Durability** | Revenue growth quality, cohort signals, retention trends, TAM ceiling |
| 11 | **Competitive Position / Moat** | Pricing power, switching costs, network effects, market share trends |
| 12 | **Management, Governance & Capital Allocation** | Insider activity, buyback quality (five required data points), compensation structure |
| 13 | **Earnings Quality & Forensic Accounting** | Accrual ratios, Beneish M-Score, critical audit matters, auditor opinion |
| 14 | **Macro, Sector & External Risks** | Rate sensitivity, regulatory exposure, cyclicality, geopolitical exposure |
| 15 | **Historical Price & Volatility** | Beta, drawdown history, 52-week context |
| 16 | **Trading / Timing Context** ⚠️ | Short-term technical context only — cannot override fundamentals, valuation, or hard stops |
| 17 | **Valuation vs. Expected Return** | Reverse-DCF bear/base/bull scenarios; required growth rate to justify current price |
| 18 | **Quantitative Overlays** | Piotroski F-Score, Altman Z-Score (when inputs are available) |
| 19 | **Summary Weighted Scorecard** | Aggregated rating across all dimensions; valuation locked at 30–40% weight for high-multiple names |
| 20 | **Entry Price / Margin of Safety** | Fair value range with explicit compounding formula; downside protection math |
| 21 | **Catalysts to Watch** ⚠️ | Upcoming events that could move the thesis — for monitoring only, not verdict drivers |
| 22 | **Position Sizing / Portfolio Risk Framing** ⚠️ | Concentration, correlation, and sizing considerations — for execution only, not verdict drivers |
| 23 | **Thesis Breakers / Kill Criteria** | Pre-defined conditions calibrated to the reverse-DCF assumptions that would invalidate the investment case |
| 24 | **Final Verdict** | Buy / Hold / Avoid with explicit reasoning; must be consistent with scorecard weights |
| 25 | **Sources** | Every data point labeled with its filing, period, and source tier |

> ⚠️ **Sections 16, 21, and 22** (Trading/Timing, Catalysts, Position Sizing) are supporting sections only. They inform execution and monitoring. Combined, they carry a hard cap of 5% weight in the final scorecard and cannot override the verdict driven by valuation, business quality, hard stops, credit red flags, or owner-earnings math.

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

### Metric consistency across the memo

A 25-section memo is long enough that the same metric can appear under different names in different sections, with values that don't match. This happens silently — the model doesn't notice, the reader may not notice on a first pass, and the contradiction quietly undermines the analysis.

The skill enforces a single-value rule: if a metric is stated in Section 7, the same figure must appear in Section 17, Section 19, and wherever else it is referenced. Transportation revenue, fee-based revenue, and total services revenue are not interchangeable unless the filing uses them as the same line item. A DCF/share figure used in the valuation section must reconcile to the dividend/payout ratio used in the coverage section. If two numbers for the same concept appear in the same memo, one of them is wrong — and the skill is required to flag the conflict rather than silently pick one.

### Analysis gate before narrative

The Hard Stop Scan (Section 3) runs before any other analysis. If it surfaces a qualified auditor opinion, SEC investigation, material weakness in internal controls, or credible fraud allegation, the default verdict is AVOID — and no downstream financial strength can override it. This prevents the model from building a compelling analysis on top of a disqualified company.

### Valuation as a structural override

In a naive scoring system, a cluster of green qualitative checks can outvote a red valuation flag. This skill explicitly disables that behavior. For high-growth or high-multiple names, valuation and expected return is locked at 30–40% of the weighted scorecard. That weight cannot be set lower than the dominant-risk weight declared earlier in the memo. Strong business quality cannot outvote a poor entry price.

The rule also enforces internal consistency: if the final verdict says "wait for a better price," the numerical scorecard must not look like a strong buy. A memo that scores the business 8/10 overall but recommends waiting has a contradiction in it — and contradictions are resolved in favor of the harder constraint, which is price.

### Expected-return math, not just multiples

Valuation analysis stops too early when it only reports P/E and EV/EBITDA. Section 17 adds a reverse-DCF table with bear, base, and bull scenarios answering one question: *what has to be true about this business for the stock to beat the market from current prices?* This forces the analysis to take a position rather than describe a range.

The required sequence for the reverse-DCF is fixed and cannot be reversed: start with today's market cap or EV, apply the target return over the holding period to get the required exit value, divide by the exit multiple to get required future FCF or owner earnings, then compare that to current FCF or owner earnings to calculate the required CAGR. Always compound today's market cap forward first, then derive the required exit FCF. Deriving it in the opposite order produces systematically misleading results.

### Income stocks require a different valuation grammar

The reverse-DCF framework is built for capital-appreciation stocks, where the return comes from price. Applied to a pipeline, utility, REIT, or dividend-compounding stock, it systematically understates value by ignoring the dividend stream — which is often the majority of total return.

For income stocks, the skill switches valuation frameworks. The controlling metrics are DCF per share or AFFO per share, dividend coverage ratio, payout sustainability, and Debt/EBITDA. Intrinsic value is estimated as the present value of dividends plus the present value of terminal equity — where terminal equity is derived from the archetype-appropriate multiple (P/DCF, P/AFFO), not from an FCF exit. The reverse-DCF may still appear as a secondary cross-check, but it is explicitly labeled as a capital-appreciation-only calculation that excludes dividends.

The Final Verdict language also changes. "Strong Buy" and "Avoid" are the right labels for a growth stock trading far below or above intrinsic value. For a mature income stock trading at fair value with solid coverage, the right verdict is "Hold / Starter" or "Fairly valued — wait for better entry." Calling it a Strong Buy because the business quality is excellent, when there is no margin of safety, is a scoring error — not an insight.

This distinction matters because income investors are solving a different problem. They are not asking whether the stock will double. They are asking whether the dividend is safe, whether it will grow, and whether the current price gives them an adequate yield on cost. The memo must answer those questions in those terms.

### Kill criteria tied to the entry thesis

Generic exit signals ("if growth slows, reconsider") are not actionable. The kill criteria in Section 23 are derived directly from the reverse-DCF assumptions in Section 17. If the thesis requires 25% revenue growth to justify the current multiple, the kill criterion is calibrated to that number — and it is designed to trigger before the business visibly collapses, not after. For expensive growth stocks, a visible collapse means the multiple has already re-rated violently downward.

### Trading, catalysts, and sizing are capped at 5%

Three sections in the memo — Trading / Timing Context (16), Catalysts to Watch (21), and Position Sizing / Portfolio Risk Framing (22) — serve execution and monitoring. They exist because the right business at the wrong entry point, or sized incorrectly for a portfolio, produces bad outcomes even when the thesis is correct.

What they cannot do is drive the core verdict. Technicals, analyst price targets, RSI, moving averages, short interest, or upcoming catalysts do not change whether a business is cheap or expensive relative to its owner earnings. A stock that fails on valuation, cash-flow quality, a hard stop, or a thesis-breaking risk does not become a buy because the 50-day moving average is rising or because earnings are three weeks away. The combined scorecard weight for these three sections is hard-capped at 5%.

### Per-share economics alongside totals

Total FCF can grow while per-share FCF quietly falls through dilution. Many investors track the wrong number. The skill requires showing diluted share count trends, SBC-driven dilution rate, and FCF per share alongside absolute FCF — so the picture is complete even for companies running aggressive equity compensation programs.

### Confidence tagging on every claim

Every material data point carries a tag indicating its epistemic status: `[Verified]` for values pulled directly from primary filings or clearly identified company releases; `[Derived]` for calculations built from verified values; `[Market Data]` for stock price, market cap, beta, 52-week ranges, analyst estimates, and third-party price data; `[Estimate]` where the exact value was approximated; `[Qualitative judgment]` for subjective assessments; and `[Unverified]` where sourcing is absent or unclear. A hard rule prohibits any `[Unverified]` claim from driving the scorecard verdict. The distinction between `[Verified]` and `[Derived]` matters: a calculated ratio is not the same as a filed number, and calling it Verified when it is actually a derivation overstates confidence.

### Memo format over checklist format

Early versions produced a checklist — fine for coverage but easy to skim past. The final structure produces a 25-section investor memo with a fixed output order, a structured Final Verdict field, and prose reasoning rather than bullet ratings. The format change mattered: a memo forces synthesis; a checklist permits avoidance.

### Business-model-aware KPI layer

A single universal metric set produces shallow analysis across sectors. NRR is meaningless for a bank; combined ratio is irrelevant for a SaaS company; credit losses as a percentage of revenue matter for a BNPL lender but not for an industrial. The skill classifies each company into one of 15 archetypes and loads the appropriate KPI library from `references/business-model-kpis.md`. One framework, calibrated per sector.

### Archetype classification before KPI selection

Section 2A runs before any KPI analysis begins. The skill classifies the business model first, then selects the correct metric library — not the other way around. A company cannot be evaluated against SaaS retention benchmarks if it is actually a marketplace, and cannot be held to marketplace take-rate standards if it is primarily a lender.

Hybrid companies trigger multiple KPI libraries simultaneously. A fintech that combines a subscription product, a payment network, and a merchant lending book is evaluated against all three. Some examples of how archetype determines the metrics that matter:

- **SaaS / software** — Net revenue retention, ARR/MRR growth, Rule of 40, gross margin profile, SBC as % of revenue and FCF
- **Marketplace / platform** — GMV/GTV/TPV growth, take rate (calculated, not asserted), supply-demand balance, cohort health, liquidity density
- **Payments / lending / BNPL** — Transaction loss rate, charge-offs, allowance coverage ratio, delinquency aging, credit-loss growth vs. revenue growth
- **Banks / lenders** — Net interest margin, provision expense, charge-offs, CET1 ratio, deposit and funding mix
- **REITs** — AFFO/FFO per share, debt maturity profile, cap rate trends, occupancy, same-store NOI, dividend coverage
- **Pipeline / utility / income stock** — DCF per share, dividend yield, payout ratio, Debt/EBITDA, regulatory risk, rate cases, dividend-inclusive intrinsic value
- **Industrial / railroad** — Operating ratio, volume and yield trends, capex intensity, ROIC, network productivity, regulatory risk
- **Cyclicals** — Normalized margins across the cycle, current cycle position, inventory levels, commodity price sensitivity

The classification also determines what gets skipped. A pipeline company should not be evaluated against SaaS churn benchmarks. A railroad does not need a take-rate calculation. Each memo explicitly lists the KPI libraries that were loaded and those that were skipped as not applicable — so the reader knows exactly what lens was applied and why.

Misclassifying the archetype propagates errors through every downstream section. Getting this right first is not a formality — it is a prerequisite.

### Credit and lending risk cannot be buried

When a company has any exposure to lending, payments, BNPL, merchant cash advances, card issuing, or credit risk, the memo must surface that exposure explicitly. Revenue growth alone does not tell you whether the business is healthy — a lender growing revenue while credit losses grow faster is deteriorating, not expanding.

The skill requires four distinct credit disclosures to be shown separately, not combined:

1. **Income-statement transaction and loan losses** — the P&L impact in the period
2. **Provision expense** — the cash-flow statement non-cash add-back (a different number)
3. **Allowance coverage and charge-offs** — from the notes, showing how much buffer exists against future losses
4. **Delinquency and aging data** — where disclosed, showing whether problems are building in the pipeline

On top of that, the memo must calculate and compare credit-loss growth versus revenue growth and loan-book growth. A single quarter where credit losses grow more than 2× revenue growth is a yellow/orange watch flag. Two consecutive quarters above that threshold, or falling allowance coverage combined with rising charge-offs, becomes a hard-red thesis breaker. The skill will not let a strong headline revenue number hide a deteriorating credit book.

### SBC must come from primary filings

Stock-based compensation is the most commonly misdescribed line item in AI financial analysis. Third-party data providers (Macrotrends, Yahoo Finance, StockAnalysis, AlphaQuery, TIKR, and others) sometimes aggregate SBC differently from the primary filing — rolling in payroll taxes, miscounting periods, or pulling from the wrong statement. When a 10-K or 10-Q is available, the filing is authoritative and the aggregator is ignored.

The skill requires SBC to be shown three ways before any directional statement is made: absolute dollars, percentage of revenue, and percentage of FCF. If SBC is falling as a share of revenue but rising in absolute dollars, both facts must appear. If SBC is low as a percentage of revenue but consumes 25%+ of FCF, the FCF picture is stated clearly — not papered over with the percentage framing.

If primary filing SBC cannot be extracted, owner earnings are marked **Needs Review** and the memo is downgraded to a framework draft. No valuation or final verdict is produced until the number is sourced correctly.

Owner earnings = FCF − SBC, period. A business that generates $1B of FCF but pays $400M in SBC has $600M of owner earnings. Calling that "$1B FCF company" is not wrong — it is just incomplete in a way that systematically flatters the valuation.

One important exception: for pipelines, utilities, railroads, REITs, and other mature capital-intensive businesses, SBC is often not the controlling issue. In those cases the memo states that explicitly — "SBC is not the primary owner-earnings concern for this archetype" — and shifts focus to the archetype-appropriate metric (DCF/share, AFFO/share, operating ratio). The SaaS-style SBC lens is not applied where it does not belong.

### Cash-flow comparability flags

Companies occasionally change how they classify cash flows between operating, investing, and financing activities. A reclassification that moves a recurring cost out of operating cash flow and into investing cash flow will make OCF and FCF look structurally better without any economic improvement. The skill is required to flag any announced or enacted presentation changes, explain whether the change reflects economic improvement or is purely a comparability issue, and normalize all period-over-period FCF comparisons across the change date.

### Clean output, no process narration

A memo that says "let me gather the data now" or "wait — recalculating" is not a memo. It is a transcript of an LLM working out loud. The skill prohibits any workflow narration from appearing in the final output. Phrases like "I found," "in the previous session," "now I have the data," and "let me check" are not permitted in the delivered memo.

If data is missing or uncertain, it is stated as "Needs Review" in the relevant section — not as a narrative explanation of why it could not be retrieved. The memo begins with the disclaimer and ends cleanly after Sources. Limitations are facts about the analysis, not commentary about the process.

### Source hierarchy with explicit tier labels

Every data point must be labeled with its source and tier. The hierarchy is enforced top-down: SEC filings first, then company releases and regulatory filings, then reputable financial data providers. News is acceptable for context only. Blogs and SEO content are explicitly prohibited for market-share claims, moat assessments, or any figure that feeds the scorecard. If two sources conflict on the same data point, the conflict must be flagged openly — never silently resolved. A standing rule makes it explicit: if a filing is cited anywhere in the analysis, it cannot later be declared unavailable.

---

## Evolution

This skill started as a 9-item checklist adapted from a YouTube video and was rebuilt through seven distinct rounds of iteration. The driving question at each round was the same: *what can still produce a falsely confident output, and how do we close that gap?*

**Round 1 — From checklist to framework.** Added forensic accounting as a standalone check, ROIC analysis to separate valuable growth from value-destroying growth, per-share economics to catch dilution, and three quantitative overlays (Piotroski, Beneish, Altman). Added Hard Stop conditions that bypass the scorecard entirely.

**Round 2 — Source discipline and weighted scoring.** All checks had been treated as equally important. Added dominant-risk weighting by company archetype, kill criteria tied to the thesis, reverse-DCF expected-return math, and confidence tags on every claim. Added a Data Integrity Check that runs before scoring begins.

**Round 3 — Professional-grade rebuild.** Output still read like a checklist, not an investor memo. Rebuilt as a 22-section structured memo (later expanded to 25). Added business-model-specific risk checks backed by a 300-line sector KPI reference file. Added mandatory SBC-adjusted owner earnings, full balance sheet debt separation, and a structured Final Verdict format.

**Round 4 — Closing specific accuracy gaps.** Eleven targeted fixes: buyback analysis required five specific data points; SBC required both absolute and percentage trends; take rates required explicit calculation rather than assertion; credit losses gained hard-red thresholds; kill criteria for expensive growth stocks were calibrated to fire before visible distress.

**Round 5 — Filing-data extraction discipline.** EV calculation was corrected to deduct marketable securities and short-term investments, not just cash. Data Integrity Check expanded from 26 to 49 rows. "Needs Review" was restricted to data genuinely absent from all reviewed filings — it can no longer be applied to items present in a 10-Q or 10-K that was cited. Entry-price table now shows the formula for each column.

**Round 6 — Decision-usefulness and portfolio framing.** Added three new sections — Trading / Timing Context, Catalysts to Watch, and Position Sizing / Portfolio Risk Framing — to make the memo more useful at the point of actual execution, while capping their combined scorecard weight at 5% so they cannot override the fundamental verdict. Added Section 2A (Company Archetype Classification) as an explicit prerequisite step before KPI selection. Tightened SBC sourcing to require primary filings when available, with a hard block on owner-earnings calculations if the filing value cannot be extracted. Added structured credit and lending risk disclosure rules with severity tiers (watch, red flag, thesis breaker). Added cash-flow comparability flags for classification changes. Enforced scorecard consistency: if the verdict says "wait for a better price," the numerical score must not look like a buy. Fixed the reverse-DCF sequence to always compound today's market cap forward first. The goal throughout Round 6 was the same as every prior round — improve practical decision support without turning the skill into a trading signal generator.

**Round 7 — Archetype precision and income-stock grammar.** The framework had been built primarily around growth and quality-compounding stocks. Applying it to pipelines, utilities, REITs, and railroads produced technically correct but analytically wrong output — the reverse-DCF ignored dividends, SBC thresholds were applied where they were irrelevant, and verdict language calibrated for growth stocks was used on income stocks with no margin of safety. Round 7 added dedicated valuation rules for income-stock archetypes (DCF/share, AFFO/share, DDM, dividend coverage, Debt/EBITDA), introduced income-appropriate verdict language (Hold / Starter / Wait for better entry / Fairly valued), prohibited SaaS-style SBC analysis on capital-intensive businesses where it does not apply, added a metric-consistency rule to prevent the same figure appearing with two different values across sections, expanded the confidence-tag vocabulary to distinguish `[Derived]` from `[Verified]`, and enforced clean output — no workflow narration in the delivered memo.

The skill grew from 9 checks to a 25-section framework covering growth stocks, income stocks, cyclicals, and capital-intensive businesses. Each round made it harder for bad inputs to produce confident outputs, and harder for a strong operational story to paper over a broken valuation.

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
