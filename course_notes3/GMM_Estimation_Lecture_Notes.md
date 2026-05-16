# Generalized Method of Moments (GMM) Estimation

**Econometrics II**  
Rasmus Søndergaard Pedersen

---

## Table of Contents

1. Introduction
2. Method of Moments (MM) Estimation
3. Generalized Method of Moments (GMM) Estimation
4. Efficient GMM
5. Weight Matrix Estimation
6. Examples: C-CAPM and 2SLS
7. Comparison with Maximum Likelihood

---

## 1. Introduction

### Overview

Generalized method of moments is a general estimation principle. Estimators are derived from moment conditions.

### Three Main Motivations

1. **Unifying Framework**: Many estimators can be seen as special cases of GMM (MM, OLS, IV, 2SLS, GIVE, ML).

2. **Alternative to ML**: ML estimators have the smallest variance in the class of consistent and asymptotically normal estimators. However, we need a full description of the DGP and correct specification. GMM is an alternative based on minimal assumptions.

3. **Partial Specification**: GMM estimation is possible where likelihood analysis is difficult. We only need a partial specification of the model. Example: Forward-looking models under rational expectations.

---

## 2. Method of Moments (MM) Estimation

### Moment Conditions and Identification

A **moment condition** is a statement involving data and parameters:

$$g(\theta_0) = E(f(w_t, z_t, \theta_0)) = 0$$

where:
- $\theta$ is a $K \times 1$ vector of parameters with true value $\theta_0$
- $f(\cdot)$ is an $R \times 1$ vector of (non-linear) functions
- $w_t$ contains model variables
- $z_t$ contains instruments

If we could evaluate the expectation, we could in principle solve the equations and find $\theta_0$. If there is a unique solution such that $E(f(w_t, z_t, \theta)) = 0$ if and only if $\theta = \theta_0$, then the system is **identified**.

### Identification Levels

**Formal Identification**: Is the model constructed such that $\theta_0$ is unique?

**Empirical Identification**: Are the data informative enough?

### Models with Instrumental Variables

In many applications, the moment condition has the specific form:

$$f(w_t, z_t, \theta) = z_t \cdot u(w_t, \theta)$$

where the $R$ instruments in $z_t$ are multiplied by $u(w_t, \theta)$ (the error term equivalent). The moment condition becomes:

$$g(\theta_0) = E[z_t u(w_t, \theta_0)] = 0$$

The instruments are uncorrelated with the error term. This class is referred to as **instrumental variables estimators**. The function $u(w_t, \theta)$ may be linear or non-linear in $\theta$.

### The MM Estimator

We cannot evaluate $E(\cdot)$, which is a complicated integral. For a sample $w_t$ and $z_t$ for $t = 1, 2, \ldots, T$, we replace with sample averages to obtain the sample moments:

$$g_T(\theta) = \frac{1}{T} \sum_{t=1}^{T} f(w_t, z_t, \theta)$$

We can try to derive an estimator $\hat{\theta}$ from the condition:

$$g_T(\hat{\theta}) = 0$$

To find a unique estimator, we need as many equations as parameters. The **order condition** for identification is $R \geq K$.

- $R = K$ is called **exact identification**. The solution to the condition is the MM estimator, $\hat{\theta}_{MM}$.
- $R > K$ is called **over-identification**. Because of randomness from estimation, the condition does not hold. We define a minimization problem to find the GMM estimator, $\hat{\theta}_{GMM}$.

### Example: MM Estimator of the Mean

Assume $y_t$ is a random variable drawn from a population with expectation $\mu_0$, such that $E(y_t) = \mu_0$.

We write the single moment condition:

$$g(\mu_0) = E[f(y_t, \mu_0)] = E(y_t - \mu_0) = 0$$

where $f(y_t, \mu_0) = y_t - \mu_0$.

For a sample $\{y_t\}_{t=1}^T$, we have the sample moment condition:

$$g_T(\hat{\mu}) = \frac{1}{T} \sum_{t=1}^{T} (y_t - \hat{\mu}) = 0$$

The MM estimator of the mean $\mu_0$ is the solution:

$$\hat{\mu}_{MM} = \frac{1}{T} \sum_{t=1}^{T} y_t$$

### Example: OLS as a MM Estimator

Consider the linear regression model of $y_t$ on $x_t$ ($K \times 1$):

$$y_t = x_t' \beta_0 + e_t$$

Assume the model represents the conditional expectation:

$$E(y_t | x_t) = x_t' \beta_0$$

so that $E(e_t | x_t) = 0$.

The model variables and instruments are $w_t = (y_t, x_t')$ and $z_t = x_t$, such that:

$$f(w_t, z_t, \beta) = x_t(y_t - x_t' \beta)$$

This implies the $K$ unconditional moment conditions:

$$g(\beta_0) = E(f(w_t, z_t, \beta_0)) = E(x_t(y_t - x_t' \beta_0)) = E(x_t e_t) = 0$$

which we recognize as the minimal assumption for consistency of the OLS estimator.

We define the corresponding sample moment conditions:

$$g_T(\hat{\beta}) = \frac{1}{T} \sum_{t=1}^{T} f(w_t, z_t, \hat{\beta}) = \frac{1}{T} \sum_{t=1}^{T} x_t(y_t - x_t' \hat{\beta}) = \frac{1}{T} \sum_{t=1}^{T} x_t y_t - \frac{1}{T} \sum_{t=1}^{T} x_t x_t' \hat{\beta} = 0$$

The MM estimator is derived as the unique solution:

$$\hat{\beta}_{MM} = \left(\frac{1}{T} \sum_{t=1}^{T} x_t x_t'\right)^{-1} \frac{1}{T} \sum_{t=1}^{T} x_t y_t$$

provided that $\frac{1}{T} \sum_{t=1}^{T} x_t x_t'$ is non-singular.

Method of moments is one way to motivate the OLS estimator and highlights the minimal (or identifying) assumptions for OLS.

### Example: Under-Identification

Consider again a regression model:

$$y_t = x_t' \beta_0 + e_t = x_{1t}' \gamma_0 + x_{2t}' \delta_0 + e_t$$

Assume that the $K_1$ variables in $x_{1t}$ are predetermined, while the $K_2 = K - K_1$ variables in $x_{2t}$ are endogenous:

$$E(x_{1t} e_t) = 0 \quad (K_1 \times 1)$$
$$E(x_{2t} e_t) \neq 0 \quad (K_2 \times 1)$$

We have $K$ parameters in $\beta_0 = (\gamma_0', \delta_0')'$, but only $K_1 < K$ moment conditions (i.e., $K_1$ equations to determine $K$ unknowns).

**The parameters are not identified and cannot be estimated consistently.**

### Example: Simple IV Estimator

Assume $K_2$ new variables, $z_{2t}$, that are correlated with $x_{2t}$ but uncorrelated with $e_t$:

$$E(z_{2t} e_t) = 0$$

The $K_2$ moment conditions can replace the problematic condition.

To simplify notation, we define:

$$x_t = \begin{pmatrix} x_{1t} \\ x_{2t} \end{pmatrix}, \quad z_t = \begin{pmatrix} x_{1t} \\ z_{2t} \end{pmatrix}$$

Here:
1. $w_t = (y_t, x_t')' = (y_t, (x_{1t}', x_{2t}'))'$ are model variables
2. $z_{2t}$ are new instruments
3. $z_t = (x_{1t}', z_{2t}')'$ are instruments

We say that the variables $x_{1t}$ are instruments for themselves.

Using both conditions, we have $K$ moment conditions:

$$g(\beta_0) = \begin{pmatrix} E(x_{1t} e_t) \\ E(z_{2t} e_t) \end{pmatrix} = E(z_t e_t) = E(z_t(y_t - x_t' \beta_0)) = 0$$

which are sufficient to identify the $K$ parameters in $\beta$.

The corresponding sample moment conditions are given by:

$$g_T(\hat{\beta}) = \frac{1}{T} \sum_{t=1}^{T} z_t(y_t - x_t' \hat{\beta}) = 0$$

The method of moments estimator is the unique solution:

$$\hat{\beta}_{MM} = \left(\frac{1}{T} \sum_{t=1}^{T} z_t x_t'\right)^{-1} \frac{1}{T} \sum_{t=1}^{T} z_t y_t$$

provided that the $K \times K$ matrix $\frac{1}{T} \sum_{t=1}^{T} z_t x_t'$ is non-singular.

### Notes on the IV Example

1. We need the instruments in $z_t$ to identify the parameters.
2. The MM estimator coincides with the simple IV estimator.
3. Non-singularity of $\sum_{t=1}^{T} z_t x_t'$ requires relevant instruments. If $z_{2t}$ is uncorrelated with $x_{2t}$, the matrix is singular.
4. The MM procedure only works with $K_2$ new instruments. If $R > K$, the matrix $\sum_{t=1}^{T} z_t x_t'$ is not a square matrix, and hence not invertible.

---

## 3. Generalized Method of Moments (GMM) Estimation

### The GMM Framework

Recall the moment condition:

$$g(\theta_0) = E(f(w_t, z_t, \theta_0)) = 0$$

with parameters $\theta$ ($K \times 1$) and $f(\cdot)$ is an $R \times 1$ vector of functions.

The case $R > K$ is called **over-identification**. Note that this is a fortunate situation—not a problem!

More equations than parameters means no solution to $g_T(\theta) = 0$ in general. Recall that in general:

$$g(\theta_0) = 0, \quad \text{while} \quad g_T(\theta_0) = \frac{1}{T} \sum_{t=1}^{T} f(w_t, z_t, \theta_0) \neq 0$$

Instead, we **minimize the distance from $g_T(\theta)$ to zero**. The distance is measured by the quadratic form:

$$Q_T(\theta) = g_T(\theta)' W_T g_T(\theta)$$

where $W_T$ is an $R \times R$ symmetric and positive definite **weight matrix**.

The GMM estimator depends on the weight matrix:

$$\hat{\theta}_{GMM}(W_T) = \arg \min_{\theta} \{g_T(\theta)' W_T g_T(\theta)\}$$

We can find the estimator by solving the $K$ equations:

$$\frac{\partial Q_T(\theta)}{\partial \theta} = \frac{\partial(g_T(\theta)' W_T g_T(\theta))}{\partial \theta} = 0 \quad (K \times 1)$$

Sometimes analytically but often by numerical methods.

### Distances and Weight Matrices

Consider a simple example with $R = 3$ moment conditions:

$$g_T(\theta) = \begin{pmatrix} g_1 \\ g_2 \\ g_3 \end{pmatrix} = \begin{pmatrix} \frac{1}{T} \sum_{t=1}^{T} z_{1t}(y_t - x_t' \theta) \\ \frac{1}{T} \sum_{t=1}^{T} z_{2t}(y_t - x_t' \theta) \\ \frac{1}{T} \sum_{t=1}^{T} z_{3t}(y_t - x_t' \theta) \end{pmatrix}$$

**First**, consider a simple weight matrix, $W_T = I_3$:

$$Q_T(\theta) = (g_1 \; g_2 \; g_3) \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} g_1 \\ g_2 \\ g_3 \end{pmatrix} = g_1^2 + g_2^2 + g_3^2$$

which is the sum of squares; the coordinates are equally important.

**Second**, look at a different weight matrix:

$$Q_T(\theta) = (g_1 \; g_2 \; g_3) \begin{pmatrix} 4 & 0 & 0 \\ 0 & 2 & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} g_1 \\ g_2 \\ g_3 \end{pmatrix} = 4g_1^2 + 2g_2^2 + g_3^2$$

which attaches more weight to the first moments.

**Finally**, consider a non-diagonal weight matrix:

$$Q_T(\theta) = (g_1 \; g_2 \; g_3) \begin{pmatrix} 1 & 0.5 & 0 \\ 0.5 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} g_1 \\ g_2 \\ g_3 \end{pmatrix} = g_1^2 + g_2^2 + g_1 g_2 + g_3^2$$

The cross product, $g_1 g_2$, adjusts for covariance between $g_1$ and $g_2$.

### Consistency of GMM

Assume that a law of large numbers (LLN) applies to $f(w_t, z_t, \theta)$, i.e.:

$$T^{-1} \sum_{t=1}^{T} f(w_t, z_t, \theta) \xrightarrow{p} E(f(w_t, z_t, \theta)) \quad \text{for} \quad T \to \infty$$

Typically implied by i.i.d. or stationarity + weak dependence.

**If the moment conditions hold, $g(\theta_0) = 0$, then GMM is consistent:**

$$\hat{\theta}_{GMM}(W_T) \xrightarrow{p} \theta_0 \quad \text{as} \quad T \to \infty$$

for any $W_T$ positive definite.

If a LLN applies, then $g_T(\theta_0)$ converges to $g(\theta_0)$. Since $\hat{\theta}_{GMM}(W_T)$ minimizes the distance from $g_T(\theta)$ to zero, it will be a consistent estimator of the solution to $g(\theta_0) = 0$.

The weight matrix $W_T$ has to be positive definite, so that we put a positive and non-zero weight on all moment conditions.

### Asymptotic Distribution of GMM

Assume a central limit theorem for $f(w_t, z_t, \theta_0)$, i.e.:

$$\sqrt{T} \cdot g_T(\theta_0) = \frac{1}{\sqrt{T}} \sum_{t=1}^{T} f(w_t, z_t, \theta_0) \xrightarrow{d} N(0, S)$$

Then it holds that for any positive definite weight matrix $W_T$, with $\text{plim}_{T \to \infty} W_T = W$, the asymptotic distribution of the GMM estimator is given by:

$$\sqrt{T}(\hat{\theta}_{GMM} - \theta_0) \xrightarrow{d} N(0, V)$$

The asymptotic variance is given by:

$$V = (D' W D)^{-1} D' W S W D (D' W D)^{-1}$$

where:

$$D = E\left(\frac{\partial f(w_t, z_t, \theta)}{\partial \theta'}\bigg|_{\theta=\theta_0}\right)$$

is the expected value of the $R \times K$ matrix of first derivatives.

---

## 4. Efficient GMM

### The Efficient Weight Matrix

The variance of $\hat{\theta}_{GMM}$ depends on the weight matrix $W_T$. The **efficient GMM estimator** has the smallest asymptotic variance.

**Intuition**: A moment with small variance should have large weight. The **optimal weight matrix**, $W_T^{opt}$, has the property that:

$$\text{plim}_{T \to \infty} W_T^{opt} = S^{-1}$$

With $W = S^{-1}$, the asymptotic variance simplifies to:

$$V = (D' S^{-1} D)^{-1} D' S^{-1} S S^{-1} D (D' S^{-1} D)^{-1} = (D' S^{-1} D)^{-1}$$

With $W_T = S^{-1}$, the criterion function corresponds to a Wald statistic for $g(\hat{\theta}) = 0$:

$$T \cdot Q_T(\hat{\theta}) = T \cdot g_T(\hat{\theta})' S^{-1} g_T(\hat{\theta}) \approx g_T(\hat{\theta})' V(g_T(\hat{\theta}))^{-1} g_T(\hat{\theta})$$

### Properties of Good Moment Conditions

The best moment conditions have small $S$ and large $D$.

- A **small $S$** means that the sample variation of the moment is small. The noise-level is low.
- A **large $D$** means that the moment condition is "much" violated if $\theta \neq \theta_0$. The moment is very informative on the true values $\theta_0$. Related to the curvature of the criteria function as in ML.

### Weight Matrix Example

Consider again the case:

$$g_T(\theta) = \begin{pmatrix} g_1 \\ g_2 \\ g_3 \end{pmatrix}$$

with:

$$S = V(\sqrt{T} \cdot g_T(\theta_0)) = T \begin{pmatrix} V(g_1) & \text{cov}(g_1, g_2) & \text{cov}(g_1, g_3) \\ \text{cov}(g_1, g_2) & V(g_2) & \text{cov}(g_2, g_3) \\ \text{cov}(g_1, g_3) & \text{cov}(g_2, g_3) & V(g_3) \end{pmatrix} = \begin{pmatrix} 2 & 0.8 & 0 \\ 0.8 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

The optimal weight is:

$$W^{opt} = S^{-1} = \begin{pmatrix} 0.735 & -0.588 & 0 \\ -0.588 & 1.471 & 0 \\ 0 & 0 & 1.0 \end{pmatrix}$$

such that:

$$Q_T(\theta) = (g_1 \; g_2 \; g_3) \begin{pmatrix} 0.735 & -0.588 & 0 \\ -0.588 & 1.471 & 0 \\ 0 & 0 & 1.0 \end{pmatrix} \begin{pmatrix} g_1 \\ g_2 \\ g_3 \end{pmatrix} = 0.735 \cdot g_1^2 + 1.471 \cdot g_2^2 - 1.176 \cdot g_1 g_2 + g_3^2$$

**Observations:**

1. Higher variance gives lower weight.
2. Weights adjust for the covariance. Positively correlated moments are downweighted.

### Hypothesis Testing

Hypothesis testing can be based on the asymptotic distribution:

$$\hat{\theta}_{GMM} \xrightarrow{a} N(\theta_0, T^{-1} \hat{V})$$

An estimator of the asymptotic variance is given by:

$$\hat{V} = (D_T' S_T^{-1} D_T)^{-1}$$

1. $D = E(\partial f(\cdot) / \partial \theta')$, which we can estimate by the average:

$$D_T \underbrace{(R \times K)}_{} = \frac{1}{T} \sum_{t=1}^{T} \frac{\partial f(w_t, z_t, \theta)}{\partial \theta'}\bigg|_{\theta=\hat{\theta}} = \frac{\partial g_T(\hat{\theta})}{\partial \theta'}$$

2. $S = T \cdot V(g_T(\theta_0))$. If observations are independent, an estimator is:

$$S_T = \frac{1}{T} \sum_{t=1}^{T} f(w_t, z_t, \hat{\theta}) f(w_t, z_t, \hat{\theta})'$$

**Estimation of $W_T$ is typically the most tricky part of GMM.**

---

## 5. Computational Issues

### Two-Step Efficient GMM

Recall that $W^{opt} = S^{-1}$, but that depends on the parameters!

**Two-step efficient GMM:**

1. Choose an initial weight matrix, e.g., $W_{[1]} = I_R$, and find a consistent but inefficient first-step GMM estimator:

$$\hat{\theta}_{[1]} = \arg \min_{\theta} g_T(\theta)' W_{[1]} g_T(\theta)$$

2. Find the optimal weight, $W_{[2]}^{opt}$, based on $\hat{\theta}_{[1]}$, and update:

$$\hat{\theta}_{[2]} = \arg \min_{\theta} g_T(\theta)' W_{[2]}^{opt} g_T(\theta)$$

The estimator is not unique as it depends on the initial weight matrix $W_{[1]}$.

### Iterated GMM Estimator

From $\hat{\theta}_{[2]}$ it is natural to update the weights, $W_{[3]}^{opt}$, and update $\hat{\theta}_{[3]}$. We can iterate between $W_{[\cdot]}^{opt}$ and $\hat{\theta}_{[\cdot]}$ until convergence.

**Iterated GMM does not depend on the initial weight matrix.** The two approaches are asymptotically equivalent.

### Continuously Updated GMM Estimator

A third approach is to recognize from the outset that the weight matrix depends on the parameters, and minimize:

$$Q_T(\theta) = g_T(\theta)' W_T(\theta) g_T(\theta)$$

That is never possible to solve analytically.

---

## 6. Test for Overidentifying Moment Conditions

### Hansen's J-Test

Recall that $K$ moment conditions are sufficient to estimate $\theta$. If $R > K$, we can test the validity of the $R - K$ conditions.

By MM estimation we can set $K$ moment conditions equal to zero. If all $R$ conditions are valid then the $R - K$ moments should also be close to zero.

From CLT we have:

$$g_T(\theta_0) \xrightarrow{a} N(0, T^{-1} S)$$

If we use the optimal weights, $W_T^{opt} \xrightarrow{p} S^{-1}$, then:

$$\xi_J = T \cdot g_T(\hat{\theta}_{GMM})' W_T^{opt} g_T(\hat{\theta}_{GMM}) = T \cdot Q_T(\hat{\theta}_{GMM}) \xrightarrow{d} \chi^2(R - K)$$

This is the **J-test** or the **Hansen test** for overidentifying restrictions.

### Interpreting the J-Test

In linear models, the J-test is referred to as the **Sargan test**.

$\xi_J$ is **not a test of the validity of the model.** $\xi_J$ considers whether the $R - K$ moments are in line with the $K$ identifying moments.

We **cannot see from $\xi_J$ which moments cause rejection.** We may try to remove some moment conditions, reestimate and reconsider the statistic. If the second estimation is based on $R_1 < R$ conditions, with $R_1 \geq K$, then the difference in the J-statistic is $\chi^2(R - R_1)$.

Both estimations are based on same $S_T$.

---

## 7. Weight Matrix Estimation

### Univariate Case: Heteroskedasticity Consistent Covariance

The optimal weight is $W_T^{opt} = S_T^{-1}$ where $S_T$ is an estimator of:

$$S = \lim_{T \to \infty} V(\sqrt{T} \cdot g_T(\theta_0)) = \lim_{T \to \infty} \frac{1}{T} \cdot V\left(\sum_{t=1}^{T} f_t\right)$$

where $f_t = f(w_t, z_t, \theta_0)$.

If $f_t$ and $f_s$ are uncorrelated, then the variance of the sum is the sum of the variances:

$$\frac{1}{T} \cdot V\left(\sum_{t=1}^{T} f_t\right) = \frac{1}{T} \sum_{t=1}^{T} V(f_t) = \frac{1}{T} \sum_{t=1}^{T} E(f_t^2)$$

A natural estimator is:

$$S_T = \frac{1}{T} \sum_{t=1}^{T} f_t^2 \quad (*)$$

This is robust to heteroskedasticity and is referred to as the **heteroskedasticity consistent (HC) covariance estimator**.

### Accounting for Autocorrelation

If $f_t$ and $f_s$ are correlated, the variance includes the covariances:

$$S = \frac{1}{T} \cdot V\left(\sum_{t=1}^{T} f_t\right) = T^{-1} E[(f_1 + f_2 + \ldots + f_T)(f_1 + f_2 + \ldots + f_T)']$$

$$= T^{-1} \{E(f_1^2) + E(f_1 f_2') + \ldots + E(f_1 f_T') + E(f_2 f_1') + E(f_2^2) + \ldots + E(f_2 f_T') + \ldots + E(f_T f_1') + \ldots + E(f_T^2)\}$$

Defining the autocovariances of the moments as:

$$\gamma_j = \frac{1}{T} \sum_{t=j+1}^{T} E(f_t f_{t-j}')$$

we can write $S$ as:

$$S = \gamma_0 + 2 \gamma_1 + 2 \gamma_2 + 2 \gamma_3 + \ldots + 2 \gamma_{T-1} = \gamma_0 + \sum_{j=1}^{T-1} 2 \gamma_j$$

which is known as the **long-run variance**.

### Kernel Estimators

A more general trick is to use a weight $w_j \to 0$ on covariance $j$. This class of so-called **kernel estimators** can be written as:

$$S_T = \hat{\gamma}_0 + \sum_{j=1}^{T-1} w_j \cdot 2 \hat{\gamma}_j$$

where $w_j$ is a kernel weight depending on the lag $j$ and a **bandwidth parameter**, $q > 0$.

The **Bartlett kernel** (Newey-West estimator) uses:

$$w_j = k(j, q) = \begin{cases} 1 - |j|/q & \text{for} \; |j| < q \\ 0 & \text{for} \; |j| \geq q \end{cases}, \quad j \in \mathbb{Z}$$

Allows $q - 1$ lags to enter.

---

## 8. Examples

### Example 1: The Consumption-Based Capital Asset Pricing (C-CAPM) Model

#### Setup

Consider the consumption-based capital asset pricing (C-CAPM) model of Hansen and Singleton (1982).

A representative agent maximizes the discounted value of lifetime utility subject to a budget constraint:

$$\max \sum_{s=1}^{\infty} E(\delta^s \cdot u(c_{t+s}) | \mathcal{I}_t)$$

$$A_{t+1} = (1 + r_{t+1}) A_t + y_{t+1} - c_{t+1}$$

where $A_t$ is financial wealth, $y_t$ is income, $0 \leq \delta \leq 1$ is a discount factor, and $\mathcal{I}_t$ is the information set at time $t$.

The first order condition is given by the **Euler equation**:

$$u'(c_t) = E[\delta \cdot u'(c_{t+1}) \cdot R_{t+1} | \mathcal{I}_t]$$

where $u'(\cdot)$ is the derivative and $R_{t+1} = 1 + r_{t+1}$ is the return factor.

#### Utility Function and Parameterization

Assume a constant relative risk aversion (CRRA) utility function:

$$u(c_t) = \frac{c_t^{1-\gamma}}{1 - \gamma}, \quad \gamma < 1$$

so that $u'(c_t) = c_t^{-\gamma}$. This gives the explicit Euler equation:

$$c_t^{-\gamma} - E[\delta \cdot c_{t+1}^{-\gamma} \cdot R_{t+1} | \mathcal{I}_t] = 0$$

To ensure stationarity, we reformulate:

$$E\left(\delta \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma} R_{t+1} - 1 \bigg| \mathcal{I}_t\right) = 0$$

which is a conditional moment condition.

This implies the unconditional moment conditions:

$$g(\delta_0, \gamma_0) = E\left[\left(\delta_0 \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma_0} R_{t+1} - 1\right) z_t\right] = 0$$

for all variables $z_t \in \mathcal{I}_t$ included in the formation set.

#### Estimation

To estimate the parameters, $\theta = (\delta, \gamma)'$, we need at least $R = 2$ instruments in $z_t$. We try with $R = 3$ instruments:

$$z_t = \left(1, \frac{c_t}{c_{t-1}}, R_t\right)'$$

With $w_t = \left(\frac{c_{t+1}}{c_t}, R_{t+1}\right)'$ the model variables, we have the moment conditions:

$$E[u(w_t, \theta_0) z_t] = 0$$

where:

$$u(w_t, \theta) = \delta \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma} R_{t+1} - 1$$

This gives three moment conditions for $t = 1, 2, \ldots, T$:

$$E\left[\left(\delta_0 \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma_0} R_{t+1} - 1\right) \cdot 1\right] = 0$$

$$E\left[\left(\delta_0 \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma_0} R_{t+1} - 1\right) \left(\frac{c_t}{c_{t-1}}\right)\right] = 0$$

$$E\left[\left(\delta_0 \left(\frac{c_{t+1}}{c_t}\right)^{-\gamma_0} R_{t+1} - 1\right) R_t\right] = 0$$

#### Results

Results for US data, 1959:3–1978:12 show that the model is formally identified but $\gamma$ is poorly determined. This raises questions about:

- Weak instruments?
- Little variation in the data?
- Or wrong model?

### Example 2: Two-Stage Least Squares (2SLS)

#### Setup

Consider again a regression model:

$$y_t = x_t' \beta_0 + e_t = x_{1t}' \gamma_0 + x_{2t}' \delta_0 + e_t$$

where $E(x_{1t} e_t) = 0$ and $E(x_{2t} e_t) \neq 0$. Assume that you have $R > K$ valid instruments in $z_t$:

$$g(\beta_0) = E(z_t e_t) = E(z_t(y_t - x_t' \beta_0)) = 0$$

#### Derivation as GMM

The corresponding sample moments are given by:

$$g_T(\beta) \underbrace{(R \times 1)}_{} = \frac{1}{T} \sum_{t=1}^{T} z_t(y_t - x_t' \beta) = \frac{1}{T} Z'(Y - X\beta)$$

where $Y$ ($T \times 1$), $X$ ($T \times K$), and $Z$ ($T \times R$) are matrices.

We cannot solve $g_T(\beta) = 0$ directly; $Z'X$ is $R \times K$ and not invertible.

Instead, derive the GMM estimator by minimizing the criteria function:

$$Q_T(\beta) = g_T(\beta)' W_T g_T(\beta) = (T^{-1} Z'(Y - X\beta))' W_T (T^{-1} Z'(Y - X\beta))$$

$$= T^{-2}(Y'Z W_T Z'Y - 2\beta' X'Z W_T Z'Y + \beta' X'Z W_T Z'X\beta)$$

We take the first derivative, and the GMM estimator is the solution to:

$$\frac{\partial Q_T(\beta)}{\partial \beta} = -2T^{-2} X'Z W_T Z'Y + 2T^{-2} X'Z W_T Z'X\beta = 0$$

Find:

$$\hat{\beta}_{GMM}(W_T) = (X'Z W_T Z'X)^{-1} X'Z W_T Z'Y$$

depending on $W_T$.

#### Optimal Weight Matrix

The optimal weight matrix, $W_T^{opt} = S_T^{-1}$, is:

$$S_T = \frac{1}{T} \sum_{t=1}^{T} f(w_t, z_t, \theta) f(w_t, z_t, \theta)' = \frac{1}{T} \sum_{t=1}^{T} \hat{e}_t^2 z_t z_t'$$

which allows for general heteroskedasticity of the disturbance term.

#### Asymptotic Distribution and Connection to 2SLS

For the asymptotic distributions, recall that:

$$\hat{\beta}_{GMM} \xrightarrow{a} N\left(\beta_0, T^{-1}(D' S^{-1} D)^{-1}\right)$$

The derivative is given by:

$$D_T \underbrace{(R \times K)}_{} = \frac{\partial g_T(\beta)}{\partial \beta'} = \frac{\partial(T^{-1} \sum_{t=1}^{T} z_t(y_t - x_t' \beta))}{\partial \beta'} = -T^{-1} \sum_{t=1}^{T} z_t x_t'$$

so the variance of the estimator becomes:

$$V(\hat{\beta}_{GMM}) = T^{-1} (D_T' W_T^{opt} D_T)^{-1}$$

$$= T^{-1} \left(\left(-T^{-1} \sum_{t=1}^{T} x_t z_t'\right) \left(T^{-1} \sum_{t=1}^{T} \hat{e}_t^2 z_t z_t'\right)^{-1} \left(-T^{-1} \sum_{t=1}^{T} z_t x_t'\right)\right)^{-1}$$

$$= \left(\sum_{t=1}^{T} x_t z_t'\right)^{-1} \sum_{t=1}^{T} \hat{e}_t^2 z_t z_t' \left(\sum_{t=1}^{T} z_t x_t'\right)^{-1}$$

This is the **heteroskedasticity consistent (HC) variance** (White). **GMM with allowance for heteroskedastic errors automatically produces heteroskedasticity consistent standard errors!**

#### Connection to 2SLS under Homoskedasticity

If the error terms are assumed i.i.d., the weight matrix simplifies:

$$S_T = \frac{\hat{\sigma}^2}{T} \sum_{t=1}^{T} z_t z_t' = T^{-1} \hat{\sigma}^2 Z'Z$$

where $\hat{\sigma}^2$ is a consistent estimator for $\sigma^2$.

In this case the efficient GMM estimator becomes:

$$\hat{\beta}_{GMM} = (X'Z S_T^{-1} Z'X)^{-1} X'Z S_T^{-1} Z'Y$$

$$= \left(X'Z \left(T^{-1} \hat{\sigma}^2 Z'Z\right)^{-1} Z'X\right)^{-1} X'Z \left(T^{-1} \hat{\sigma}^2 Z'Z\right)^{-1} Z'Y$$

$$= \left(X'Z (Z'Z)^{-1} Z'X\right)^{-1} X'Z (Z'Z)^{-1} Z'Y$$

which is identical to the **two stage least squares (2SLS)** estimator.

The variance of the estimator is:

$$V(\hat{\beta}_{GMM}) = T^{-1} (D_T' S_T^{-1} D_T)^{-1} = \hat{\sigma}^2 (X'Z (Z'Z)^{-1} Z'X)^{-1}$$

which again coincides with the 2SLS variance.

---

## 9. Comparison with Maximum Likelihood and Quasi-ML Estimation

### Quasi-ML (QML) Estimation

The first order conditions for ML estimation can be seen as a sample counterpart to a moment condition:

$$\frac{1}{T} S(\hat{\theta}) = \frac{1}{T} \sum_{t=1}^{T} s_t(\hat{\theta}) = 0 \quad \text{corresponds to} \quad E(s_t(\theta_0)) = 0$$

and ML becomes a special case of GMM.

$\hat{\theta}_{ML}$ is consistent for weaker assumptions than maintained by ML. The FOC for a normal regression model corresponds to:

$$E(x_t(y_t - x_t' \beta_0)) = 0$$

which is weaker than the assumption that the entire distribution is correctly specified. OLS is consistent even if $e_t$ is not normal.

The variance matrix is no longer the inverse information.

### ML vs. GMM Comparison

| Aspect | Maximum Likelihood | Generalized Method of Moments |
|--------|------------------|------------------------------|
| **Assumptions** | Full specification. Know Density($\theta_0$) apart from $\theta_0$. | Partial specification/weak assumptions. Moment conditions: $E(f($data$;\theta_0)) = 0$. Strong economic assumptions. |
| **Efficiency** | Cramér Rao lower bound. (Smallest possible variance). | Efficient based on moment condition. Never smaller than Cramér Rao. |
| **Typical Approach** | Statistical description of the data. Misspecification testing. Restrictions recover economics. | Estimate deep parameters of economic model. |
| **Robustness** | First order conditions should hold! PML is a GMM interpretation of ML. Use larger PML variance. | Moment conditions should hold! Weights and variances can be made robust. |

---

## References

This lecture is based on:

- Hansen, L. P., & Singleton, K. J. (1982). Generalized instrumental variables estimation of nonlinear rational expectations models. *Econometrica*, 50(5), 1269-1286.
- Newey, W. K., & West, K. D. (1987). A simple, positive semi-definite, heteroskedasticity and autocorrelation consistent covariance matrix. *Econometrica*, 55(3), 703-708.
- Hall, A. R. (2005). *Generalized method of moments*. Oxford University Press.

