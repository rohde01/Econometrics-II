# Analysis of Non-Stationary and Co-Integrated Time Series

**Econometrics II**  
**Rasmus Søndergaard Pedersen**

---

## Outline

1. Co-integration defined
2. Co-integration and equilibrium
3. Engle-Granger co-integration analysis
4. Co-integration analysis based on ADL/ECM model

---

## 1. Combination of I(1) Time Series

A unit-root non-stationary, I(1), time series can be written as:

$$x_t = c \sum_{i=1}^{t} e_i + c^* e_t + c^*_1 e_{t-1} + \ldots + c^*_{t-1} e_1 + A = \tau_t + S_t + A$$

### Two-Variable System

Let $X_t = (x_{1t}, x_{2t})^{\prime}$ contain $p = 2$ variables:

$$x_{1t} = \tau_{1t} + S_{1t} + A_1$$
$$x_{2t} = \tau_{2t} + S_{2t} + A_2$$

Define $\beta = (1, -\beta_2)^{\prime}$ and consider the linear combination:

$$\beta^{\prime} X_t = \begin{pmatrix} 1 & -\beta_2 \end{pmatrix} \begin{pmatrix} x_{1t} \\ x_{2t} \end{pmatrix} = (\tau_{1t} - \beta_2 \tau_{2t}) + (S_{1t} - \beta_2 S_{2t}) + (A_1 - \beta_2 A_2)$$

**In general, $\beta^{\prime} X_t$ will also have a random walk and be I(1).**

---

## 2. Co-integration: An Important Exception

> **Definition:** If there exists a non-zero $\beta$ such that $\beta^{\prime} X_t$ is stationary, then we say that $x_{1t}$ and $x_{2t}$ **co-integrate** with **co-integration vector** $\beta$.

### Key Points on Co-integration

1. **Common Stochastic Trends:** Co-integration occurs if the stochastic trends cancel: $\tau_{1t} - \beta_2 \tau_{2t} = 0$. This is called a **common stochastic trend**.

2. **Equilibrium Equation:** You can think of an equation eliminating the random walks:
   $$x_{1t} = \beta_2 x_{2t} + u_t$$
   If $u_t$ is stationary, then $\beta = (1, -\beta_2)^{\prime}$ is a co-integrating vector.

3. **Normalization:** The co-integrating vector is unique up to normalization:
   $$\beta = \begin{pmatrix} 1 \\ -\beta_2 \end{pmatrix} \quad \text{or} \quad \tilde{\beta} = \begin{pmatrix} -\tilde{\beta}_1 \\ 1 \end{pmatrix}$$

4. **Extension:** Co-integration is easily extended to more variables.

---

## 3. Co-integration and Economic Equilibrium

Consider an equation for two I(1) variables, $x_{1t}$ and $x_{2t}$:

$$x_{1t} = \mu + \beta_2 x_{2t} + u_t = x^*_{1t} + u_t \quad (*)$$

The term $u_t$ is the deviation from the relation in $(*)$.

### Interpretation Based on Co-integration

**If $x_{1t}$ and $x_{2t}$ co-integrate**, then the deviation:
$$u_t = x_{1t} - \mu - \beta_2 x_{2t}$$
is a stationary process with mean zero. We think of $(*)$ as defining an **equilibrium** between $x_{1t}$ and $x_{2t}$.

**If $x_{1t}$ and $x_{2t}$ do NOT co-integrate**, then the deviation $u_t$ is I(1). There is no interpretation of $(*)$ as an equilibrium relation.

---

## 4. Example: Consumption and Income

Log consumption, $c_t$, and log income, $y_t$, are likely to be I(1).

The vector $X_t = (c_t, y_t)^{\prime}$ is co-integrated with co-integration vector $\beta = (1, -1)^{\prime}$ if the consumption-income ratio:

$$\beta^{\prime} X_t = (1, -1) \begin{pmatrix} c_t \\ y_t \end{pmatrix} = c_t - y_t$$

is a stationary equilibrium relationship.

**Empirical observation:** Both consumption and income trend upward, but the ratio fluctuates around a stable mean, indicating co-integration.

---

## 5. Example of a Data Generating Process

Consider $X_t = (c_t, y_t)^{\prime}$ with DGP:

$$c_t = \mu + \beta_2 y_{t-1} + e_{c,t}$$
$$\Delta y_t = e_{y,t}$$

### Solving for $y_t$

$$y_t = \sum_{i=1}^{t} e_{y,i} + y_0$$

This is a random walk. The lagged value:

$$y_{t-1} = \sum_{i=1}^{t-1} e_{y,i} + y_0 = \sum_{i=1}^{t} e_{y,i} - e_{y,t} + y_0$$

### Solving for $c_t$

$$c_t = \mu + \beta_2 y_{t-1} + e_{c,t}$$
$$= \mu + \beta_2 \left( \sum_{i=1}^{t} e_{y,i} + y_0 - e_{y,t} \right) + e_{c,t}$$
$$= \mu + \beta_2 \sum_{i=1}^{t} e_{y,i} + e_{c,t} - \beta_2 e_{y,t} + \beta_2 y_0$$

**The random walks are the same.**

### Co-integration Result

$c_t$ and $y_t$ co-integrate with co-integration vector $\beta = (1, -\beta_2)^{\prime}$:

$$\beta^{\prime} X_t = c_t - \beta_2 y_t = \mu + e_{c,t} - \beta_2 e_{y,t}$$

which is **stationary**.

### MA Solution in Matrix Form

$$\begin{pmatrix} c_t \\ y_t \end{pmatrix} = \begin{pmatrix} 0 & \beta_2 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} \sum_{i=1}^{t} e_{c,i} \\ \sum_{i=1}^{t} e_{y,i} \end{pmatrix} + \begin{pmatrix} 1 & -\beta_2 \\ 0 & 0 \end{pmatrix} \begin{pmatrix} e_{c,t} \\ e_{y,t} \end{pmatrix} + \begin{pmatrix} \mu \\ 0 \end{pmatrix} + \begin{pmatrix} 0 & \beta_2 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} c_0 \\ y_0 \end{pmatrix}$$

Or simply:

$$X_t = C \sum_{i=1}^{t} e_i + C_0^* e_t + \tilde{\mu} + A$$

The $2 \times 2$ matrix $C$ has reduced rank:

$$C = \begin{pmatrix} 0 & \beta_2 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} \beta_2 \\ 1 \end{pmatrix} (0 \quad 1)$$

And:

$$\beta^{\prime} C = (1 \quad -\beta_2) \begin{pmatrix} 0 & \beta_2 \\ 0 & 1 \end{pmatrix} = (0 \quad 0)$$

**Fewer stochastic trends than variables.**

---

## 6. How is the Equilibrium Sustained?

There must be forces pulling $x_{1t}$ or $x_{2t}$ towards the equilibrium.

> **Granger Representation Theorem:** $x_{1t}$ and $x_{2t}$ co-integrate if and only if there exist an **error correction model** for either $x_{1t}$, $x_{2t}$ or both.

### Simple Example

$$c_t = \mu + \beta_2 y_{t-1} + e_{c,t}$$

Taking first differences:

$$\Delta c_t = c_t - c_{t-1} = -c_{t-1} + \mu + \beta_2 y_{t-1} + e_{c,t}$$
$$\Delta c_t = -(c_{t-1} - \mu - \beta_2 y_{t-1}) + e_{c,t}$$

**Error-Correction Interpretation:** If consumption is larger than the equilibrium value:
$$c_{t-1} > c^*_{t-1} = \mu + \beta_2 y_{t-1}$$

then there will be a downward pressure on consumption: $E[\Delta c_t | I_{t-1}] < 0$.

---

## 7. More on Error-Correction

In general, both variables could error correct:

$$\Delta x_{1t} = \alpha_1 (x_{1t-1} - \beta_2 x_{2t-1}) + \Gamma_{11} \Delta x_{1t-1} + \Gamma_{12} \Delta x_{2t-1} + e_{1t}$$
$$\Delta x_{2t} = \alpha_2 (x_{1t-1} - \beta_2 x_{2t-1}) + \Gamma_{21} \Delta x_{1t-1} + \Gamma_{22} \Delta x_{2t-1} + e_{2t}$$

### Vector Error Correction Model (VECM)

$$\begin{pmatrix} \Delta x_{1t} \\ \Delta x_{2t} \end{pmatrix} = \begin{pmatrix} \alpha_1 \\ \alpha_2 \end{pmatrix} (x_{1t-1} - \beta_2 x_{2t-1}) + \Gamma_1 \begin{pmatrix} \Delta x_{1t-1} \\ \Delta x_{2t-1} \end{pmatrix} + \begin{pmatrix} e_{1t} \\ e_{2t} \end{pmatrix}$$

Or simply:
$$\Delta x_t = \alpha \beta^{\prime} x_{t-1} + \Gamma \Delta x_{t-1} + e_t$$

**Key observations:**
- $\beta^{\prime} x_{t-1} = x_{1t-1} - \beta_2 x_{2t-1}$ appears in both equations
- For $x_{1t}$ to error correct we need $\alpha_1 < 0$
- For $x_{2t}$ to error correct we need $\alpha_2 > 0$ if $\beta_2 > 0$

### Numerical Example

Consider:
$$\begin{pmatrix} \Delta x_{1t} \\ \Delta x_{2t} \end{pmatrix} = \begin{pmatrix} -0.2 \\ 0.1 \end{pmatrix} (x_{1t-1} - x_{2t-1}) + \begin{pmatrix} e_{1t} \\ e_{2t} \end{pmatrix}$$

**Graphs show:**
- (A) Two co-integrated variables tracking each other closely
- (B) Deviation from equilibrium oscillating around zero
- (C) Speed of adjustment: when deviation is large, it pulls back strongly
- (D) Cross-plot showing linear relationship with dynamic adjustments

---

## 8. Engle-Granger (Two-Step) Co-integration Analysis

### Basic Principle

Co-integration implies that $\beta_2$ exists such that the error term $u_t$ in:

$$x_{1t} = \mu + \beta_2 x_{2t} + u_t \quad (*)$$

is stationary.

### Super-Consistency of OLS Estimator

Under co-integration, the OLS estimator in $(*)$ is **consistent**:
$$\hat{\beta}_2 \xrightarrow{p} \beta_2 \quad \text{as } T \to \infty$$

**Important property:** Consistency holds even if dynamic terms are neglected, because the stochastic trends in $x_{1t}$ and $x_{2t}$ dominate.

We can even get consistent estimators in the reverse regression:
$$x_{2t} = \delta + \gamma_1 x_{1t} + v_t$$

### Critical Limitation: Lack of Asymptotic Normality

**Unfortunately, $\hat{\beta}_2$ is NOT asymptotically normal in general.**

The normal inferential procedures do NOT apply to $\hat{\beta}_2$!

$$\text{We can use (*) for estimation — NOT for testing.}$$

---

## 9. Super-Consistency

For **stationary series**, the variance of $\hat{\beta}_2$ declines at rate $T^{-1}$.

For **co-integrated I(1) series**, $V(\hat{\beta}_2)$ declines at faster rate $T^{-2}$.

### Intuition

- If $\hat{\beta}_2 = \beta_2$ then $u_t$ is stationary
- If $\hat{\beta}_2 \neq \beta_2$ then the error is I(1) and will have large variance
- The "information" on the parameter grows very fast

**Visual demonstration:** Distribution of $\hat{\beta}_2$ becomes increasingly concentrated at true value as sample size increases from $T=50$ to $T=100$ to $T=500$, with much faster concentration for non-stationary case.

---

## 10. Test for No Co-integration: Known $\beta$

### Setup

Suppose that $x_{1t}$ and $x_{2t}$ are I(1), and assume that $\beta = (1, -\beta_2)^{\prime}$ is **known**.

The series co-integrate if:
$$z_t = x_{1t} - \beta_2 x_{2t}$$

is stationary.

### Procedure

Use an **ADF unit root test**, testing for $H_0: \pi = 0$ in:

$$\Delta z_t = \delta + \pi z_{t-1} + \sum_{i=1}^{k} c_i \Delta z_{t-i} + \eta_t$$

The usual DF critical values apply to $t_{\pi=0}$.

**Note:** The null $H_0: \pi = 0$ is a unit root (no co-integration).

---

## 11. Test for No Co-integration: Estimated $\beta$

### Engle-Granger (1987) Two-Step Procedure

If $\beta = (1, -\beta_2)^{\prime}$ is unknown, we may **super-consistently estimate it**:

$$x_{1t} = \mu + \beta_2 x_{2t} + u_t \quad (**)$$

$\hat{\beta}$ is a co-integration vector if $\hat{u}_t = x_{1t} - \hat{\mu} - \hat{\beta}_2 x_{2t}$ is stationary.

### Step 2: ADF Test on Residuals

Use ADF unit root test for $H_0: \pi = 0$ in:

$$\Delta \hat{u}_t = \pi \hat{u}_{t-1} + \sum_{i=1}^{k} c_i \Delta \hat{u}_{t-i} + \eta_t$$

### Critical Remarks

1. **No deterministics:** The residual $\hat{u}_t$ has mean zero. No deterministics appear in the DF regression.

2. **Critical values depend on specification:** The critical value for $t_{\pi=0}$ depends on the deterministic terms in $(**)$.

3. **Estimation bias matters:** The fact that $\hat{\beta}_2$ is estimated changes the critical values. OLS minimizes the variance of $\hat{u}_t$, making it look "as stationary as possible." Critical value depends on the number of I(1) regressors.

### Critical Values: Case 1 (Constant in *)

| # I(1) regressors | 1% | 5% | 10% |
|------------------|----|----|-----|
| 0 | -3.43 | -2.86 | -2.57 |
| 1 | -3.90 | -3.34 | -3.04 |
| 2 | -4.29 | -3.74 | -3.45 |
| 3 | -4.64 | -4.10 | -3.81 |
| 4 | -4.96 | -4.42 | -4.13 |

### Critical Values: Case 2 (Constant + Trend in *)

| # I(1) regressors | 1% | 5% | 10% |
|------------------|----|----|-----|
| 0 | -3.96 | -3.41 | -3.13 |
| 1 | -4.32 | -3.78 | -3.50 |
| 2 | -4.66 | -4.12 | -3.84 |
| 3 | -4.97 | -4.43 | -4.15 |
| 4 | -5.25 | -4.72 | -4.43 |

---

## 12. Dynamic Modelling

With the estimated $\beta$, we can define the **error correction term**:

$$\text{ecm}_t = \hat{u}_t = x_{1t} - \hat{\mu} - \hat{\beta}_2 x_{2t}$$

which is, by definition, a stationary stochastic variable.

Since $\hat{\beta}_2$ converges to $\beta_2$ very fast, we can treat it as a fixed regressor:

$$\Delta x_{1t} = \delta + \lambda_1 \Delta x_{1t-1} + \kappa_0 \Delta x_{2t} + \kappa_1 \Delta x_{2t-1} + \alpha \cdot \text{ecm}_{t-1} + e_t$$

where $\alpha < 0$ is consistent with error-correction.

### Inference

Given co-integration, all terms are stationary. **Normal inference applies** to $\delta$, $\lambda_1$, $\kappa_0$, $\kappa_1$, and $\alpha$.

We could estimate ECM models for all variables.

---

## 13. Outline of an Engle-Granger Analysis

1. **Test individual variables** (e.g., $x_{1t}$ and $x_{2t}$) for unit roots.

2. **Estimate $\beta$** using a static co-integrating regression:
   $$x_{1t} = \mu + \beta_2 x_{2t} + u_t$$
   **Note:** The t-ratios cannot be used for inference.

3. **Test for no co-integration** using a unit-root test on the residual $\hat{u}_t$.

4. **If no co-integration is rejected**, estimate a dynamic (ECM) model like:
   $$\Delta x_{1t} = \delta + \lambda_1 \Delta x_{1t-1} + \kappa_0 \Delta x_{2t} + \kappa_1 \Delta x_{2t-1} + \alpha \hat{u}_{t-1} + e_t$$

All terms are stationary. Remaining inference is standard.

---

## 14. Empirical Example: Danish Interest Rates

### Data and Variables

Consider two Danish interest rates:
- $r_t$: Money market interest rate
- $b_t$: Bond Yield

Period: $t = 1972:1 - 2003:2$

### Step 1: Unit Root Tests (5% critical value: -2.86)

**Money market rate:**
$$\Delta r_t = \underbrace{0.00638}_{(1.35)} - \underbrace{0.126}_{(-2.39)} \Delta r_{t-1} - \underbrace{0.234}_{(-2.70)} \Delta r_{t-4} - \underbrace{0.0827}_{(-1.80)} r_{t-1}$$

**Bond yield:**
$$\Delta b_t = \underbrace{0.00117}_{(0.658)} + \underbrace{0.395}_{(4.67)} \Delta b_{t-1} - \underbrace{0.0129}_{(-0.909)} b_{t-1}$$

**Conclusion:** Cannot reject unit roots.

### Step 2: Test Spread for I(1) Status

Let $s_t = r_t - b_t$ (5% critical value: -2.86):

$$\Delta s_t = \underbrace{0.00849}_{(3.71)} + \underbrace{0.2076}_{(2.56)} \Delta s_{t-3} - \underbrace{0.379}_{(-5.35)} s_{t-1}$$

**Conclusion:** Easily rejected that $b_t$ and $r_t$ are not co-integrating.

### Estimated Relationship

$$r_t = 0.865 b_t$$

The spread $r_t - b_t$ is stationary, indicating co-integration with $\beta_2 = 1$ (approximately).

### Step 3: Test with Estimated $\beta$

Test residuals $\hat{e}_t = \hat{u}_t$ (5% critical value: -3.34):

$$\Delta \hat{e}_t = \underbrace{0.230}_{(2.95)} \Delta \hat{e}_{t-3} - \underbrace{0.499}_{(-6.77)} \hat{e}_{t-1}$$

**Conclusion:** Again reject no co-integration.

### Step 4: Error Correction Models

Based on the spread $r_{t-1} - b_{t-1}$:

**Money market rate:**
$$\Delta r_t = \underbrace{-0.774}_{(-3.23)} + \underbrace{1.18}_{(4.55)} \Delta b_t - \underbrace{0.406}_{(-5.22)} (r_{t-1} - b_{t-1})$$

**Bond yield:**
$$\Delta b_t = \underbrace{-0.182}_{(-2.11)} + \underbrace{0.439}_{(4.16)} \Delta b_{t-1} - \underbrace{0.067}_{(-2.01)} \Delta r_t - \underbrace{0.0638}_{(-2.22)} (r_{t-1} - b_{t-1})$$

**Key finding:** The short rate ($r_t$) error corrects strongly (coefficient -0.406), while the bond yield ($b_t$) shows weak error correction (coefficient -0.0638).

Could have used either $r_{t-1} - b_{t-1}$ or $\text{ecm}_{t-1} = \hat{u}_{t-1}$.

---

## 15. Co-integration Analysis Based on ADL/ECM Model

### Alternative Approach

The estimator of $\beta_2$ from a static regression is super-consistent but often **biased**, and **hypotheses cannot be tested**.

Instead, estimate based on an **unrestricted ADL model**:

$$x_{1t} = \delta + \theta_1 x_{1t-1} + \theta_2 x_{1t-2} + \varphi_0 x_{2t} + \varphi_1 x_{2t-1} + \varphi_2 x_{2t-2} + e_t$$

where $e_t$ is i.i.d.

### Equivalent Representations

This is **equivalent** to a linear error correction model:

$$\Delta x_{1t} = \delta + \lambda_1 \Delta x_{1t-1} + \kappa_0 \Delta x_{2t} + \kappa_1 \Delta x_{2t-1} + \alpha x_{1t-1} + \gamma x_{2t-1} + e_t$$

with $\alpha = \theta_1 + \theta_2 - 1$ and $\gamma = \varphi_0 + \varphi_1 + \varphi_2$.

Also equivalent to the **non-linear regression model**:

$$\Delta x_{1t} = \lambda_1 \Delta x_{1t-1} + \kappa_0 \Delta x_{2t} + \kappa_1 \Delta x_{2t-1} + \alpha(x_{1t-1} - \mu - \beta_2 x_{2t-1}) + e_t$$

### Estimation of Long-Run Parameters

An estimate of $\beta_2$ can be found from the long-run solutions:

$$\hat{\beta}_2 = \frac{\hat{\varphi}_0 + \hat{\varphi}_1 + \hat{\varphi}_2}{1 - \hat{\theta}_1 - \hat{\theta}_2} = \frac{-\hat{\gamma}}{\hat{\alpha}}$$

$$\hat{\mu} = \frac{\hat{\delta}}{1 - \hat{\theta}_1 - \hat{\theta}_2} = \frac{-\hat{\delta}}{\hat{\alpha}}$$

### Advantages and Inference

**Main advantage:** The model is **well-specified**.

**Optimal when:** The approach is optimal if only $x_{1t}$ error corrects.

**Inference:** Inference on all parameters to I(0) terms is standard.

**Non-Gaussian distribution:** $\hat{\beta}_2$ is not Gaussian, but inference is nevertheless standard:
$$t_{\beta_2=b} = \frac{\hat{\beta}_2 - b}{\text{se}(\hat{\beta}_2)} \xrightarrow{d} N(0,1)$$

---

## 16. Test for No Co-integration (ADL/ECM)

### Granger Representation Theorem Recall

No co-integration corresponds to **no-error-correction**.

A simple test is the **PcGive test for no co-integration**.

### Procedure

Consider the unrestricted ADL or ECM:

$$\Delta x_{1t} = \delta + \lambda_1 \Delta x_{1t-1} + \kappa_0 \Delta x_{2t} + \kappa_1 \Delta x_{2t-1} + \alpha x_{1t-1} + \gamma x_{2t-1} + e_t \quad (\#)$$

Test the hypothesis:
$$H_0: \alpha = 0$$

against the co-integration alternative $\alpha < 0$.

### Test Statistic

This is a **unit root test** (not $N(0,1)$). The distribution of:

$$t_{\alpha=0} = \frac{\hat{\alpha}}{\text{se}(\hat{\alpha})}$$

depends on the deterministics and the number of I(1) variables in $(\#)$.

### Critical Values: Case 1 (Constant in #)

| # I(1) regressors in long-run | 1% | 5% | 10% |
|-------------------------------|----|----|-----|
| 1 | -3.79 | -3.21 | -2.91 |
| 2 | -4.09 | -3.51 | -3.19 |
| 3 | -4.36 | -3.76 | -3.44 |
| 4 | -4.59 | -3.99 | -3.66 |

### Critical Values: Case 2 (Constant + Trend in #)

| # I(1) regressors in long-run | 1% | 5% | 10% |
|-------------------------------|----|----|-----|
| 1 | -4.25 | -3.69 | -3.39 |
| 2 | -4.50 | -3.93 | -3.62 |
| 3 | -4.72 | -4.14 | -3.83 |
| 4 | -4.93 | -4.34 | -4.03 |

---

## 17. Outline of ADL Co-integration Analysis

1. **Test individual variables** (e.g., $x_{1t}$ and $x_{2t}$) for unit roots.

2. **Estimate an ADL or ECM model:**
   $$x_{1t} = \delta + \theta_1 x_{1t-1} + \theta_2 x_{1t-2} + \varphi_0 x_{2t} + \varphi_1 x_{2t-1} + \varphi_2 x_{2t-2} + e_t$$
   
   OR equivalently:
   $$\Delta x_{1t} = \delta + \lambda_1 \Delta x_{1t-1} + \kappa_0 \Delta x_{2t} + \kappa_1 \Delta x_{2t-1} + \alpha x_{1t-1} + \gamma x_{2t-1} + e_t$$

3. **Test for no co-integration** with $t_{\alpha=0}$. Given co-integration, the co-integrating relation is the long-run solution:
   $$x_{1t} = \hat{\mu} + \hat{\beta}_2 x_{2t}$$
   
   **Inference on $\beta_2$ is standard** (under some conditions).

4. **Rest of the analysis is standard:** All N(0,1). Look at dynamics.

---

## 18. Empirical Example: Interest Rates Revisited

### ADL Model Estimation

Based on an ADL model, the significant terms are:

**Model Results:**
- IMM_1 (lagged dependent): 0.615 (t = 7.78)
- Constant: -0.0025 (insignificant)
- IBZ (current): 1.199 (t = 5.11)
- IBZ_1 (lagged): -0.866 (t = -3.27)

**Model statistics:**
- R² = 0.841
- F(3,115) = 203.4
- DW = 2.16

### Test for No Co-integration

**PcGive Unit-root t-test:** -4.8661

**5% critical value:** -3.21

**Conclusion:** Strongly reject no co-integration.

### Long-Run Solution

$$x_t = -0.0065 + 0.867 \times IBZ$$

with standard errors and t-values:
- Constant: se = 0.0118, t = -0.550
- IBZ: se = 0.0949, t = 9.13

**Key result:** $\hat{\beta}_2 = 0.867$ is not significantly different from unity.

### Dynamic Multipliers

The dynamic multipliers $\partial x_{1t}/\partial x_{2t}$, $\partial x_{1t}/\partial x_{2t-1}$, etc., and the cumulated $\sum \partial x_{1t}/\partial x_{2t-i}$ can be graphed to show the short-run dynamics and convergence to long-run equilibrium.

---

## 19. Further Remarks

### Engle-Granger Analysis

**Drawbacks:**
1. Less efficient than other approaches ("Dynamically incomplete")
2. Does not allow for inference on $\beta$ (at least not when estimated by OLS)
3. Assumes only one co-integration relation

**Merit:**
- Allows for multiple error-correcting variables

### Dynamic (ADL/ECM) Analysis

**Drawbacks:**
1. Allows for only one co-integration relation
2. Allows for only one error-correcting variable

**Merits:**
1. "Dynamically complete"
2. Allows for inference on $\beta$

---

## Summary

**Key Concepts:**

- **Co-integration:** When I(1) variables share a common stochastic trend, allowing a stationary linear combination (the co-integrating relationship)
  
- **Equilibrium:** The co-integrating relationship represents a long-run equilibrium between variables

- **Error Correction:** Co-integrating variables must exhibit error-correction behavior (Granger representation theorem)

- **Super-consistency:** OLS estimation of the co-integrating vector converges at rate T², not T^(1/2)

- **Two Approaches:**
  - **Engle-Granger:** Two-step procedure (static then dynamic). Simple but less efficient.
  - **ADL/ECM:** Unrestricted dynamic model. More efficient and allows inference on co-integrating vector.

- **Testing:** Different critical values for different specifications and number of regressors

