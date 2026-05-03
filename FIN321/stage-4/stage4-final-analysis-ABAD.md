# Stage 4 – Final Analysis & Strategic Recommendation
## FX Hedging Model | EUR Receivable | Executive Memorandum

**Prepared by:** Kiani Abad  
**Date:** May 2, 2026  
**Course:** FIN 321  
**Scenario:** U.S. Solar Equipment Importer – EUR 4,500,000 Receivable (1-Year Horizon)

---

## A. Exposure Summary

The firm expects to receive **€4,500,000** in **360 days** as payment for solar equipment exported to a European buyer. Because the receivable is denominated in euros but the firm reports in USD, the company bears direct translation risk: any depreciation of the EUR/USD exchange rate between today and settlement will reduce the dollar value of its inflow.

**Market conditions at inception:**

| Variable | Value |
|---|---|
| Foreign-currency receivable (FC_AMT) | €4,500,000 |
| Spot rate (S0_in) | ~1.0900 USD/EUR (implied by market context) |
| Forward rate — 1-year (F0_in) | 1.0875 USD/EUR |
| USD interest rate (R_USD) | 5.00% (annual, simple) |
| EUR interest rate (R_FC) | 3.00% (annual, simple) |
| Put strike (K_PUT) | 1.0900 USD/EUR (ATM) |
| Put premium (PREM_PUT) | $0.015 per EUR |
| Call strike (K_CALL) | 1.0900 USD/EUR (ATM) |
| Call premium (PREM_CALL) | $0.018 per EUR |
| Days to settlement (T_DAYS) | 360 days (T = 1.0 year) |

**Quantifying the risk:** A 5% adverse move in EUR/USD — from 1.09 to approximately 1.035 — would reduce USD proceeds by roughly **$247,500**, directly compressing cash flows, budget accuracy, and margin recognition. For a solar equipment importer with dollar-denominated operating costs, this exposure is material and must be managed proactively.

---

## B. Summary of Hedge Outcomes

The table below presents USD proceeds under each strategy at the base case (S_T = spot) and illustrates the core trade-offs.

### Base-Case Results (S_T ≈ 1.0900)

| Strategy | Gross USD Proceeds | Premium Cost | Net USD Proceeds | vs. Forward |
|---|---|---|---|---|
| **Forward Hedge** | $4,893,750 | $0 | **$4,893,750** | — |
| **Money Market Hedge** | ~$4,893,750 | $0 | **~$4,893,750** | ≈ $0 (parity) |
| **Put Hedge (ATM K=1.09)** | $4,905,000 | ($67,500) | **$4,837,500** | ($56,250) |
| **Call Hedge (ATM K=1.09)** | $4,905,000 | ($81,000) | **$4,824,000** | ($69,750) |
| **No Hedge** | $4,905,000 | $0 | **$4,905,000** | +$11,250 (at spot) |

> *Note: Forward proceeds = FC_AMT × F0_in = 4,500,000 × 1.0875 = $4,893,750. Money Market Hedge proceeds validated via borrow-convert-invest mechanics and covered interest parity.*

### Strategy Narratives

**Forward Hedge:** Locks in $4,893,750 unconditionally. No upside participation; no downside risk. The appropriate benchmark for all other strategies. Simple to execute, operationally clean, and auditable.

**Money Market Hedge:** Replicates the forward synthetically — borrow EUR today (discounted at R_FC), convert to USD at spot, invest at R_USD for one year. The result approximates forward proceeds within rounding, validating covered interest parity. This strategy requires access to credit facilities and ties up liquidity, making it less practical than a direct forward contract for most corporate treasurers.

**Put Hedge:** Pays a $67,500 upfront premium (1.38% of forward proceeds) to establish a USD floor. If EUR falls below 1.09, the put is exercised and the firm receives no less than $4,837,500 net. If EUR rises above 1.09, the put expires worthless and the firm benefits from appreciation — net of the sunk premium cost. The break-even rate is approximately **1.075 USD/EUR** (strike minus premium per EUR).

**Call Hedge:** Less relevant for a EUR receivable. A call on EUR caps upside — the firm sells EUR at the strike even if the market moves higher — while still paying a premium. This strategy is included for analytical completeness and symmetry but would not be recommended for this exposure type.

**No Hedge:** Maximizes upside if EUR appreciates; maximizes downside if EUR depreciates. Appropriate only if management has a high conviction EUR bullish view and can tolerate cash-flow variance in its budget model.

---

## C. Sensitivity Interpretation

The sensitivity table below models USD net proceeds across S_T from 1.0355 (−5%) to 1.1445 (+5%):

| S_T (USD/EUR) | Forward ($) | Money Mkt ($) | Put Hedge ($) | Call Hedge ($) | No Hedge ($) |
|---|---|---|---|---|---|
| 1.0355 (−5%) | 4,893,750 | ~4,893,750 | 4,837,500 | 4,579,500 | 4,659,750 |
| 1.0528 (−3%) | 4,893,750 | ~4,893,750 | 4,837,500 | 4,656,600 | 4,737,600 |
| 1.0718 (−1%) | 4,893,750 | ~4,893,750 | 4,837,500 | 4,742,100 | 4,823,100 |
| **1.0900 (base)** | **4,893,750** | **~4,893,750** | **4,837,500** | **4,824,000** | **4,905,000** |
| 1.1082 (+2%) | 4,893,750 | ~4,893,750 | 4,918,500 | 4,824,000 | 4,986,900 |
| 1.1273 (+4%) | 4,893,750 | ~4,893,750 | 5,002,350 | 4,824,000 | 5,072,850 |
| 1.1445 (+5%) | 4,893,750 | ~4,893,750 | 5,077,500 | 4,824,000 | 5,150,250 |

**EUR Depreciation Scenarios (S_T < 1.09):** The forward and money market hedges hold steady at $4,893,750 regardless of how far EUR falls — this is the value of certainty. The put hedge provides a floor of ~$4,837,500 net, slightly below the forward due to the premium, but protects against catastrophic EUR decline. The unhedged position suffers in full; a move to 1.0355 costs the firm ~$234,000 vs. the forward.

**EUR Appreciation Scenarios (S_T > 1.09):** The put hedge participates fully in EUR upside above the strike (net of the sunk premium), eventually outperforming the forward when S_T exceeds approximately **1.105**. The forward forgoes all appreciation. The call caps proceeds and underperforms. The unhedged position captures the most upside but with no floor.

**Key insight:** The forward and money market hedges offer identical cash flow certainty at different liquidity cost structures. The put hedge costs 1.38% of proceeds to buy optionality worth capturing only if EUR appreciates meaningfully. In a stable-to-mildly-bullish EUR environment, the put offers the best risk-adjusted outcome.

---

## D. Strategic Recommendation

**Recommended Strategy: Forward Hedge (Primary) with a Put Hedge as an Alternative**

For a U.S. solar equipment importer with dollar-denominated input costs, payroll, and operating budgets, **cash flow certainty is the paramount objective.** The Forward Hedge at 1.0875 locks in **$4,893,750** of USD inflows with zero residual FX uncertainty, zero premium cost, and minimal operational complexity.

If the CFO and treasury committee have a moderate EUR-bullish view or if the business strategy benefits from upside participation — for example, if the firm is tendering competitively priced contracts priced in USD — the **Put Hedge** at K = 1.09 is the preferred alternative. It guarantees a USD floor of $4,837,500 (only $56,250 below the forward) while preserving full upside if EUR strengthens beyond 1.105.

The Money Market Hedge validates covered interest parity but is inferior to the forward on operational simplicity and liquidity grounds. The Call Hedge is not recommended — it caps USD proceeds for a EUR seller, combining premium cost with upside forfeiture.

---

## E. Executive Justification

**Cash Flow Stability:** The forward hedge eliminates variance entirely. Treasury can commit the $4,893,750 inflow to budget models, working capital projections, and debt service schedules with full confidence. This is especially valuable for a company managing dollar-denominated supplier payments against a euro-denominated revenue stream.

**Budget Certainty:** Modern FP&A workflows depend on point estimates, not distributions. A $234,000 swing in proceeds (the unhedged ±5% range) would require material variance explanations to the board and potentially reforecast the annual operating plan. The forward hedge eliminates this management overhead.

**Liquidity Impact:** The forward requires no upfront cash. The put costs $67,500 in premium today — manageable for a firm receiving $4.9M but a real cash outflow that must be budgeted. The money market hedge requires credit facility access and ties up USD liquidity for 12 months, which may conflict with operating capital needs.

**Optionality Value:** The put's $67,500 premium buys a genuine financial option: the firm retains full participation in EUR appreciation while being insulated from depreciation below 1.09. This is rational when EUR outlook is uncertain but skewed modestly bullish — a realistic assumption given current macroeconomic conditions in 2026.

**Premium Costs:** At 1.38% of forward proceeds, the put premium is within the range of typical hedging costs and is deductible as a cost of the hedging program. The call at $81,000 (1.65% of proceeds) provides no asymmetric benefit for a seller of EUR and should be declined.

**Accounting Implications (Optional):** Under ASC 815, a designated cash flow hedge (forward or option) would allow effective hedge results to flow through OCI rather than P&L, reducing earnings volatility. This designation requires contemporaneous documentation — a spec like Stage 3 serves as the analytical foundation for that documentation.

---

## F. Structured AI Prompt (Appendix)

---

```
# GOAL
Generate a complete, production-grade Excel workbook (.xlsx) modeling FX hedging 
strategies for a EUR-denominated receivable. The model must be fully formula-driven, 
use named ranges for all inputs, apply the specified color-coding convention, and 
include a sensitivity table, payoff chart, and executive summary sheet.

---

# INPUT VARIABLES
Use the following values exactly as provided. Do not infer or substitute any value.

Named Range      | Description                      | Unit     | Value
-----------------|----------------------------------|----------|----------
FC_AMT           | Foreign-currency receivable      | EUR      | 4,500,000
T_DAYS           | Days to settlement               | Days     | 360
S0_in            | Spot rate at inception           | USD/EUR  | 1.0900
F0_in            | Forward rate (1-year)            | USD/EUR  | 1.0875
R_USD            | USD interest rate (simple, ann.) | %        | 5.00%
R_FC             | EUR interest rate (simple, ann.) | %        | 3.00%
K_PUT            | Put option strike                | USD/EUR  | 1.0900
K_CALL           | Call option strike               | USD/EUR  | 1.0900
PREM_PUT         | Put premium per EUR              | USD      | 0.0150
PREM_CALL        | Call premium per EUR             | USD      | 0.0180
T                | Time to maturity (derived)       | Years    | =T_DAYS/360

---

# WORKBOOK STRUCTURE
Create a workbook with the following four sheets in this order:
  1. 1_Inputs      — All named ranges and assumptions
  2. 2_Model       — All hedge calculations and sensitivity table
  3. 3_Summary     — Strategy comparison table and executive recommendation
  4. README        — Legend for named ranges, color codes, and formula audit notes

---

# COLOR CODING CONVENTION
Apply the following formatting to all cells:
  - YELLOW background  → Input cells (user-editable values on 1_Inputs only)
  - BLUE background    → Assumption cells (documented but not primary inputs)
  - GREEN background   → Formula output cells (calculated, not hardcoded)
  - GRAY background    → Final output / summary cells on 3_Summary

All input values must be defined ONLY on 1_Inputs. All other sheets must reference 
inputs via cross-sheet named ranges. Never hardcode scenario values outside 1_Inputs.

---

# MODEL LOGIC

## Sheet: 1_Inputs
- Create a header block: "FX HEDGING MODEL – INPUTS"
- Subtitle: "EUR Receivable | 1-Year Horizon | Yellow = Input | Blue = Assumption"
- Three labeled sections: EXPOSURE, MARKET RATES, OPTION PARAMETERS
- Each row: Named Range | Description | Unit | Value | Source
- Assign Excel named ranges matching the Named Range column exactly
- Derived cell T = T_DAYS / 360 (formula, green background)
- Key Assumptions block (blue background):
    • Day-count: ACT/360; rates are simple annual (not compounded)
    • No transaction costs, bid-ask spreads, or credit risk
    • Forward rate reflects covered interest parity
    • Options are European-style; premiums paid upfront in USD
    • All exchange rates: USD per EUR; 100% of exposure hedged

## Sheet: 2_Model

### A. Forward Hedge
- USD_forward = FC_AMT × F0_in
- Label: "Locked-in USD proceeds regardless of S_T"

### B. Money Market Hedge (3-Step)
Step 1: EUR_borrow = FC_AMT / (1 + R_FC × T)
         Label: "PV of EUR receivable — amount to borrow today in EUR"
Step 2: USD_today = EUR_borrow × S0_in
         Label: "Convert borrowed EUR to USD at spot"
Step 3: USD_mm = USD_today × (1 + R_USD × T)
         Label: "Invest USD proceeds at USD rate for T years"
Parity Check: Parity_diff = USD_mm − USD_forward
         Apply conditional formatting: RED fill if ABS(Parity_diff) > $2,000

### C. Option Costs & Break-Evens
- Total_put_premium  = FC_AMT × PREM_PUT
- Total_call_premium = FC_AMT × PREM_CALL
- Put break-even S_T  = K_PUT  − PREM_PUT
- Call break-even S_T = K_CALL + PREM_CALL

### D. Sensitivity Table
- S_T range: 0.95 × S0_in to 1.05 × S0_in, step = 0.01 USD/EUR → 11 rows
- Columns: S_T | Forward ($) | Money Mkt ($) | Put Hedge ($) | Call Hedge ($) | No Hedge ($) | Δ Put vs. Fwd | Best Strategy
- Formulas:
    Forward   = USD_forward  (constant for all rows)
    Money Mkt = USD_mm       (constant for all rows)
    Put Hedge = FC_AMT × MAX(S_T, K_PUT) − Total_put_premium
    Call Hedge= FC_AMT × MIN(S_T, K_CALL) − Total_call_premium
    No Hedge  = FC_AMT × S_T
    Δ Put vs. Fwd = Put Hedge − Forward
    Best Strategy = INDEX of highest value among Forward, MM, Put, Call, No Hedge
- Apply IFERROR() wrappers on all formula cells
- Bold and shade the header row (dark blue fill, white text)

### E. Payoff Chart
- Insert a line chart of the sensitivity table
- X-axis: S_T values
- Series: Forward, Money Market, Put Hedge, Call Hedge, No Hedge (5 lines)
- Title: "USD Proceeds by Hedging Strategy vs. EUR/USD at Maturity"
- Legend: bottom; gridlines: horizontal only; no chart border

---

## Sheet: 3_Summary

### Strategy Comparison Table (at base case S_T = S0_in)
Columns: Strategy | Gross Proceeds ($) | Premium Cost ($) | Net Proceeds ($) | vs. Forward ($)
Rows: Forward Hedge | Money Market Hedge | Put Hedge | Call Hedge
Format: currency $#,##0; differences with +/− sign

### Key Decision Metrics Block
- USD floor (Put, net of premium): =FC_AMT × K_PUT − Total_put_premium
- Put break-even S_T
- Call break-even S_T
- Parity diff (Money Mkt − Forward)
- Put premium as % of forward proceeds: =Total_put_premium / USD_forward

### Executive Recommendation Block (gray background)
Write a 2-paragraph qualitative recommendation:
Paragraph 1: Recommend the Forward Hedge for cash-flow certainty; explain why.
Paragraph 2: Offer the Put Hedge as an alternative for upside participation; state cost.

---

# VERIFICATION
1. Parity check: ABS(USD_mm − USD_forward) < $2,000 → flag in green; else flag in red
2. Put payoff at S_T = K_PUT: should equal FC_AMT × K_PUT − Total_put_premium
3. At S_T far below K_PUT: Put Hedge should be flat (floor behavior confirmed)
4. At S_T far above K_PUT: Put Hedge should rise linearly with slope = FC_AMT
5. Call payoff at S_T = K_CALL: should equal FC_AMT × K_CALL − Total_call_premium
6. Document all checks in a "Verification" row below the sensitivity table

---

# FORMATTING REQUIREMENTS
- Font: Arial 10pt throughout
- Column widths: Named Range = 18, Description = 35, Unit = 10, Value = 15, Source = 20
- Currency cells: $#,##0 format
- Percentage cells: 0.00% format
- Rate cells (S_T, S0, F0, K): 4 decimal places
- Freeze top row on all sheets
- Print area set to fit one page wide on 2_Model and 3_Summary

---

# EXPORT
- Save as: FX_Hedging_Model_[LastName]_Stage4.xlsx
- Ensure all formulas are recalculated before saving
- No external links — all data self-contained within the workbook
- No circular references
- No formula errors (#REF!, #DIV/0!, #VALUE!, #NAME?)
```

---

## Extra Credit: Areas for Further Study

### 1. AI Skills & Automation

The most significant near-term enhancement to this model would be integrating a live market data feed with AI-driven regeneration. An AI tool equipped with web search — such as Claude with search enabled — could query Bloomberg, Reuters, or a broker API to pull the current EUR/USD spot rate, 1-year forward points, and ATM option premiums at model run time. This would replace static inputs with live data, transforming the model from a point-in-time snapshot into a continuous monitoring tool. Further, a Monte Carlo simulation layer (10,000 simulated S_T paths drawn from an implied volatility surface) would replace the ±5% sensitivity table with a full probability distribution of hedge outcomes — enabling the CFO to see not just "what if EUR moves 5%" but "what is the 95th percentile worst-case USD shortfall." Claude's Code Interpreter or a Python-connected agent could rebuild and email this report daily with no human input required.

### 2. Multi-File Reasoning

The three-stage deliverable structure of this project — specification (Stage 3), model (Stage 2/4), and prompt (Stage 4, Section F) — mirrors the documentation triad used in production treasury environments: a functional spec, a working model, and a regeneration recipe. An AI with multi-file context could read all three simultaneously, detect inconsistencies (e.g., a named range in the spec that differs from the Excel model), enforce naming conventions across updates, and automatically rebuild the spreadsheet when inputs change. For example, if the CFO updates the receivable amount from €4.5M to €6.0M in the spec document, the AI could propagate that change through the model and regenerate the sensitivity table and summary memo without analyst intervention. This is the treasury analyst automation workflow of the next decade — and this project is a direct prototype of it.

### 3. GitHub & Version Control

Committing each stage to a GitHub repository creates an immutable, timestamped audit trail of every modeling decision. A reviewer — whether an internal audit team, external auditor, or regulatory examiner — can reconstruct exactly what assumptions were in place on any given date, why they changed, and who approved them. For hedge accounting under ASC 815, this audit trail is not merely useful — it is a documentation requirement. The hedge designation, effectiveness methodology, and quantitative testing must be contemporaneously documented at inception. A GitHub repository containing the Stage 3 spec, Stage 2 model, and Stage 4 prompt — committed on the hedge designation date — satisfies that requirement in a reproducible, version-controlled format that any Big 4 auditor can examine. This is a practical, immediately deployable governance improvement over the typical "emailed Excel with initials in the filename" approach still common in mid-market treasury operations.

---

*Document prepared for FIN 321 — Stage 4 Final Analysis. All model outputs derived from the Stage 2 Excel workbook (FX_Hedging_Model_ABAD.xlsx) and the Stage 3 Technical Specification.*
