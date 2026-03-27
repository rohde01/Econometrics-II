# Vector Autoregressive Models
## Econometrics II
**Instructor:** Rasmus Søndergaard Pedersen

---

## Table of Contents
1. [Introduction: Single- vs. Multi-Equation Models](#introduction)
2. [VAR Models](#var-models)
3. [Stationarity Conditions](#stationarity-conditions)
4. [Conditioning and Single-Equation Models](#conditioning)
5. [Estimation and Inference](#estimation-inference)
6. [Impulse-Responses and Structural VAR Models](#impulse-responses)
7. [Forecasting](#forecasting)
8. [Granger Causality](#granger-causality)

---

## Introduction: Single- vs. Multi-Equation Models {#introduction}

### Conditional Models
Conditional models start from an assumed contemporaneous causality, e.g., **x_t ↝ y_t**.

**Autoregressive Distributed Lag (ADL) Model:**
```
y_t = δ + θy_{t-1} + φ₀x_t + φ₁x_{t-1} + η_t
```

### Vector Autoregressive Models
Vector autoregressive models consider **Z_t = (y_t, x_t)'** given the past:

```
⎡ y_t ⎤   ⎡ μ₁ ⎤   ⎡ Π₁₁ Π₁₂ ⎤ ⎡ y_{t-1} ⎤   ⎡ e₁ₜ ⎤
⎢     ⎥ = ⎢    ⎥ + ⎢       ⎥ ⎢       ⎥ + ⎢    ⎥
⎣ x_t ⎦   ⎣ μ₂ ⎦   ⎣ Π₂₁ Π₂₂ ⎦ ⎣ x_{t-1} ⎦   ⎣ e₂ₜ ⎦
```

Or more generally, allowing more lags:
```
Z_t = μ + Π₁Z_{t-1} + Π₂Z_{t-2} + ... + Π_kZ_{t-k} + e_t
```

---

## VAR Models {#var-models}

### The VAR(k) Model Definition

Let **Z_t = (z₁ₜ, ..., z_pₜ)' ∈ ℝᵖ** be a p-dimensional vector.

The **VAR(k)** model is defined as the p equations:
```
Z_t = μ + Π₁Z_{t-1} + Π₂Z_{t-2} + ... + Π_kZ_{t-k} + e_t,    t = 1, 2, ..., T
```

**Conditional on** the k initial values Z₀, Z₋₁, ..., Z₋₍ₖ₋₁₎

### Assumptions
For likelihood analysis, assume:
```
e_t | Z_{t-1}, Z_{t-2}, ... ~ N(0, Ω)
```

where e_t is serially uncorrelated and Ω is symmetric and positive definite.

### Model Parameters
- **Conditional mean parameters:** p + kp² parameters
- **Covariance matrix:** p(p+1)/2 parameters

Total: p + kp² + p(p+1)/2 parameters

### The Bivariate Case

For p = 2, Z_t = (y_t, x_t)' with k = 1:

```
⎡ y_t ⎤   ⎡ μ₁ ⎤   ⎡ Π₁₁ Π₁₂ ⎤ ⎡ y_{t-1} ⎤   ⎡ e₁ₜ ⎤
⎢    ⎥ = ⎢    ⎥ + ⎢        ⎥ ⎢        ⎥ + ⎢    ⎥
⎣ x_t ⎦   ⎣ μ₂ ⎦   ⎣ Π₂₁ Π₂₂ ⎦ ⎣ x_{t-1} ⎦   ⎣ e₂ₜ ⎦
```

Can also be written as two equations:
```
y_t = μ₁ + Π₁₁y_{t-1} + Π₁₂x_{t-1} + e₁ₜ
x_t = μ₂ + Π₂₁y_{t-1} + Π₂₂x_{t-1} + e₂ₜ
```

**Note:** e₁ₜ and e₂ₜ can be correlated:
```
Cov(e₁ₜ, e₂ₜ) = Ω₁₂
```

### Example: Danish Consumption

VAR(1) model for Danish quarterly data, 1974(2)-2017(3):

**Variables (yearly growth rates):**
- Δ₄cₜ = cₜ - cₜ₋₄ (consumption growth)
- Δ₄yₜ = yₜ - yₜ₋₄ (income growth)
- Δ₄wₜ = wₜ - wₜ₋₄ (wealth growth)

**Estimated model:**
```
⎡ Δ₄cₜ ⎤   ⎡ 0.0037 ⎤   ⎡  0.48   0.13   0.055 ⎤ ⎡ Δ₄c_{t-1} ⎤   ⎡ e₁ₜ ⎤
⎢ Δ₄yₜ ⎥ = ⎢ 0.0077 ⎥ + ⎢  0.097  0.40   0.0058⎥ ⎢ Δ₄y_{t-1} ⎥ + ⎢ e₂ₜ ⎥
⎣ Δ₄wₜ ⎦   ⎣ 0.0084 ⎦   ⎣ -0.80   0.28   0.95  ⎦ ⎣ Δ₄w_{t-1} ⎦   ⎣ e₃ₜ ⎦
```

**Residual correlations:**
```
⎡  1.000  0.228  0.180 ⎤
⎢  0.228  1.000  0.132 ⎥
⎣  0.180  0.132  1.000 ⎦
```

---

## Stationarity Conditions {#stationarity-conditions}

### MA Solution and Stationarity for VAR(1)

Consider the VAR(1) model:
```
Z_t = μ + Π₁Z_{t-1} + e_t,    with Z₀ given
```

By recursive substitution:
```
Z_t = (I_p + Π₁ + Π₁² + ... + Π₁^{t-1})μ 
      + e_t + Π₁e_{t-1} + Π₁²e_{t-2} + ... + Π₁^{t-1}e₁ + Π₁^t Z₀
```

The convergence depends on **matrix powers** Π₁, Π₁², Π₁³, etc.

The sequence converges (Π₁^k → 0 as k → ∞) if and only if **all eigenvalues of Π₁ satisfy |λᵢ| < 1**.

### Eigenvalue Decomposition

A p × p matrix Π₁ can be written using spectral decomposition:
```
Π₁ = VΛV⁻¹
```

where:
- **V = (v₁, ..., vᵢ, ..., vₚ)** contains eigenvectors
- **Λ = diag(λ₁, ..., λₚ)** contains eigenvalues

Then:
```
Π₁^k = VΛ^k V⁻¹
```

where Λ^k = diag(λ₁^k, ..., λₚ^k)

### Stationarity Condition for VAR(1)

**The VAR(1) model is stable (stationary) if all eigenvalues of Π₁ are inside the unit circle:**
```
|λᵢ| < 1  for all i = 1, 2, ..., p
```

When stationary, **Z_t is stationary and weakly dependent.**

### Example 1: Stable VAR

Consider:
```
⎡ z₁ₜ ⎤   ⎡ 0.7  0.1 ⎤ ⎡ z₁,ₜ₋₁ ⎤   ⎡ e₁ₜ ⎤
⎢      ⎥ = ⎢         ⎥ ⎢        ⎥ + ⎢    ⎥
⎣ z₂ₜ ⎦   ⎣ 0.3  0.8 ⎦ ⎣ z₂,ₜ₋₁ ⎦   ⎣ e₂ₜ ⎦
```

**Eigenvalue problem:**
```
|Π₁ - λᵢIₚ| = (0.7 - λᵢ)(0.8 - λᵢ) - 0.3 × 0.1
             = λᵢ² - 1.5λᵢ + 0.53 = 0
```

**Solutions:**
- λ₁ = 0.930 (with v₁ = (0.398, 0.907)')
- λ₂ = 0.570 (with v₂ = (0.609, -0.793)')

Since both |λᵢ| < 1, **the VAR is stable.** Z_t is a stationary process.

### Example 2: Unstable VAR

Consider the modified model:
```
⎡ z₁ₜ ⎤   ⎡ 0.7  0.1 ⎤ ⎡ z₁,ₜ₋₁ ⎤   ⎡ e₁ₜ ⎤
⎢      ⎥ = ⎢         ⎥ ⎢        ⎥ + ⎢    ⎥
⎣ z₂ₜ ⎦   ⎣ 0.3  0.9 ⎦ ⎣ z₂,ₜ₋₁ ⎦   ⎣ e₂ₜ ⎦
```

**Eigenvalue problem:**
```
λᵢ² - 1.6λᵢ + 0.6 = 0
```

**Solutions:**
- λ₁ = 1.0 (with v₁ = (0.316, 0.949)')
- λ₂ = 0.6 (with v₂ = (0.707, -0.707)')

Since λ₁ = 1.0 is on the unit circle, **the VAR is not stable.** Z_t is a **unit root process** (non-stationary).

### Stability for VAR(k)

To generalize, write the VAR(k) as a VAR(1):

For a VAR(3):
```
Z_t = μ + Π₁Z_{t-1} + Π₂Z_{t-2} + Π₃Z_{t-3} + e_t
```

Define **W_t = (Z_t', Z_{t-1}', Z_{t-2}')'** ∈ ℝ^{3p}

**Companion form:**
```
⎡ Z_t     ⎤   ⎡ μ ⎤   ⎡ Π₁  Π₂  Π₃ ⎤ ⎡ Z_{t-1}   ⎤   ⎡ e_t ⎤
⎢ Z_{t-1} ⎥ = ⎢ 0 ⎥ + ⎢ I_p  0   0  ⎥ ⎢ Z_{t-2}   ⎥ + ⎢  0  ⎥
⎣ Z_{t-2} ⎦   ⎣ 0 ⎦   ⎣ 0   I_p  0  ⎦ ⎣ Z_{t-3}   ⎦   ⎣  0  ⎦
```

This is a VAR(1) of dimension 3p. **The process is stable if all 3p eigenvalues of the companion matrix are inside the unit circle.**

### General Stability Result

The VAR(k) model has a **(pk × pk) companion matrix:**
```
Π̃₁ = ⎡ Π₁  Π₂  Π₃  ...  Π_k ⎤
      ⎢ I_p  0   0   ...   0   ⎥
      ⎢ 0   I_p  0   ...   0   ⎥
      ⎢  ⋮    ⋮   ⋮  ⋱    ⋮   ⎥
      ⎣ 0   ...  0   I_p  0   ⎦
```

**If all pk eigenvalues satisfy |λᵢ| < 1, then Z_t is stationary and weakly dependent.**

### MA Representation

Under stationarity:
```
Z_t = e_t + C₁e_{t-1} + C₂e_{t-2} + ... + C_{t-1}e₁ + C₀
```

where C₀ depends on the constant term and initial values, and {C₁, C₂, C₃, ...} converges to zero exponentially fast.

---

## Conditioning and Single-Equation Models {#conditioning}

### Joint Density Factorization

The VAR(k) model for Z_t = (y_t, x_t)' represents the Gaussian density:
```
f(y_t, x_t | I_{t-1}; θ)
```

where I_{t-1} = {y_{t-1}, x_{t-1}, ..., y_{t-k}, x_{t-k}} is the information set.

We can always **factorize the joint density:**
```
f(y_t, x_t | I_{t-1}; θ) = f(y_t | x_t, I_{t-1}; φ) × f(x_t | I_{t-1}; φ)
                            ┴─────────────────────────┬─────────────────────────┘
                              conditional density      marginal density
```

### Conditioning in a Multivariate Gaussian Distribution

For the bivariate normal:
```
⎡ x₁ ⎤     ⎡ μ₁ ⎤   ⎡ Ω₁₁ Ω₁₂ ⎤
⎢    ⎥ ~ N ⎢    ⎥ , ⎢        ⎥
⎣ x₂ ⎦     ⎣ μ₂ ⎦   ⎣ Ω₂₁ Ω₂₂ ⎦
```

The **conditional distribution is Gaussian:**
```
x₁ | x₂ ~ N(μ₁.₂, Ω₁.₂)
```

where:
```
μ₁.₂ = μ₁ + Ω₁₂Ω₂₂⁻¹(x₂ - μ₂) = (μ₁ - ωμ₂) + ωx₂

ω = Ω₁₂Ω₂₂⁻¹  (the OLS correction)

Ω₁.₂ = Ω₁₁ - Ω₁₂Ω₂₂⁻¹Ω₂₁
```

### Structural Form

Starting with:
```
⎡ x₁ ⎤   ⎡ μ₁ ⎤   ⎡ e₁ ⎤         ⎡ e₁ ⎤
⎢    ⎥ = ⎢    ⎥ + ⎢    ⎥,   with ⎢    ⎥ ~ N(0, Ω)
⎣ x₂ ⎦   ⎣ μ₂ ⎦   ⎣ e₂ ⎦         ⎣ e₂ ⎦
```

We can write in **structural form:**
```
⎡ 1  -ω ⎤ ⎡ x₁ ⎤   ⎡ μ₁ - ωμ₂ ⎤   ⎡ e₁ - ωe₂ ⎤
⎢       ⎥ ⎢    ⎥ = ⎢         ⎥ + ⎢         ⎥
⎣ 0   1 ⎦ ⎣ x₂ ⎦   ⎣    μ₂   ⎦   ⎣    e₂   ⎦
```

or equivalently:
```
⎡ x₁ ⎤   ⎡ μ₁.₂ ⎤   ⎡ u₁ ⎤
⎢    ⎥ = ⎢      ⎥ + ⎢    ⎥
⎣ x₂ ⎦   ⎣  μ₂  ⎦   ⎣ u₂ ⎦
```

where u₁ = e₁ - ωe₂ and u₂ = e₂ are **uncorrelated by construction.**

### The Autoregressive Distributed Lag (ADL) Model

For the Gaussian VAR, the **conditional density f(y_t | x_t, I_{t-1}; φ) is an ADL model.**

The **marginal density f(x_t | I_{t-1}; φ) is a VAR equation.**

Example with causal direction **x_t ↝ y_t:**
```
⎡ y_t ⎤   ⎡ ωx_t ⎤   ⎡ δ   ⎤   ⎡ θ₁  α₁   ⎤ ⎡ y_{t-1} ⎤   ⎡ u₁ₜ ⎤
⎢     ⎥ = ⎢      ⎥ + ⎢     ⎥ + ⎢        ⎥ ⎢       ⎥ + ⎢     ⎥
⎣ x_t ⎦   ⎣  0   ⎦   ⎣ μ₂  ⎦   ⎣ Π₂₁ Π₂₂ ⎦ ⎣ x_{t-1} ⎦   ⎣ u₂ₜ ⎦
```

We reinterpret covariance Ω₁₂ as a **causal regression effect:**
```
ω = Ω₁₂Ω₂₂⁻¹
```

**Based on postulated causal direction:** x_t ↝ y_t

⚠️ **Note:** The structural form is sometimes controversial. We could also use the opposite causal interpretation, y_t ↝ x_t.

### Empirical Example

Consider a VAR(2) for yearly growth: Z_t = (Δ₄cₜ, Δ₄yₜ)'

**Estimated covariance matrix:**
```
Ω̂ = ⎡ 4.7485   1.3810 ⎤ × 10⁻⁴
     ⎣ 1.3810   9.5685 ⎦
```

**OLS correction factor:**
```
ω̂ = Ω̂₁₂/Ω̂₂₂ = 1.3810/9.5685 = 0.14433
```

The ADL equation includes contemporaneous income in the consumption equation, showing that a 1% increase in income is associated with approximately 0.14% increase in consumption contemporaneously (after controlling for lagged values).

---

## Estimation and Inference {#estimation-inference}

### Maximum Likelihood Estimation

For the VAR(1) model, the log-likelihood function is:
```
log L(θ) = Σ log f(Z_t | Z_{t-1}; θ)
```

where θ = {μ, Π₁, Ω}.

**Multivariate Gaussian density:**
```
f(Z_t | Z_{t-1}; θ) = (2π)^{-p/2} |Ω|^{-1/2} exp(-1/2 e_t(θ)'Ω⁻¹e_t(θ))
```

with e_t(θ) = Z_t - μ - Π₁Z_{t-1}

**Log-likelihood:**
```
log L(θ) = -Tp/2 log(2π) - T/2 log|Ω| - 1/2 Σ e_t(θ)'Ω⁻¹e_t(θ)
```

**Key result:** The MLE is **identical to OLS**.

### Estimation for VAR(k)

For the VAR(k), write:
```
e_t(θ) = Z_t - μ - Π₁Z_{t-1} - ... - Π_kZ_{t-k} = Z_t - ΦZ̃_{t-1}
```

where:
- **Φ** (p × (1+pk)) = (μ, Π₁, ..., Π_k)
- **Z̃_{t-1}** ((1+pk) × 1) = (1, Z_{t-1}', ..., Z_{t-k}')'

**MLE (= OLS) estimators:**
```
Φ̂ = [Σ Z_t Z̃'_{t-1}] [Σ Z̃_{t-1}Z̃'_{t-1}]⁻¹

Ω̂ = 1/T Σ ê_t ê'_t
```

with ê_t = Z_t - Φ̂Z̃_{t-1}

**Important:** The coefficients of the jth equation are given by the jth row of Φ. Their estimates are equivalent to OLS estimates obtained by regressing the jth element of Z_t on Z̃_{t-1}.

### Inference

**Asymptotic distribution (under stationarity):**
```
√T vec((μ̂, Π̂₁, ..., Π̂_k) - (μ, Π₁, ..., Π_k)) →^d N(0, V)
```

where:
```
V = E(Z̃_{t-1}Z̃'_{t-1})⁻¹ ⊗ Ω    with Z̃_{t-1} = (1, Z'_{t-1}, ..., Z'_{t-k})'
```

**Results:**
- The MLE has a **Gaussian distribution**
- Test statistics have standard N(0,1) and χ²(·) distributions
- **Useful for lag length determination**
- Misspecification tests parallel AR models
- **"Robust" test statistics should be used in the presence of heteroskedasticity**

### Example of Robust Inference

**VAR(2) for US real GDP and S&P 500 returns (1990:1-2018:4)**

Results show:
- Standard and HCSE (Heteroskedasticity-Consistent Standard Error) estimates
- t-HCSE: Wald statistics using robust standard errors
- Key finding: Differences between standard and robust test statistics indicate heteroskedasticity in the residuals

---

## Impulse-Responses and Structural VAR Models {#impulse-responses}

### Impulse-Response Functions

Consider the reduced form VAR:
```
Z_t = μ + Π₁Z_{t-1} + Π₂Z_{t-2} + ... + Π_kZ_{t-k} + e_t,    e_t | I_{t-1} ~ N(0, Ω)
```

**Contemporaneous effects** are captured in Ω.

To interpret the coefficients {μ, Π₁, ..., Π_k}, use an **impulse-response analysis**.

We make a shock to e_t and look at dynamic propagation using the **MA representation:**
```
Z_t = e_t + C₁e_{t-1} + C₂e_{t-2} + ... + C_{t-1}e₁ + C₀
```

**Impulse-response derivatives:**
```
∂Z_t/∂e'_t = I_p

∂Z_{t+1}/∂e'_t = C₁

∂Z_{t+2}/∂e'_t = C₂

...
```

**Presented as p × p graphs** called impulse-response functions.

### Reduced Form IRFs Example

For the consumption-income model, the reduced form IRFs show:
- Response of consumption to own shocks (C₁₁): Rapidly decaying
- Response of income to consumption shocks (I₂₁): Small, with some lag structure
- Response of consumption to income shocks (C₁₂): Positive, peaks after several quarters
- Response of income to own shocks (I₂₂): Decays gradually

The uncertainty bands (shown as shaded areas) widen over longer horizons.

### Structural VAR Model

**Problem with reduced form:** The economic interpretation of a shock to e₁ₜ is problematic because historically e₁ₜ is correlated with e₂ₜ and e₃ₜ. The reduced form impulse-response neglects **contemporaneous effects.**

**Solution:** Use a structural form, e.g.:
```
⎡ 1    0    0  ⎤ ⎡ y_t  ⎤   ⎡ A₁₁ A₁₂ A₁₃ ⎤ ⎡ y_{t-1} ⎤   ⎡ u₁ₜ ⎤
⎢ ω₂₁  1    0  ⎥ ⎢ w_t  ⎥ = ⎢ A₂₁ A₂₂ A₂₃ ⎥ ⎢ w_{t-1} ⎥ + ⎢ u₂ₜ ⎥
⎣ ω₃₁ ω₃₂  1  ⎦ ⎣ c_t  ⎦   ⎣ A₃₁ A₃₂ A₃₃ ⎦ ⎣ c_{t-1} ⎦   ⎣ u₃ₜ ⎦
```

such that u₁ₜ, u₂ₜ, and u₃ₜ are **uncorrelated**.

**Equivalent representation:**
```
⎡ y_t  ⎤   ⎡      0      ⎤   ⎡ A₁₁ A₁₂ A₁₃ ⎤ ⎡ y_{t-1} ⎤   ⎡ u₁ₜ ⎤
⎢ w_t  ⎥ = ⎢ ω₂₁y_t      ⎥ + ⎢ A₂₁ A₂₂ A₂₃ ⎥ ⎢ w_{t-1} ⎥ + ⎢ u₂ₜ ⎥
⎣ c_t  ⎦   ⎣ ω₃₁y_t+ω₃₂w_t ⎦   ⎣ A₃₁ A₃₂ A₃₃ ⎦ ⎣ c_{t-1} ⎦   ⎣ u₃ₜ ⎦
```

**Orthogonalized impulse-responses require a causal ordering:**
```
y_t ↝ w_t  and  (y_t, w_t) ↝ c_t
```

### Structural vs. Reduced Form IRFs

The structural form IRFs differ from the reduced form by explicitly modeling the contemporaneous relationships. The structural ordering imposes:
- y_t affects w_t and c_t contemporaneously
- w_t affects c_t contemporaneously
- No feedback from w_t to y_t or from c_t to y_t and w_t in the same period

This results in **orthogonal shocks** that are more economically interpretable.

---

## Forecasting {#forecasting}

### Forecast Problem

Given the information set **I_T = {Z_T, Z_{T-1}, Z_{T-2}, ...}**, we want:
```
y_{T+h|T} = E(y_{T+h} | I_T)
```

This is similar to forecasts based on univariate autoregressive models.

### VAR(1) Forecasting

For the VAR(1) model:
```
Z_t = μ + Π₁Z_{t-1} + e_t,    t = 1, 2, ..., T
```

**One-step-ahead forecast:**
```
Z_{T+1|T} = E(Z_{T+1} | I_T) = E(μ + Π₁Z_T + e_{T+1} | I_T) = μ + Π₁Z_T
```

**Multi-step forecasts:**
```
Z_{T+2|T} = E(μ + Π₁Z_{T+1} + e_{T+2} | I_T) = μ + Π₁Z_{T+1|T}

Z_{T+3|T} = E(μ + Π₁Z_{T+2} + e_{T+3} | I_T) = μ + Π₁Z_{T+2|T}
```

where we use E(Z_{T+1} | I_T) = Z_{T+1|T}

### Forecast Error and Forecast Error Variance

**First period forecast error:**
```
η₁ = Z_{T+1} - Z_{T+1|T} = e_{T+1}
```

**Forecast error variance:**
```
FEV(1) = E(η₁η'₁ | I_T) = E(e_{T+1}e'_{T+1} | I_T) = Ω
```

**General forecast error:**
```
η_h = Z_{T+h} - Z_{T+h|T} = e_{T+h} + C₁e_{T+h-1} + C₂e_{T+h-2} + ... + C_{h-1}e_{T+1}
```

**Forecast error variances:**
```
FEV(1) = Ω

FEV(2) = Ω + C₁ΩC'₁

...

FEV(h) = Ω + C₁ΩC'₁ + C₂ΩC'₂ + ... + C_{h-1}ΩC'_{h-1}
```

### Forecast Example

For consumption and income (Danish quarterly data):
- Forecasts are generated using the estimated VAR(2) model
- Confidence bands reflect the increasing forecast error variance at longer horizons
- Both consumption and income grow over time with the forecast band width increasing
- The forecast mean approaches the steady-state growth rate as h → ∞

---

## Granger Causality {#granger-causality}

### Definition: Predictive Causality

**Clive Granger** suggested a specific notion of causality based on prediction.

For the bivariate case:

Let **η_h** be the forecast error obtained by forecasting y_{T+h} based on:
```
I_T = {y_T, x_T, y_{T-1}, x_{T-1}, ...}
```

Let **η̃_h** be the forecast error obtained by forecasting y_{T+h} based on only:
```
Ĩ_T = {y_T, y_{T-1}, ...}
```

**Definition:**

The series **x is said to be Granger causal for y** if for some forecasting horizon h > 0:
```
E(η²_h | I_T) < E(η̃²_h | I_T)
```

This means: **Including x in the information set reduces the forecast error variance of y.**

### Maintained Assumptions

1. **The cause comes prior to the effect** (temporal precedence)
2. **The causal variable is helpful in forecasting** (predictive power)

### Testing Granger Causality

For a bivariate VAR(k) model:
```
⎡ y_t ⎤   ⎡ A₁₁ A₁₂ ⎤ ⎡ y_{t-1} ⎤   ⎡ B₁₁ B₁₂ ⎤ ⎡ y_{t-2} ⎤   ⎡ μ₁ ⎤   ⎡ e₁ₜ ⎤
⎢     ⎥ = ⎢        ⎥ ⎢        ⎥ + ⎢        ⎥ ⎢        ⎥ + ⎢    ⎥ + ⎢    ⎥
⎣ x_t ⎦   ⎣ A₂₁ A₂₂ ⎦ ⎣ x_{t-1} ⎦   ⎣ B₂₁ B₂₂ ⎦ ⎣ x_{t-2} ⎦   ⎣ μ₂ ⎦   ⎣ e₂ₜ ⎦
```

**Hypothesis: No Granger causality from x to y**
```
H₀: x ↛ y  ⟺  A₁₂ = B₁₂ = 0
```

**Hypothesis: No Granger causality from y to x**
```
H₀: y ↛ x  ⟺  A₂₁ = B₂₁ = 0
```

**Test statistics:** LR or Wald statistics follow **χ²(2k)** under correct specification.

**Important note:** Granger causality tests tell you **nothing about contemporaneous causality** (captured by Ω).

### Empirical Example: GDP and Stock Returns

**VAR(2) for quarterly US real GDP growth and S&P 500 returns (1990:1-2018:4)**

**Test 1: Do returns Granger cause GDP growth?**
```
H₀: Ds_{-1}, Ds_{-2} excluded from GDP equation

Wald χ²(2) = 8.1145 [p-value = 0.0173]*
HCSE χ²(2) = 8.8611 [p-value = 0.0119]*
```

**Result:** We **REJECT** the null. Stock market returns DO Granger cause GDP growth.

**Test 2: Does GDP growth Granger cause returns?**
```
H₀: Dy_{-1}, Dy_{-2} excluded from returns equation

Wald χ²(2) = 1.7246 [p-value = 0.4222]
HCSE χ²(2) = 1.3365 [p-value = 0.5126]
```

**Result:** We **CANNOT REJECT** the null. GDP growth does NOT Granger cause returns.

**Economic interpretation:** Stock market movements help predict future GDP growth, but GDP growth does not help predict future stock returns. This is consistent with the view that financial markets are forward-looking and incorporate information about future economic growth.

---

## Key Formulas Summary

### VAR(k) Model
```
Z_t = μ + Π₁Z_{t-1} + Π₂Z_{t-2} + ... + Π_kZ_{t-k} + e_t
```

### Stationarity Condition
```
All eigenvalues of companion matrix must satisfy |λᵢ| < 1
```

### MA Representation
```
Z_t = e_t + C₁e_{t-1} + C₂e_{t-2} + ...
```

### OLS Estimator
```
Φ̂ = [Σ Z_t Z̃'_{t-1}] [Σ Z̃_{t-1}Z̃'_{t-1}]⁻¹
```

### Forecast
```
Z_{T+h|T} = μ + Π₁Z_{T+h-1|T}
```

### Forecast Error Variance
```
FEV(h) = Ω + Σ C_jΩC'_j  for j=1 to h-1
```

### Granger Causality Test
```
x ↛ y: A₁₂ = B₁₂ = ... = 0
```

---

## References and Further Reading

- Pedersen, R. S. (2026). Vector Autoregressive Models. Lecture notes, Econometrics II course.
- Data files referenced: DataForVARSlides.xlsx, GDP_StockMarket.xlsx
- All empirical examples use quarterly economic data from Denmark and the United States

---

*Last updated: Based on Econometrics II lecture slides, Spring 2026*
