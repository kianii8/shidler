# FX Hedging Model – Technical Specification

**Created by:** Kiani Abad  
**Updated by:** Kiani Abad  
**Date Created:** April 24, 2026  
**Date Updated:** April 24, 2026  
**Version:** 1.0  
**LLM Used:** Claude (Anthropic)

**Role:** Financial Analyst / Treasury Analyst  
**Audience:** CFO / Director of Treasury

**Purpose:** Provide a structured, quantitative specification for evaluating and comparing FX hedging strategies for a EUR-denominated receivable, and to document improvements over the Stage 2 prototype for implementation in a refined model.

---

## 1. Problem Statement

The firm expects to receive **€1,200,000 (EUR)** in **180 days**, creating direct exposure to fluctuations in the EUR/USD exchange rate. As a EUR receivable, the firm bears the risk that the euro will depreciate against the USD between the trade date and settlement, reducing the USD value of its cash inflow.

An adverse move — for example, EUR/USD declining from 1.10 to 1.04 — would reduce gross USD proceeds by approximately **$72,000**, directly impacting revenue recognition, margin, and cash flow forecasting. Treasury must evaluate available hedging instruments and select a strategy that balances certainty of outcome, cost, and preservation of upside.

This specification covers three strategies:
- **Forward hedge** — eliminates all exchange rate risk; establishes a fixed USD outcome
- **Money market hedge** — synthetic forward via borrow-convert-invest; validates covered interest parity
- **Option hedges** — EUR put (downside floor) and EUR call (reference/symmetry)

---

## 2. Inputs (Known Variables)

| Named Range | Description | Unit | Value | Source |
|-------------|-------------|------|-------|--------|
| FC_AMT | Foreign-currency receivable | EUR | 1,200,000 | Company data |
| S0_in | Spot rate at inception | USD/EUR | 1.1000 | Market data |
| F0_in | Forward rate (180-day) | USD/EUR | 1.0950 | Market data |
| R_USD | USD interest rate | Annual % | 5.00% | Market data |
| R_FC | EUR interest rate | Annual % | 3.00% | Market data |
| K_PUT | Put option strike | USD/EUR | 1.1000 | Analyst choice |
| K_CALL | Call option strike | USD/EUR | 1.1000 | Analyst choice |
| PREM_PUT | Put premium per EUR | USD | 0.0200 | Market estimate |
| PREM_CALL | Call premium per EUR | USD | 0.0250 | Market estimate |
| T_DAYS | Days to settlement | Days | 180 | Contract terms |

**Derived:**  
`T = T_DAYS / 360 = 0.5000 years`

---

## 3. Assumptions & Constraints

- **Day-count convention:** ACT/360 applied to all interest rate calculations
- **Rate type:** All interest rates are quoted as simple annual rates (not compounded)
- **Transaction costs:** Excluded — no bid-ask spreads, brokerage fees, or financing charges
- **Covered interest parity:** Forward rate is assumed to satisfy CIP; money market hedge result should closely approximate forward proceeds
- **Option style:** European — exercise at maturity only; no early exercise
- **Premium payment:** Option premiums are paid upfront in USD at inception
- **Quote convention:** All exchange rates expressed as USD per EUR (direct quote, USD perspective)
- **Credit/counterparty risk:** Excluded from all calculations
- **Margin requirements:** Not modeled
- **Accounting treatment:** Hedge accounting (ASC 815 / IFRS 9) is out of scope

These simplifications enable a clean analytical comparison. A production model would relax each in turn.

---

## 4. Calculation Flow

### A. Forward Hedge

1. Obtain forward rate `F0_in`
2. Compute locked-in USD proceeds:  
   `USD_forward = FC_AMT × F0_in`
3. Result is fixed and independent of future spot rate `S_T`

### B. Money Market Hedge

1. Discount the EUR receivable to a present value (amount to borrow today):  
   `EUR_borrow = FC_AMT / (1 + R_FC × T)`
2. Convert borrowed EUR to USD at today's spot rate:  
   `USD_today = EUR_borrow × S0_in`
3. Invest USD proceeds at the USD interest rate for the hedge period:  
   `USD_mm = USD_today × (1 + R_USD × T)`
4. At maturity, the EUR receivable repays the EUR loan exactly
5. **Parity check:** `USD_mm` should approximate `USD_forward`; document the difference

### C. Put Option Hedge (Primary Protection Strategy)

1. Calculate total upfront premium cost:  
   `Total_put_premium = FC_AMT × PREM_PUT`
2. At maturity, evaluate payoff condition:  
   - If `S_T < K_PUT`: exercise the put → sell EUR at `K_PUT`  
   - If `S_T ≥ K_PUT`: let put expire → sell EUR at market rate `S_T`  
3. Compute gross proceeds and subtract premium:  
   `USD_put(S_T) = FC_AMT × MAX(S_T, K_PUT) − Total_put_premium`

### D. Call Option Hedge (Reference / Symmetry)

1. Calculate total upfront premium cost:  
   `Total_call_premium = FC_AMT × PREM_CALL`
2. At maturity, evaluate payoff condition:  
   - If `S_T > K_CALL`: exercise the call → sell EUR at `K_CALL`  
   - If `S_T ≤ K_CALL`: let call expire → sell EUR at market rate `S_T`  
3. Compute net proceeds:  
   `USD_call(S_T) = FC_AMT × MIN(S_T, K_CALL) − Total_call_premium`  
   *(Note: for a receivable, the call caps upside and is less practically relevant)*

### E. Scenario Analysis

1. Define `S_T` range: `0.95 × S0_in` to `1.05 × S0_in`, step `0.01`
2. For each `S_T`, compute USD proceeds under all four strategies
3. Compile into a sensitivity table; chart all strategies on a single line graph

---

## 5. Outputs

| Output | Description | Format | Purpose |
|--------|-------------|--------|---------|
| USD_forward | USD proceeds under forward hedge | Scalar | Certainty benchmark |
| USD_mm | USD proceeds under money market hedge | Scalar | Parity validation vs. forward |
| Parity_diff | USD_mm − USD_forward | Scalar | Model audit check |
| USD_put | USD proceeds under put hedge by S_T | 11-row table | Downside protection analysis |
| USD_call | USD proceeds under call hedge by S_T | 11-row table | Upside/cost comparison |
| Sensitivity_Table | All four strategies vs. S_T | Table | Full scenario comparison |
| Chart_1 | Payoff profiles for all strategies | Line chart | Visual decision tool |
| Summary_Output | Qualitative recommendation | 1–2 paragraphs | Executive decision support |

---

## 6. Model Review — What Worked & What to Improve

### What Worked Correctly
- Core hedge logic is correctly implemented for all four strategy types
- Forward and money market hedge results are consistent (covered interest parity holds within rounding)
- The sensitivity table clearly illustrates how payoff profiles diverge as `S_T` moves away from spot
- Option payoff structure correctly captures asymmetry: floor protection (put) vs. cap (call)

### Improvements Required for the Refined Version

| Issue | Current State | Improved Design |
|-------|---------------|-----------------|
| Hardcoded values | Values embedded directly in formulas | All inputs as named ranges on a dedicated Inputs sheet |
| Sheet structure | Calculations mixed with inputs | Separate Inputs / Calculations / Outputs / Sensitivity sheets |
| Parity validation | Not explicitly flagged | Add `Parity_diff` cell with conditional formatting if gap exceeds $500 |
| Sensitivity range | Limited to ±5% | Retain ±5% base; document that range can be extended by changing step parameters |
| Auditability | No formula documentation | Add in-cell comments and a legend explaining color conventions |
| Error handling | None | Add `IFERROR()` wrappers on key formulas |

### Enhancements for Stage 4 Build
- Modular sheet structure with clear tab naming
- Break-even `S_T` computation for each option strategy: `S_T_breakeven = K − PREM` (put) or `K + PREM` (call)
- Summary comparison table ranking strategies by USD proceeds at base case
- Strategy selection toggle (dropdown) to highlight preferred hedge on chart

---

## 7. Sensitivity Plan

**Variable tested:** EUR/USD spot rate at maturity (`S_T`)

| Parameter | Value |
|-----------|-------|
| Lower bound | `0.95 × S0_in` = 1.0450 |
| Upper bound | `1.05 × S0_in` = 1.1550 |
| Step size | 0.0100 USD/EUR |
| Number of scenarios | 11 |

For each `S_T`, the model computes USD proceeds under all strategies. Key observations:
- **Forward / Money Market:** Flat horizontal lines — no sensitivity to `S_T`
- **Put hedge:** Flat at floor `(FC_AMT × K_PUT − Total_put_premium)` for `S_T < K_PUT`; rises with `S_T` above strike
- **Call hedge:** Rises with `S_T` below strike; flat at cap for `S_T > K_CALL`

The chart communicates the **cost of certainty** (forward vs. market) and the **value of optionality** (put participation above the strike). The ±5% range reflects a realistic short-horizon shock; wider ranges should be modeled for stress-testing.

---

## 8. Limitations & Next Steps

### Limitations
- No implied volatility or Black-Scholes pricing — option premiums are analyst-estimated inputs
- Transaction costs, bid-ask spreads, and brokerage fees are excluded
- No counterparty or credit risk modeling
- Static hedge only — no dynamic rebalancing or delta-hedging
- No hedge accounting treatment (ASC 815 / IFRS 9 designation and effectiveness testing)
- Assumes full hedge of 100% of exposure; partial hedges not modeled

### Next Steps
This specification feeds directly into the **Stage 4 AI prompt**. Specifically:
- Standardized named ranges (`FC_AMT`, `S0_in`, etc.) prevent the AI from improvising variable definitions
- The step-by-step calculation flow in Section 4 translates directly into formula construction instructions
- Explicit output definitions in Section 5 drive chart and table generation requirements
- Model review notes in Section 6 instruct the AI to build the **improved version**, not merely replicate the prototype

> *This document serves as the machine-readable blueprint that transforms a working prototype into an auditable, production-grade financial model — demonstrating the analyst-to-automation workflow used by modern treasury teams.*
