# FX Risk Management Memo – EUR Receivable Hedge

**Created by:** Kianii  
**Updated by:** Kianii  
**Date Created:** 2026-04-03  
**Date Updated:** 2026-04-03  
**Version:** 1.0  
**LLM Used:** ChatGPT (GPT-5.3)

---

## Executive Summary (≤150 words)
Our firm expects to receive €4,500,000 in one year, creating exposure to EUR/USD exchange rate fluctuations. If the euro weakens against the U.S. dollar, the USD value of this receivable will decline, reducing realized revenue. To manage this risk, we evaluate three hedge strategies: a forward contract, options (put on EUR), and a money market hedge. Each approach balances cost, flexibility, and certainty differently. A forward hedge locks in a guaranteed rate, eliminating uncertainty but removing upside potential. Options provide downside protection while preserving upside, at the cost of a premium. The money market hedge replicates a forward using borrowing and lending. Our next steps include building an Excel model to quantify outcomes under different exchange rate scenarios and recommending the optimal strategy based on risk tolerance and financial impact.

---

## Background & Objectives
The firm has a €4,500,000 receivable due in one year. The current EUR/USD spot rate is assumed to be approximately 1.08, with a quoted 1-year forward rate of 1.0875. This creates transaction exposure, as future USD proceeds depend on exchange rate movements.

**Risk:**  
If the euro depreciates (e.g., EUR/USD falls to 1.00), the firm receives fewer USD than expected. This directly impacts revenue and profitability.

**Objectives:**  
- Protect the USD value of the receivable  
- Reduce earnings volatility  
- Evaluate cost vs. flexibility of hedging strategies  

---

## Methods

### 1. Forward Hedge
- Lock in rate: 1.0875  
- USD proceeds = €4,500,000 × 1.0875  

**Pros:** Certainty, no upfront cost  
**Cons:** No upside if EUR appreciates  

---

### 2. Options Hedge (Put on EUR)
- Strike (K): 1.08 (at-the-money)  
- Premium: $0.015 per EUR  

**Pros:** Downside protection + upside participation  
**Cons:** Upfront premium cost  

---

### 3. Money Market Hedge
- Borrow EUR today, convert to USD at spot, invest USD  

**Assumptions:**  
- USD interest rate: 5.00%  
- EUR interest rate: 3.00%  

**Pros:** Locks in effective rate similar to forward  
**Cons:** More complex, uses balance sheet capacity  

---

## Limitations & Next Steps

**Limitations:**
- Assumes static interest rates and no transaction costs  
- Spot and rates approximated; will refine with real market data  
- Does not incorporate credit risk or liquidity constraints  

**Next Steps:**
- **Stage 2:** Build Excel model comparing unhedged, forward, option, and money market outcomes  
- **Stage 3:** Document model logic and design improved, AI-reproducible version  
- **Stage 4:** Analyze results, select optimal hedge, and prepare CFO recommendation  

---

## References
- Bloomberg Terminal (EUR/USD spot and forward rates)  
- Yahoo Finance (FX data)  
- Corporate Finance textbooks (FX hedging strategies)  
- Covered Interest Parity framework  