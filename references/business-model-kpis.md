# Business-Model KPI Library

Reference file for Section 6 of the stock-evaluator skill.
Load the relevant archetype(s) only. Skip metrics that don't apply.

---

## SaaS / Software

**Key metrics to check:**
- ARR (Annual Recurring Revenue) / RPO (Remaining Performance Obligations) / deferred revenue trend
- Net Revenue Retention (NRR) — target > 120% is strong; < 100% means shrinking customer base
- Gross Revenue Retention / logo churn rate
- CAC payback period (months to recover customer acquisition cost) — < 18 months is healthy for SMB; < 24–36 for enterprise
- Gross margin trend (SaaS gross margins typically 70–85%+; below 60% warrants scrutiny)
- Rule of 40 = Revenue Growth % + FCF Margin % (≥ 40 is healthy)
- Cloud hosting / infrastructure cost trend as % of revenue
- SBC burden (see Section 8 for thresholds)
- Customer concentration (any customer ≥ 10% of ARR?)
- Platform dependency (built on AWS/Azure/GCP — dependency risk?)
- AI disruption risk to core product
- Cybersecurity / outage history and risk

**Red flags:**
- NRR falling toward or below 100%
- Deferred revenue or RPO growing slower than revenue (pipeline thinning)
- CAC payback worsening while sales & marketing spend rises
- Gross margins compressing toward 60% or below

---

## Marketplace / Platform

**Key metrics to check:**
- GMV / GTV / TPV (Gross Merchandise / Transaction / Payment Volume) growth
- **Take rate = Revenue ÷ GMV/GTV/TPV** — always calculate explicitly; compare current period vs. prior period; do not say take rate is rising or falling unless the calculation supports it
- Buyer and seller / supply and demand growth
- Transaction frequency per active user
- Trust and safety issues (fraud, disputes, policy violations)
- Platform outage history and frequency
- Seller or supplier concentration
- Competition from vertically integrated platforms (e.g., Amazon building its own marketplace)
- Regulatory and platform dependency risk
- Network-effect durability — how hard is it to displace the network?

**Red flags:**
- Take rate falling while volume grows (pricing pressure or competition)
- Buyer or seller side growing much faster than the other (imbalance)
- Rising fraud or dispute rates
- Major competitor entering the market with vertical integration

---

## Payments / Fintech / Lending

**Key metrics to check:**
- Payment volume growth (TPV, GPV)
- **Take rate = Net revenue ÷ TPV/GPV/GTV** — calculate explicitly; compare current vs. prior period; do not state direction without the calculation
- Transaction loss rate = transaction/credit losses ÷ revenue
- Transaction loss rate = transaction/credit losses ÷ FCF
- Loss growth rate vs. revenue growth rate
- Fraud loss rate
- Credit loss rate (if lending is involved)
- Delinquency rates by cohort
- Net charge-off rate
- Allowance for credit losses / coverage ratio
- Loan book growth and vintage quality
- Funding cost and funding structure (deposits, warehouse lines, securitization)
- Regulatory capital ratios where applicable
- Counterparty and payment processor concentration risk

**Early-warning thresholds:**
- Credit/transaction losses growing faster than revenue → 🟡 Watch
- Allowance coverage declining as loan book grows → 🟡 Watch

**Hard-red thresholds:**
- Credit/transaction losses growing > 2× faster than revenue for 2+ consecutive quarters → 🔴 Flag
- Delinquencies rising materially across multiple cohorts simultaneously → 🔴 Flag
- Allowance coverage falling while charge-offs are rising → 🔴 Flag

**Red flags:**
- Funding costs rising sharply (margin squeeze)
- Regulatory scrutiny escalating
- Loan book growing much faster than revenue (credit is being extended to grow top line)

---

## Bank / Insurance / Financial Institution

**Bank-specific:**
- Net interest margin (NIM) and trend
- Deposit growth and deposit cost
- Loan growth by category
- Non-performing loans (NPL) ratio
- Net charge-off rate
- Loan-loss provision adequacy
- CET1 / Tier 1 capital ratio (regulatory minimums)
- Liquidity coverage ratio (LCR)
- Held-to-maturity securities unrealized losses
- Deposit concentration by depositor type and size
- Commercial real estate exposure (% of loan book)
- Loan-to-deposit ratio

**Insurance-specific:**
- Combined ratio = Loss Ratio + Expense Ratio (< 100% = underwriting profit)
- Loss ratio trend
- Expense ratio trend
- Catastrophe loss exposure
- Reserve adequacy (prior-year development)
- Investment portfolio risk and duration
- Reinsurance dependency and counterparty quality

**Red flags (banking):**
- NIM compressing sharply
- Deposit outflows or rising deposit costs
- NPL or charge-off rates rising
- Capital ratios approaching regulatory minimums
- Large CRE concentration with deteriorating fundamentals

---

## Retail / Consumer Discretionary

**Key metrics to check:**
- Comparable / same-store sales growth (SSS)
- Traffic vs. average ticket decomposition
- Gross margin trend
- Inventory growth vs. sales growth (rising DSI = demand concern)
- Markdown pressure and promotional intensity
- Store count productivity (revenue per sq ft, revenue per store)
- Lease liabilities and occupancy cost as % of revenue
- Brand strength and loyalty metrics
- Consumer discretionary / macro sensitivity
- E-commerce penetration and channel mix

**Red flags:**
- SSS turning negative or decelerating sharply
- Inventory growing > 1.5× faster than revenue
- Gross margin compression from markdowns
- Occupancy costs rising as % of revenue (fixed cost leverage working in reverse)

---

## Consumer Staples

**Key metrics to check:**
- Organic sales growth (volume vs. price/mix decomposition)
- Pricing power in inflationary environment
- Input cost / commodity exposure and hedging
- Market share by category
- Private-label competitive pressure
- Distribution strength and shelf-space dynamics
- Dividend history and payout sustainability
- FCF conversion reliability

**Red flags:**
- Volume declining while price/mix grows (demand destruction from pricing)
- Market share losses to private label
- Input cost inflation outpacing pricing ability

---

## Industrial / Cyclical

**Key metrics to check:**
- Order backlog (absolute and trend)
- Book-to-bill ratio (> 1.0 = demand exceeding output)
- Capacity utilization
- Operating leverage (EBIT sensitivity to revenue changes)
- Input cost exposure (steel, copper, energy, etc.)
- End-market concentration
- Capex cycle position (early, mid, or late)
- Working-capital swings through the cycle
- Return on assets through the cycle

**Red flags:**
- Book-to-bill falling below 1.0 for multiple quarters
- Backlog declining in absolute terms
- Operating leverage amplifying losses during downturn
- Heavy fixed cost base with falling utilization

---

## Semiconductor / Hardware

**Key metrics to check:**
- Revenue cyclicality — where are we in the semi cycle?
- Inventory days (rising = demand concern; typical healthy range is 60–90 days)
- Customer concentration
- Foundry / wafer supply dependency (fabless vs. IDM)
- Gross margin trend across cycles
- Capex intensity (IDMs especially)
- Product cycle risk and next-gen roadmap
- Export control and geopolitical risk
- AI / data center demand tailwinds (if relevant)

**Red flags:**
- Customer inventory overhang appearing
- Lead times collapsing (demand pulling back)
- Gross margin compressing mid-cycle (pricing pressure)
- Export controls cutting off major revenue geography

---

## Energy / Commodities

**Key metrics to check:**
- Revenue and earnings sensitivity to commodity price (break-even analysis)
- Production volume and trend
- Reserve life (years of production at current rate)
- Lifting / operating cost per unit (BOE, tonne, etc.)
- Hedging program and % of production hedged
- Capex discipline (spending within cash flow?)
- Net debt / EBITDA through the cycle
- Environmental and regulatory risk
- Energy transition exposure

**Red flags:**
- Break-even price above current spot price
- Reserve life declining without replacement
- Leveraged balance sheet with commodity price volatility
- Capex spending exceeding FCF (especially late cycle)

---

## REIT

**Key metrics to check:**
- FFO (Funds from Operations) and AFFO (Adjusted FFO) per share
- AFFO payout ratio (dividend sustainable?)
- Dividend per share, dividend growth rate, dividend yield
- Same-property NOI growth
- Occupancy rate and trend
- Weighted average lease term (WALT)
- Tenant concentration and credit quality
- Debt maturity schedule and refinancing risk
- LTV (loan-to-value) ratio
- Interest-rate sensitivity (fixed vs. floating rate debt)
- Development pipeline and cost overrun risk

**Intrinsic value requirement:** REIT intrinsic value must be dividend-inclusive (PV of dividends + PV of terminal value). See Section 18 — Income-stock IV rules. Use AFFO/share as the key per-share cash-flow metric.

**Red flags:**
- Occupancy declining in core portfolio
- AFFO payout ratio > 95% (little cushion)
- Dividend cut signaled by declining AFFO coverage
- Short WALT with rising vacancy in a weak market
- Refinancing cliff with rising rates
- Tenant concentration in distressed sectors

---

## Utility

**Key metrics to check:**
- Regulated asset base / rate base growth
- Allowed ROE (regulator-approved return on equity)
- Realized ROE vs. allowed ROE
- Earned ROE trend
- Dividend per share, dividend growth, dividend yield
- Payout ratio
- Regulatory environment (constructive vs. challenging jurisdiction)
- Rate case outcomes and pending cases
- Capex plan and rate-base growth trajectory
- Debt / total capital ratio
- Interest coverage
- Credit rating
- Customer growth in service territory
- Fuel mix and decarbonization trajectory

**Intrinsic value requirement:** Utility intrinsic value must be dividend-inclusive (PV of dividends + PV of terminal value). See Section 18 — Income-stock IV rules.

**Red flags:**
- Realized ROE persistently below allowed ROE (operational issues)
- Hostile regulatory environment
- Heavy capex without rate-base recovery clarity
- Payout ratio > 80–85% with limited growth
- Stranded-asset risk from regulatory or technology change

---

## BDC (Business Development Company)

**Key metrics to check:**
- NAV per share
- P/NAV multiple (premium / discount)
- Net investment income (NII) per share
- Distribution per share, distribution yield
- Distribution coverage from NII (target ≥ 100%)
- Portfolio yield (weighted-average yield on investments)
- Cost of debt
- Net interest spread (portfolio yield − cost of debt)
- Non-accrual rate (% of portfolio not paying interest)
- Portfolio diversification by issuer and sector
- Senior secured % of portfolio
- Leverage (debt-to-equity)
- Regulatory leverage cap compliance

**Intrinsic value requirement:** BDC intrinsic value must be distribution-inclusive (PV of distributions + PV of terminal value, typically derived from NAV). See Section 18 — Income-stock IV rules. NAV per share is the most important anchor; P/NAV trend matters more than P/E.

**Red flags:**
- Distribution coverage from NII below 100% for multiple quarters (distribution being funded by capital, not income)
- Non-accruals rising materially
- NAV declining quarter over quarter
- Heavy reliance on unrealized gains rather than recurring income
- Leverage approaching regulatory cap
- Persistent P/NAV discount may indicate market doubts about NAV accuracy

---

## Healthcare / Biotech / Pharma

**Biotech (pre-revenue or early stage):**
- Cash runway (months at current burn rate — < 12 months is distress territory)
- Pipeline stage and diversity (Phase I/II/III)
- Probability-weighted NPV of pipeline
- Near-term clinical trial readouts (binary risk events)
- FDA / regulatory milestones
- Dilutive financing risk (how likely is next equity raise?)

**Large-cap pharma:**
- Revenue dependence on top 3 drugs (%)
- Patent cliff exposure ($ revenue at risk, timeline)
- R&D productivity (pipeline coverage of revenue at risk)
- Litigation / patent challenge risk
- Biosimilar entry risk
- Government reimbursement / pricing risk
- Acquisition pipeline to fill gaps

**Red flags (biotech):**
- Cash runway < 18 months without a clear funding path
- Phase III failure in lead asset
- Heavily concentrated in one compound
- Dilutive financing history with no clear path to profitability

---

## Telecom / Media

**Key metrics to check:**
- Subscriber growth / churn
- ARPU (Average Revenue Per User) trend
- Capex intensity (network investment)
- Debt load relative to EBITDA (telecom is typically high-leverage)
- Content costs and margin (media)
- Cord-cutting exposure (traditional media)
- Streaming / digital transition progress
- Regulatory and spectrum risk

**Red flags:**
- Subscriber churn accelerating
- ARPU declining while capex stays high
- Leverage rising without FCF coverage improvement

---

## Asset Manager / Broker / Exchange

**Key metrics to check:**
- AUM (Assets Under Management) trend
- Net flows (inflows vs. outflows)
- Fee rate / management fee trend (compression risk from passive)
- Performance fees (volatile and lumpy)
- Trading volumes (brokers/exchanges)
- Market sensitivity of revenue
- Cost efficiency (compensation as % of revenue)
- Regulatory and fiduciary risk

**Red flags:**
- Net outflows for multiple consecutive quarters
- Fee compression accelerating
- Performance well below benchmark (active managers)
- Compensation ratio rising as revenue falls

