---
name: stock-evaluator
description: >
  Use this skill whenever the user wants to evaluate, analyze, or assess a stock before buying it.
  Trigger on any request like "should I buy [stock]?", "evaluate [ticker] for me", "is [company] a good investment?",
  "analyze this stock", "run your checklist on [stock]", "help me decide whether to buy [stock]",
  or any mention of wanting to research or vet a company before investing. Also trigger when the user
  shares a stock ticker, company name, or investment idea and asks for an opinion or analysis.
  This skill runs a structured, multi-dimensional checklist grounded in private equity best practices
  and covers financials, cash flow quality, earnings forensics, ROIC, per-share economics, competitive
  position, growth, valuation, debt stress, governance, concentration, and quantitative red-flag overlays.
---

# Stock Evaluator — Pre-Purchase Analysis Framework

A professional-grade, general-purpose framework for evaluating any publicly traded stock before buying.
Produces a finished investor memo — not a transcript of a process.

**Output structure (always follow this order):**

1. Disclaimer
2. Company Snapshot
2A. Company Archetype Classification (prerequisite — determines which KPI libraries apply)
3. Hard Stop Scan
4. Data Integrity Check
5. Dominant-Risk Weighting
6. Business-Model-Specific Risk Check
7. P&L Health
8. Cash-Flow Quality & Owner Earnings
9. Balance Sheet & Liquidity
10. Growth Durability
11. Competitive Position / Moat
12. Management, Governance & Capital Allocation
13. Earnings Quality & Forensic Accounting
14. Macro, Sector & External Risks
15. Historical Price & Volatility
16. Trading / Timing Context
17. Valuation vs. Expected Return
18. Quantitative Overlays (only if inputs are available)
19. Summary Weighted Scorecard
20. Entry Price / Margin of Safety
21. Catalysts to Watch
22. Position Sizing / Portfolio Risk Framing
23. Thesis Breakers / Kill Criteria
24. Final Verdict
25. Sources

**Important separation principle:**
- Sections 1–15, 17, 19, 20, 23: drive the business thesis, valuation thesis, and red-flag analysis.
- Sections 16 (Trading/Timing), 21 (Catalysts), 22 (Position Sizing): support **timing, monitoring, and risk framing only**. They must never override fundamentals, valuation, or red flags. Their collective influence on the final verdict is capped at **5%**.

For business-model-specific KPI libraries, read: `references/business-model-kpis.md`

---

## Quality-Control Rules (non-negotiable)

Before producing any output, follow every rule below without exception.

**Source consistency**
- Never label data **Verified** unless the exact source and filing period are both explicit.
- Never use stale financials when a newer 10-Q, 10-K, 20-F, annual report, or interim filing exists.
- If a 10-Q, 10-K, annual report, or interim filing is cited anywhere in the analysis, do not say that filing was unavailable or not reviewed.
- Use the latest quarterly filing for current balance sheet, share count, SBC, buybacks, loans, and cash/debt data. Do not substitute guidance or estimates when actual filed results exist.
- Only use forward guidance when actual filed results are genuinely unavailable.

**Period and label discipline**
- Never mix fiscal-year, quarterly, and TTM figures without labeling each explicitly.
- Never call fiscal-year revenue "TTM." Calculate TTM correctly: latest FY revenue + current-year interim revenue − prior-year comparable interim revenue.
- Never say "revenue growth beat expectations by X%" unless analyst consensus figures are sourced. Say "revenue grew X% year-over-year" unless the beat is directly supported.
- Always calculate growth rates directly from the two filed values: growth = (current period − comparable prior period) ÷ comparable prior period. Do not approximate, round to the nearest convenient figure, or carry forward a growth rate from another source without verification. This applies to revenue, FCF, OCF, SBC, loan book, losses, and every other metric where a YoY or QoQ growth rate is asserted.

**Debt and balance sheet**
- Never confuse total liabilities with financial debt.
- Always separate: cash and equivalents / marketable securities / short-term financial debt / long-term financial debt / finance leases / operating leases / operating liabilities / total liabilities.
- Never say "effectively debt-free" unless financial debt is truly minimal relative to cash and FCF generation.
- For financial companies, use industry-specific capital and liquidity metrics rather than generic debt ratios.

**SBC and owner earnings**
- Never ignore SBC in owner-earnings calculations.
- Always use actual SBC from the latest filing (10-K or 10-Q), not guided or estimated SBC.
- **Primary-filing requirement:** Do not use SBC figures from Macrotrends, Yahoo Finance, Koyfin, or any other third-party data provider if the 10-K or 10-Q discloses the number. Third-party providers sometimes report different aggregations (e.g., they may combine SBC with related payroll taxes, or sum the wrong periods). The filing is authoritative.
- **TTM SBC calculation:** TTM SBC = latest FY SBC + current-year interim SBC − prior-year comparable interim SBC. Use the same period boundaries as TTM revenue. Do not multiply a single quarter by 4. Do not sum unrelated periods.
- Always show SBC three ways: absolute dollars, % of revenue, % of FCF.
- If SBC rises in absolute dollars but falls as % of revenue, describe both accurately. Do not say it is "declining" if only the percentage declined.
- Distinguish **stock-based compensation** (the GAAP SBC line in the cash-flow statement and notes) from **stock-based compensation plus related payroll taxes** (a broader figure some companies disclose separately). The two are often different by several percent. If you use the broader figure, label it explicitly as "SBC plus related payroll taxes." Do not call an exact filing value an Estimate. When in doubt, use the narrower GAAP SBC line and flag the difference.
- **Owner earnings = TTM FCF − TTM SBC** (using TTM SBC calculated as above). Do not subtract a single year's SBC from TTM FCF, and do not subtract a number that sums non-comparable periods.
- **SBC extraction failure rule (hard):** If the filing value for SBC cannot be extracted — whether because the filing has not been reviewed, the disclosure is unclear, or the period boundaries cannot be reconciled — mark SBC as **Needs Review** and **do not calculate owner earnings, do not calculate SBC-adjusted FCF, and do not produce a Decision-Grade valuation or final verdict.** Downgrade the memo to Framework Draft and list SBC in the Refresh Checklist. Never let a third-party SBC figure drive owner earnings or valuation when primary filings exist but have not yet been reviewed.
- SBC < 5% of revenue: note, generally acceptable — still check dilution. Use phrasing such as "low SBC burden."
- SBC 5–10% of revenue: yellow flag. Use phrasing such as "moderate SBC burden — watch for dilution."
- SBC > 10% of revenue: red flag. Use phrasing such as "high SBC burden — material to owner earnings."
- SBC > 20–25% of FCF: material impact on owner earnings — flag explicitly. Use phrasing such as **"manageable but material SBC burden"** when SBC is in the 20–25% of FCF range, and **"heavy SBC burden materially reducing owner earnings"** when above 25% of FCF. Do not use phrasing like "low SBC dilution" when SBC consumes 20%+ of FCF — that combination is contradictory and misleading.

**Buybacks**
- Always distinguish buyback authorization from actual repurchases executed.
- If actual repurchases occurred in the period under review, always show: shares repurchased, dollars spent, average repurchase price, remaining authorization, and whether repurchases appear value-accretive relative to current valuation.
- Do not say repurchase activity was undisclosed or unavailable if a 10-Q or 10-K covers the period.
- Buybacks at high valuations should be analyzed skeptically. A buyback is only shareholder-friendly if value-accretive or efficiently offsetting dilution.

**Take rate and KPI calculations (marketplace/platform companies)**
- Calculate take rate explicitly as: revenue ÷ GMV, GTV, TPV, or equivalent volume metric.
- Show current period vs. prior period.
- Do not say take rate is rising or falling unless the calculation supports the direction.

**Credit and loss metrics (payments, lending, BNPL, merchant advances, receivables financing)**
- **Mandatory disclosure when the archetype applies:** When the company has payments, lending, BNPL, merchant cash advances, receivables financing, or other credit exposure, the memo **must include** the income-statement transaction and loan loss figure for: current period, prior comparable period, year-over-year growth rate, current period as % of revenue, prior period as % of revenue, and a direct comparison of loss growth rate vs. revenue growth rate. Do not omit this line. Do not say it "needs to be pulled" if the 10-Q/10-K discloses it.
- Always calculate and show: transaction/credit losses as % of revenue, losses as % of FCF, loss growth rate vs. revenue growth rate, loan book growth rate, allowance coverage ratio, delinquency and charge-off trends if disclosed.
- Always **separate three distinct items** when they appear in the filing — do not confuse or combine them:
  1. **Transaction and loan losses** on the income statement (P&L line)
  2. **Provision for transaction and loan losses** in the operating cash flow statement (non-cash add-back, not the same number as the P&L line)
  3. **Loan / MCA allowance, charge-offs, and provisions** disclosed in the notes
- Use the income statement figure for the P&L impact. Use the OCF figure only when discussing cash-flow reconciliation. Use the notes figures for allowance, coverage, and charge-off analysis.
- If discussing only lending-specific or merchant-cash-advance-specific losses, label them clearly as "lending-specific" or "MCA-specific" — do not present them as total transaction and loan losses.
- Use the latest filed value for the loan and MCA book size. Do not use stale prior-quarter figures or range estimates when the most recent 10-Q discloses a precise net carrying value.
- **Credit-loss severity classification (three categories, in order of severity):**
  1. **🟡 Ongoing Yellow/Orange Watch** — Credit losses growing faster than revenue for any single quarter. Elevates concern but does not break the thesis.
  2. **🔴 Red Flag (single period)** — One full fiscal year with credit losses growing more than 2× faster than revenue. Material red flag in the scorecard, but recoverable if subsequent periods normalize.
  3. **☠️ Hard-Red / Thesis Breaker** — Either (a) two consecutive quarters with credit losses growing more than 2× faster than revenue, OR (b) worsening allowance coverage combined with rising charge-offs. Treat as a hard stop equivalent: default verdict to AVOID unless there is compelling, specific evidence of imminent reversal. Add to Section 23 Kill Criteria as ☠️ Kill.
- Each of these three severity levels must be applied **separately** — do not collapse them into a single "red flag" treatment. The scorecard and final verdict consequences differ.

**Cash-flow comparability**
- If the company changes cash-flow classification or presentation between periods, flag it clearly.
- **Always check the latest 10-Q and 10-K for announced future reclassifications** between operating, investing, and financing activities — including changes that will take effect in a future quarter or fiscal year. These are disclosed in the notes to the financial statements (often under "Recent Accounting Pronouncements" or business-specific disclosure). Do not state "no classification changes were found" without reviewing these notes.
- **Prohibition on denial:** If the filing discloses any past or upcoming reclassification — whether already in effect or scheduled for a future period — do not state that no reclassification was identified. Quote the disclosure language or paraphrase it accurately, including the effective date.
- A reclassification is a **comparability issue, not an economic improvement or deterioration**. Reported OCF or FCF can rise or fall purely because of the reclassification — do not attribute the change to operating performance.
- **Mandatory normalization warning:** When a future reclassification has been announced, include an explicit warning in the memo such as: *"Future OCF and FCF comparisons must be normalized for the [item] reclassification effective [date]. Pre- and post-effective-date figures are not directly comparable."* This warning must appear in Section 8 (Cash-Flow Quality) and again in Section 13 (Earnings Quality) where comparability matters.
- Normalize FCF where possible and label the normalization (e.g., "FCF excluding reclassified [item] for comparability").
- Flag reclassifications as catalysts only in the comparability sense (Section 21 rule), never as economic catalysts.

**Forensic and audit discipline**
- Always review the auditor opinion and critical audit matters (CAMs).
- If the 10-K has been reviewed, list each CAM by its actual title from the auditor report — do not summarize generically or say "no CAMs flagged" when they exist. Example titles take the form *"Revenue Recognition — Principal versus Agent Considerations,"* *"Valuation of Goodwill,"* etc.
- Do not say a gross-vs-net or principal-vs-agent judgment is "not flagged" if the auditor report identifies a CAM on that exact topic.
- A CAM is not automatically a red flag — mention it neutrally when it touches revenue recognition, reserves, fair value, inventory, goodwill, or other significant judgments.
- Never say "earnings quality is clean" solely because there are no restatements.

**Moat and market-share sourcing**
- Use SEC/company filings first for company-specific facts.
- Use reputable market-data providers for market-share claims and label them as third-party market data — do not treat them as Verified.
- Do not rely on SEO blogs, agency posts, or PR-adjacent content for core scorecard claims.

**Valuation weighting**
- For high-growth or high-multiple stocks, valuation / expected return must carry 30–40% of the weighted scorecard.
- Do not allow a collection of green business-quality checks to overpower a major valuation red flag.
- The scorecard interpretation and the final verdict must be consistent with each other.

**Kill criteria calibration**
- For expensive growth stocks, kill criteria must trigger before the business visibly collapses.
- Tie kill thresholds directly to the valuation thesis: required revenue growth rate, FCF margin floor, gross margin floor, credit/loss growth limit, SBC ceiling, and valuation staying extreme while growth decelerates.

**Language precision**
- Say "financial distress risk appears very low" — never "bankruptcy risk is zero."
- Do not call a pullback a "margin of safety" unless the expected-return math explicitly supports it.
- Do not present a precise forensic score (Piotroski, Beneish, Altman) unless it is actually calculated from inputs. If estimated, label it Estimated. If inappropriate for the company type, label it Not Applicable.

**Timing, catalysts, and position sizing (Sections 16, 21, 22)**
- Never let technical analysis override a broken business thesis.
- Never let analyst targets override expected-return math.
- Never call a stock cheap only because it is down from its highs.
- Never call support/resistance levels "thesis breakers."
- Never use stale technical or market data without labeling it.
- Never turn a long-term investment memo into a short-term trading call.
- Never reduce the weight of valuation or red flags because the chart looks bullish.
- Always separate these four threads in the output and in your reasoning: (1) business thesis, (2) valuation thesis, (3) timing setup, (4) position-sizing implication. They are distinct questions and should not contaminate each other.
- Trading/timing context, catalysts, and position-sizing framing must never collectively carry more than **5%** of the final verdict. They inform timing and risk sizing; they do not determine intrinsic value.

**General**
- Never overfit the framework to the most recently evaluated company. Apply it dynamically to any public company in any industry.
- Never let many green qualitative checks hide one major red financial or valuation risk.

**Operating mode (decision-grade vs framework-draft)**

For any real stock purchase, add, trim, or hold decision, the default mode is **Decision-Grade** — meaning the analysis is based on the latest available filings and current market data.

| Mode | When it applies | Required inputs | Output |
|---|---|---|---|
| **Decision-Grade** | User wants an actionable Buy / Hold / Add / Trim / Sell verdict | Latest 10-Q or 10-K reviewed, current price and market cap as of recent date, all relevant filings within their reporting cycle | Full memo with final verdict, valuation, owner earnings, entry price, IRR, margin of safety |
| **Framework Draft** | User explicitly opts into training-data-only mode, stale-data mode, or asks Claude to evaluate without fresh data; or the latest filing has not been reviewed; or critical inputs (current price, latest filing) are unavailable | Whatever data is at hand, clearly labeled stale | Memo labeled **"Framework Draft — Not Trade-Ready"** |

**Framework Draft rules (mandatory when in this mode):**
- The memo header must say: **"Framework Draft — Not Trade-Ready. Refresh required before any real decision."**
- Do not present a final Buy / Hold / Sell / Add / Trim verdict as decision-grade. If a verdict is requested, give a directional sketch only and label it Indicative, not Actionable.
- Do not calculate precise valuation, owner earnings, entry price, IRR, or margin of safety unless the user has supplied current numbers. Show the formulas and what inputs are needed — do not produce point estimates from stale data.
- Stale data may be used only to (a) explain the framework, (b) demonstrate how each section would be filled in, (c) identify exactly which data points need to be refreshed before the memo becomes decision-grade.
- End every Framework Draft memo with a **"Refresh Checklist"** — a list of specific items the user must provide or refresh before the memo can be promoted to Decision-Grade. At minimum: latest 10-Q or 10-K, current stock price as of the decision date, current diluted share count, current cash and financial debt, latest disclosed SBC and buybacks, and any archetype-relevant KPIs (per Section 2A).

**Mode-detection defaults:**
- If the user provides current price and latest filing → Decision-Grade.
- If the user asks "what do you think of X" or "should I buy X" without supplying data, and Claude cannot retrieve current data → Framework Draft.
- If the user explicitly says "use training data only," "don't search the web," "based on what you know," or equivalent → Framework Draft.
- If in doubt about freshness, default to Framework Draft and ask the user whether to retrieve current data.

**Pre-output verification checklist (run before delivering any Decision-Grade memo):**

The rules above are not optional — they govern whether the memo can be trusted. Before delivering a Decision-Grade memo, mentally walk through this checklist and confirm each item. If any answer is "no," fix the memo before sending. Failing to verify against rules that already exist is the most common cause of inaccurate output.

| # | Verification question | Where the rule lives |
|---|---|---|
| 1 | Was every SBC figure sourced from the actual 10-K or 10-Q (not Macrotrends / Yahoo / third-party)? | SBC and owner earnings |
| 2 | Was TTM SBC calculated as FY + current interim − prior comparable interim? | SBC and owner earnings |
| 3 | If SBC plus related payroll taxes was used anywhere, is it explicitly labeled? | SBC and owner earnings |
| 4 | Is "Owner earnings = TTM FCF − TTM SBC" (not FY SBC, not multiplied SBC)? | SBC and owner earnings |
| 5 | Were transaction/credit loss figures pulled from the income statement, OCF, and notes — separately, not conflated? | Credit and loss metrics |
| 6 | If a 10-Q or 10-K was reviewed, are all disclosed loss/allowance/charge-off figures actually used (not flagged "needs pulling")? | Filing-data extraction discipline |
| 7 | Were the latest 10-Q and 10-K notes checked for announced future cash-flow reclassifications? | Cash-flow comparability |
| 8 | If a reclassification was found, is it labeled a comparability issue (not an economic change)? | Cash-flow comparability |
| 9 | Does Section 17 show the full reverse-DCF table with all columns: current value → required exit value → required exit FCF → required CAGR? Not just a verbal summary? | Reverse DCF required output table |
| 10 | Does the entry-price table (Section 20) show IRRs that are consistent with the Section 17 base-case exit value? | Entry-price IRR-consistency rule |
| 11 | Was every growth rate calculated directly from two filed values, not approximated or carried over? | Period and label discipline |
| 12 | If a primary filing and a third-party source conflicted on any figure, was the primary filing used and the conflict flagged? | Source Hierarchy |
| 13 | If any third-party figure was used as a shortcut, is it labeled Unverified and excluded from the valuation and verdict? | Source Hierarchy |
| 14 | Were only the archetype-relevant KPIs analyzed (not forcing irrelevant metrics)? | Section 2A — Company Archetype Classification |
| 15 | If the archetype has credit exposure, does the memo include the income-statement transaction/loan loss line with current vs. prior period, % of revenue, and loss-growth-vs-revenue-growth comparison? | Credit and loss metrics — mandatory disclosure |
| 16 | If a future cash-flow reclassification has been announced in any reviewed filing, is it stated clearly with effective date, and is the normalization warning present in Sections 8 and 13? | Cash-flow comparability — prohibition on denial |
| 17 | If the memo mentions any valuation zone, fair-value range, or entry zone, does the reverse-DCF table justify it arithmetically? | Reverse DCF — no narrative-only zones |
| 18 | Is the SBC language internally consistent with the burden bands? (E.g., "low SBC dilution" is never used when SBC is ≥ 20% of FCF.) | SBC required phrasing |
| 19 | Does the memo open without hollow preambles ("before I dive in, a few questions…" when there are none)? | Analyst Guidance — Format |
| 20 | If SBC could not be extracted from a primary filing, was the memo downgraded to Framework Draft and SBC marked Needs Review — with no Decision-Grade owner-earnings or valuation calculated? | SBC extraction failure rule |
| 21 | Do all Section 5 weights sum to exactly 100%, with the sum stated explicitly in the memo? | Section 5 — Weight arithmetic check |
| 22 | For high-growth / high-multiple stocks, does Valuation / Expected Return carry 30–40%, and do Trading/Catalysts/Sizing carry no more than **5%** combined? If credit losses are a major business-model risk, does Credit / Loan-Loss Trajectory carry 10–15%? | Section 5 — Weight constraints |
| 23 | If the company has credit exposure, has each loss observation been classified into the correct severity tier (🟡 Watch / 🔴 Red Flag / ☠️ Thesis Breaker), with downstream scorecard and verdict consequences applied accordingly? | Credit-loss severity classification |
| 24 | Do the weights shown in Section 19 (Summary Weighted Scorecard) exactly match the weights stated in Section 5 (Dominant-Risk Weighting)? Any divergence is a QC failure. | Section 19 — Weight propagation rule |
| 25 | If Valuation / Expected Return is rated 🔴 and carries 30%+ weight, has the verdict been overridden to WATCH or AVOID — regardless of the numerical score? | Section 19 — Score-verdict alignment rule |
| 26 | Does the final numerical score align with the final verdict? If they appear to diverge (e.g., score ≥ 70 but verdict is WATCH), is the override reason stated explicitly in the memo? | Section 19 — Score-verdict consistency check |

If a single item fails, the memo is not Decision-Grade. Fix the failure and re-verify before delivery. If structural fixes are impossible with available data, downgrade the memo to **Framework Draft — Not Trade-Ready** rather than ship inaccurate Decision-Grade output.

---

## Source Hierarchy

Always use the highest available tier. Label every data point with its source and period.

1. **Primary** — SEC filings (10-K, 10-Q, 20-F), annual/interim reports, audited financials
2. **Company releases** — earnings releases, investor presentations, shareholder letters
3. **Regulatory filings** — exchange filings, proxy statements (DEF 14A), Form 4 (insider activity)
4. **Financial data providers** — reputable third-party data; label provider name and data date
5. **News sources** — reputable media for context only; never the basis for a scorecard rating
6. **Blogs / agency posts / SEO content** — never acceptable as primary evidence; never use for market-share claims, moat assessments, or financial figures

**Additional source rules:**
- If a primary filing (10-K, 10-Q, 20-F, annual report, interim report) exists and is cited, it must be used — do not say it was unavailable.
- Market-share and competitive-position figures from third-party sources must be labeled **Third-Party Market Data** — do not mark them Verified.
- **Primary-filing precedence on conflicts:** If a primary filing and a third-party source disagree on any figure (SBC, revenue, share count, debt, cash, KPIs, etc.), the primary filing always wins. Flag the conflict explicitly, state both values, and note which was used and why. Never silently resolve conflicts.
- **Convenience-shortcut rule:** If a third-party figure was used because it was easier to obtain than the filing value, that figure must be labeled **Unverified** and must not drive the valuation, the Section 17 reverse DCF, the entry-price math, or the final verdict. Decision-grade outputs are built only from filing-sourced data.
- Insider activity must come from SEC Form 4 or equivalent regulatory filing. If not reviewed, mark it Needs Review — never Verified.

---

## Section 1 — Disclaimer

> ⚠️ This analysis is for educational purposes only. It is not financial advice, investment advice, or a recommendation to buy or sell any security. Always do your own research and consult a qualified financial advisor before making investment decisions. Past performance does not guarantee future results.

---

## Section 2 — Company Snapshot

| Field              | Value                          |
|--------------------|-------------------------------|
| Ticker / Exchange  | [TICKER] / [Exchange]          |
| Stock Price        | $[X.XX] as of [date]           |
| Market Cap         | $[X]B                          |
| Enterprise Value   | $[X]B (= mkt cap + financial debt + preferred equity + minority interest − cash − cash equivalents − marketable securities − short-term investments; subtract long-term investments only if liquid and not strategic) |
| TTM Revenue        | $[X]B [source, period]         |
| Business Model     | [1–2 sentence summary]         |
| Company Archetype  | [See list below]               |

**Archetype classification** (pick primary; note if mixed):
SaaS/Software · Marketplace/Platform · Payments/Fintech/Lending · Bank/Insurance ·
Retail/Consumer Discretionary · Consumer Staples · Industrial/Cyclical · Semiconductor/Hardware ·
Energy/Commodities · Utility · REIT · Healthcare/Biotech/Pharma · Telecom/Media ·
Asset Manager/Broker · Conglomerate/Mixed

---

## Section 2A — Company Archetype Classification

**Prerequisite step. Run before any KPI work.** This section determines which KPI libraries apply, which red flags matter, and which metrics must be skipped.

**Step 1 — Classify the company into one or more archetypes:**

| Archetype                          | Trigger characteristics                                                |
|------------------------------------|-----------------------------------------------------------------------|
| SaaS / Software                    | Subscription revenue, recurring billings, deferred revenue            |
| Marketplace / Platform             | Two-sided network, GMV/GTV/TPV is a primary disclosed metric          |
| Payments / Fintech                 | Transaction processing, payment volume, take rate                     |
| Lending / Bank / Consumer Finance  | Loan book, deposits, credit losses, NIM                               |
| Insurance                          | Premiums earned, reserves, combined ratio                             |
| Retail / Consumer Discretionary    | Physical stores or e-commerce, inventory turns, SSS                   |
| Consumer Staples                   | Brand-driven, low-cyclicality consumer products                       |
| Semiconductor / Hardware           | Cyclical product cycles, foundry dependency, capex-heavy              |
| Industrial / Cyclical              | Backlog, book-to-bill, utilization, end-market cyclicality            |
| Energy / Commodities               | Commodity price exposure, reserves, lifting cost                      |
| Utility                            | Regulated returns, rate base, allowed ROE                             |
| REIT                               | Real-estate portfolio, FFO/AFFO, occupancy                            |
| Healthcare / Biotech / Pharma      | Drug pipeline, regulatory milestones, patent cliffs                   |
| Telecom / Media                    | Subscribers, ARPU, churn, content costs                               |
| Asset Manager / Exchange / Broker  | AUM, fee rate, performance fees                                       |
| Conglomerate / Mixed               | Multiple distinct business units with different economics             |

**Step 2 — State the classification explicitly in the output:**
- *Primary archetype:* [name]
- *Secondary archetype(s):* [if mixed]
- *KPI libraries activated:* [list]
- *KPI libraries explicitly skipped:* [list — to confirm they were not forgotten]

**Step 3 — Activate only the relevant KPI library from `references/business-model-kpis.md`.**

**Archetype-conditional rules (do NOT apply universally):**

| Metric category | Apply only if archetype is… |
|---|---|
| GMV, take rate, payment penetration, marketplace liquidity, buyer/seller growth | Marketplace / Platform / Payments |
| Credit losses, charge-offs, provisions, delinquencies, allowance coverage, loan book | Lending / Bank / Consumer Finance / Payments / Insurance / any company with material credit exposure |
| ARR, NRR, RPO, churn, CAC payback, Rule of 40 | SaaS / Software / subscription-heavy |
| Inventory turns, same-store sales, traffic, markdowns, lease burden | Retail / Consumer Discretionary / inventory-heavy |
| CET1, NIM, deposits, CRE exposure, NPLs | Bank / Lender |
| FFO, AFFO, occupancy, tenant concentration, debt maturity ladder | REIT |
| Combined ratio, loss ratio, reserves, catastrophe exposure | Insurer |
| Reserve life, lifting costs, hedging, commodity sensitivity | Energy / Commodities |
| Pipeline, patent cliffs, PDUFA dates, cash runway | Biotech / Pharma / Healthcare |
| Backlog, book-to-bill, capacity utilization | Industrial / Hardware / Semiconductor / Cyclical |

**Rules:**
- Do not force irrelevant metrics into the analysis. If the metric is archetype-specific and the company is not that archetype, skip it — do not mark it Needs Review.
- If the company is **mixed** (e.g., a SaaS company with a meaningful lending arm, or a retailer with a payments business), analyze each major segment separately using its own KPI library and call out the mix explicitly.
- When debugging or refining the framework based on a single company's output, convert that company's specifics into **archetype-conditional rules**, not universal requirements. The framework must remain general-purpose. Do not hardcode any individual company's metric values, thresholds, or terminology into the universal checklist.

---

## Section 3 — Hard Stop Scan

Run this before all other analysis. If any item is found, flag it prominently and default verdict to **AVOID** unless there is a compelling reason otherwise.

| Hard Stop Trigger                                                 | Found? | Notes |
|-------------------------------------------------------------------|--------|-------|
| Auditor resignation                                               | —      |       |
| Qualified or adverse auditor opinion                              | —      |       |
| Material weakness in ICFR (internal controls)                    | —      |       |
| Restatement or delayed filing                                     | —      |       |
| SEC / regulatory investigation                                    | —      |       |
| Credible fraud allegation                                         | —      |       |
| Going-concern warning                                             | —      |       |
| Covenant breach                                                   | —      |       |
| Debt maturity wall within 24 months with unclear funding          | —      |       |
| Liquidity crisis                                                  | —      |       |
| Massive dilution needed to continue operations                    | —      |       |
| Management resignation cluster (CEO/CFO/auditor together)        | —      |       |
| Bankruptcy, restructuring, or distressed-debt signals             | —      |       |

Output: **"No hard stops found"** only if actually checked. If not fully checked, say **"Hard Stop Scan incomplete."**

---

## Section 4 — Data Integrity Check

Run before scoring. Goal: catch stale, inconsistent, or low-confidence data. Use the latest 10-Q or 10-K as the primary source for all balance sheet, SBC, buyback, KPI, and audit items. Do not mark an item Needs Review if it is disclosed in a filing that has been reviewed.

| Item                                         | Source | Period | Value Used | Status   | Notes                                               |
|----------------------------------------------|--------|--------|------------|----------|-----------------------------------------------------|
| Revenue (TTM)                                |        |        |            |          | = latest FY + current interim − prior comparable    |
| Revenue (last FY)                            |        |        |            |          |                                                     |
| Gross profit / gross margin                  |        |        |            |          |                                                     |
| Operating income                             |        |        |            |          |                                                     |
| Net income                                   |        |        |            |          |                                                     |
| Operating cash flow                          |        |        |            |          |                                                     |
| Capex                                        |        |        |            |          |                                                     |
| Free cash flow (OCF − Capex)                 |        |        |            | Derived  |                                                     |
| Stock-based compensation                     |        |        |            |          | Actual filed figure, not guidance                   |
| SBC as % of revenue                          |        |        |            | Derived  |                                                     |
| SBC as % of FCF                              |        |        |            | Derived  |                                                     |
| SBC-adjusted FCF (= FCF − SBC)               |        |        |            | Derived  |                                                     |
| Cash & cash equivalents                      |        |        |            |          | Balance sheet line item; separate from investments  |
| Marketable securities — short-term           |        |        |            |          | Deduct from EV if disclosed                         |
| Short-term investments                       |        |        |            |          | Deduct from EV if liquid                            |
| Long-term investments                        |        |        |            |          | Deduct from EV only if liquid and non-strategic     |
| Total liquid assets (sum of above four rows) |        |        |            | Derived  | Used in EV calculation                              |
| Financial debt — short-term                  |        |        |            |          | Exclude operating liabilities                       |
| Financial debt — long-term                   |        |        |            |          |                                                     |
| Finance leases                               |        |        |            |          |                                                     |
| Total financial debt                         |        |        |            | Derived  |                                                     |
| Net cash / net debt (liquid assets − fin. debt)|      |        |            | Derived  |                                                     |
| Diluted share count                          |        |        |            |          | From latest 10-Q/10-K                               |
| Stock price                                  |        |        |            | Market Data |                                                  |
| Market cap (price × diluted shares)          |        |        |            | Derived  |                                                     |
| Enterprise value                             |        |        |            | Derived  | = mkt cap + fin. debt + preferred + minority interest − total liquid assets |
| P/E                                          |        |        |            | Derived  |                                                     |
| P/S                                          |        |        |            | Derived  |                                                     |
| EV/EBITDA                                    |        |        |            | Derived  |                                                     |
| EV/FCF                                       |        |        |            | Derived  |                                                     |
| FCF yield (FCF ÷ mkt cap)                    |        |        |            | Derived  |                                                     |
| SBC-adjusted FCF yield                       |        |        |            | Derived  |                                                     |
| Buybacks — authorization outstanding         |        |        |            |          |                                                     |
| Buybacks — shares repurchased (period)       |        |        |            |          | From 10-Q/10-K; not estimated                       |
| Buybacks — dollars spent (period)            |        |        |            |          |                                                     |
| Buybacks — average repurchase price          |        |        |            |          | From filing if disclosed; do not estimate           |
| Buybacks — remaining authorization           |        |        |            |          |                                                     |
| Insider activity (net buying/selling)        |        |        |            |          | Must be from Form 4; else Needs Review              |
| Auditor opinion                              |        |        |            |          | From 10-K auditor report                            |
| Critical audit matters (CAMs)               |        |        |            |          | List each one; do not mark Needs Review if 10-K reviewed |
| Material weaknesses / ICFR                  |        |        |            |          |                                                     |
| Disclosed operating KPIs (GMV/TPV/NRR/etc.) |        |        |            |          | Use filed figures; Needs Review only if genuinely not disclosed |
| Credit/transaction losses — current period  |        |        |            |          | With prior-year comparison and growth rate          |
| Credit/transaction losses as % of revenue   |        |        |            | Derived  |                                                     |
| Loan/advance book size                       |        |        |            |          | If applicable                                       |
| Allowance / delinquency data                |        |        |            |          | If applicable                                       |
| Segment / business-line mix                  |        |        |            |          | Only if material                                    |

**Status labels:**
- **Verified** — confirmed from primary filing; source and period explicit
- **Derived** — calculated from verified inputs; formula shown
- **Estimate** — assumption-based; assumptions disclosed
- **Market Data** — from financial data provider; provider and date noted
- **Needs Review** — stale, conflicting, missing, or not disclosed in any reviewed filing

**Rules:**
- "Needs Review" items may not produce a 🟢 rating in the relevant check — default to 🟡.
- If a 10-Q or 10-K has been reviewed, do not mark items Needs Review that are disclosed in that filing. Reserve Needs Review for data that is genuinely absent from all reviewed sources.
- EV must deduct all liquid assets: cash, cash equivalents, marketable securities, and short-term investments. Do not deduct only cash if marketable securities are material and disclosed.
- Any data conflict must be disclosed in the relevant section, not silently resolved.
- Valuation multiples must show the "as of" date. Stale multiples on a volatile stock can be materially wrong.
- TTM revenue must be calculated correctly (see formula above). Never call FY revenue "TTM."
- Distinguish financial debt from total liabilities throughout the entire analysis.
- SBC must come from the latest actual filing — not from guidance or estimates.
- Buyback average repurchase price must come from the filing if disclosed — do not estimate it.
- CAMs must be listed from the 10-K auditor report; do not mark Needs Review if the 10-K was reviewed.
- Disclosed operating KPIs (only those relevant to the company's archetype — e.g., GMV/TPV for marketplaces, NRR/ARR for SaaS, NIM/CET1 for banks, FFO/AFFO for REITs, etc.) must be sourced from the filing and marked Verified — not Needs Review.
- Credit/transaction loss data must show current period, prior-year comparison, and growth rate vs. revenue growth.
- Insider activity marked anything other than Needs Review requires a Form 4 or equivalent as source.
- Market-share figures from third-party data must be labeled Third-Party Market Data, not Verified.
- Company filings override third-party articles for company-specific facts: app counts, cash, KPIs, share count, buybacks, audit matters, and disclosed operating metrics.

---

## Section 5 — Dominant-Risk Weighting

Not all risks matter equally. Before scoring, assign weights based on the company's archetype and most likely failure modes. Show your weights and rationale explicitly.

**Weight constraints (hard rules):**
- Weights must sum to **exactly 100%** — verify the arithmetic before delivering the scorecard.
- For any high-growth or high-multiple stock, **Valuation / Expected Return must carry 30–40%** of the weighted scorecard.
- Trading / Timing, Catalysts, and Position Sizing (Sections 16, 21, 22) **may not exceed 5% combined**. They inform timing and sizing — not the buy / watch / avoid decision itself.
- If credit losses or loan-loss trajectory is identified as a major business-model-specific risk (e.g., for payments, lending, BNPL, MCA, insurance, or any company with material credit exposure), the **Credit / Loan-Loss Trajectory dimension must carry 10–15%** of the weighted scorecard. This is a sub-component of Business-Model Specific Risks but, when material, must be carved out and weighted explicitly.

**Default weights by archetype:**

| Risk Dimension                 | High-Growth/SaaS | Value/Dividend | Turnaround | Cyclical/Industrial | Bank/Fintech | Biotech |
|-------------------------------|-----------------|----------------|------------|---------------------|--------------|---------|
| Valuation / Expected Return   | 30–40%          | 10–15%         | 5–10%      | 20–25%              | 10%          | 5%      |
| Growth Durability             | 20–25%          | 10%            | 15%        | 15%                 | 10%          | 15%     |
| Cash Flow / Margin Durability | 10–15%          | 20%            | 20%        | 15%                 | 10%          | 10%     |
| Balance Sheet / Liquidity     | 5%              | 10%            | 20–25%     | 15–20%              | 25%          | 30%     |
| Competitive Position          | 10%             | 20%            | 10%        | 10%                 | 10%          | 10%     |
| Governance / Capital Alloc.   | 5–10%           | 10%            | 15%        | 5%                  | 10%          | 10%     |
| Business-Model Specific Risks | 10%             | 15%            | 10%        | 15%                 | 25%          | 35%     |
| Earnings Quality / Forensics  | 5%              | 5%             | 5%         | 5%                  | 10%          | 5%      |

State weights explicitly before proceeding. Example:
*"[TICKER] is a high-growth SaaS company trading at a premium. Valuation weighted at 35%. Growth durability at 20%. Business-model risks (NRR, churn, SBC) at 15%."*

**Valuation override rule:** For any high-growth or high-multiple stock, Valuation / Expected Return must carry at least 30% of the weighted score. The scorecard interpretation must be consistent with the final verdict — a collection of green business-quality ratings must not override a 🔴 valuation rating when valuation carries 30–40% of the score.

**Weight arithmetic check (mandatory before Section 19 scorecard):** After assigning all weights, sum them. If they do not equal exactly 100%, adjust before producing the scorecard. State the sum explicitly in the memo so the reader can verify.

---

## Section 6 — Business-Model-Specific Risk Check

**Read `references/business-model-kpis.md` for the full KPI library by sector.**

Steps:
1. Confirm the company archetype from Section 2.
2. Load the relevant KPI set from the reference file.
3. Check each relevant metric. Skip metrics that don't apply — do not force irrelevant checks.
4. Rate each dimension 🔴 / 🟡 / 🟢 with source tags.

The goal is to evaluate the company through the lens of how its actual business model works and fails — not through a generic one-size-fits-all lens.

---

## Section 7 — P&L Health

*Is the business genuinely growing and profitable?*

Use 3–5 year trends. Label all periods explicitly.

**Check:**
- Revenue trend (absolute and per-share) `[Verified]`
- Gross margin trend — stable, expanding, or compressing? `[Verified]`
- Operating margin (EBIT margin) `[Verified]`
- Net income trend — watch for one-off items `[Verified]`
- EPS trend — but always cross-check with dilution (Section 12) `[Verified]`
- Segment-level margins if disclosed — a healthy aggregate can hide a deteriorating segment `[Verified]`

**Red flags:**
- Revenue growing but gross/operating margins shrinking
- Profits driven by tax benefits, one-off gains, or below-the-line items
- EPS rising only because of buybacks, not earnings growth
- One segment masking deterioration in another

**Rating:** 🔴 Weak / 🟡 Mixed / 🟢 Strong

---

## Section 8 — Cash-Flow Quality & Owner Earnings

*Reported profits mean nothing if cash isn't actually arriving.*

**Check:**
- Operating cash flow (OCF) — absolute and trend `[Verified]`
- Capex — maintenance vs. growth capex where disclosed `[Verified]`
- Free cash flow = OCF − Capex `[Derived]`
- FCF margin = FCF / Revenue `[Derived]`
- FCF yield = FCF / Market Cap `[Derived]`
- Cash conversion: OCF vs. net income — large persistent gaps signal accrual risk `[Verified]`
- Working-capital impact on OCF — is cash flow helped by payables stretching or receivables acceleration? `[Verified]`
- Capex intensity — rising or falling relative to revenue? `[Verified]`
- Capitalized software or R&D — if material, flag it as a cash-flow-timing issue `[Verified]`
- One-time cash-flow benefits (asset sales, tax refunds, timing) `[Verified]`
- Cash-flow classification changes — if the company reclassified items, flag that YoY comparisons may not be apples-to-apples `[Verified]`

**For companies with lending, financing, merchant advances, insurance float, or customer deposits:**
Check whether OCF is distorted by these financial-services activities. Flag if so.

**SBC-Adjusted FCF (Owner Earnings):**

| Metric                    | Value      | Source / Period |
|---------------------------|------------|-----------------|
| Reported FCF              | $X         |                 |
| Stock-based compensation  | $X         |                 |
| SBC as % of revenue       | X%         |                 |
| SBC as % of FCF           | X%         |                 |
| SBC as % of OCF           | X%         |                 |
| SBC-adjusted FCF          | $X (= FCF − SBC) |            |
| SBC-adjusted FCF yield    | X%         |                 |
| SBC trend (absolute $)    | Rising / Flat / Falling |    |
| SBC trend (% of revenue)  | Rising / Flat / Falling |    |

**Rules:**
- Do not say SBC is "declining" if it only declined as a % of revenue but increased in absolute dollars. Describe both trends accurately.
- Always use actual SBC from the latest filed 10-Q or 10-K — not from guidance or estimates.
- SBC < 5% of revenue: note but generally acceptable — still check dilution.
- SBC 5–10% of revenue: yellow flag.
- SBC > 10% of revenue: red flag.
- SBC > 20–25% of FCF: material impact on owner earnings — flag explicitly.
- If share count is not falling despite buybacks, buybacks may only be offsetting dilution.
- **Cash-flow comparability:** If the company has changed how it classifies items between operating, investing, and financing activities in any period covered, flag it prominently and note that OCF/FCF comparisons across those periods may not be apples-to-apples. Normalize FCF where possible and label the normalization.

**Rating:** 🔴 Weak / 🟡 Mixed / 🟢 Strong

---

## Section 9 — Balance Sheet & Liquidity

*Can the business survive a downturn and fund itself through the next 12–24 months?*

**Key distinctions:**
- Report **financial debt** (bank loans, bonds, notes payable, finance leases) separately from total liabilities.
- Report **operating liabilities** (accounts payable, deferred revenue, accruals) separately.
- Do not say "debt" when you mean "total liabilities."
- For EV, always deduct all liquid assets — not just cash and equivalents. If marketable securities or short-term investments are material and disclosed in the filing, they must be deducted.

**Liquid assets breakdown (show each line separately):**
- Cash & cash equivalents `[Verified]`
- Marketable securities — short-term `[Verified]`
- Short-term investments `[Verified]`
- Long-term investments (only if liquid and non-strategic) `[Verified]`
- **Total liquid assets** (sum above) `[Derived]`

**Financial debt breakdown (show each line separately):**
- Short-term financial debt `[Verified]`
- Long-term financial debt `[Verified]`
- Finance leases `[Verified]`
- **Total financial debt** `[Derived]`

**Net cash / net debt** = Total liquid assets − Total financial debt `[Derived]`

**Enterprise value** = Market cap + Total financial debt + Preferred equity + Minority interest − Total liquid assets `[Derived — show the arithmetic explicitly]`

**Additional balance sheet checks:**
- Debt maturity schedule — when do major tranches come due? `[Verified]`
- Net debt / EBITDA (where EBITDA is meaningful) `[Derived]`
- Interest coverage = EBIT / interest expense (target > 3×) `[Derived]`
- Current ratio (only where relevant to the business model) `[Derived]`
- Operating lease liabilities — economically debt-like `[Verified]`
- Pension obligations `[Verified]`
- Off-balance-sheet obligations `[Verified]`
- Goodwill and intangibles — impairment risk `[Verified]`
- Covenant headroom `[Verified / Qualitative judgment]`
- Variable-rate debt exposure `[Verified]`
- FX / commodity exposure from market-risk disclosures `[Verified]`

**Forward liquidity stress test:**
- 12-month cash needs (operations + debt service + capex)
- Cash sources available (cash on hand, revolver capacity, FCF generation)
- Refinancing dependency within 24 months?

**Hard stop if:** covenant breach or refinancing cliff within 12 months with no clear resolution.

**For financial companies:** Use industry-specific capital and liquidity metrics (CET1, LCR, etc.) instead of generic debt ratios.

**Rating:** 🔴 Stressed / 🟡 Moderate / 🟢 Strong

---

## Section 10 — Growth Durability

*Is the company growing, and is that growth likely to continue and create value?*

**Check:**
- Revenue CAGR: 1-year, 3-year, 5-year `[Verified]`
- Revenue growth vs. industry peers `[Market Data]`
- Analyst consensus for next 2–3 years `[Market Data — note provider and date]`
- TAM and remaining penetration headroom `[Market Data / Qualitative judgment]`
- New product, geography, or business-line pipeline `[Qualitative judgment]`
- Management's track record of hitting guidance `[Verified]`
- Industry tailwinds / headwinds `[Qualitative judgment]`
- ROIC on new investments — is the company growing profitably? (link to Section 8) `[Derived / Estimate]`
- Reinvestment rate and whether capital is deployed into high-return opportunities `[Derived]`

**Questions to answer explicitly:**
- Is this company in a growing or shrinking industry?
- What realistic revenue CAGR is achievable over 3–5 years?
- Is management investing for the future or harvesting the business?

**Red flags:**
- Growth decelerating faster than peers
- Repeated guidance misses without accountability
- Heavy reinvestment with declining returns on new capital
- TAM claims that are implausible relative to competitive dynamics

**Rating:** 🔴 Weak / 🟡 Mixed / 🟢 Strong

---

## Section 11 — Competitive Position / Moat

*Does the company have a durable edge that protects future cash flows?*

**Check:**
- Moat type: brand, switching costs, network effects, cost advantages, regulatory license, data advantage `[Qualitative judgment]`
- Market share trend — gaining, holding, or losing? `[Third-Party Market Data — label provider]`
- Pricing power — can they raise prices without losing customers? `[Qualitative judgment]`
- Barriers to entry — how hard is it for a well-funded competitor to replicate this? `[Qualitative judgment]`
- Customer concentration — any customer ≥ 10% of revenue? `[Verified]`
- Product / geography concentration `[Verified]`

**Key questions:**
- Why would a customer choose this company over the next best alternative?
- What stops a well-funded competitor from replicating this in 3–5 years?

**Sourcing rules:**
- Company-specific facts (customer concentration, disclosed market share, contract wins) must come from SEC/company filings → label Verified.
- Market-share estimates from third-party research must be labeled Third-Party Market Data — do not treat as Verified.
- Do not use SEO blogs, agency posts, or PR-adjacent content for market-share or moat claims. If no reputable source is available for market share, say so and mark it Needs Review.

**Red flags:**
- Commoditized product with no differentiation
- Losing market share in a growing industry
- Pricing power eroding (volume maintained only through discounting)
- Single customer > 30% of revenue

**Rating:** 🔴 Weak / 🟡 Mixed / 🟢 Strong

---

## Section 12 — Management, Governance & Capital Allocation

*Are the people in control trustworthy, competent, and aligned with shareholders?*

**Check:**
- Founder-led or professional management? CEO/CFO tenure? `[Verified]`
- Management execution vs. prior guidance `[Verified]`
- Insider ownership — meaningful skin in the game? `[Verified — proxy / Form 4]`
- Insider buying/selling — patterns over past 12 months `[Verified — Form 4]`
  - Note: selling is not automatically bearish (diversification is normal)
  - Flag: heavy selling after promotional commentary, or selling while fundamentals weaken
  - If not fully reviewed, mark **Needs Review**, not Verified
- 10b5-1 or automatic trading plans — disclose if relevant `[Verified]`
- Dual-class share structure — note voting power concentration `[Verified]`
- Related-party transactions — clear business purpose? `[Verified]` ← hard stop if purpose is weak
- Board independence `[Verified]`
- Executive compensation — tied to per-share value creation or just absolute metrics? `[Verified]`
- Acquisition and divestiture history — value-accretive or destructive? `[Verified / Qualitative judgment]`
- Buybacks — distinguish authorization from actual repurchases executed `[Verified]`
  - If actual repurchases occurred in the period, always show: shares repurchased, dollars spent, average repurchase price, remaining authorization, and whether repurchases appear value-accretive relative to current valuation
  - Do not say repurchase activity was undisclosed or unavailable if a 10-Q or 10-K covers the period
  - Buybacks at high valuations should be analyzed skeptically
  - A buyback is only shareholder-friendly if value-accretive or efficiently offsetting dilution from SBC
- Dividends and payout sustainability `[Derived]`
- Dilution history — share count 3–5 years ago vs. today `[Verified]`
- Per-share value creation: revenue/share, FCF/share trend `[Derived]`
- ICFR material weaknesses — any unresolved? `[Verified]` ← hard stop if unresolved
- Auditor tenure and changes `[Verified]`

**Rating:** 🔴 Concern / 🟡 Neutral / 🟢 High Confidence

---

## Section 13 — Earnings Quality & Forensic Accounting

*Are the reported numbers trustworthy?*

Do not say "earnings quality is clean" solely because there are no restatements.

**Check:**
- Auditor opinion — clean, qualified, adverse, or disclaimer of opinion? `[Verified]`
- Auditor changes — sudden changes are a red flag `[Verified]`
- Critical audit matters (CAMs) — always review these. Mention each one neutrally. A CAM is not automatically a red flag, but flag it when it involves revenue recognition, reserves, fair value, inventory, goodwill, contingencies, or other areas requiring significant judgment. `[Verified]`
- Material weaknesses in ICFR `[Verified]`
- Restatements or delayed filings `[Verified]`
- Revenue recognition complexity — any judgment-heavy policies? `[Verified]`
- Principal-vs-agent or gross-vs-net revenue presentation — and whether it changed `[Verified]`
- Cash-flow classification changes — if any items were reclassified between operating, investing, and financing activities, flag it. Note that OCF/FCF comparisons across the affected periods may not be apples-to-apples. `[Verified]`
- Non-GAAP adjustments: SBC add-backs, restructuring, acquisition-related, other `[Verified]`
- Accruals ratio = (Net Income − OCF) / Average Total Assets `[Derived]`
  - Above ~5% of assets sustained over multiple years: yellow/red flag
- Receivables growth vs. revenue growth `[Verified]`
  - Growing > 1.5× faster than revenue: flag
- Inventory growth vs. revenue growth `[Verified]`
- Deferred revenue trend `[Verified]`
- Contract assets / capitalized costs — growing faster than revenue? `[Verified]`
- Goodwill impairments `[Verified]`
- OCF vs. net income comparison — persistent large gaps `[Derived]`
- Segment margin changes — deterioration hidden by aggregate reporting? `[Verified]`
- One-time gains/losses inflating reported earnings `[Verified]`
- Accounting estimate changes year-over-year `[Verified]`

**Rating:** 🔴 Concerning / 🟡 Neutral / 🟢 Clean

---

## Section 14 — Macro, Sector & External Risks

Only include risks genuinely relevant to this company. Skip irrelevant items.

**Check as applicable:**
- Interest-rate sensitivity (revenue, cost of funding, asset values)
- Inflation sensitivity (input costs, pricing power)
- FX exposure (revenue, costs, translation risk)
- Commodity exposure
- Consumer spending sensitivity
- Enterprise IT / software budget sensitivity
- Housing / construction exposure
- Credit cycle exposure
- Regulatory risk and antitrust risk
- Litigation risk
- Tariff / trade / geopolitical risk
- Supply-chain risk
- Cybersecurity and data privacy risk
- Climate / weather risk where material
- Government reimbursement risk (healthcare)
- Patent cliff (pharma)
- Export controls (semiconductors)

**Rating:** 🔴 High Exposure / 🟡 Moderate / 🟢 Low / Well-Managed

---

## Section 15 — Historical Price & Volatility

*Understand risk, sentiment, and position-sizing danger — not for trading signals.*

**Check:**
- 1-year, 3-year, 5-year price performance vs. relevant benchmark `[Market Data]`
- 52-week high and low `[Market Data]`
- Distance from 52-week high (%) `[Market Data]`
- Distance from 50-day and 200-day moving averages `[Market Data]`
- Beta `[Market Data]`
- Maximum drawdown (if available) `[Market Data]`
- Post-earnings volatility — how wild are reactions? `[Market Data]`
- Short interest (if relevant) `[Market Data]`
- Multiple expansion/compression history — did stock move because of fundamentals or sentiment? `[Market Data / Qualitative judgment]`

**Warning to include:**
A high-quality company can still be a painful investment if bought at a stretched multiple just before multiple compression. Highly volatile stocks require careful attention to entry price and position sizing.

**Rating:** 🔴 High Risk / 🟡 Moderate / 🟢 Low / Manageable

---

## Section 16 — Trading / Timing Context

*Help with timing and position sizing — not intrinsic value.*

This section provides market sentiment, volatility, and technical context. It complements Section 15 (Historical Price & Volatility) with timing-relevant data. **It does not determine intrinsic value.** Fundamentals, valuation, and red flags decide whether a stock is fundamentally attractive; this section helps frame *when* and *how much* to commit.

| Metric                           | Value | Date / Source | Interpretation                          |
|----------------------------------|-------|---------------|-----------------------------------------|
| Current price                    |       |               | Anchor point                            |
| 52-week high / 52-week low       |       |               | Drawdown and range context              |
| Distance from 52-week high       |       |               | Sentiment / valuation-reset context     |
| 50-day moving average            |       |               | Short-term trend                        |
| 200-day moving average           |       |               | Long-term trend                         |
| Price vs. 50D MA (%)             |       |               | Short-term momentum                     |
| Price vs. 200D MA (%)            |       |               | Long-term momentum                      |
| Beta                             |       |               | Volatility / position-sizing context    |
| RSI (if available)               |       |               | Momentum only — do not overemphasize    |
| Short interest (if relevant)     |       |               | Sentiment / squeeze risk                |
| Recent post-earnings move        |       |               | Market expectations vs. reality         |

**Rules:**
- Label every market/technical data point with date and source. Mark stale items Needs Review.
- Do not use technical signals as a substitute for valuation.
- Do not say "thesis broken" because a stock falls below a moving average or support level.
- A stock being down from its highs is not a margin of safety. Only the expected-return math (Section 17) can establish that.
- Use phrasing like: *"This section helps with timing and position sizing. It does not determine intrinsic value."*

**Short interpretation (keep concise — 3–5 bullets):**
- Is the stock technically strong, weak, or neutral?
- Is the stock volatile relative to the market (beta context)?
- Is the stock near obvious support/resistance levels worth noting?
- Is the stock already rebounding, still falling, or consolidating?
- Does the chart suggest patience may improve entry price?

---

## Section 17 — Valuation vs. Expected Return

*Are you paying a fair price — and what does the price imply about the future?*

**Multiples (as of [date]):**

| Metric              | Value       | vs. Peers | vs. Own History | Notes               |
|---------------------|-------------|-----------|-----------------|---------------------|
| P/E                 |             |           |                 |                     |
| P/S                 |             |           |                 |                     |
| EV/EBITDA           |             |           |                 |                     |
| EV/FCF              |             |           |                 |                     |
| FCF yield           |             |           |                 |                     |
| SBC-adj. FCF yield  |             |           |                 |                     |

**Reverse DCF / Required Growth Calculation:**

What must be true for the investor to earn a target return from the current price?

```
Current market cap:             $X bn
Current FCF (TTM, SBC-adjusted):$X bn
Target annual returns:          8%, 10%, 12%
Holding period:                 5 years and 10 years
Exit multiples tested:          Conservative (Nx), Base (Nx), Aggressive (Nx)
```

**Required calculation sequence (always follow this order):**

1. **Compound today's market cap forward** to find the required exit market cap:
   Required exit market cap = Current market cap × (1 + target return)^holding period
   Example: $100B × (1.10)^10 = $259B required exit market cap

2. **Derive required exit FCF (or required exit owner earnings)** from the required exit market cap and the assumed exit multiple:
   Required exit FCF = Required exit market cap ÷ exit P/FCF multiple
   (Or use EV/FCF if working from EV rather than market cap — be consistent throughout.)

3. **Derive the required FCF CAGR** from current FCF to required exit FCF:
   Required FCF CAGR = (Required exit FCF ÷ Current FCF)^(1/years) − 1

4. **Assess realism**: compare the required FCF CAGR to the company's historical growth, analyst consensus, and the thesis-case growth from Section 10.

Show these four steps explicitly whenever the report states "to earn X% annually over Y years." Never derive a required growth rate without first compounding the market cap forward. Do not work backwards from an assumed FCF growth rate to imply a return without showing the exit market cap check.

**Required output table — show every column for every scenario.** Do not present a verbal summary in place of this table. **Narrative-only valuation zones** (e.g., "the stock looks fair around $X–$Y" without showing the underlying compounding math) **are not acceptable** as a substitute. If the memo mentions any "fair value zone," "buy zone," "attractive entry zone," or similar, the table above must appear and must justify the zone arithmetically.

| Field | Bear | Base | Bull |
|---|---|---|---|
| Current market cap (or EV) | $X bn | $X bn | $X bn |
| Target annual return | X% | X% | X% |
| Holding period (years) | N | N | N |
| **Required exit market cap (or EV)** = current × (1+r)^N | $X bn | $X bn | $X bn |
| Assumed exit multiple (P/FCF or EV/FCF) | Xx | Xx | Xx |
| **Required exit FCF (or owner earnings)** = exit value ÷ multiple | $X bn | $X bn | $X bn |
| Current FCF (or owner earnings, TTM, SBC-adjusted) | $X bn | $X bn | $X bn |
| **Required CAGR** = (exit FCF ÷ current FCF)^(1/N) − 1 | X% | X% | X% |
| Realism vs. history / consensus / Section 10 | | | |

**Common error to avoid — inverted math:**
Do not state that a small year-N FCF or owner-earnings figure "justifies" today's market cap. The math runs in one direction: today's market cap, compounded at the target return, defines the required exit value; the exit multiple then defines the required exit FCF. A small required exit FCF means the price is justified — but the only way to know what counts as "small" is to run the compounding step first.

*Worked example of the error:* "$5–6B of year-10 owner earnings justifies a $135B market cap at 10% return and 25× exit multiple" — this is wrong. $135B × (1.10)^10 = ~$350B required exit market cap. At a 25× exit multiple, that requires ~$14B of year-10 owner earnings, not $5–6B. Always compute the exit value first.

State all assumptions. Tag as `[Estimate]`. Explain whether base-case assumptions are realistic given history and sector.

**Rules:**
- Never use a single-point estimate. Always show a range.
- Always compound today's market cap forward first — then calculate required exit FCF. Do not reverse the order.
- A great business can still be a bad stock if valuation already prices in perfection.
- **Valuation has override power.** If valuation is extreme, the verdict should not be BUY unless expected-return math supports it.
- If the base case requires top-decile execution for a decade, say so plainly.
- Link required FCF CAGR back to Section 10 (Growth Durability) for consistency.

**Rating:** 🔴 Expensive / 🟡 Fair / 🟢 Attractive

---

## Section 18 — Quantitative Overlays

Only include an overlay if the required inputs are available. Show the component inputs, not just the final score. If estimated, label clearly.

**Output labels:** Calculated | Estimated | Not Applicable | Insufficient Data

---

### Piotroski F-Score (Accounting Quality & Financial Strength)
More useful for value/quality screening than early-stage growth companies.

| Signal | Description | Result (1/0) |
|--------|-------------|-------------|
| F1 | ROA > 0 | |
| F2 | OCF > 0 | |
| F3 | ROA increasing YoY | |
| F4 | OCF > Net Income (cash-backed) | |
| F5 | Leverage decreasing YoY | |
| F6 | Current ratio improving YoY | |
| F7 | No new share issuance in past year | |
| F8 | Gross margin improving YoY | |
| F9 | Asset turnover improving YoY | |
| **Total** | | **/9** |

- 8–9: 🟢 Strong
- 5–7: 🟡 Average
- 0–4: 🔴 Weak (value trap risk)

---

### Beneish M-Score (Earnings Manipulation Probability)
Requires actual input calculation. Do not simply say "no manipulation flags."
Not ideal for banks and insurance companies.

| Variable | Description | Value |
|----------|-------------|-------|
| DSRI | Days Sales Receivable Index | |
| GMI | Gross Margin Index | |
| AQI | Asset Quality Index | |
| SGI | Sales Growth Index | |
| DEPI | Depreciation Index | |
| SGAI | SGA Index | |
| LVGI | Leverage Index | |
| TATA | Total Accruals to Total Assets | |
| **M-Score** | | |

- M > −1.78: 🔴 Probable manipulator — flag for deep review
- −2.22 to −1.78: 🟡 Grey zone
- M < −2.22: 🟢 Unlikely manipulator

---

### Altman Z-Score (Distress Risk)
Less useful for asset-light software and financial institutions. Use Z' for private firms; Z'' for non-manufacturers.

Z = 1.2×(WC/TA) + 1.4×(RE/TA) + 3.3×(EBIT/TA) + 0.6×(MktCap/TL) + 1.0×(Rev/TA)

| Component | Value |
|-----------|-------|
| Working Capital / Total Assets | |
| Retained Earnings / Total Assets | |
| EBIT / Total Assets | |
| Market Cap / Total Liabilities | |
| Revenue / Total Assets | |
| **Z-Score** | |

- Z > 2.99: 🟢 Safe zone
- 1.81–2.99: 🟡 Grey zone
- Z < 1.81: 🔴 Distress zone → feeds into Section 9 hard stop

---

### Rule of 40 (SaaS / Software only)
Rule of 40 = Revenue Growth % + FCF Margin %

- ≥ 40: 🟢
- 20–39: 🟡
- < 20: 🔴

---

## Section 19 — Summary Weighted Scorecard

**Weight propagation rule (hard):** The weights used in this scorecard must be the **exact same weights** stated in Section 5 (Dominant-Risk Weighting). The two sections cannot disagree. If Section 5 says Valuation / Expected Return is 35%, Section 19 must show Valuation / Expected Return at 35%. Any divergence is a QC failure and the memo must be regenerated.

**Required weights for high-multiple growth stocks:**
- Valuation / Expected Return: **30–40%** (must match the 30–40% rule from Section 5)
- Credit / Loan-Loss Trajectory: **10–20%** when the company has meaningful lending, BNPL, MCA, or credit exposure (carved out from Business-Model Specific Risks)
- Trading / Catalysts / Position Sizing: combined cap of **5%** (or excluded entirely)
- All other dimensions: distributed across the remaining weight

Apply weights from Section 5. Score: 🟢 = 2, 🟡 = 1, 🔴 = 0. Multiply by weight. Sum for weighted score (×50 to scale to 0–100).

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  STOCK EVALUATION SCORECARD — [TICKER]
  Archetype: [type] | Date: [date]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  ⚠️  HARD STOPS TRIGGERED?   YES / NO
      (list each one if YES)

  Section  Area                                  Rating   Weight  Score
  -------  ------------------------------------  ------   ------  -----
  7.       P&L Health                            🟢/🟡/🔴  [%]
  8.       Cash-Flow Quality & Owner Earnings    🟢/🟡/🔴  [%]
  9.       Balance Sheet & Liquidity             🟢/🟡/🔴  [%]
  10.      Growth Durability                     🟢/🟡/🔴  [%]
  11.      Competitive Position / Moat           🟢/🟡/🔴  [%]
  12.      Management, Governance & Alloc.       🟢/🟡/🔴  [%]
  13.      Earnings Quality & Forensics          🟢/🟡/🔴  [%]
  14.      Macro & External Risks                🟢/🟡/🔴  [%]
  15.+16.  Historical Price & Trading/Timing     🟢/🟡/🔴  [%]   ← combined ≤ 5%
  17.      Valuation vs. Expected Return         🟢/🟡/🔴  [%]   ← 30–40% if high-mult.
  6a.      Business-Model Specific Risks         🟢/🟡/🔴  [%]
  6b.      Credit / Loan-Loss Trajectory         🟢/🟡/🔴  [%]   ← 10–20% if applicable
  21.+22.  Catalysts + Position Sizing           🟢/🟡/🔴  [%]   ← combined ≤ 5%
                                                          -----
                                                          100%

  QUANTITATIVE OVERLAYS (informational — not weighted)
  Piotroski F-Score:   [X/9]    🟢/🟡/🔴   [Calculated / Estimated / N/A]
  Beneish M-Score:     [X.XX]   🟢/🟡/🔴   [Calculated / Estimated / N/A]
  Altman Z-Score:      [X.XX]   🟢/🟡/🔴   [Calculated / Estimated / N/A]
  Rule of 40:          [X]      🟢/🟡/🔴   [Calculated / N/A]

  WEIGHTED SCORE:   [XX / 100]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Verdict guidance (base mapping):**
- **BUY / BUY ONLY IF PRICE IS ATTRACTIVE** — Score ≥ 70, no hard stops, valuation supports expected return
- **WATCH / WAIT FOR BETTER ENTRY** — Score 45–69, or strong business with stretched valuation
- **AVOID / TOO RISKY** — Any hard stop, OR score < 45, OR dominant-risk dimension is 🔴

**Score-verdict alignment rule (hard override):**

The numerical score must align with the verdict. The mapping above is the *base case* — but the following overrides take precedence whenever they apply:

1. **🔴 Valuation override** — If Valuation / Expected Return is rated 🔴 and carries 30%+ weight, the verdict cannot be BUY regardless of the numerical score. Default to **WATCH / WAIT FOR BETTER ENTRY** even if the score is ≥ 70. A "Wait for better price" verdict must not be paired with a score that looks like a strong buy. If the score and verdict appear inconsistent, the verdict wins — but the score itself should also be re-examined; a high score with a 🔴 valuation likely means other weights were misapplied.

2. **🔴 Dominant-risk override** — If the dimension identified as the dominant risk in Section 5 (regardless of which one it is) is rated 🔴, the verdict cannot be BUY regardless of the numerical score. Default to **WATCH** or **AVOID** depending on severity.

3. **Hard-Red credit-loss override** — If Credit / Loan-Loss Trajectory is at the ☠️ Thesis Breaker tier (per Section 8 credit-loss severity classification), default the verdict to **AVOID** regardless of the numerical score.

4. **Score-verdict consistency check** — Before finalizing the memo, verify that the numerical score and the stated verdict tell the same story. If the score says "BUY territory" (≥ 70) but the verdict says "WATCH / WAIT," explain explicitly in the memo why the override applies. Do not deliver a memo where the score and verdict appear to contradict each other without explanation.

---

## Section 20 — Entry Price / Margin of Safety

If the stock is high quality but expensive, show what different price levels imply for risk/reward.

| Price Scenario    | Implied Mkt Cap | Implied EV | FCF Yield | SBC-Adj. FCF Yield | EV/FCF | Req. FCF CAGR (base) | Implied IRR (base) | Risk/Reward |
|-------------------|-----------------|------------|-----------|-------------------|--------|----------------------|--------------------|-------------|
| Current price     |                 |            |           |                   |        |                      |                    |             |
| 10% lower         |                 |            |           |                   |        |                      |                    |             |
| 20% lower         |                 |            |           |                   |        |                      |                    |             |
| 30% lower         |                 |            |           |                   |        |                      |                    |             |

**Calculation rules:**
- Implied market cap = price scenario × diluted share count.
- Implied EV = implied market cap + total financial debt + preferred + minority interest − total liquid assets (same deductions as Section 9).
- FCF yield = FCF ÷ implied market cap.
- EV/FCF = implied EV ÷ FCF.
- Required FCF CAGR = derived by first compounding the implied market cap at that price forward by the holding period at the target return to get the required exit market cap, then dividing by the exit multiple to get required exit FCF, then solving for the CAGR from current FCF to that exit FCF. Never derive this rate without the compounding step.
- **Implied IRR (base case)** = the annualized return at that price given the **base-case exit EV (or market cap) from Section 17**. Calculate it as: IRR = (Base-case exit market cap ÷ implied market cap at this price)^(1/years) − 1. Every IRR figure in this table must be derived from the same base-case exit value used in Section 17 — they cannot diverge.
- Show enough arithmetic that the user can sanity-check each cell. Do not state an implied multiple, yield, or IRR unless the formula supports it.
- Do not assign an IRR range to a price band unless the math at each price tier confirms it. If the base-case exit is $X bn over Y years, then for a price implying market cap $A bn the IRR is exactly $(X/A)^{1/Y} - 1$ — not a guess and not a generic "10–13%" label.
- Do not claim an entry zone implies a low FCF multiple unless the EV/FCF calculation at that price actually confirms it.

**Language rules:**
- Do not claim a pullback creates a "margin of safety" unless the expected-return math supports it.
- Use: *"A pullback improves risk/reward but the stock may still be expensive."*
- Use: *"This price creates a more reasonable expected return under base-case assumptions."*
- Never imply a lower price automatically makes a stock a buy.

---

## Section 21 — Catalysts to Watch

*Specific upcoming events that could change the thesis, valuation, or sentiment.*

Catalysts inform monitoring and timing. They do not establish whether the stock is fundamentally attractive — fundamentals and valuation do.

| Catalyst | Expected Timing | What to Watch | Bullish / Neutral / Bearish Trigger |
|----------|-----------------|---------------|--------------------------------------|
|          |                 |               |                                      |

**General catalysts to consider:**
- Next earnings report (date, key metrics expected)
- Guidance update
- Revenue growth trend
- Margin trend
- Free cash flow trend
- Buyback / dividend announcement
- Debt refinancing or maturity
- Product launch
- Regulatory decision
- Investor day
- Major contract renewal
- M&A or divestiture
- Litigation milestone
- Macro data relevant to the business
- Industry-specific catalyst

**Business-model-specific catalysts** (use only those relevant to the archetype from Section 6):

| Archetype | Common Catalysts |
|-----------|------------------|
| SaaS/Software | ARR/RPO update, NRR disclosure, AI product monetization, cloud cost trends, enterprise customer growth |
| Marketplace/Platform | GMV/GTV/TPV growth, take rate, buyer/seller growth, payment penetration, platform outages or policy changes |
| Payments/Lending/Fintech | Credit losses, delinquencies, loan book growth, funding costs, regulatory changes, allowance coverage |
| Bank | NIM, deposits, NPLs, charge-offs, CET1 / capital ratios |
| Retail | Same-store sales, inventory levels, markdown pressure, holiday season performance |
| Industrial/Cyclical | Backlog, book-to-bill, utilization, capex cycle indicators |
| Energy/Commodities | Commodity price moves, production updates, reserve replacement |
| REIT | Occupancy, NOI growth, debt refinancing, dividend coverage |
| Biotech/Pharma | Trial readouts, FDA/PDUFA dates, cash runway, patent/litigation events |

**Rules:**
- Catalysts must be **specific and actionable** — avoid vague items like "good news" or "more growth."
- Tie each catalyst to the investment thesis. Explain what outcome would be bullish, neutral, or bearish.
- If the next earnings date is not verified from the IR page or filing calendar, mark it Estimated or Needs Review.
- Catalysts are monitoring tools. They do not replace the kill criteria in Section 23.
- **Treat accounting classification changes as comparability issues, not true economic catalysts.** A reclassification between operating, investing, and financing cash flows, or between revenue line items, changes how numbers are reported — not the underlying economics. Note them in this section only as comparability warnings, and flag them in Section 13 (Earnings Quality) where they belong. Do not present them as bullish or bearish drivers of value.

---

## Section 22 — Position Sizing / Portfolio Risk Framing

*Should this stock be a core position, small position, speculative position, or avoided entirely?*

This is a risk-framing tool, **not personalized financial advice**. It translates the analysis above into how aggressively the stock should be sized in a diversified portfolio.

| Risk Factor                          | Assessment       | Position-Sizing Implication                              |
|--------------------------------------|------------------|----------------------------------------------------------|
| Business quality                     | High / Med / Low | Core candidate or not                                    |
| Valuation risk                       | High / Med / Low | Avoid over-sizing if expensive                           |
| Balance sheet risk                   | High / Med / Low | Lower risk if net cash; higher risk if leveraged         |
| Earnings / cash-flow quality         | High / Med / Low | Higher confidence if cash-backed                         |
| Volatility / beta                    | High / Med / Low | Smaller position if highly volatile                      |
| Cyclicality / macro sensitivity      | High / Med / Low | Smaller position if cyclical                             |
| Red flags                            | None / Mod / Sev | Reduce size or avoid                                     |
| Investor thesis confidence           | High / Med / Low | Affects starter vs. full position                        |

**Sizing bucket (qualitative):**
- Avoid / Watchlist only
- Tiny / speculative position
- Small starter position
- Medium position
- Core position candidate

**Generic risk buckets (not personalized advice; assumes a diversified equity portfolio):**

| Bucket            | Generic Range |
|-------------------|---------------|
| Tiny / speculative| 0.5–1%        |
| Small             | 1–3%          |
| Medium            | 3–6%          |
| Core              | 6–10%+        |

These ranges are illustrative risk buckets, not allocations. Do not give personalized percentages unless the user provides portfolio context.

**Action framing:** state which of the following applies:
- Starter position
- Add-on only after pullback
- Hold existing position
- Avoid new money
- Exit / reduce

**Rules (risk-framing, not prescriptive):**
- For high-quality but expensive stocks, the risk profile usually suggests **Small or Medium** sizing rather than Core, unless valuation is attractive on the expected-return math.
- For high-risk or red-flag stocks, the risk profile usually suggests **Tiny / Watchlist / Avoid** even if upside looks large.
- Do not recommend averaging down unless the thesis remains intact and the valuation has actually improved per Section 20 and Section 17.
- Severe red flags or any hard stop in Section 3 → default to Avoid regardless of upside.
- Use risk-framing language ("the risk profile suggests…", "this sizing reflects…") rather than prescriptive absolutes ("never concentrate", "always small"). Position sizing is a function of the user's portfolio, risk tolerance, and time horizon — none of which the skill knows. Frame the implication; do not dictate the decision.

**Suggested language:** *"Position sizing should follow risk, not excitement. A great company at a stretched valuation may deserve a smaller position than a good company at a great price."*

---

## Section 23 — Thesis Breakers / Kill Criteria

*What would make the investment thesis wrong after purchase?*

Kill criteria must be **specific, measurable, and directly connected to the thesis.** Generic warnings are not useful.

| Kill / Watch Trigger                                          | Why It Matters                                      | Severity        |
|---------------------------------------------------------------|-----------------------------------------------------|-----------------|
| [Specific metric falls below specific threshold]              | [Directly tied to thesis]                           | ☠️ Kill / ⚠️ Watch |
| [Specific event or disclosure]                                | [What it signals]                                   | ☠️ Kill / ⚠️ Watch |

**Severity codes:**
- ☠️ **Kill** — exit immediately; thesis is broken
- ⚠️ **Watch** — elevate concern; re-evaluate within 1–2 quarters

Generate 6–10 company-specific triggers. Draw from:
- The dominant-risk dimensions identified in Section 5
- Business-model-specific metrics from Section 6
- Any yellow/red flags found in earlier sections

**Universal kill triggers (always include):**
- Auditor change, material weakness, or restatement → ☠️ Kill
- Revenue growth falls below thesis-required rate for 2+ consecutive quarters → ☠️ Kill
- Gross margin compresses > [X]pp without credible explanation → ⚠️ Watch
- Net debt rises above [X×] EBITDA → ⚠️ Watch / ☠️ Kill depending on severity
- Management misses guidance 3+ consecutive quarters without accountability → ⚠️ Watch

**For expensive growth stocks — triggers must fire before the business visibly collapses:**
The kill criteria should be calibrated to the valuation thesis, not to obvious distress. At a premium multiple, the thesis breaks much earlier than at a value multiple. Always derive thresholds from the reverse DCF in Section 17.

| Valuation-Thesis-Linked Trigger | Why It Fires Early | Severity |
|---|---|---|
| Revenue growth decelerates below the rate required by the base-case DCF for 2+ quarters | Premium multiple is priced on that growth rate | ☠️ Kill |
| FCF margin compresses below the floor assumed in the base-case scenario | Owner earnings are worse than the price implies | ⚠️ Watch → ☠️ Kill if sustained |
| Gross margin deteriorates by more than [X]pp with no credible recovery path | Unit economics are worse; growth is less valuable | ⚠️ Watch |
| SBC rises above [X]% of revenue or [Y]% of FCF for 2+ consecutive quarters | Owner earnings are being diluted away | ⚠️ Watch |
| Valuation remains extreme (EV/FCF > [X]×) while revenue growth decelerates materially | Risk/reward deteriorates; exit multiple may compress | ⚠️ Watch → ☠️ Kill |
| Credit/transaction losses grow more than 2× faster than revenue for 2+ quarters (where applicable) | Credit quality is deteriorating faster than top-line | ☠️ Kill |

*Fill in the bracketed thresholds using the actual numbers from the reverse DCF and business-model analysis. Generic thresholds are not useful.*

---

## Section 24 — Final Verdict

The verdict must be driven **primarily by fundamentals, valuation, balance sheet, cash flow, and red flags**. Technical setup, analyst sentiment, and catalysts may inform timing — they do not establish intrinsic value.

Use this exact structure:

**Business Quality:** [Excellent / Good / Mixed / Poor] — [1–2 sentence rationale]

**Financial Health:** [Strong / Adequate / Stretched / Distressed] — [1–2 sentence rationale]

**Valuation / Expected Return:** [Attractive / Fair / Stretched / Extreme] — [1–2 sentence rationale including implied return from Section 17]

**Main Red Flags:** [The most important red flags from Sections 3, 13, and other relevant sections — or "None material"]

**Technical / Timing Context:** [1–2 sentences from Section 16 — *timing only, not valuation*]

**Main Catalysts:** [2–3 specific upcoming events from Section 21 that could move the thesis or sentiment]

**Position-Sizing Implication:** [The bucket from Section 22: Avoid / Watchlist / Tiny / Small / Medium / Core]

**Biggest Risk:** [Single most important risk in plain language]

**What Must Go Right:** [The 2–3 specific things that must happen for the investment to work]

**What Would Change My Mind:** [The 2–3 specific developments that would flip the verdict]

**Verdict:** BUY / BUY ONLY IF PRICE IS ATTRACTIVE / WATCH / WAIT FOR BETTER ENTRY / HOLD / AVOID / TOO RISKY

**Confidence Level:** High / Medium / Low — [reason for uncertainty if Medium or Low]

**Next Things to Monitor:** [3–5 specific metrics or events to watch next quarter, drawing from Section 21]

---

**Important:**
- Do not let many green operational checks overpower one large red valuation or balance-sheet risk.
- If the company is excellent but valuation requires near-perfect execution, the verdict should usually be **WATCH**, not **BUY**.
- Technical context, catalysts, and position-sizing framing must collectively influence the verdict by no more than **5%**. They refine **timing and sizing**, not the **buy/watch/avoid decision** itself.
- If confidence is Low due to data gaps, say so explicitly rather than masking uncertainty with false precision.

---

## Section 25 — Sources

List every source used, with filing period and access date where relevant.

| # | Source | Type | Period / Date |
|---|--------|------|--------------|
| 1 | SEC 10-K | Primary | FY [year] |
| 2 | SEC 10-Q | Primary | Q[X] [year] |
| 3 | Earnings release | Company | Q[X] [year] |
| 4 | [Data provider] | Market Data | As of [date] |
| … | | | |

---

## Analyst Guidance (internal instructions for Claude)

- **Tone:** Skeptical but fair. Evidence-based. Not promotional. Not fearmongering. Clear about uncertainty.
- **Format:** Produce a finished investor memo. No internal narration ("Now I have enough data…", "Let me compile…"). No filler. **No hollow preambles** — do not write phrases like "before I dive in, a couple of questions," "before I kick off, let me ask…", "let me first clarify a few things," "I'd like to ask…", or any other process-text opener, unless the memo actually contains follow-up questions and stops to wait for user answers. If the skill is producing the memo end-to-end without pausing for input, there is no place for such openers. Start the memo with the disclaimer and Section 2 (Company Snapshot).
- **Jargon:** Briefly explain technical terms (ROIC, WACC, EV/FCF, SBC, GMV, NRR, AFFO, CAM) the first time they appear.
- **Per-share discipline:** Always express key metrics per share as well as in absolute terms.
- **Trend discipline:** Use 3–5 year trends. Point-in-time snapshots mislead.
- **Period discipline:** Label every figure as FY, quarterly, or TTM. Never call FY revenue "TTM."
- **Language precision:** Say "revenue grew X% year-over-year" — not "beat expectations by X%" unless analyst consensus is sourced. Say "financial distress risk appears very low" — not "bankruptcy risk is zero."
- **Filing-data extraction discipline:** If a 10-Q or 10-K has been reviewed, extract all disclosed items from it. Do not mark Needs Review for items present in the filing. This applies to: SBC, buyback details (shares, dollars, average price, remaining authorization), cash, marketable securities, short-term investments, diluted share count, all operating KPIs management discloses relevant to the company's archetype (see Section 2.5 — Company Archetype Classification), credit/transaction loss data, CAMs, auditor opinion, and ICFR status. Company filings are authoritative for all company-specific facts; third-party articles are not.
- **EV discipline:** Always deduct all liquid assets from EV: cash, cash equivalents, marketable securities, short-term investments, and liquid long-term investments. Do not deduct only cash if material liquid assets are separately disclosed. Show the arithmetic. Do not assert an EV-based multiple unless the formula is transparent.
- **Gap discipline:** If data is genuinely unavailable after reviewing all available filings, say so and mark Needs Review. Never fill gaps with silent assumptions.
- **Source discipline:** Use primary filings first. If a 10-Q or 10-K covers the period, do not say data was unavailable. Label market-share figures as Third-Party Market Data. Company filings override third-party articles for company-specific facts.
- **SBC discipline:** Never treat SBC as harmless. Always compute owner earnings. Use actual filed SBC, not guided SBC. Describe both absolute and percentage trends accurately.
- **Buyback discipline:** Always distinguish authorization from execution. Show shares, dollars, average price from filing, and remaining authorization. Compare average repurchase price to current price and estimated intrinsic value. Assess value-accretiveness. Do not estimate average price if the filing discloses it.
- **Take-rate discipline:** For marketplace/platform companies, always calculate take rate explicitly (revenue ÷ volume metric). Compare periods. Do not assert direction without the calculation.
- **Credit discipline:** For any company with lending, BNPL, merchant advances, or receivables exposure, always calculate loss rates vs. revenue and vs. FCF, and track against revenue growth.
- **Debt discipline:** Always distinguish financial debt from total liabilities. Never say "debt-free" loosely.
- **Entry-price math discipline:** Show the arithmetic behind every implied multiple and yield in the entry-price table. Do not assert a number unless the formula supports it.
- **Valuation discipline:** Valuation has override power. A great business at an extreme price is still a Watch or Avoid. For high-growth stocks, valuation carries 30–40% of the weighted score. The scorecard interpretation must match the final verdict.
- **Kill criteria discipline:** For expensive growth stocks, calibrate kill thresholds to the valuation thesis — they must fire before the business visibly collapses. Derive thresholds from the reverse DCF numbers.
- **Overlay discipline:** Never present forensic scores unless inputs are calculated or clearly estimated. Label Calculated / Estimated / Not Applicable. Note Altman Z limitations for asset-light software and banks.
- **Weighting discipline:** Weight checks by archetype. Don't treat all checks equally.
- **Data sources:** SEC EDGAR, company IR pages, Yahoo Finance, Macrotrends, Tikr, Koyfin, Wisesheets, Bloomberg (if available). Reputable news for context only. Never SEO/agency content for financial claims or KPIs.

