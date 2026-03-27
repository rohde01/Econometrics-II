# Measuring Geopolitical Risk: A Structural VAR Analysis

**Caldara & Iacoviello (2022, AER), Section III**

**Instructor:** Rasmus Søndergaard Pedersen  
**Course:** Econometrics II, Spring 2026

---

## Context

Caldara & Iacoviello (2022) construct a **Geopolitical Risk (GPR) index** by counting newspaper articles related to geopolitical tensions, threats, and events.

**Section III** asks: what are the **macroeconomic effects of an unexpected increase in geopolitical risk**?

### Approach

- Estimate a **p = 8 variable structural VAR (SVAR)** at monthly frequency
- **Time period:** 1986:M3–2019:M12
- **Identify a single structural shock** — the GPR shock — via a Cholesky decomposition of the reduced-form covariance matrix
- **VAR estimated with k = 2 lags**
- **Impulse responses reported over a 12-month horizon**

---

## Variables

The system Z_t consists of eight monthly variables, ordered as they appear in the Cholesky decomposition:

| # | Variable | Description | Transformation |
|---|----------|-------------|-----------------|
| 1 | GPR | Geopolitical Risk index | Log |
| 2 | VIX | Implied equity volatility (VIX) | Level |
| 3 | INV | US business investment p.c. | Log |
| 4 | HRS | US hours worked p.c. | Log |
| 5 | SP500 | US S&P 500 | Log |
| 6 | OIL | WTI crude oil price | Log |
| 7 | FCM2 | 2-year Treasury yield | Level |
| 8 | NFCI | National Financial Conditions | Level |

**Source:** vardatagpr from haver.csv in the replication files.

---

## The Structural VAR

### Reduced Form (k = 2 lags)

$$Z_t = \Pi_1 Z_{t-1} + \Pi_2 Z_{t-2} + \mu + \varepsilon_t$$

where $\varepsilon_t \stackrel{d}{=} N(0, \Omega)$ and $E[\varepsilon_t \varepsilon_t'] = \Omega$

### Cholesky Identification

$$\Omega = L_C \cdot L_C', \quad L_C \text{ lower triangular}$$

$$u_t = L_C^{-1} \varepsilon_t \stackrel{d}{=} N(0, I_8)$$

### Structural Form — The Triangular Equation System

$$\text{GPR}_t = \beta_1' \text{lags}_t + u_t^{\text{GPR}}$$
← **no contemporaneous regressors**

$$\text{VIX}_t = \alpha_{21} \text{GPR}_t + \beta_2' \text{lags}_t + u_t^{\text{VIX}}$$

$$\text{INV}_t = \alpha_{31} \text{GPR}_t + \alpha_{32} \text{VIX}_t + \beta_3' \text{lags}_t + u_t^{\text{INV}}$$

$$\vdots$$

$$\text{NFCI}_t = \alpha_{81} \text{GPR}_t + \cdots + \alpha_{87} \text{FCM2}_t + \beta_8' \text{lags}_t + u_t^{\text{NFCI}}$$

### Key Restriction

> **GPR is ordered first** ⟹ it does not respond **contemporaneously** to any other variable in the system. This is the sole identifying restriction.

---

## Interpretation of GPR Shocks

### The Impact Matrix

The **impact matrix is L_C** (lower triangular). Its j-th column gives the contemporaneous response of all variables to structural shock j. The paper reports only **impulse responses to shock 1** (the GPR shock, column 1 of L_C).

### Why Only Column 1?

Full identification of p = 8 structural shocks requires **p(p − 1)/2 = 28 zero restrictions** on the contemporaneous coefficient matrix $A_0 = (L_C')^{-1}$.

- The authors defend **exactly one restriction economically** (GPR is predetermined within the month)
- The remaining 27 are **mechanical artefacts of the triangular ordering**

### Invariance Result

**Column 1 of L_C depends only on Var(GPR_t) and Cov(GPR_t, Z_{it}).** It is therefore **unchanged under any reordering of variables 2–8** — unlike columns 2–8, which are **not invariant** and carry **no stable structural interpretation**.

---

## Impulse Responses to a GPR Shock

![Figure 9: The Impact of Increased Geopolitical Risk](./impulse_responses.png)

**Eight-panel figure showing median impulse responses** to a two-standard-deviation increase in the GPR index across a 12-quarter horizon:

1. **GPR** — The shock itself, declining gradually from ~50% on impact
2. **VIX** — Sharp increase to ~2.5 index points, then gradual return to baseline
3. **Private Fixed Investment** — Significant negative response, declining ~2% at peak
4. **Hours Worked** — Modest negative response, reaching ~0.7% decline
5. **S&P 500** — Substantial decline, bottoming at ~5% lower than baseline
6. **Oil Price** — Brief decline of ~5%, quick recovery to baseline
7. **Two-Year Treasury Yield** — Modest decline initially, then slight increase
8. **NFCI Index** — Spike followed by return to baseline

**Bands:** Dark bands represent 68% pointwise credible sets; light bands represent 90% pointwise credible sets.

**Source:** Caldara & Iacoviello (2022), Figure 9.

---

## Key Takeaways

- An unexpected increase in geopolitical risk causes **measurable macroeconomic contraction**
- Effects are strongest on **financial variables** (VIX, stock prices) with **rapid onset**
- Real variables like **investment and hours worked** respond with **longer lags and persistence**
- The **Cholesky identification** is justified by the economically meaningful restriction that geopolitical risk is predetermined within a month
- The **invariance of column 1** under variable reordering provides credibility to the GPR shock estimates
