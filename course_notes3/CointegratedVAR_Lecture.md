# The Co-Integrated Vector Autoregression

**Econometrics II**  
Rasmus Søndergaard Pedersen

---

## Outline: The Co-integrated VAR Model

1. The Vector Error-Correction Model (VECM)
2. Granger's Representation
3. Test for Co-integration Rank and Asymptotic Inference in the VECM
4. Empirical Example: Private Consumption
5. Normalization and Identification
6. Deterministic Terms

---

## 1. The Vector Autoregressive Model

Let $X_t = (x_{1t}, \ldots, x_{pt})' \in \mathbb{R}^p$ and consider a VAR(1):

$$X_t = \Pi_1 X_{t-1} + e_t, \quad t = 1, 2, \ldots, T$$

conditional on $X_0$ and $e_t | X_{t-1} \stackrel{d}{=} N(0, \Omega)$.

Using the lag-operator to rewrite the VAR:

$$X_t - \Pi_1 L X_t = e_t$$
$$(I_p - \Pi_1 L) X_t = e_t$$
$$\Theta(L) X_t = e_t$$

where $\Theta(z) = I_p - \Pi_1 z$ is a $p \times p$ matrix of polynomials, $z \in \mathbb{C}$.

The characteristic equation is defined as $\det(\Theta(z)) = 0$.

Note that:
$$\Theta(1) = I_p - \Pi_1$$

such that the VAR model has a unit root if:
$$\det(\Theta(1)) = \det(I_p - \Pi_1) = 0$$

---

## The Vector Error Correction Model

Similarly to the univariate case, we can rewrite:

$$X_t = \Pi_1 X_{t-1} + e_t$$
$$X_t - X_{t-1} = (\Pi_1 - I_p) X_{t-1} + e_t$$
$$\Delta X_t = \Pi X_{t-1} + e_t$$

where $\Pi = \Pi_1 - I_p = -\Theta(1)$.

The process $X_t$ has a unit root if:
$$\det(\Theta(1)) = \det(\Pi) = 0$$

such that $\Pi$ has **reduced rank**.

This is parallel to the univariate case, $p = 1$, where $\Pi$ is $1 \times 1$ and a unit root requires that $\Pi$ has reduced rank, $\Pi = 0$.

---

## Reduced Rank Vector Autoregression

A $p \times p$ matrix $\Pi$ with reduced rank,
$$\text{rank}(\Pi) = r < p$$

has only $r$ linearly independent columns (and rows) and can be written as:
$$\Pi = \alpha \beta'$$

where $\alpha, \beta$ are $p \times r$ matrices.

We can write the VECM as:
$$\Delta X_t = \alpha \beta' X_{t-1} + e_t \quad (*)$$

---

## Three Different Cases

1. **Stationarity**: If $X_t$ is a stationary process, then there are no unit roots, and $\Pi = -\Theta(1)$ is a full rank matrix. This is a stationary VAR.

2. **Unit-Roots and Co-integration**: If $X_t$ is unit-root non-stationary (*) looks unbalanced. Because $\Pi = -\Theta(1)$ has reduced rank we could have $\beta' X_t$ as stationary. Error-correction is given by $\alpha$.

3. **Unit-Roots and No Co-integration**: $\Pi$ has reduced rank and (*) is only balanced if $\Pi = 0$ ($\Rightarrow \text{rank}(\Pi) = 0$). This is a VAR model in first differences.

### The steps of the co-integration analysis is to

- Determine the **rank** of $\Pi$
- Characterize the **equilibrium relations** in $\beta$
- Characterize the structure of the **error correction** in $\alpha$

---

## Example: Unstable VAR (from VAR slides)

Consider the VAR(1) model for $X_t = (x_{1t}, x_{2t})'$:

$$\begin{pmatrix} x_{1t} \\ x_{2t} \end{pmatrix} = \begin{pmatrix} 0.7 & 0.1 \\ 0.3 & 0.9 \end{pmatrix} \begin{pmatrix} x_{1t-1} \\ x_{2t-1} \end{pmatrix} + \begin{pmatrix} e_{1t} \\ e_{2t} \end{pmatrix}$$

The characteristic equation is:

$$|I_2 - \Pi_1 z| = (1 - 0.7z)(1 - 0.9z) - (0.3z)(-0.1z)$$
$$= 0.6z - 1.6z + 1 = 0$$

The solutions/roots are:
$$z_i = \left\{ 1, \frac{5}{3} \right\}$$

and the VAR is **not stable**. $X_t$ is not stationary (a unit root process).

### Continuing the Example

We have that, with $\Delta X_t = \Pi X_{t-1} + e_t$:

$$\det(\Pi) = \det(\Pi_1 - I_2) = 0$$

In particular, $\Pi$ has $\text{rank}(\Pi) = 1$:

$$\Pi = \Pi_1 - I_2 = \begin{pmatrix} -0.3 & 0.1 \\ 0.3 & -0.1 \end{pmatrix} = \begin{pmatrix} -0.3 \\ 0.3 \end{pmatrix} \left( 1 \quad -\frac{1}{3} \right) = \alpha \beta'$$

Note that:
$$\beta' X_t = (1 + \beta' \alpha) \beta' X_{t-1} + \beta' e_t$$

is a stationary AR(1) process, as $1 + \beta' \alpha = 1 - 0.4 = 0.6$.

---

## Example: Organic and Regular Orange Prices

Consider $X_t = (p_t^{\text{org}}, p_t^{\text{reg}})'$. A VAR(1) is given by:

$$\begin{pmatrix} \Delta p_t^{\text{org}} \\ \Delta p_t^{\text{reg}} \end{pmatrix} = \begin{pmatrix} \Pi_{11} & \Pi_{12} \\ \Pi_{21} & \Pi_{22} \end{pmatrix} \begin{pmatrix} p_{t-1}^{\text{org}} \\ p_{t-1}^{\text{reg}} \end{pmatrix} + \begin{pmatrix} \mu_1 \\ \mu_2 \end{pmatrix} + \begin{pmatrix} e_t^{\text{org}} \\ e_t^{\text{reg}} \end{pmatrix}$$

The information on the long-run properties is contained in $\Pi$.

If $\Pi = 0$, then the equation would be only in first differences.

If $\text{rank}(\Pi) = 1$, then $\Pi = \alpha \beta'$ and:

$$\begin{pmatrix} \Delta p_t^{\text{org}} \\ \Delta p_t^{\text{reg}} \end{pmatrix} = \begin{pmatrix} \alpha_1 \\ \alpha_2 \end{pmatrix} (1, \beta_2) \begin{pmatrix} p_{t-1}^{\text{org}} \\ p_{t-1}^{\text{reg}} \end{pmatrix} + \begin{pmatrix} \mu_1 \\ \mu_2 \end{pmatrix} + \begin{pmatrix} e_t^{\text{org}} \\ e_t^{\text{reg}} \end{pmatrix}$$

Estimates are given by:

$$\begin{pmatrix} \Delta p_t^{\text{org}} \\ \Delta p_t^{\text{reg}} \end{pmatrix} = \begin{pmatrix} -0.90 \\ -0.01 \end{pmatrix} (1, -1.03) \begin{pmatrix} p_{t-1}^{\text{org}} \\ p_{t-1}^{\text{reg}} \end{pmatrix} + \begin{pmatrix} 22.5 \\ 1.14 \end{pmatrix} + \begin{pmatrix} \hat{e}_t^{\text{org}} \\ \hat{e}_t^{\text{reg}} \end{pmatrix}$$

---

## 2. Granger's Representation

Let $\alpha_\perp$ and $\beta_\perp$ be $p \times (p-r)$ (orthogonal) matrices such that:
$$\alpha' \alpha_\perp = \beta' \beta_\perp = 0_{r \times (p-r)}$$

From the VECM:
$$\Delta X_t = \alpha \beta' X_{t-1} + e_t$$

we have that:
$$\alpha_\perp' \Delta X_t = \alpha_\perp' e_t$$

so that:
$$\alpha_\perp' X_t = \sum_{i=1}^t \alpha_\perp' e_i + \alpha_\perp' X_0 \quad (1)$$

Here, $\sum_{i=1}^t \alpha_\perp' e_i$ are the **common stochastic trends** (permanent effects).

---

### The Granger Representation (continued)

From the VECM, we also have that:

$$\beta' \Delta X_t = \beta' \alpha \beta' X_{t-1} + \beta' e_t$$

or, equivalently:

$$\beta' X_t = (I_r + \beta' \alpha) \beta' X_{t-1} + \beta' e_t$$
$$= \sum_{i=1}^{t-1} (I_r + \beta' \alpha)^i \beta' e_{t-i} + (I_r + \beta' \alpha)^t \beta' X_0$$

That is, a VAR(1) for $\beta' X_t$.

**Fact 1**: The matrix $(I_r + \beta' \alpha)$ has eigenvalues inside unit circle.  
Consequently, $\beta' X_t$ is **stationary**.

---

### The Granger Representation (Fact 2)

**Fact 2**: The identity matrix $I_p$ has representation:

$$I_p = \alpha(\beta' \alpha)^{-1} \beta' \underbrace{}_{\text{CS}} + \beta_\perp (\alpha_\perp' \beta_\perp)^{-1} \alpha_\perp' \underbrace{}_{\text{B}} \quad (2)$$

Consequently, using (1):

$$X_t = C_S \beta' X_t + B \alpha_\perp' X_t$$
$$= \underbrace{C_S \beta' X_t}_{\text{"stationary"}} + \underbrace{B \sum_{i=1}^t \alpha_\perp' e_i}_{\text{"random walk"}} + C X_0$$

For the interpretation of the model, we can use that:

1. Only the linear combinations $\alpha_\perp' e_i$ have permanent effects.
2. The random walks affect the variables with coefficients $B$, where $\beta' B = 0$.

This carries over to VAR(k) models with deterministics.

---

## What About Stationary Variables?

Consider $X_t = (x_{1t}, x_{2t})'$ where $x_{1t}$ is I(1), while $x_{2t}$ is stationary, I(0). The co-integration analysis is still valid.

We should find that $\text{rank}(\Pi) = 1$, and:

$$\beta = \begin{pmatrix} 0 \\ 1 \end{pmatrix}, \quad \text{such that} \quad \beta' X_t = \begin{pmatrix} 0 & 1 \end{pmatrix} \begin{pmatrix} x_{1t} \\ x_{2t} \end{pmatrix} = x_{2t}$$

which is stationary.

The model includes levels of $x_{2t}$ and first differences of $x_{1t}$.

**Not important to do unit root tests for individual $x_{it}$.**

---

## 3. Test for the Co-Integration Rank

For a VAR(2):
$$X_t = \Pi_1 X_{t-1} + \Pi_2 X_{t-2} + \mu + e_t$$

the VECM is given by:
$$\Delta X_t = \Pi X_{t-1} + \Gamma_1 \Delta X_{t-1} + \mu + e_t$$

with $\Pi = \Pi_1 + \Pi_2 - I_p$ and $\Gamma_1 = -\Pi_2$.

Consider the case $p = 2$, such that $\Pi$ is $2 \times 2$ with 4 parameters.

- If $\Pi = 0$, then $X_t$ is unit-root non-stationary without co-integration. The number of parameters in $\Pi$ is zero.

- If $\text{rank}(\Pi) = r = 1$, then:
$$\Pi = \begin{pmatrix} \alpha_1 \\ \alpha_2 \end{pmatrix} (1, \beta_2)$$

and (because of the normalization) $\Pi$ has three parameters.

---

### Three Nested Models

We have three nested models:

$$H_0: \Delta X_t = \Gamma_1 \Delta X_{t-1} + \mu + e_t$$
$$H_1: \Delta X_t = \alpha \beta' X_{t-1} + \Gamma_1 \Delta X_{t-1} + \mu + e_t$$
$$H_2: \Delta X_t = \Pi X_{t-1} + \Gamma_1 \Delta X_{t-1} + \mu + e_t$$

The models are estimated by **maximum likelihood**, assuming that $e_t$ is Gaussian.

- For models with zero rank and full rank, i.e., $H_0$ and $H_2$ respectively, **ML estimation corresponds to OLS estimation**.

- For models with reduced rank (greater than zero), i.e. $H_1$, **ML estimation corresponds to so-called Reduced Rank Regression (RRR)**.

---

### Likelihood Ratio Tests for Co-integration Rank

We can test for the co-integration rank using likelihood ratio tests:

$$LR(H_0 | H_2) = -2(\log L(H_0) - \log L(H_2))$$
$$LR(H_1 | H_2) = -2(\log L(H_1) - \log L(H_2))$$

where $\log L(H_i)$ denote the maximized log-likelihood values.

The LR statistic is known as the **trace test statistic**.  
They have squared Dickey-Fuller type distributions as $T \to \infty$.

---

## Asymptotic Inference

Assume that $X_t$ is a unit-root non-stationary process.

- Estimators of parameters to first differences, $\hat{\Gamma}_i$, are $\sqrt{T}$-Gaussian. Use standard $\chi^2$ inference to determine the lag-length.

- $\beta' X_{t-1}$ is stationary, and given co-integration, $\hat{\alpha}$ is $\sqrt{T}$-Gaussian.

- $\hat{\beta}$ is **super-consistent** and $T(\hat{\beta} - \beta)$ converges in distribution to a mixed Gaussian:

$$T(\hat{\beta} - \beta) \stackrel{d}{\to} N(0, V_\beta), \quad \text{where } V_\beta \text{ is random}$$

We can estimate $V_\beta$ and test statistics have standard $N(0, 1)$ and $\chi^2$ distributions.

---

## Summary of a Co-Integrated VAR Analysis

**1. Estimate a well-specified VAR model for the variables in $X_t$.** [OLS]  
Test statistics for lag-length have standard $\chi^2$ distributions.

**2. Determine the co-integration rank from the sequence:**
$$H_0 \subseteq H_1 \subseteq \ldots \subseteq H_r \subseteq \ldots \subseteq H_p$$

using the likelihood ratio (trace) statistics:
$$LR(H_0 | H_p), LR(H_1 | H_p), \ldots LR(H_{p-1} | H_p)$$

Stop at the smallest rank not rejected. [RRR]

The distributions of the trace statistics depend on deterministics and $p - r$.

**3. For the preferred model, $H_r$:**
   - Characterize the **equilibrium relationships**, $\beta$
   - Characterize the **speed of adjustment**, $\alpha$

Likelihood ratio statistics for $\alpha$ and $\beta$ are $\chi^2$.

---

## 4. Empirical Example: Private Consumption

**Data:** DataForVARSlides.xlsx; 1974:3–2017:3

Consider the analysis for consumption, $X_t = (c_t, y_t, w_t)'$.

Determine the lag-length using LR test and $\chi^2$ distributions.  
We end with a VAR(2) model that appear well-specified:

$$\begin{pmatrix} \hat{c}_t \\ \hat{y}_t \\ \hat{w}_t \end{pmatrix} = \begin{pmatrix} 0.541^{(5.3)} & 0.0246^{(0.35)} & 0.151^{(1.0)} \\ 0.269^{(2.0)} & 0.600^{(6.5)} & -0.0433^{(-0.23)} \\ -0.181^{(-2.7)} & 0.0693^{(1.5)} & 0.997^{(10)} \end{pmatrix} \begin{pmatrix} c_{t-1} \\ y_{t-1} \\ w_{t-1} \end{pmatrix}$$

$$+ \begin{pmatrix} 0.153^{(1.5)} & 0.135^{(1.9)} & -0.0342^{(-0.2)} \\ -0.348^{(-2.6)} & 0.356^{(3.7)} & 0.147^{(0.75)} \\ 0.0906^{(1.4)} & 0.0515^{(1.1)} & -0.0215^{(-0.22)} \end{pmatrix} \begin{pmatrix} c_{t-2} \\ y_{t-2} \\ w_{t-2} \end{pmatrix} + \begin{pmatrix} -0.0759^{(0.72)} \\ -0.0996^{(-0.71)} \\ 0.0117^{(0.17)} \end{pmatrix}$$

with t-ratios in parentheses.

---

### Co-integration Analysis Results

To start the co-integration analysis, look at $\Pi = \Pi_1 + \Pi_2 - I_p$:

$$\hat{\Pi} = \begin{pmatrix} -0.306^{(-4.1)} & 0.160^{(3.3)} & 0.117^{(2.3)} \\ -0.0783^{(-0.8)} & -0.044^{(-0.7)} & 0.104^{(1.5)} \\ -0.0904^{(-1.8)} & 0.121^{(3.8)} & -0.0248^{(-0.7)} \end{pmatrix}$$

Not easy to see the rank, but second row is not very significant.

The likelihood ratio tests for reduced rank are given by:

| Rank | Log-Likelihood | $LR(H_r\|H_p)$ | 5% cv | p-value |
|------|---|---|---|---|
| 0 | 978.259 | 30.08 | 29.80 | 0.046 |
| 1 | 988.938 | 8.72 | 15.41 | 0.399 |
| 2 | 993.239 | 0.12 | 3.84 | 0.727 |
| 3 | 993.300 | — | — | — |

---

### Preferred Model: r = 1

We end with $r = 1$.

Estimates are given by:

$$\begin{pmatrix} \Delta \hat{c}_t \\ \Delta \hat{y}_t \\ \Delta \hat{w}_t \end{pmatrix} = \begin{pmatrix} -0.222^{(-3.8)} \\ 0.0234^{(0.30)} \\ -0.135^{(-3.5)} \end{pmatrix} \left( 1 \quad -0.812^{(-5.9)} \quad -0.141^{(-1.1)} \right) \begin{pmatrix} c_{t-1} \\ y_{t-1} \\ w_{t-1} \end{pmatrix} + \ldots$$

Corresponding to the equilibrium:
$$c_t = 0.812^{(-5.9)} y_t + 0.141^{(-1.1)} w_t$$

---

### Testing Restrictions on β and α

The sum of coefficients is close to one: $0.812 + 0.141 = 0.953$.  
Impose the restriction to get:

$$\begin{pmatrix} \Delta \hat{c}_t \\ \Delta \hat{y}_t \\ \Delta \hat{w}_t \end{pmatrix} = \begin{pmatrix} -0.172^{(-3.4)} \\ 0.0358^{(0.50)} \\ -0.123^{(-3.7)} \end{pmatrix} \left( 1 \quad -0.965^{(-6.7)} \quad -0.035^{(-0.20)} \right) \begin{pmatrix} c_{t-1} \\ y_{t-1} \\ w_{t-1} \end{pmatrix} + \ldots$$

The LR statistic is 0.535, which is not significant in a $\chi^2(1)$.

Also impose no error-correction for income:

$$\begin{pmatrix} \Delta \hat{c}_t \\ \Delta \hat{y}_t \\ \Delta \hat{w}_t \end{pmatrix} = \begin{pmatrix} -0.188^{(-3.9)} \\ 0 \\ -0.126^{(-3.7)} \end{pmatrix} \left( 1 \quad -0.936^{(-6.6)} \quad -0.064^{(-0.2)} \right) \begin{pmatrix} c_{t-1} \\ y_{t-1} \\ w_{t-1} \end{pmatrix} + \ldots$$

The joint test statistic is 0.797, which is not significant in a $\chi^2(2)$.

---

## 5. Normalization and Identification

$\alpha$ and $\beta$ only enter the model as a product:
$$\Pi = \alpha \beta'$$

and $\Pi$ is unchanged if we change normalization.

For $p = 3$ and $r = 1$, consider the example:

$$\begin{pmatrix} -0.3 & 0.15 & 0.15 \\ 0.2 & -0.1 & -0.1 \\ 0.1 & -0.05 & -0.05 \end{pmatrix} = \begin{pmatrix} -0.3 \\ 0.2 \\ 0.1 \end{pmatrix} \left( 1 \quad -0.5 \quad -0.5 \right)$$

$$= \begin{pmatrix} -0.15 \\ 0.1 \\ 0.05 \end{pmatrix} \left( 2 \quad -1 \quad -1 \right)$$

---

### Identification with r ≥ 2

When $r \geq 2$, we can still scale, but now also take linear combinations.

As an example:

$$\begin{pmatrix} -0.3 & 0.25 & -0.05 \\ 0.2 & -0.4 & 0.5 \\ 0.1 & 0.15 & -0.45 \end{pmatrix} = \begin{pmatrix} -0.3 & 0.1 \\ 0.2 & -0.3 \\ 0.1 & 0.2 \end{pmatrix} \begin{pmatrix} 1 & -0.5 & -0.5 \\ 0 & 1 & 2 \end{pmatrix}$$

$$= \begin{pmatrix} -0.3 & -0.05 \\ 0.2 & 0.5 \\ 0.1 & -0.45 \end{pmatrix} \begin{pmatrix} 1 & -0.75 & 0 \\ 0 & -0.5 & 1 \end{pmatrix}$$

We find a version we can interpret or that matches economic theory.

We may give relations names from their structure:
- Supply vs. demand
- Goods market equilibrium vs. financial market, etc.

---

## 6. Deterministic Terms

### Interpretation of the Constant Term

The constant term cumulates as in the univariate case, and:
$$\Delta X_t = \alpha \beta' X_{t-1} + \Gamma_1 \Delta X_{t-1} + \mu + e_t$$

has a solution given by:
$$X_t = C \sum_{i=1}^t (\mu + e_i) + C_0^* (\mu + e_t) + \ldots + C_{t-1}^* (\mu + e_1) + A$$

with $C = B \alpha_\perp'$.

Observe that $X_t$ now has a trend:
$$C \sum_{i=1}^t \mu + (C_0^* + C_1^* + \ldots + C_{t-1}^*) \mu = C \mu t + \text{constant}$$

but $\beta' C = 0$ and $\beta' X_t$ has no trend.

---

### Restricted Constant Term

To avoid the trend, we may restrict the constant term:
$$\mu = \alpha \rho_0'$$

It holds that $C \alpha = 0$, such that the accumulation vanishes:
$$C \sum_{i=1}^t \mu = C \sum_{i=1}^t \alpha \rho_0' = 0$$

We can write the model as:
$$\Delta X_t = \alpha \beta' X_{t-1} + \Gamma_1 \Delta X_{t-1} + \alpha \rho_0' + e_t$$
$$= \alpha \begin{pmatrix} \beta \\ \rho_0' \end{pmatrix}' \begin{pmatrix} X_{t-1} \\ 1 \end{pmatrix} + \Gamma_1 \Delta X_{t-1} + e_t$$

The constant is **restricted to the co-integration space**.

---

### Restricted Trend Term

For a case with a trend we can do the same and use the model with a restricted trend term:

$$\Delta X_t = \alpha \beta' X_{t-1} + \Gamma_1 \Delta X_{t-1} + \mu + \alpha \rho_1' t + e_t$$
$$= \alpha \begin{pmatrix} \beta \\ \rho_1' \end{pmatrix}' \begin{pmatrix} X_{t-1} \\ t \end{pmatrix} + \Gamma_1 \Delta X_{t-1} + \mu + e_t$$

This is parallel to considering the combined hypotheses in univariate unit root testing, e.g.
$$\Delta y_t = \pi y_{t-1} + \delta + e_t \quad \text{with} \quad H_0^*: \pi = \delta = 0$$

or in the case of a trend:
$$\Delta y_t = \pi y_{t-1} + \delta + \gamma t + e_t \quad \text{with} \quad H_0^*: \pi = \gamma = 0$$

---

### Critical Values for Different Deterministic Specifications

The different treatment of constant and trend changes the critical values.

**95 Percent Quantile**

| Model | p−r = 5 | p−r = 4 | p−r = 3 | p−r = 2 | p−r = 1 |
|-------|---------|---------|---------|---------|---------|
| Constant unrestricted (DF²) | 69.61 | 47.71 | 29.80 | 15.41 | 3.84 |
| Constant restricted (DF²_c) | 76.81 | 53.94 | 35.07 | 20.16 | 9.14 |
| Trend restricted (DF²_t) | 88.55 | 63.66 | 42.77 | 25.73 | 12.45 |

---

**End of Lecture**
