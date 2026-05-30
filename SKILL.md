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
18. Intrinsic Value / Fair Value Estimate
19. Quantitative Overlays (only if inputs are available)
20. Summary Weighted Scorecard
21. Entry Price / Margin of Safety
22. Catalysts to Watch
23. Position Sizing / Portfolio Risk Framing
24. Thesis Breakers / Kill Criteria
25. Final Verdict
26. Sources

**Important separation principle:**
- Sections 1–15, 17, 19, 20, 23: drive the business thesis, valuation thesis, and red-flag analysis.
- Sections 16 (Trading/Timing), 22 (Catalysts), 23 (Position Sizing): support **timing, monitoring, and risk framing only**. They must never override fundamentals, valuation, or red flags. Their collective influence on the final verdict is capped at **5%**.

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
- **TTM consistency check (hard rule):** Before producing the memo, verify every TTM figure by re-applying the formula. If the value stated for "TTM revenue" (or TTM FCF, TTM SBC, TTM losses, etc.) does not match `latest FY + current-year interim − prior-year comparable interim`, the output fails QC and must be regenerated with corrected arithmetic. Show the three component figures alongside the TTM total so the reader can verify.
- Never say "revenue growth beat expectations by X%" unless analyst consensus figures are sourced. Say "revenue grew X% year-over-year" unless the beat is directly supported.
- Always calculate growth rates directly from the two filed values: growth = (current period − comparable prior period) ÷ comparable prior period. Do not approximate, round to the nearest convenient figure, or carry forward a growth rate from another source without verification. This applies to revenue, FCF, OCF, SBC, loan book, losses, and every other metric where a YoY or QoQ growth rate is asserted.

**Currency discipline**
- **Label every monetary figure with its currency** (USD, CAD, EUR, GBP, JPY, etc.). Do not assume the reader can infer.
- **Never mix currencies in a single calculation.** This applies especially to dual-listed stocks and companies that report financials in one currency but trade in another (e.g., a Canadian company reporting in CAD but with a U.S. ADR price in USD).
- **Dividend yield must use the same currency for numerator and denominator.** Convert dividend per share and stock price into a single currency at a stated exchange rate (date shown) before dividing. A CAD dividend divided by a USD price is not a yield.
- **Per-share intrinsic value, multiples, and valuation outputs** must be in a single declared currency. State the currency at the top of Section 2 (Company Snapshot) and use it consistently throughout.
- If financials are reported in one currency and the user holds the stock in a different listing (e.g., U.S. holder owns a Canadian listing, or a European ADR), present per-share figures in **both** currencies with the exchange rate and date explicit. The intrinsic-value comparison must be made in the holder's purchase currency.
- For companies with significant FX translation exposure, note constant-currency vs. reported growth separately when material.

**Debt and balance sheet**
- Never confuse total liabilities with financial debt.
- Always separate: cash and equivalents / marketable securities / short-term financial debt / long-term financial debt / finance leases / operating leases / operating liabilities / total liabilities.
- Never say "effectively debt-free" unless financial debt is truly minimal relative to cash and FCF generation.
- For financial companies, use industry-specific capital and liquidity metrics rather than generic debt ratios.
- **Debt-leverage reconciliation rule:** When the memo reports both adjusted EBITDA (or adjusted EBITDAX, distributable cash flow, etc.) and a Debt/EBITDA ratio, the implied debt figure must reconcile with the reported debt figure on the balance sheet:
  `Implied debt = Adjusted EBITDA × Debt/EBITDA`
  If reported debt differs from implied debt by more than 10–15%, the memo must explain the difference. Common reasons:
  - Adjusted debt vs. balance-sheet debt (analysts often adjust)
  - Net debt vs. gross debt (one subtracts cash, one doesn't)
  - Preferred equity or hybrid securities included as debt-equivalent
  - Project-level / non-recourse debt at subsidiaries
  - Operating leases capitalized into the debt figure
  - FX conversion between reporting currency and debt currency
  - Non-controlling interest in subsidiary debt
  - Pro-forma adjustments for recent acquisitions or divestitures
  If the difference cannot be explained from the filing, **mark EV, debt, and leverage as Needs Review** rather than report a Debt/EBITDA figure that does not reconcile. Do not silently use one definition in one section and a different definition in another.
- For pipeline, utility, infrastructure, and other leverage-intensive archetypes where Debt/EBITDA is a primary metric: the reconciliation must be shown explicitly in the Data Integrity Check Notes column for the debt row.

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
- **Buyback source-of-truth rule:** All five figures (shares, dollars, average price, total authorization, remaining authorization) must come from the **repurchase activity table** disclosed in the 10-Q/10-K (typically in Part II Item 2 — Unregistered Sales of Equity Securities and Use of Proceeds, or in the equity/notes section). Do **not** derive average repurchase price by dividing total cash spent on repurchases (from the cash-flow statement's financing activities) by total shares — this can be inaccurate because of timing differences, accrued repurchases, and rounding. Use the average price disclosed in the repurchase activity table directly.
- Do not say repurchase activity was undisclosed or unavailable if a 10-Q or 10-K covers the period.
- Buybacks at high valuations should be analyzed skeptically. A buyback is only shareholder-friendly if value-accretive or efficiently offsetting dilution.

**Take rate and KPI calculations (marketplace/platform companies)**
- Calculate take rate explicitly as: revenue ÷ GMV, GTV, TPV, or equivalent volume metric.
- Show current period vs. prior period.
- **Take-rate source-of-truth rule:** If the filing discloses GMV/GTV/TPV for the period, use that exact figure. Do not approximate, round, or substitute a different period's value. If presenting a TTM take rate, calculate it as `TTM revenue ÷ TTM GMV` (using TTM components built per the TTM consistency formula in Period and label discipline) — not as a single quarter ratio applied to TTM revenue, and not as a generic approximation.
- Do not say take rate is rising or falling unless the calculation supports the direction.
- Do not say the volume metric is unavailable for the period if the 10-Q/10-K discloses it.

**KPI definition discipline (applies to all archetype-specific KPIs)**
- **Do not conflate different metrics.** Common confusions to avoid:
  - **Penetration vs. growth:** Penetration is `[segment volume] ÷ [total volume]` (a ratio, %); growth is the YoY change in that segment (also %, but a different number). A 41% growth rate in Payments volume is not the same as 41% penetration. Report both separately when both are disclosed.
  - **GPV vs. GMV vs. payment volume vs. TPV:** These are distinct disclosed figures. Use the company's exact label. Do not substitute one for another.
  - **Gross vs. net:** Gross take rate vs. net take rate, gross merchandise vs. net merchandise, gross revenue vs. net revenue — always use the company's defined term and state which is being used.
  - **% of revenue vs. % of volume vs. % of customers:** A metric "as a % of revenue" is not the same as "as a % of GMV" or "as a % of merchants." Specify the denominator every time.
- **Always state the formula** for any KPI being reported. Example: *"Payments penetration = Payments GPV ÷ total GMV = $X ÷ $Y = Z%."* If the formula cannot be shown, mark the KPI Needs Review rather than report a number whose definition is ambiguous.
- **Always show both numerator and denominator** for any ratio-type KPI (penetration, take rate, attach rate, etc.), in addition to the resulting percentage.
- **Distinguish levels from changes.** Penetration of 67% is a level. Penetration up from 64% to 67% is a 3-percentage-point change (or a ~4.7% relative change). Do not report a change as a level or vice versa.
- **Multiple-labeling rule (market-cap vs. enterprise-value multiples):** Always pair the numerator and denominator correctly and label the resulting ratio precisely:
  - **Market-cap-based multiples** (numerator = market cap or share price) pair with **equity-level** cash-flow metrics. Acceptable labels: `P/E`, `P/FCF`, `P/DCF`, `P/AFFO`, `P/FFO`, `P/B`, `P/TBV`, `Price/Sales`. The "P" denotes Price (i.e., market cap).
  - **Enterprise-value-based multiples** (numerator = EV) pair with **enterprise-level** cash-flow metrics. Acceptable labels: `EV/EBITDA`, `EV/EBIT`, `EV/Sales`, `EV/FCF` (where FCF here is unlevered FCF or enterprise FCF, not equity FCF).
  - **Common error:** Computing market-cap ÷ DCF and labeling it `EV/DCF`. This is wrong. Either keep market cap in the numerator and call it `P/DCF`, or use EV in the numerator and pair it with an enterprise-level cash-flow metric (typically EBITDA, not DCF — because DCF is calculated after interest, which is an equity-level figure).
  - For pipelines, MLPs, utilities, and other income-stock archetypes: **P/DCF** uses market cap; **EV/EBITDA** uses enterprise value. Do not cross-label them.
  - If a multiple is reported, the memo must state both numerator and denominator the first time it appears (e.g., *"P/DCF (price ÷ distributable cash flow per share)"*). Subsequent references can use the shorthand.

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
  3. **☠️ Hard-Red / Thesis Breaker** — Either (a) two consecutive quarters with credit losses growing more than 2× faster than revenue, OR (b) worsening allowance coverage combined with rising charge-offs. Treat as a hard stop equivalent: default verdict to AVOID unless there is compelling, specific evidence of imminent reversal. Add to Section 24 Kill Criteria as ☠️ Kill.
- Each of these three severity levels must be applied **separately** — do not collapse them into a single "red flag" treatment. The scorecard and final verdict consequences differ.

**Cash-flow comparability**
- If the company changes cash-flow classification or presentation between periods, flag it clearly.
- **Always check the latest 10-Q and 10-K for announced future reclassifications** between operating, investing, and financing activities — including changes that will take effect in a future quarter or fiscal year. These are disclosed in the notes to the financial statements (often under "Recent Accounting Pronouncements" or business-specific disclosure). Do not state "no classification changes were found" without reviewing these notes.
- **Mandatory search-term sweep:** Before concluding no reclassification was disclosed, search the full MD&A and notes for these terms: *"reclassification," "reclassified," "presentation change," "cash flows," "operating activities," "investing activities," "financing activities," "merchant cash advances," "loans receivable," "previously reported," "prospectively,"* and any other phrase that signals a presentation change. If any of these surface a disclosure, include it in the memo.
- **Prohibition on denial:** If the filing discloses any past or upcoming reclassification — whether already in effect or scheduled for a future period — do not state that no reclassification was identified. Quote the disclosure language or paraphrase it accurately, including the effective date.
- A reclassification is a **comparability issue, not an economic improvement or deterioration**. Reported OCF or FCF can rise or fall purely because of the reclassification — do not attribute the change to operating performance.
- **Mandatory normalization warning:** When a future reclassification has been announced, include an explicit warning in the memo such as: *"Future OCF and FCF comparisons must be normalized for the [item] reclassification effective [date]. Pre- and post-effective-date figures are not directly comparable."* This warning must appear in Section 8 (Cash-Flow Quality) and again in Section 13 (Earnings Quality) where comparability matters.
- Normalize FCF where possible and label the normalization (e.g., "FCF excluding reclassified [item] for comparability").
- Flag reclassifications as catalysts only in the comparability sense (Section 22 rule), never as economic catalysts.

**Forensic and audit discipline**
- Always review the auditor opinion and critical audit matters (CAMs).
- If the 10-K has been reviewed, list each CAM by its actual title from the auditor report — do not summarize generically or say "no CAMs flagged" when they exist. Example titles take the form *"Revenue Recognition — Principal versus Agent Considerations,"* *"Valuation of Goodwill,"* etc.
- **Auditor identity:** State the actual auditor named in the 10-K (e.g., PricewaterhouseCoopers LLP, Ernst & Young LLP, Deloitte & Touche LLP, KPMG LLP, BDO USA LLP, or other). Do not guess. Do not substitute a different Big-Four name for the one listed in the auditor report.
- **CAM completeness rule (hard):** Use only the CAMs actually listed in the auditor report. Do not infer additional CAMs based on the business model or topics that "should be" CAMs. If the auditor report lists one CAM, the memo lists one CAM. Do not invent or augment.
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

**Timing, catalysts, and position sizing (Sections 16, 22, 23)**
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
| 10 | Does the entry-price table (Section 21) show IRRs that are consistent with the Section 17 base-case exit value? | Entry-price IRR-consistency rule |
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
| 24 | Do the weights shown in Section 20 (Summary Weighted Scorecard) exactly match the weights stated in Section 5 (Dominant-Risk Weighting)? Any divergence is a QC failure. | Section 20 — Weight propagation rule |
| 25 | If Valuation / Expected Return is rated 🔴 and carries 30%+ weight, has the verdict been overridden to WATCH or AVOID — regardless of the numerical score? | Section 20 — Score-verdict alignment rule |
| 26 | Does the final numerical score align with the final verdict? If they appear to diverge (e.g., score ≥ 70 but verdict is WATCH), is the override reason stated explicitly in the memo? | Section 20 — Score-verdict consistency check |
| 27 | Does Section 18 include the bear/base/bull scenario table, the summary table, and a probability-weighted intrinsic value? | Section 18 — Required outputs |
| 28 | Is the valuation label (undervalued / fairly valued / overvalued) consistent with the classification rules, and softened when confidence is Low? | Section 18 — Classification + label-softening rules |
| 29 | Does Section 25 (Final Verdict) include the intrinsic-value summary: current price, base-case IV/share, probability-weighted IV/share, valuation label with confidence, and margin of safety? | Section 18 — Integration with Final Verdict |
| 30 | If the intrinsic-value estimate relies on stale or unverified data, is confidence marked Low and is the estimate excluded from justifying a Buy rating? | Section 18 — QC rule |
| 31 | Has every TTM figure been verified against the formula (latest FY + current interim − prior comparable interim), with all three component figures shown? | TTM consistency check |
| 32 | Is the auditor named exactly as listed in the 10-K, and are CAMs listed exactly as titled in the auditor report (no inferred or invented CAMs)? | Auditor identity + CAM completeness rules |
| 33 | Has the full MD&A and notes been searched for reclassification keywords ("reclassification," "presentation change," "operating activities," "investing activities," etc.) before concluding no reclassification was disclosed? | Cash-flow comparability — mandatory search-term sweep |
| 34 | Does Section 18 reconcile with Section 17? If Section 17 implies a weak base-case IRR, has Section 18 avoided calling the stock "clearly undervalued" or explained the divergence? | Section 18 — Reconciliation with Section 17 |
| 35 | If bull-case IV is more than 2× base-case IV, has the memo flagged probability-weighted IV as bull-case sensitive, lowered confidence, and judged margin of safety against base-case (not probability-weighted) value? | Section 18 — Bull-case sensitivity guardrail |
| 36 | Is Section 18 output free of scratchwork phrases ("wait, let me recalculate", "correcting the bear case", etc.)? | Section 18 — Output cleanliness |
| 37 | Does the Section 25 Intrinsic Value Summary include the bull-case-sensitive flag and margin of safety vs. **both** base case and bear case? | Section 18 — Final Verdict integration |
| 38 | Are all per-share intrinsic-value figures in Section 18 **present values** (year-N value discounted to today at a stated discount rate), with the discount rate and horizon shown explicitly? Is the valuation label based on present value, not undiscounted year-N value? | Section 18 — Present-value discipline |
| 39 | Does the Section 18 Scenario table show year-N value and PV of year-N value as **separate columns**, with present intrinsic value per share computed from the PV? | Section 18 — Scenario table format |
| 40 | If buyback details are reported, did they come from the repurchase activity table in the filing — not from dividing financing-activities cash flow by share count? | Buyback source-of-truth rule |
| 41 | If a take rate is reported, was the volume metric (GMV/GTV/TPV) sourced from the exact filing value for the period, and is TTM take rate calculated as TTM revenue ÷ TTM GMV? | Take-rate source-of-truth rule |
| 42 | For any archetype-specific KPI (penetration, take rate, attach rate, NRR, churn, etc.), is the formula stated, are numerator and denominator shown, and are levels never confused with changes? Are GPV/GMV/TPV/payment volume kept distinct from each other and from their growth rates? | KPI definition discipline |
| 43 | Is one EV convention (Strict or Adjusted) declared in the Company Snapshot and applied consistently across every section that references EV? Are the same long-term investments classified the same way throughout? | EV convention consistency rule |
| 44 | For every displayed TTM figure (revenue, FCF, OCF, SBC, losses, etc.), does the formula `latest FY + current interim − prior comparable interim` produce the displayed value? If not, the output fails QC. | TTM consistency hard rule (also enforced by checklist row 31) |
| 45 | If the company is an income-stock archetype (REIT, utility, pipeline/MLP, dividend aristocrat, BDC), does Section 18 calculate intrinsic value as PV of dividends + PV of terminal value (both shown explicitly in a table), and does Section 17 include current yield as an explicit component of expected return? | Section 18 — Income-stock intrinsic value rules |
| 46 | For REITs specifically, is AFFO/share used as the key cash-flow metric (not EPS, FCF, or FFO alone), with payout ratio and dividend sustainability shown? | Section 18 — REIT-specific rules |
| 47 | If a 10-K was reviewed, are CAMs listed by their exact title from the auditor report — not guessed based on the company's business model (e.g., "likely impairment-related" is not acceptable)? | Auditor identity + CAM completeness rules |
| 48 | Does the final memo show only one clean scorecard — no failed weighting attempts, "weights sum to 97% — adjusting" text, multiple drafts, or recalculation notes? | Hard-Fail HF-4 — Scorecard cleanliness |
| 49 | Is every monetary figure labeled with its currency (USD, CAD, EUR, etc.), and does every per-share calculation, multiple, dividend yield, and intrinsic-value comparison use a single declared currency throughout? For dual-listed stocks, are figures shown in both reporting and trading currencies with the exchange rate stated? | Currency discipline |
| 50 | For income-stock archetypes, does the verdict use the income-stock language table (Attractive / Fairly valued / Slightly overvalued — Starter only / Overvalued / Hold-Starter)? Has "Strong Buy" been avoided unless margin of safety vs. base-case IV is 15%+ AND distribution coverage is healthy (payout < ~85%)? | Section 18 — Income-stock verdict language |
| 51 | Are all intrinsic-value reports presented as bear/base/bull ranges (not a single fake-precise number), with the classification label anchored to the base case? | Section 18 — Fair-value ranges, not single numbers |
| 52 | If the memo reports both adjusted EBITDA and Debt/EBITDA, does implied debt (adj. EBITDA × Debt/EBITDA) reconcile with reported balance-sheet debt within 10–15%? If not, is the difference explained explicitly (adjusted vs. balance-sheet, net vs. gross, preferred, project-level debt, leases, FX, NCI)? | Debt-leverage reconciliation rule |
| 53 | For income-stock archetypes, does Section 17 use the yield-plus-growth-plus-multiple decomposition as the **primary** expected-return framework? If a terminal-value-only reverse DCF is shown, is it explicitly labeled "capital-appreciation-only — secondary cross-check"? | Section 18 — Income-stock expected-return framework |
| 54 | For pipeline/utility/infrastructure/income-stock archetypes, is **Full-Strict EV** used by default (including preferred equity and non-controlling interest in additions)? If Simplified EV was used, is preferred equity and NCI confirmed immaterial? | EV convention — income-stock default |
| 55 | For commodity-pass-through archetypes (pipelines, midstream, utilities, energy marketers), is valuation primarily anchored to adjusted EBITDA, DCF, DCF/share, distribution coverage, and Debt/EBITDA — not Price/Sales, EV/Revenue, or revenue growth? | Section 7 — Commodity pass-through rule |
| 56 | Are all multiples labeled correctly? P-prefix multiples (P/E, P/FCF, P/DCF, P/AFFO, P/B) use market cap; EV-prefix multiples (EV/EBITDA, EV/EBIT, EV/Sales) use enterprise value. No mislabeling such as "EV/DCF" for a market-cap ÷ DCF calculation. | Multiple-labeling rule |
| 57 | Is the base-case exit multiple near the current trading multiple or mid-cycle historical multiple? If the base-case exit multiple is materially higher than current, is the re-rating explicitly justified by a documented catalyst — and not silently embedded into the base case? | Section 18 — Exit-multiple discipline |

If a single item fails, the memo is not Decision-Grade. Fix the failure and re-verify before delivery. If structural fixes are impossible with available data, downgrade the memo to **Framework Draft — Not Trade-Ready** rather than ship inaccurate Decision-Grade output.

### Hard-Fail QC Triggers (auto-regenerate)

A handful of failure modes are severe enough that the memo must be **regenerated** before delivery — they cannot be patched in-place or shipped with caveats. When any of the following are present in a draft, the memo fails QC and must be regenerated cleanly:

| # | Trigger | Mandatory Action |
|---|---------|------------------|
| HF-1 | Memo states "no cash-flow reclassification was found" when the latest 10-Q or 10-K actually discloses one (past, current, or scheduled for a future period) | Regenerate with the reclassification disclosed in Section 8 and/or Section 6, with effective date, treated as a comparability issue (never as economic improvement), and with the normalization warning per Section 8 rules |
| HF-2 | Auditor or CAM listed as "Needs Review" when the 10-K has been cited or reviewed | Regenerate with the auditor's actual name and the exact CAM titles from the auditor report — no inference, no substitution, no extras |
| HF-3 | Buyback average repurchase price derived by dividing financing-activities cash flow by share count, rather than taken from the repurchase activity table in the filing | Regenerate using the repurchase activity table figures (shares, dollars, average price, total authorization, remaining authorization). The cash-flow-statement figure may be mentioned only as cash paid / settlement timing — never as the source of average price |
| HF-4 | Section 19/20 scorecard contains weight scratchwork, failed sum attempts ("weights sum to 97% — adjusting"), or multiple scorecard versions | Regenerate with a single clean scorecard summing to exactly 100% |
| HF-5 | Score label numerically maps to a different verdict than the stated verdict (e.g., score 75 displayed but verdict is WATCH / WAIT) without an explicit override explanation per Section 20 rules | Regenerate so the score band aligns with the verdict, OR explicitly state the override and reason inline |
| HF-6 | Market/technical data (52-week high/low, beta, RSI, moving averages, post-earnings move) presented as numbers without a source and date, or estimated/guessed | Regenerate with sourced data + dates, OR mark each unsourced field "Needs Review" and omit from interpretation. Never present guessed market data as fact |
| HF-7 | Memo opens with internal process text ("I now have all the data...", "let me compile the memo...", "before I dive in...", calculation scratchpad) | Regenerate so the memo begins directly with the disclaimer and Section 2 (Company Snapshot) |
| HF-8 | Per-share intrinsic-value figures in Section 18 presented as undiscounted year-N values rather than present values | Regenerate with explicit discounting (year-N value ÷ (1 + discount rate)^N), discount rate and horizon stated, valuation label based on present value |
| HF-9 | Displayed TTM value conflicts with the formula shown beside it (e.g., TTM revenue formula gives $12,366M but the memo says $13,330M) | Regenerate with arithmetic recomputed; show the three component values and the resulting TTM value on the same line so the math is verifiable |
| HF-10 | Two different metrics conflated (e.g., growth rate reported as penetration %, GPV reported as GMV, gross substituted for net, level reported as change), or a ratio reported without its numerator and denominator | Regenerate with each metric clearly labeled, formula stated, numerator and denominator shown |
| HF-11 | EV convention drifts between sections — e.g., one section deducts long-term investments as "liquid," another classifies them as "strategic / illiquid" | Regenerate with one EV convention declared in the Company Snapshot (Strict or Adjusted) and applied consistently everywhere |
| HF-12 | Income-stock archetype (REIT, utility, pipeline/MLP, dividend aristocrat, BDC, or other income-oriented business) and Section 18 calculates intrinsic value from terminal value only — without an explicit PV-of-dividends or PV-of-distributions component | Regenerate Section 18 with the dividend-inclusive formula: present intrinsic value / share = PV of expected dividends over horizon + PV of terminal equity value. Show both components in the required table. For REITs, use AFFO/share; for MLPs, DCF/share; for BDCs, NII/share. Section 17 expected-return decomposition must also include current yield as an explicit component |
| HF-13 | Auditor report from a reviewed 10-K is available but the memo lists a guessed or generic CAM ("likely related to fair value of investments…", "probably impairment of long-lived assets…") instead of the exact CAM title from the auditor report | Regenerate using the exact CAM title(s) from the auditor report. If the 10-K is cited but the CAM cannot be extracted, mark Needs Review — do not guess. For income stocks, CAMs often involve impairment, lease intangibles, fair value, or long-lived assets, but the memo must use the actual auditor wording, not these examples |
| HF-14 | Dividend yield, intrinsic value, or any per-share calculation mixes currencies (e.g., CAD dividend ÷ USD price, or per-share IV in one currency compared to a price in another) | Regenerate with a single declared currency throughout. Convert at a stated exchange rate with date. For dual-listed stocks, show per-share figures in both the reporting and trading currencies, with the exchange rate explicit |
| HF-15 | Income-stock archetype (REIT, utility, pipeline/MLP, dividend aristocrat, BDC) with verdict "Strong Buy" or "Compelling" assigned to a stock that is fairly valued or only slightly below base-case IV, OR with dividend coverage weakening (payout > ~95% of AFFO/DCF/NII) | Regenerate using the Income-stock verdict language table. An excellent income business at fair value is "Hold / Starter / Wait for better entry" — never "Strong Buy." A Strong Buy on an income stock requires both 15%+ margin of safety vs. base-case present IV AND well-covered distribution |
| HF-16 | Income-stock archetype and Section 17 uses a terminal-value-only reverse DCF as the main expected-return framework without an explicit dividend/distribution component | Regenerate Section 17 with the dividend-inclusive decomposition as the primary framework: `Expected return ≈ current yield + per-share growth + multiple change`. If a reverse DCF without dividends is also shown, label it "capital-appreciation-only — secondary cross-check" and do not draw the main conclusion from it |
| HF-17 | Memo reports both adjusted EBITDA and a Debt/EBITDA ratio, but the implied debt (adjusted EBITDA × Debt/EBITDA) differs from reported balance-sheet debt by more than 10–15% with no explanation | Regenerate with the reconciliation shown explicitly. Identify the source of the difference (adjusted vs. balance-sheet debt, net vs. gross, preferred equity, project-level debt, leases, FX, NCI). If the difference cannot be explained from the filing, mark EV, debt, and leverage as Needs Review rather than report figures that do not reconcile |
| HF-18 | Commodity-pass-through archetype (pipeline, midstream, utility, energy marketer, commodity trader) and the memo uses Price/Sales, EV/Revenue, or revenue growth as a primary valuation anchor | Regenerate using adjusted EBITDA, DCF, DCF per share, distribution coverage, and Debt/EBITDA as the primary anchors. Reported revenue may be shown for context only, with explicit note that gross revenue includes commodity pass-throughs |
| HF-19 | A multiple is mislabeled — e.g., market cap ÷ DCF presented as "EV/DCF," or EV ÷ a per-share equity-level metric labeled as a P-style multiple | Regenerate with correct labels. P-prefix multiples use market cap and pair with equity-level cash-flow metrics; EV-prefix multiples use enterprise value and pair with enterprise-level cash-flow metrics (typically EBITDA). State numerator and denominator explicitly the first time each multiple appears |
| HF-20 | Base-case exit multiple is materially higher than the current trading multiple or the mid-cycle historical range without explicit justification, silently embedding a re-rating into the "base" outcome | Regenerate with base-case exit multiple at or near current / mid-cycle, bear case below current, bull case as the multiple-expansion scenario. Any base-case multiple above current must be explicitly justified by a documented catalyst or structural change |

If a hard-fail trigger is detected, **do not deliver the draft** — silently regenerate the final memo from scratch and deliver only the clean version. Do not narrate the regeneration to the user.

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
Asset Manager/Broker · BDC · Pipeline/MLP · Dividend Aristocrat/Mature Compounder · Conglomerate/Mixed

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
| BDC (Business Development Company) | Investment portfolio, NAV per share, NII, distribution coverage       |
| Pipeline / MLP                     | Distributable cash flow per unit, distribution yield, fee-based revenue |
| Dividend Aristocrat / Mature Compounder | Long dividend track record, modest growth, high payout ratio    |
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
| **Dividend/distribution-inclusive intrinsic value, dividend yield as component of expected return, payout ratio, distribution coverage** | **REIT / Utility / Pipeline-MLP / Dividend Aristocrat / BDC / any income-oriented archetype** |
| **Allowed ROE, rate base, regulated-utility peer multiples** | **Utility** |
| **NAV per share, P/NAV, NII, distribution coverage, non-accruals** | **BDC** |
| **Distributable cash flow (DCF) per unit, distribution yield, fee-based revenue %** | **Pipeline / MLP** |
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
- Trading / Timing, Catalysts, and Position Sizing (Sections 16, 22, 23) **may not exceed 5% combined**. They inform timing and sizing — not the buy / watch / avoid decision itself.
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

**Weight arithmetic check (mandatory before Section 20 scorecard):** After assigning all weights, sum them. If they do not equal exactly 100%, adjust before producing the scorecard. State the sum explicitly in the memo so the reader can verify.

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

**Commodity pass-through and gross-vs-net revenue rule** (applies to pipelines, midstream, utilities, energy marketing, commodity trading, and any company where reported revenue includes pass-through costs):
- For pipelines, midstream, utilities, and similar businesses, **reported gross revenue may include commodity pass-throughs** (the cost of gas, oil, power, or other commodities passed through to customers at little or no margin). These pass-throughs can be 50%+ of reported revenue but contribute almost nothing to economics.
- Revenue figures may still be shown for context, but **valuation must rely primarily on**:
  - Adjusted EBITDA (or adjusted EBITDAX for upstream)
  - Distributable cash flow (DCF) — for pipelines/MLPs/utilities, this is the per-unit/per-share cash available for distributions
  - DCF per share / DCF per unit
  - Distribution coverage ratio (DCF ÷ distributions paid)
  - Debt / EBITDA
  - Fee-based revenue % (the portion of revenue under long-term contracts, not commodity-exposed)
- **Do not use Price/Sales, EV/Revenue, or revenue-growth metrics as primary valuation anchors** for commodity-pass-through businesses. They mislead because they treat $1 of commodity cost passed through identically to $1 of margin earned.
- Show **net revenue or margin-bearing revenue** alongside gross revenue if the disclosure permits, and use the net figure when discussing margins or growth quality.

**Red flags:**
- Revenue growing but gross/operating margins shrinking
- Profits driven by tax benefits, one-off gains, or below-the-line items
- EPS rising only because of buybacks, not earnings growth
- One segment masking deterioration in another
- For commodity-pass-through businesses: reported revenue growth driven entirely by commodity-price moves while fee-based revenue is flat or declining

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
- **No-estimation rule (hard):** Do not estimate, approximate, or guess 52-week range, beta, RSI, moving averages, short interest, post-earnings move, or any other market/technical data point. Each value must come from a sourced market-data provider with the as-of date shown. If exact data is unavailable, **omit the row** rather than guess — or mark it Needs Review and exclude it from the interpretation paragraph below. Presenting a guessed market-data value as fact is a Hard-Fail QC trigger (HF-6).
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

## Section 18 — Intrinsic Value / Fair Value Estimate

*Estimate what the business is worth **today** based on fundamentals — not analyst targets, not recent stock movement, not undiscounted future projections.*

This section produces a **scenario-based, assumption-driven** estimate of fair value, not a fake-precise single number. It complements Section 17 (Valuation vs. Expected Return) — Section 17 asks "what return does the current price imply?", this section asks "what is the business worth today?"

### Present-value discipline (hard rule — overrides everything else in this section)

**All intrinsic values in this section must be expressed as present values discounted to today.** The current price is a present value; comparing it to an undiscounted year-N projection is a category error and produces false labels.

- For a multi-year scenario (e.g., 5-year), the present intrinsic value of equity is:
  `Present intrinsic value = Year-N equity value ÷ (1 + discount rate)^N`
- The discount rate must be stated explicitly. Use the company's estimated cost of equity (or WACC if working from EV) — typically 8–12% for established businesses, higher for riskier profiles. Show the rate.
- **Never** compare the current price to an undiscounted year-N value and call the comparison a fairness or undervaluation judgment. This is the most common analytical error in this section.
- **Naming rule:** If the section is titled "Intrinsic Value / Fair Value Estimate," every reported value must be a present value. If for any reason you want to report undiscounted year-N projections, rename that block **"Scenario Target Value / Future Value Estimate"** and state explicitly that the figures are future target values, not present intrinsic values. The two cannot be mixed under one heading.
- **Valuation label rule:** The final valuation label (Undervalued / Fairly Valued / Overvalued / etc.) must be based on the comparison of current price to **present** intrinsic value per share — never to undiscounted year-N value per share.

### Worked example of the error (for illustration only)

If a base-case scenario projects $138.6B of year-5 equity value at a 10% discount rate:
- Present value of equity = $138.6B ÷ (1.10)^5 ≈ $86.1B
- Present value per share (at e.g. 1.3B diluted shares) ≈ $66/share
- If the current price is ~$105, the stock is **above** base-case present intrinsic value — not "fairly valued."

The same scenario, if reported undiscounted as "$105.80/share base-case fair value," would falsely suggest the current price is on top of intrinsic value. That is the trap this rule eliminates.

**The section must answer all of:**
- What is the bear-case intrinsic value?
- What is the base-case intrinsic value?
- What is the bull-case intrinsic value?
- What is the probability-weighted intrinsic value?
- Is the current stock price below, near, or above that range?
- What margin of safety exists, if any?
- How confident is the estimate?

### Required output — Scenario table

Show the discounting step explicitly. Year-N value and present value must be in separate columns.

| Case | Key Assumptions | Year-N Equity Value | Discount Rate | PV of Year-N Equity Value | Present Intrinsic Value / Share | Current Price | Upside / Downside vs Current | Probability | Notes |
|------|----------------|--------------------:|--------------:|---------------------------:|--------------------------------:|--------------:|------------------------------:|------------:|-------|
| Bear |                |                     |               |                            |                                 |               |                               |             |       |
| Base |                |                     |               |                            |                                 |               |                               |             |       |
| Bull |                |                     |               |                            |                                 |               |                               |             |       |

Where:
- **Year-N Equity Value** = projected equity value at end of horizon (e.g., year 5)
- **PV of Year-N Equity Value** = Year-N value ÷ (1 + discount rate)^N
- **Present Intrinsic Value / Share** = PV of equity ÷ diluted share count
- **Upside / Downside vs Current** is computed against the **present** intrinsic value per share, not the year-N projection

### Required output — Summary table

All per-share values below are **present intrinsic values** (year-N value discounted to today). Do not put undiscounted future values in this table.

| Summary | Value |
|---|---:|
| Current price | $X |
| Discount rate used | X% |
| Horizon (years) | N |
| Bear-case **present** intrinsic value / share | $X |
| Base-case **present** intrinsic value / share | $X |
| Bull-case **present** intrinsic value / share | $X |
| Probability-weighted **present** intrinsic value / share | $X |
| Current discount / premium to probability-weighted present value | X% |
| Current discount / premium to base-case present value | X% |
| Margin of safety vs. base case | None / Thin / Moderate / Strong |
| Margin of safety vs. bear case | None / Thin / Moderate / Strong |
| Confidence level | Low / Medium / High |

### Classification rules

Based on current price vs. **probability-weighted intrinsic value**:

| Discount / Premium | Classification |
|--------------------|---------------|
| Current price > 25% below probability-weighted value | **Potentially undervalued** |
| Current price 10–25% below probability-weighted value | **Slightly undervalued** |
| Current price within ±10% of probability-weighted value | **Fairly valued** |
| Current price 10–25% above probability-weighted value | **Somewhat overvalued** |
| Current price > 25% above probability-weighted value | **Overvalued** |

**Extended classification labels (use in conjunction with the table above, based on current price vs. each scenario):**

| Condition | Classification |
|-----------|---------------|
| Current price below the bear case AND data confidence is High | **Deeply undervalued** |
| Current price more than 20% below the base case | **Undervalued** |
| Current price within ±10% of the base case | **Fairly valued** |
| Current price above the base case but below the bull case | **Bull-case dependent** |
| Current price more than 20% above the base case | **Overvalued unless bull case is highly probable** |
| Probability-weighted IV is materially higher than base-case IV because of an extreme bull case | **Bull-case sensitive** (use this label rather than "Undervalued") |

When the probability-weighted and base-case labels disagree, use the more conservative of the two and explain why.

**Label-softening rule:** When confidence is Low, soften the classification label. Use phrasing like "appears slightly undervalued under conservative assumptions, but confidence is Low" rather than asserting the label as fact.

### Language requirements

**Use phrasing such as:**
- "Appears fairly valued under base-case assumptions."
- "Appears overvalued unless the bull case plays out."
- "Undervalued relative to conservative assumptions."
- "Valuation is too assumption-sensitive for high confidence."

**Never use phrasing such as:**
- "The stock is worth exactly $X."
- "Guaranteed upside."
- "Safe because below intrinsic value."

### Method selection by archetype

Select the valuation methods that match the company's archetype from Section 2A. Do not force inappropriate methods.

| Archetype | Required / Recommended Methods |
|-----------|-------------------------------|
| **Profitable software / platform / asset-light compounder** | DCF on FCF or owner earnings; EV/FCF or P/owner-earnings exit multiple; historical multiple check; peer multiple check; SBC-adjusted owner earnings |
| **High-growth / high-multiple** | Reverse DCF; bear/base/bull scenario valuation; probability-weighted intrinsic value; required FCF or owner-earnings CAGR; sensitivity to exit multiple compression |
| **Bank / lender / consumer finance** | Tangible book value; ROE vs. cost of equity; residual income model; credit-loss normalization; P/TBV and P/E through-cycle. **Do not use generic EV/EBITDA.** |
| **Insurance** | Book value / tangible book value; ROE vs. cost of equity; combined ratio normalization; investment portfolio sensitivity; reserve adequacy |
| **REIT** | AFFO / FFO multiple; NAV estimate; cap rate sensitivity; debt maturity / interest-rate sensitivity; dividend coverage. **Intrinsic value must be dividend-inclusive — see Income-stock IV rules below.** |
| **Cyclical industrial** | Normalized mid-cycle revenue and margins; mid-cycle EPS / FCF; EV/EBITDA through-cycle. **Avoid valuing only peak earnings.** |
| **Commodity / energy** | NAV / reserves; commodity price deck; production volume; FCF sensitivity to commodity prices; capex and depletion. **For pipeline MLPs and other income-distributing energy structures, intrinsic value must be distribution-inclusive — see Income-stock IV rules below.** |
| **Biotech / pharma** | Pipeline probability weighting; patent cliff analysis; cash runway; product concentration; regulatory milestone risk |
| **Dividend / mature compounder / dividend aristocrat** | Dividend discount model (often the primary method, not just secondary); FCF payout ratio; dividend growth durability; P/E and FCF yield vs. history. **Intrinsic value must be dividend-inclusive — see Income-stock IV rules below.** |
| **Utility** | Regulated-asset-base × allowed ROE; dividend discount model; P/E vs. regulated-utility peer median; rate-case outlook; debt maturity / interest-rate sensitivity. **Intrinsic value must be dividend-inclusive — see Income-stock IV rules below.** |
| **BDC (Business Development Company)** | NAV per share; P/NAV multiple; distribution coverage from net investment income; portfolio quality / non-accruals. **Intrinsic value must be distribution-inclusive — see Income-stock IV rules below.** |
| **Conglomerate / holding company** | Sum-of-the-parts; look-through earnings; net cash/debt adjustment; holding-company discount where appropriate |

### Income-stock intrinsic value (REITs, utilities, pipelines/MLPs, dividend aristocrats, BDCs, and other income-oriented archetypes)

For income-oriented stocks, dividends or distributions are a **primary component of total return**, not a footnote. Intrinsic value calculated only from terminal value will systematically understate fair value for these archetypes.

**Mandatory formula:**

```
Present Intrinsic Value / Share =
    PV of expected dividends or distributions over the forecast period
  + PV of terminal equity value at the end of the forecast period
```

Both components must be calculated and shown explicitly. Do **not** compute intrinsic value from terminal value alone and mention dividends only in prose.

**Required output for income stocks:**

| Component | Year 1 | Year 2 | ... | Year N | PV Sum |
|-----------|-------:|-------:|-----|-------:|-------:|
| Forecast dividend / distribution per share | $X | $X | | $X | |
| Discount factor at rate r | 1/(1+r) | 1/(1+r)² | | 1/(1+r)^N | |
| PV of each year's dividend / share | $X | $X | | $X | **$X (PV of dividends)** |
| Terminal equity value / share at year N | — | — | | $X | |
| PV of terminal equity value / share | — | — | | $X | **$X** |
| **Present Intrinsic Value / Share** | | | | | **$X (total)** |

**For REITs specifically:**
- Use **AFFO / share** as the key per-share cash-flow metric (not FCF, not EPS, not FFO — AFFO is the closest analog to distributable cash flow).
- Forecast both dividend per share and AFFO per share over the horizon.
- Show **payout ratio** (dividend / AFFO) for each forecast year.
- Show **dividend sustainability**: payout ratio trend, AFFO growth assumption, leverage trajectory.
- Terminal equity value should typically be derived from an AFFO multiple, NAV, or cap-rate-based estimate.

**For pipelines / MLPs, BDCs, utilities:** apply the same structure with the appropriate cash-flow metric (DCF for MLPs, NII for BDCs, regulated earnings for utilities).

**Expected-return framework for income stocks:**

For REITs, utilities, pipelines/MLPs, dividend aristocrats, BDCs, and other income-oriented archetypes, Section 17 (Valuation vs. Expected Return) **must primarily use** a dividend/distribution-inclusive total-return decomposition:

```
Expected total return ≈ current dividend / distribution yield
                       + expected AFFO / DCF / NII per-share growth
                       + multiple change (expansion or compression)
```

This is the **primary** expected-return framework for income stocks, not a secondary check. State each component explicitly. If yield is a meaningful part of total return (typically >2–3 percentage points of expected total return), it cannot be omitted or absorbed into a generic "growth" figure.

**Prohibition on terminal-value-only reverse DCF as the main framework:**
- A reverse DCF that compounds market cap forward and solves for required exit FCF growth — without explicitly including dividends or distributions paid during the holding period — is a **capital-appreciation-only** framework. It systematically understates expected return for income stocks because it ignores cash returned to shareholders along the way.
- If a reverse DCF without dividends is presented for an income stock, label it explicitly as **"capital-appreciation-only — does not include dividend/distribution component."** Do not use this version as the main valuation conclusion. Use the yield-plus-growth-plus-multiple decomposition above as the main framework, and present the capital-appreciation-only reverse DCF only as a secondary cross-check.

**Rules:**
- If the income-stock archetype applies and the memo's intrinsic value section does not include a PV-of-dividends component alongside PV-of-terminal-value, the output fails QC (Hard-Fail trigger HF-12).
- If the income-stock archetype applies and Section 17 uses a terminal-value-only reverse DCF as the main expected-return framework — without an explicit dividend/distribution component — the output fails QC (Hard-Fail trigger HF-16 below).
- Distinguish between **dividend per share** (the actual cash distribution) and **AFFO / DCF / NII per share** (the underlying cash flow). Payout ratio is the link.
- Do not assume a constant payout ratio without justification. Show the payout assumption explicitly.
- For variable distributions (BDCs, MLPs), forecast a distribution range and note the variability.

**Income-stock verdict language (overrides the generic classification labels for these archetypes):**

For income-stock archetypes, use verdict language that reflects the holding nature of these stocks — they are typically bought for current yield plus modest growth, not for explosive upside. Apply the following bands based on current price vs. **base-case** present intrinsic value per share:

| Condition | Recommended Verdict Language |
|-----------|------------------------------|
| Current price more than 15% below base-case present IV AND dividend/distribution is well covered (payout < ~85% of AFFO/DCF/NII) | **Attractive** |
| Current price within ±10% of base-case present IV | **Fairly valued** |
| Current price 10–20% above base-case present IV | **Slightly overvalued — Starter position only** |
| Current price more than 20% above base-case present IV | **Overvalued — Wait for better entry** |
| Current price above base case but with weakening dividend coverage (payout > 95% of AFFO/DCF/NII) | **Overvalued — dividend at risk** |
| Excellent business trading at fair value with healthy coverage | **Hold / Starter / Wait for better entry** — never "Strong Buy" |

**Income-stock scorecard alignment rule:** For income stocks, a "Strong Buy" verdict requires *both* (a) margin of safety vs. base-case present IV of at least 15% AND (b) well-covered dividend (payout below ~85% of AFFO/DCF/NII). An excellent income business at fair value is a Hold or Starter, not a Strong Buy. The numerical score must reflect this — do not let an 80+ score appear next to a "Fairly valued" income stock without an explicit override explanation.

### Calculation rules

- **Present value is mandatory for all per-share intrinsic-value figures.** Whatever method is used (DCF, exit multiple, NAV, residual income, sum-of-the-parts), the final per-share number reported must be a present value. If the method naturally produces a year-N projection (e.g., exit-multiple valuation), discount it back: `Present value = Year-N value ÷ (1 + discount rate)^N`. State the discount rate and the horizon explicitly.
- **Use fair-value ranges, not fake-precise single numbers.** Always report bear / base / bull values as a range — never a single "intrinsic value = $X" number. The classification label is anchored to the base case, but the range must be visible.
- **For DCF:** show revenue growth, margin, discount rate, terminal growth (or terminal multiple).
- **For exit-multiple valuation:** show current FCF / owner earnings, growth assumptions, exit multiple, and implied value.
- **Exit-multiple discipline (especially for mature income stocks):**
  - The **base-case exit multiple should usually be near the current multiple or the mid-cycle historical multiple**, not a materially higher figure.
  - Do not assume large multiple expansion in the base case unless explicitly justified (e.g., a documented re-rating catalyst, structural improvement in the business, or current multiple sitting well below long-term historical range).
  - Suggested default exit-multiple distribution:
    - **Bear:** below current multiple (multiple compression scenario)
    - **Base:** near current multiple **or** mid-cycle historical multiple, whichever is more representative
    - **Bull:** clear multiple-expansion case with justification
  - **Example of a violation to avoid:** If current P/DCF is ~13x, a base-case exit multiple of 18x is too bullish unless explicitly labeled as the bull case. The base case at 18x would silently embed a 38% re-rating into the "base" outcome.
  - For high-growth stocks, multiple compression is more likely than expansion over a 5–10 year horizon. The default base-case exit multiple should be flat to lower vs. current, not higher.
  - For mature income stocks, multiples tend to be range-bound; the base case should sit inside the historical range, not at a new high.
- **For EV-based valuation:** convert enterprise value to equity value:
  `Equity value = EV − financial debt + cash & equivalents + non-operating assets − minority interest − preferred claims`
- **For equity-value valuation:** divide by diluted shares outstanding (consistent with Section 9 figures).
- Do not double count cash or non-operating investments.
- Do not use analyst price targets as intrinsic value.
- Do not use the bull-case value as fair value.
- Do not call a stock undervalued unless current price is below probability-weighted (or base-case) value by a meaningful margin.
- Do not call a stock cheap solely because it is below its 52-week high.
- If inputs are too uncertain, mark intrinsic value confidence as Low.

### Sensitivity requirement

When valuation is highly assumption-sensitive (which is the default for high-growth, cyclical, or commodity companies), include at least one sensitivity table:

| Variable | Conservative | Base | Aggressive |
|----------|-------------|------|------------|
| Revenue CAGR | X% | X% | X% |
| FCF / owner-earnings margin | X% | X% | X% |
| Exit multiple | Xx | Xx | Xx |
| Discount rate (if DCF) | X% | X% | X% |
| Terminal growth (if DCF) | X% | X% | X% |
| **Implied value / share** | **$X** | **$X** | **$X** |

### Reconciliation with Section 17 (Valuation vs. Expected Return)

The intrinsic-value conclusion in this section must reconcile with Section 17. The two angles cannot tell contradictory stories without explanation.

- If **Section 17 says the base-case IRR is weak** (i.e., the current price implies a return below the target hurdle rate), Section 18 **cannot call the stock clearly undervalued** unless the memo explains explicitly why the assumptions differ — for example, a different exit multiple, different reinvestment assumption, or different time horizon.
- If the two sections appear to diverge, the memo must say so plainly and resolve the tension. A reader should not have to choose between Section 17 and Section 18.
- The final valuation label must reflect all of:
  - Base-case intrinsic value
  - Probability-weighted intrinsic value
  - Downside (bear) case
  - Confidence level
  - Margin of safety vs. base case AND vs. bear case

### Bull-case sensitivity guardrail (right-skewed scenarios)

Probability-weighted intrinsic value can be artificially inflated by a single large bull-case value. Do not let this masquerade as undervaluation.

**Trigger:** If the bull-case intrinsic value is more than 2× the base-case intrinsic value, the probability-weighted IV is **bull-case sensitive** and the following rules apply:

- State explicitly in the memo that probability-weighted IV is bull-case sensitive.
- Emphasize **base-case value** and a **downside-adjusted value** rather than leaning on the probability-weighted figure.
- Lower confidence to **Low** or **Low-Medium**.
- Do **not** call margin of safety "Moderate" unless the current price is below **base-case value** by at least 20%. Margin of safety must be judged against base-case value, not probability-weighted value, when the scenario distribution is right-skewed.
- Do **not** label the stock "Potentially undervalued" solely because probability-weighted IV is high. Use the **"Bull-case sensitive"** label from the Classification rules table.

**For right-skewed growth stocks, always show all three reference points side by side:**
- Median / base-case IV
- Probability-weighted IV
- Downside-adjusted IV (e.g., bear case, or a 25th-percentile estimate)

The final classification label must be conservative — closer to the base-case and downside-adjusted values than to the bull-case-driven probability-weighted figure.

### Output cleanliness — no scratchwork

The Section 18 output must be a clean final memo. Never include:

- "Wait, let me recalculate…"
- "Correcting the bear case…"
- "I made a mistake earlier…"
- "Let me redo this…"
- Any internal scratchpad or reasoning text from the calculation process.

If a calculation is corrected during preparation, regenerate the final tables silently and present only the clean final version. The reader sees finished output, not work-in-progress.

### Quality-control rule

If the intrinsic value section relies on stale data, unverified data, or third-party estimates, mark **Confidence: Low** and **do not use the intrinsic value estimate to justify a Buy rating**. The estimate becomes informational only.

### Integration with later sections

- **Section 21 (Entry Price / Margin of Safety)** should use the intrinsic value range from this section as one input to the entry-zone analysis.
- **Section 20 (Summary Weighted Scorecard):** intrinsic value informs the Valuation / Expected Return rating but **must not be double-counted as a separate weighted dimension**. Section 17 and Section 18 are two angles on the same risk; together they produce one Valuation rating.
- **Section 25 (Final Verdict)** must include the following intrinsic-value fields explicitly:
  - Current price
  - Base-case intrinsic value / share
  - Probability-weighted intrinsic value / share
  - Valuation label (undervalued / fairly valued / overvalued) with confidence
  - Margin of safety (None / Thin / Moderate / Strong)

---

## Section 19 — Quantitative Overlays

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

## Section 20 — Summary Weighted Scorecard

**Weight propagation rule (hard):** The weights used in this scorecard must be the **exact same weights** stated in Section 5 (Dominant-Risk Weighting). The two sections cannot disagree. If Section 5 says Valuation / Expected Return is 35%, Section 20 must show Valuation / Expected Return at 35%. Any divergence is a QC failure and the memo must be regenerated.

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

**Verdict guidance (base mapping — refined score bands aligned with verdicts):**

| Score Band | Verdict Label | Interpretation |
|------------|---------------|----------------|
| 80–100 | **Strong Buy / Compelling** | High conviction; fundamentals, valuation, and risks all support purchase |
| 65–79 | **Good Business — Price/Risk Dependent** | Quality is there but valuation or one risk dimension prevents a clean Buy |
| 45–64 | **Watch / Wait for Better Entry** | Mixed signals or stretched valuation; revisit on price improvement or thesis evolution |
| Below 45 | **Avoid / High Risk** | Multiple red flags, hard stops, or extreme valuation |

**Visual-alignment rule:** The score must visually match the verdict. A "Watch / Wait" verdict must not be paired with a score of 75. A "Strong Buy" verdict must not be paired with a score of 60. If the raw arithmetic produces a band-verdict mismatch, either (a) re-examine the weights — a mismatch usually indicates a weighting error — or (b) explicitly state the override reason inline (e.g., "Score 75 but verdict WATCH because Valuation / Expected Return is 🔴 at 35% weight, per the override rules below"). Never ship a memo with an unexplained score-verdict visual mismatch.

**Score-verdict alignment rule (hard override):**

The numerical score must align with the verdict. The mapping above is the *base case* — but the following overrides take precedence whenever they apply:

1. **🔴 Valuation override** — If Valuation / Expected Return is rated 🔴 and carries 30%+ weight, the verdict cannot be BUY regardless of the numerical score. Default to **WATCH / WAIT FOR BETTER ENTRY** even if the score is ≥ 70. A "Wait for better price" verdict must not be paired with a score that looks like a strong buy. If the score and verdict appear inconsistent, the verdict wins — but the score itself should also be re-examined; a high score with a 🔴 valuation likely means other weights were misapplied.

2. **🔴 Dominant-risk override** — If the dimension identified as the dominant risk in Section 5 (regardless of which one it is) is rated 🔴, the verdict cannot be BUY regardless of the numerical score. Default to **WATCH** or **AVOID** depending on severity.

3. **Hard-Red credit-loss override** — If Credit / Loan-Loss Trajectory is at the ☠️ Thesis Breaker tier (per Section 8 credit-loss severity classification), default the verdict to **AVOID** regardless of the numerical score.

4. **Score-verdict consistency check** — Before finalizing the memo, verify that the numerical score and the stated verdict tell the same story. If the score says "BUY territory" (≥ 70) but the verdict says "WATCH / WAIT," explain explicitly in the memo why the override applies. Do not deliver a memo where the score and verdict appear to contradict each other without explanation.

---

## Section 21 — Entry Price / Margin of Safety

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

## Section 22 — Catalysts to Watch

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
- Catalysts are monitoring tools. They do not replace the kill criteria in Section 24.
- **Treat accounting classification changes as comparability issues, not true economic catalysts.** A reclassification between operating, investing, and financing cash flows, or between revenue line items, changes how numbers are reported — not the underlying economics. Note them in this section only as comparability warnings, and flag them in Section 13 (Earnings Quality) where they belong. Do not present them as bullish or bearish drivers of value.

---

## Section 23 — Position Sizing / Portfolio Risk Framing

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
- Do not recommend averaging down unless the thesis remains intact and the valuation has actually improved per Section 21 and Section 17.
- Severe red flags or any hard stop in Section 3 → default to Avoid regardless of upside.
- Use risk-framing language ("the risk profile suggests…", "this sizing reflects…") rather than prescriptive absolutes ("never concentrate", "always small"). Position sizing is a function of the user's portfolio, risk tolerance, and time horizon — none of which the skill knows. Frame the implication; do not dictate the decision.

**Suggested language:** *"Position sizing should follow risk, not excitement. A great company at a stretched valuation may deserve a smaller position than a good company at a great price."*

---

## Section 24 — Thesis Breakers / Kill Criteria

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

## Section 25 — Final Verdict

The verdict must be driven **primarily by fundamentals, valuation, balance sheet, cash flow, and red flags**. Technical setup, analyst sentiment, and catalysts may inform timing — they do not establish intrinsic value.

Use this exact structure:

**Business Quality:** [Excellent / Good / Mixed / Poor] — [1–2 sentence rationale]

**Financial Health:** [Strong / Adequate / Stretched / Distressed] — [1–2 sentence rationale]

**Valuation / Expected Return:** [Attractive / Fair / Stretched / Extreme] — [1–2 sentence rationale including implied return from Section 17]

**Intrinsic Value Summary** (from Section 18 — all per-share figures are **present** intrinsic values discounted to today):
- Current price: $X
- Discount rate / horizon used: X% / N years
- Base-case **present** intrinsic value / share: $X
- Probability-weighted **present** intrinsic value / share: $X
- Bull-case-sensitive flag: Yes / No (Yes if bull case > 2× base case, per Section 18 guardrail)
- Confidence level: [Low / Medium / High]
- Valuation label: [Deeply undervalued / Undervalued / Slightly undervalued / Fairly valued / Bull-case dependent / Bull-case sensitive / Somewhat overvalued / Overvalued unless bull case is highly probable / Overvalued]
- Margin of safety vs. **base-case present value**: [None / Thin / Moderate / Strong]
- Margin of safety vs. **bear-case present value**: [None / Thin / Moderate / Strong]

The verdict must be driven by base-case **present** value and margin of safety, **not only** probability-weighted present value, and never by undiscounted year-N figures.

**Main Red Flags:** [The most important red flags from Sections 3, 13, and other relevant sections — or "None material"]

**Technical / Timing Context:** [1–2 sentences from Section 16 — *timing only, not valuation*]

**Main Catalysts:** [2–3 specific upcoming events from Section 22 that could move the thesis or sentiment]

**Position-Sizing Implication:** [The bucket from Section 23: Avoid / Watchlist / Tiny / Small / Medium / Core]

**Biggest Risk:** [Single most important risk in plain language]

**What Must Go Right:** [The 2–3 specific things that must happen for the investment to work]

**What Would Change My Mind:** [The 2–3 specific developments that would flip the verdict]

**Verdict:** BUY / BUY ONLY IF PRICE IS ATTRACTIVE / WATCH / WAIT FOR BETTER ENTRY / HOLD / AVOID / TOO RISKY

**Confidence Level:** High / Medium / Low — [reason for uncertainty if Medium or Low]

**Next Things to Monitor:** [3–5 specific metrics or events to watch next quarter, drawing from Section 22]

---

**Important:**
- Do not let many green operational checks overpower one large red valuation or balance-sheet risk.
- If the company is excellent but valuation requires near-perfect execution, the verdict should usually be **WATCH**, not **BUY**.
- Technical context, catalysts, and position-sizing framing must collectively influence the verdict by no more than **5%**. They refine **timing and sizing**, not the **buy/watch/avoid decision** itself.
- If confidence is Low due to data gaps, say so explicitly rather than masking uncertainty with false precision.

---

## Section 26 — Sources

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
- **EV convention consistency rule:** Pick **one** EV convention at the start of the memo and label it explicitly. Use the same convention everywhere EV appears (Company Snapshot, Data Integrity Check, Section 9 Balance Sheet, Section 17 Valuation, Section 18 Intrinsic Value, Section 20 Scorecard, Section 21 Entry Price). The acceptable conventions are:
  - **Full-Strict EV** — `Market cap + Financial debt + Preferred equity + Non-controlling interest − Cash and equivalents`. Most rigorous. Best for capital-structure-complex companies (pipelines, utilities, infrastructure, conglomerates).
  - **Strict EV (liquid-assets variant)** — Full-Strict EV but also deducts current marketable securities. Long-term investments stay in the EV figure.
  - **Adjusted EV** — Strict + deducts liquid long-term marketable securities as well. Use only when long-term investments are genuinely liquid and non-strategic.
  - **Simplified EV** — `Market cap + Net debt` (where Net debt = financial debt − cash). A common shorthand but it omits preferred equity and non-controlling interest. Acceptable only when both are immaterial; otherwise use Full-Strict.
- **For pipeline / utility / infrastructure / income-stock archetypes:** the default is **Full-Strict EV**. These archetypes typically have material preferred equity, hybrid securities, and non-controlling interests that the Simplified convention would miss. Switching to Simplified for these archetypes requires an explicit reason.
- **Do not switch EV convention mid-report** unless explicitly showing both side by side and labeling them.
- Do not use third-party long-term debt figures (Macrotrends, data aggregators) if the primary filing debt tables are available.
- Do not classify the same long-term investment as "liquid and non-strategic" in one section and "strategic / illiquid" in another. The classification must be consistent across the entire memo.
- Do not deduct strategic equity stakes, joint-venture investments, or other operating non-cash assets from EV unless conducting a separate sum-of-the-parts analysis (which must be labeled as such). The default EV deduction is liquid investment assets only.
- State the chosen convention in the Company Snapshot and in the Data Integrity Check Notes column for the Enterprise Value row.
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

