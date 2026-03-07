# Likelihood Theory
**Econometrics II**  
*Rasmus Søndergaard Pedersen*

---

## Outline

1. The Statistical Model
2. The likelihood function: i.i.d. samples
3. The likelihood function: time series
4. The maximum likelihood estimator (MLE)
5. Example: Poisson model
6. Properties of the MLE
7. Example: Linear regression model
8. Three testing principles: Wald, LR, LM

---

## 1. The Statistical Model

- Observations $\{y_t\}_{t=1}^T$ are realizations of stochastic variables $\{y_t\}_{t=1}^T$.

- The distribution of $y_t$ is **assumed** to be known:

$$
(y_1, ..., y_t, ..., y_T) \overset{d}{=} \text{distribution}(\theta), \quad (*)
$$

apart from parameters $\theta \in \Theta$, where $\Theta$ is the parameter space.

- The distribution is characterized by the p.f. or p.d.f. This defines the likelihood function:

$$
L_T(\theta) = L(\theta \mid y_1, ..., y_T) = f(y_1, ..., y_T \mid \theta).
$$

Given $\theta$, $f(\cdot)$ is the 'probability' or 'likelihood' of observing the data.  
**The MLE, $\hat{\theta}_T$, maximizes the 'probability' of the data.**

- The (parametric) statistical model is defined by $L_T(\theta)$ and $\Theta$.

---

## Why Maximum Likelihood Estimation?

- The maximum likelihood estimator is the **best possible estimator** for a given statistical model.
- More importantly: It is an estimation approach that allows you to **check your assumptions** (which you should always do!).  
  Provided that your statistical model is well-specified, you will not get spurious results.

---

## 2. The Likelihood Function: i.i.d. Data

If $y_t$ and $y_s$ are independent for $t \neq s$, then

$$
f(y_1, ..., y_T \mid \theta) = \prod_{t=1}^{T} f(y_t \mid \theta),
$$

and therefore

$$
L_T(\theta) = \prod_{t=1}^{T} \ell(\theta \mid y_t),
$$

where $\ell(\theta \mid y_t) = f(y_t \mid \theta)$ is the likelihood contribution.

It follows that the log-likelihood function is a sum,

$$
\log L_T(\theta) = \sum_{t=1}^{T} \log \ell(\theta \mid y_t).
$$

This is important for optimization and application of limit results.

---

### Example: Gaussian Location Model

- Consider a sample of i.i.d. real-valued observations, $\{y_t\}_{t=1}^T$.
- Assume that $y_t$ is drawn from a Normal distribution:

$$
y_t \overset{d}{=} N(\theta, 1),
$$

such that $\theta = E(y_t)$ and $V(y_t) = 1$ (for simplicity).

- The parameter space is $\Theta = \{\theta : \theta \in \mathbb{R}\} = \mathbb{R}$.

- This may equivalently be stated as the **location model**:

$$
y_t = \theta + \varepsilon_t, \quad t = 1, \ldots, T,
$$

with $\{\varepsilon_t\}_{t=1}^T$ an i.i.d. process with $\varepsilon_t \overset{d}{=} N(0, 1)$.

---

### Small Numerical Example

Consider a data set with $T = 7$ realizations from $N(5, 1)$:

$$
y_1, ..., y_7 = 6.834, 2.924, 5.863, 5.511, 4.505, 4.624, 5.416.
$$

The likelihood function is:

$$
L_7(\theta) = \prod_{t=1}^{7} \frac{1}{\sqrt{2\pi}} \exp\!\left(-\frac{(y_t - \theta)^2}{2}\right),
$$

and

$$
\log L_7(\theta) = \sum_{t=1}^{7} \left(-\frac{1}{2}\log(2\pi) - \frac{(y_t - \theta)^2}{2}\right).
$$

#### Likelihood Values by $\theta$

| $\theta$ | $1000 \cdot \log L_T(\theta)$ |
|----------|-------------------------------|
| 3.0 | −19.973 |
| 3.5 | −13.510 |
| 4.0 | −8.797 |
| 4.5 | −5.834 |
| 5.0 | −4.621 |
| 5.5 | −5.157 |
| 6.0 | −7.444 |
| 6.5 | −11.481 |
| 7.0 | −17.268 |

---

## 3. The Likelihood Function: Time Series

- **For time series, we typically do not have independence.**

- As an example, consider data $\{y_t\}_{t=1}^T$ and the simple AR(1) model:

$$
y_t = \theta y_{t-1} + \varepsilon_t, \quad t = 2, 3, ..., T,
$$

with $\varepsilon_t$ assumed to be i.i.d. and $y_1$ is assumed to be fixed.

This gives $T - 1$ equations:

$$
y_2 = \theta y_1 + \varepsilon_2, \quad y_3 = \theta y_2 + \varepsilon_3, \quad \ldots, \quad y_T = \theta y_{T-1} + \varepsilon_T.
$$

We have no equation for $y_1$ because $y_0$ is not observed.

---

We do not have independence, but we can still factorize. Using $f(y, x) = f(y|x)f(x)$:

$$
f(y_1, ..., y_T \mid \theta) = f(y_1 \mid \theta) \cdot \prod_{t=2}^{T} f(y_t \mid y_1, ..., y_{t-1}; \theta).
$$

Each term $f(y_t \mid y_1, ..., y_{t-1}; \theta)$ corresponds to one of the AR(1) equations.

We use the density **conditional on $y_1$**:

$$
L(\theta \mid y_1, ..., y_T) = \prod_{t=2}^{T} f(y_t \mid y_1, ..., y_{t-1}; \theta).
$$

The log-likelihood function is a sum:

$$
\log L(\theta \mid y_1, ..., y_T) = \sum_{t=2}^{T} \log \ell_t(\theta),
$$

with $\ell_t(\theta) = f(y_t \mid y_1, ..., y_{t-1}; \theta)$.

---

## 4. The Maximum Likelihood Estimator (MLE)

The MLE is defined as:

$$
\hat{\theta}(y_1, ..., y_T) = \arg\max_{\theta \in \Theta} \log L(\theta \mid y_1, ..., y_T).
$$

Often denoted $\hat{\theta}_T$ or just $\hat{\theta}$.

- The random variable is called the **estimator**.
- The actual number (realization) is the **estimate**.

---

### Notation

The **score vector** is defined as the first derivative:

$$
S_T(\theta) = \frac{\partial \log L_T(\theta)}{\partial \theta} = \sum_{t=1}^{T} \frac{\partial \log \ell_t(\theta)}{\partial \theta} = \sum_{t=1}^{T} s_t(\theta),
$$

where $s_t(\theta)$ is the **score contribution**.

The first order condition is $S_T(\hat{\theta}_T) = 0$.

With $\theta \in \Theta \subset \mathbb{R}^k$, this is a $k$-dimensional vector:

$$
s_t(\theta) = \begin{pmatrix} \frac{\partial \log \ell_t(\theta)}{\partial \theta_1} \\ \vdots \\ \frac{\partial \log \ell_t(\theta)}{\partial \theta_k} \end{pmatrix}.
$$

---

The second derivative is called the **Hessian matrix**:

$$
\mathcal{H}_T(\theta) = \frac{\partial^2 \log L_T(\theta)}{\partial \theta \partial \theta'} = \sum_{t=1}^{T} H_t(\theta),
$$

where

$$
H_t(\theta) = \frac{\partial^2 \log \ell_t(\theta)}{\partial \theta \partial \theta'} \quad (**)
$$

is the contribution to the Hessian from observation $t$.

The Hessian contribution $(**)$ plays a role in the variance of $\hat{\theta}_T$.

The **information matrix** is defined as:

$$
\mathcal{I}(\theta) = -E(H_t(\theta)).
$$

---

### Approaches to Estimation

1. Maximize the log-likelihood analytically by solving the first order conditions.
2. Apply a grid search.
3. Use **numerical optimization** of $\log L_T(\theta)$. Given starting values $\theta^{(0)}$, move the sequence $\{\theta^{(j)}\}$ in a direction that increases the likelihood until $\theta^{(j)} \approx \theta^{(j-1)}$. Often based on approximations:

$$
S_T(\theta) \approx \frac{\log L_T(\theta + h) - \log L_T(\theta - h)}{2h}.
$$

---

## 5. Example: Poisson Model

- Consider a sample of count data observations $\{y_t\}_{t=1}^T$.
- Assume $y_t \overset{d}{=} \text{Poisson}(\lambda)$, such that $\lambda = E(y_t) = V(y_t) > 0$.
- Parameter space: $\Theta = \{\lambda \in \mathbb{R} \mid \lambda > 0\}$.

The likelihood contribution is:

$$
\ell(\lambda \mid y_t) = \frac{\exp(-\lambda)\lambda^{y_t}}{y_t!},
$$

and $\log \ell(\lambda \mid y_t) = -\lambda + y_t \log(\lambda) - \log(y_t!)$.

The log-likelihood function is:

$$
\log L(\lambda \mid y_1, ..., y_T) = -\lambda T + \log(\lambda)\sum_{t=1}^{T} y_t - \sum_{t=1}^{T} \log(y_t!).
$$

The score: $s_t(\lambda) = \frac{y_t}{\lambda} - 1$, and the first-order condition gives:

$$
\hat{\lambda}_T = \frac{1}{T}\sum_{t=1}^{T} y_t.
$$

The information matrix: $\mathcal{I}(\lambda) = \frac{1}{\lambda}$.

---

## 6. Properties of the MLE

Linearizing $S_T(\hat{\theta}_T)$ around $\theta_0$:

$$
\hat{\theta}_T - \theta_0 \approx \left[-\frac{1}{T}\sum_{t=1}^{T} H_t(\theta_0)\right]^{-1} \left[\frac{1}{T}\sum_{t=1}^{T} s_t(\theta_0)\right].
$$

### High Level Assumptions

Consider $\log L_T(\theta)$ with $\theta \in \Theta$, and let $\theta_0$ be an interior point of $\Theta$. Assume $\log L_T(\theta)$ is thrice continuously differentiable, such that:

- **(i)** $\frac{1}{T}\sum_{t=1}^{T} s_t(\theta_0) \xrightarrow{p} E(s_t(\theta_0)) = 0$
- **(ii)** $\frac{\sqrt{T}}{T}\sum_{t=1}^{T} s_t(\theta_0) \xrightarrow{d} N(0, \mathcal{J}(\theta_0))$
- **(iii)** $\frac{1}{T}\sum_{t=1}^{T} H_t(\theta_0) \xrightarrow{p} -\mathcal{I}(\theta_0)$, $\mathcal{I}(\theta_0)$ positive definite.
- **(iv)** $\max_{i,j,k} \left|\frac{1}{T}\sum_{t=1}^{T} \frac{\partial^3 \log \ell_t(\theta)}{\partial \theta_i \partial \theta_j \partial \theta_k}\right| \xrightarrow{p} C < \infty$.

### MLE Properties

If the likelihood function is correctly specified and assumptions (i)–(iv) hold:

1. **Consistency:** $\hat{\theta}_T \xrightarrow{p} \theta_0$

2. **Asymptotic normality:** $\sqrt{T}(\hat{\theta}_T - \theta_0) \xrightarrow{d} N(0, \Omega_\theta)$, where $\Omega_\theta(\theta_0) = \mathcal{I}(\theta_0)^{-1} = \mathcal{J}(\theta_0)^{-1}$

3. **Asymptotic efficiency:** Any other consistent and asymptotically normal estimator has asymptotic variance $\geq \mathcal{I}(\theta_0)^{-1}$.

---

### Robustness and the QMLE

An estimator based on an approximate or instrumental p.d.f. is called a **pseudo MLE (PMLE)** or **quasi MLE (QMLE)**.

If $E(s_t(\theta_0)) = 0$ and assumptions (i)–(iv) hold, then consistency and asymptotic normality still hold, with asymptotic variance replaced by the **sandwich formula**:

$$
\Omega^*_\theta(\theta_0) = \mathcal{I}(\theta_0)^{-1} \mathcal{J}(\theta_0) \mathcal{I}(\theta_0)^{-1}.
$$

---

### Estimating the Variance

Using sample averages:

$$
\hat{\mathcal{I}}(\hat{\theta}_T) = -\frac{1}{T}\sum_{t=1}^{T} \frac{\partial^2 \log \ell_t(\hat{\theta}_T)}{\partial \theta \partial \theta}
\quad \text{(observed information)}
$$

$$
\hat{\mathcal{J}}(\hat{\theta}_T) = \frac{1}{T}\sum_{t=1}^{T} s_t(\hat{\theta}_T) s_t(\hat{\theta}_T)'
\quad \text{(OPG)}
$$

---

## 7. Example: Linear Regression Model

Consider a linear regression model:

$$
y_t = x_t' \beta + \varepsilon_t, \quad t = 1, 2, ..., T.
$$

Assume $\varepsilon_t \mid x_t \overset{d}{=} N(0, \sigma^2)$, so $y_t \mid x_t \overset{d}{=} N(x_t'\beta, \sigma^2)$.

The log-likelihood is:

$$
\log L_T(\beta, \sigma^2) = -\frac{1}{2}\sum_{t=1}^{T} \left(\log(2\pi) + \log(\sigma^2) + \frac{(y_t - x_t'\beta)^2}{\sigma^2}\right).
$$

### MLE = OLS

The first order condition w.r.t. $\beta$ gives:

$$
\hat{\beta} = \left(\sum_{t=1}^{T} x_t x_t'\right)^{-1} \sum_{t=1}^{T} x_t y_t.
$$

**In a regression model with normal errors, OLS is the MLE.**

The MLE of the variance is:

$$
\hat{\sigma}^2 = \frac{1}{T}\sum_{t=1}^{T} \hat{\varepsilon}_t^2,
$$

which is biased but consistent (differs from the OLS estimator $\frac{1}{T-k}$).

### Asymptotic Distribution

$$
\hat{\beta} \overset{a}{\sim} N\!\left(\beta_0,\ \frac{\sigma_0^2}{T} E[x_t x_t']^{-1}\right),
$$

with estimated variance $\hat{\sigma}^2 \left(\sum_{t=1}^{T} x_t x_t'\right)^{-1}$.

---

## 8. Three Testing Principles: Wald, LR, LM

Consider a null hypothesis:

$$
H_0: R'_{(j \times k)}\, \theta = q \quad \text{against} \quad H_A: R'\theta \neq q.
$$

Let $\tilde{\theta}_T$ (restricted) and $\hat{\theta}_T$ (unrestricted) denote the MLEs under $H_0$ and $H_U = H_A \cup H_0$.

---

### Wald Test

Requires only **unrestricted estimation** (under $H_U$).

$$
\xi_W = T \cdot (R'\hat{\theta}_T - q)' (R'\Omega_\theta R)^{-1} (R'\hat{\theta}_T - q) \xrightarrow{d} \chi^2(j).
$$

- Two-sided test.
- **Robust version** uses sandwich matrix $\Omega^*_\theta$.

The standard **t-ratio** for $H_0: \theta_{0,i} = a$:

$$
t_{\theta_{0,i}=a} = \frac{\hat{\theta}_{i,T} - a}{\sqrt{V(\hat{\theta}_i)}} \xrightarrow{d} N(0,1).
$$

Note: $\xi_W = t^2$ for $j = 1$; the $t$-test can be made one-sided.

---

### Likelihood Ratio (LR) Test

Requires estimation under **both** $H_0$ and $H_U$.

$$
\xi_{LR} = -2\left(\log L(\tilde{\theta}_T) - \log L(\hat{\theta}_T)\right) \xrightarrow{d} \chi^2(j).
$$

- Two-sided test.
- **Non-robust**: does not apply when QMLE covariance is needed.
- Models must be **nested**.

---

### Lagrange Multiplier (LM) / Score Test

Requires only **restricted estimation** (under $H_0$).

If the restriction is true: $S_T(\tilde{\theta}_T) = \sum_{t=1}^{T} s_t(\tilde{\theta}_T) \approx 0$.

$$
\xi_{LM} = \left(\sum_{t=1}^T s_t(\tilde{\theta}_T)'\right) \left(\sum_{t=1}^T s_t(\tilde{\theta}_T) s_t(\tilde{\theta}_T)'\right)^{-1} \left(\sum_{t=1}^T s_t(\tilde{\theta}_T)\right) \xrightarrow{d} \chi^2(j).
$$

Often implemented as $\xi_{LM} = TR^2$ from an auxiliary linear regression.

---

### Example: Danish Consumption Data

Model: $\Delta c_t = \beta_0 + \beta_1 \Delta y_t + \beta_2 \Delta r_t + \beta_3 \Delta w_t + \varepsilon_t$ (1973:2 – 2003:2)

|  | $M_0$ | $M_1$ | $M_2$ | $M_3$ | $M_4$ |
|--|-------|-------|-------|-------|-------|
| Constant | 0.155 (0.095) | 0.173 (0.107) | 2.322 (1.40) | 2.467 (1.49) | 3.120 (1.84) |
| $\Delta y_t$ | 0.197 (3.13) | 0.196 (3.13) | 0.202 (2.99) | 0.209 (3.11) | 0 |
| $\Delta r_t$ | 0.238 (0.27) | 0 | −1.030 (−1.18) | 0 | 0 |
| $\Delta w_t$ | 0.572 (4.26) | 0.559 (4.45) | 0 | 0 | 0 |
| $\log L(\hat{\theta})$ | 324.545 | 324.506 | 315.825 | 315.118 | 310.385 |
| $R^2$ | 0.209 | 0.208 | 0.086 | 0.075 | 0.000 |

*t-values in parentheses.*

---

### Summary: The Classical Trinity

| Test | What is estimated | Statistic |
|------|------------------|-----------|
| **Wald** | $H_U$ only | Distance of $R'\hat{\theta}_T$ from $q$ |
| **LR** | $H_0$ and $H_U$ | Loss in log-likelihood |
| **LM** | $H_0$ only | Violation of score equation |

All three tests are **asymptotically equivalent** and distributed as $\chi^2(j)$ under $H_0$.
