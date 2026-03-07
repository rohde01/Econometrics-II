# Univariate Time-Series Models
**Econometrics II**  
*Rasmus Søndergaard Pedersen*

---

## Outline

1. Introduction
2. Recap: Stationarity and weak dependence
3. The moving average MA(q) model — Stationarity condition
4. The autoregressive AR(1) model — Stationarity condition
5. Lag operators and lag polynomials — The general AR(p) model
6. ARMA modelling, estimation, and model selection
7. Forecasting

---

## 1. Introduction

### Univariate and Multivariate Analysis

**Univariate models** consider a single time-series, $\{y_t\}_{t=1}^T$.  
The object of interest is typically $y_t \mid \text{past}$. Univariate models are useful for:

1. Characterizing the dependence (and testing for unit roots).
2. Simple forecasts.

**Conditional models** focus on the interrelationships given causality, $x_t \rightsquigarrow y_t$:

$$y_t \mid y_1, \ldots, y_{t-1}, x_1, \ldots, x_{t-1}, x_t$$

We may be interested in the **dynamic multipliers**:

$$\frac{\partial y_t}{\partial x_t}, \quad \frac{\partial y_{t+1}}{\partial x_t}, \quad \frac{\partial y_{t+2}}{\partial x_t}, \ldots$$

and **long-run multipliers**, $\frac{\partial E[y_t]}{\partial E[x_t]}$.

**Multivariate models** focus on the joint dynamics of $(y_t, x_t)$.

---

### Examples of Model Types

**Autoregressive (AR) models:**
$$y_t = \delta + \theta y_{t-1} + \varepsilon_t$$

**Moving Average (MA) models:**
$$y_t = \delta + \varepsilon_t + \alpha \varepsilon_{t-1}$$

**ARMA models:**
$$y_t = \delta + \theta y_{t-1} + \varepsilon_t + \alpha \varepsilon_{t-1}$$

**Autoregressive Distributed Lag (ADL) models:**
$$y_t = \delta + \theta y_{t-1} + \beta_0 x_t + \beta_1 x_{t-1} + \varepsilon_t$$

**Vector Autoregressive (VAR) models:**
$$\begin{pmatrix} y_t \\ x_t \end{pmatrix} = \begin{pmatrix} \delta_1 \\ \delta_2 \end{pmatrix} + \begin{pmatrix} \theta_{11} & \theta_{12} \\ \theta_{21} & \theta_{22} \end{pmatrix} \begin{pmatrix} y_{t-1} \\ x_{t-1} \end{pmatrix} + \begin{pmatrix} \epsilon_{1t} \\ \epsilon_{2t} \end{pmatrix}$$

---

## 2. Stationarity and Weak Dependence

### Definitions

A time series $\{y_t\}_{t=1}^T$ is called **strictly stationary** if the distributions of

$$(y_t, y_{t+1}, \ldots, y_{t+s}) \quad \text{and} \quad (y_{t+h}, y_{t+1+h}, \ldots, y_{t+s+h})$$

are the same for all $h$. The distribution of $y_t$ does not depend on $t$.

---

The time series is called **weakly stationary** if for all $t$:

$$E(y_t) = \mu$$
$$V(y_t) = E\big((y_t - \mu)^2\big) = \gamma_0 < \infty$$
$$\text{Cov}(y_t, y_{t-h}) = E\big((y_t - \mu)(y_{t-h} - \mu)\big) = \gamma_h \quad \text{for } h = 1, 2, \ldots$$

The time series is called **weakly dependent** if $y_t$ and $y_{t-h}$ become approximately independent for $h \to \infty$.

> Stationarity and weak dependence are different properties, but in many cases implied by the same conditions on the model.

---

### Stationarity Conditions

For the OLS estimator of the AR(1) to be consistent:

$$\hat{\theta} = \frac{\sum_{t=1}^T y_t y_{t-1}}{\sum_{t=1}^T y_{t-1}^2} \xrightarrow{p} \theta_0$$

we typically need a **Law of Large Numbers (LLN)** such that sample moments converge to population moments:

$$\frac{1}{T} \sum_{t=1}^T y_{t-1}^2 \xrightarrow{p} E(y_{t-1}^2) \quad \text{or} \quad \frac{1}{T} \sum_{t=1}^T y_t y_{t-1} \xrightarrow{p} E(y_t y_{t-1})$$

This holds if $y_t$ is stationary and weakly dependent. For each model we will derive the stationarity condition.

---

## 3. The Moving Average MA(q) Model

### White Noise Process

Define a **white noise process**, $\varepsilon_t \sim i.i.d.(0, \sigma^2)$:

$$E(\varepsilon_t) = 0, \quad E(\varepsilon_t^2) = \sigma^2, \quad E(\varepsilon_t \varepsilon_s) = 0 \text{ for } t \neq s$$

Often called an **innovation** or a **shock** to the process.

### Definition

The **moving average model of order $q$**, MA($q$), is defined by:

$$y_t = \mu + \varepsilon_t + \alpha_1 \varepsilon_{t-1} + \alpha_2 \varepsilon_{t-2} + \ldots + \alpha_q \varepsilon_{t-q} \tag{*}$$

for $t = 1, 2, \ldots, T$. We need $q$ initial values: $\varepsilon_{-(q-1)} = \varepsilon_{-(q-2)} = \ldots = \varepsilon_0 = 0$.

---

### Properties of MA(q)

**Expectation:**
$$E(y_t) = \mu$$

**Variance:**
$$\gamma_0 = V(y_t) = \left(1 + \alpha_1^2 + \alpha_2^2 + \ldots + \alpha_q^2\right)\sigma^2$$

**Autocovariances:**
$$\gamma_1 = (\alpha_1 + \alpha_2\alpha_1 + \alpha_3\alpha_2 + \ldots + \alpha_q\alpha_{q-1})\sigma^2$$
$$\gamma_2 = (\alpha_2 + \alpha_3\alpha_1 + \alpha_4\alpha_2 + \ldots + \alpha_q\alpha_{q-2})\sigma^2$$
$$\vdots$$
$$\gamma_q = \alpha_q \sigma^2$$
$$\gamma_k = 0 \quad \text{for } k > q$$

**Autocorrelation Function (ACF):**

$$\rho_k = \frac{\gamma_k}{\gamma_0} = \begin{cases} \dfrac{\alpha_k + \alpha_{k+1}\alpha_1 + \alpha_{k+2}\alpha_2 + \ldots + \alpha_q\alpha_{q-k}}{1 + \alpha_1^2 + \alpha_2^2 + \ldots + \alpha_q^2} & \text{for } k \leq q \\ 0 & \text{for } k > q \end{cases}$$

### Stationarity of MA(q)

The MA($q$) process is always stationary: $y_t$ is a combination of stationary terms, the mean and variance are constant, and autocovariances $\gamma_k$ depend on $k$ but not on $t$.

For the **infinite moving average process, MA($\infty$)**, the process is stationary if the variance is bounded:

$$V(y_t) = \left(1 + \alpha_1^2 + \alpha_2^2 + \ldots\right)\sigma^2 < \infty$$

We require $\sum_{j=0}^\infty \alpha_j^2 < \infty$, so that the infinite sum converges.

---

## 4. The Autoregressive AR(1) Model

### Definition

An **autoregressive (AR) model** with $p$ lags, AR($p$), is defined by:

$$y_t = \delta + \theta_1 y_{t-1} + \theta_2 y_{t-2} + \ldots + \theta_p y_{t-p} + \varepsilon_t \tag{**}$$

where $\varepsilon_t \sim i.i.d.(0, \sigma^2)$.

### The AR(1) Model

Consider the AR(1) model:

$$y_t = \delta + \theta y_{t-1} + \varepsilon_t \tag{#}$$

By **recursive substitution**, we obtain the MA-representation:

$$y_t = \left(1 + \theta + \theta^2 + \ldots + \theta^{t-1}\right)\delta + \varepsilon_t + \theta\varepsilon_{t-1} + \theta^2\varepsilon_{t-2} + \ldots + \theta^{t-1}\varepsilon_1 + \theta^t y_0$$

If $y_t$ started in the infinite past, we have the **infinite moving average representation**:

$$y_t = \left(1 + \theta + \theta^2 + \theta^3 + \ldots\right)\delta + \varepsilon_t + \theta\varepsilon_{t-1} + \theta^2\varepsilon_{t-2} + \ldots$$

### Stationarity Condition for AR(1)

The **stationarity condition** for the AR(1) is $|\theta| < 1$, so that the MA sum converges:

$$1 + \theta + \theta^2 + \theta^3 + \ldots = \frac{1}{1-\theta}$$

### Properties of Stationary AR(1)

**Unconditional expectation:**
$$\mu = E(y_t) = \frac{\delta}{1 - \theta}$$

**Unconditional variance:**
$$\gamma_0 = V(y_t) = \frac{\sigma^2}{1 - \theta^2}$$

**Autocovariances:**
$$\gamma_k = \text{Cov}(y_t, y_{t-k}) = \theta^k \gamma_0$$

**Autocorrelation function (ACF):**
$$\rho_k = \frac{\gamma_k}{\gamma_0} = \theta^k$$

This is an exponentially decreasing function if $|\theta| < 1$.

---

## 5. Lag Operators and Lag Polynomials

### Definitions

The **lag operator** $L$ and the **difference operator** $\Delta = 1 - L$:

$$Ly_t = y_{t-1}$$
$$\Delta y_t = (1 - L)y_t = y_t - y_{t-1}$$

### AR(2) in Lag Operator Notation

$$y_t = \delta + \theta_1 y_{t-1} + \theta_2 y_{t-2} + \varepsilon_t$$
$$\Rightarrow (1 - \theta_1 L - \theta_2 L^2)y_t = \delta + \varepsilon_t$$
$$\Rightarrow \theta(L)y_t = \delta + \varepsilon_t$$

where $\theta(L) = 1 - \theta_1 L - \theta_2 L^2$ is a polynomial in $L$.

### Geometric Series in Lag Operators

The operators $L$ and $\Delta$ can be treated as scalars. The usual convergent geometric series result holds:

$$1 + \theta L + \theta^2 L^2 + \theta^3 L^3 + \ldots = \frac{1}{1 - \theta L} \tag{*}$$

provided $|\theta| < 1$.

This defines the **inverse** of the polynomial $(1 - \theta L)$, denoted $\theta^{-1}(L) = (1 - \theta L)^{-1}$.

If $\theta(L) = 1 - \theta_1 L - \theta_2 L^2 - \ldots - \theta_p L^p$, then:

$$\theta(1) = 1 - \theta_1 - \theta_2 - \ldots - \theta_p = 1 - \sum_{i=1}^p \theta_i$$

---

### Characteristic Equation and Roots

The **AR($p$) model** can be written as:

$$\theta(L)y_t = y_t - \theta_1 y_{t-1} - \theta_2 y_{t-2} - \ldots - \theta_p y_{t-p} = \delta + \varepsilon_t$$

where $\theta(z) = 1 - \theta_1 z - \ldots - \theta_p z^p$ is the **autoregressive polynomial**.

The **characteristic equation** is: $\theta(z) = 0$

The $p$ solutions $z_1, \ldots, z_p$ are the **characteristic roots**, which may be complex:

$$z_j = r_j \pm c_j\sqrt{-1} \in \mathbb{C}, \quad r_j, c_j \in \mathbb{R}$$

The modulus of $z_j$ is $|z_j| = \sqrt{r_j^2 + c_j^2}$.

The roots $z_1, \ldots, z_p$ can factorize the polynomial:

$$\theta(z) = (1 - \phi_1 z)(1 - \phi_2 z) \cdots (1 - \phi_p z)$$

where $\phi_j = z_j^{-1}$ are the **inverse roots**.

### Stationarity Condition for AR(p)

The AR($p$) process is **stationary** (and weakly dependent) if and only if all inverse roots satisfy $|\phi_j| < 1$, or equivalently, all characteristic roots satisfy $|z_j| > 1$ for $j = 1, 2, \ldots, p$.

### MA($\infty$) Representation of AR($p$)

Under the stationarity condition, the AR($p$) model has a MA($\infty$) representation:

$$y_t = \theta^{-1}(L)(\delta + \varepsilon_t) = (1 + c_1 + c_2 + c_3 + \ldots)\delta + \varepsilon_t + c_1\varepsilon_{t-1} + c_2\varepsilon_{t-2} + \ldots$$

The **impulse responses** (dynamic impact of a shock) are:

$$\frac{\partial y_t}{\partial \varepsilon_t} = 1, \quad \frac{\partial y_t}{\partial \varepsilon_{t-1}} = c_1, \quad \frac{\partial y_t}{\partial \varepsilon_{t-2}} = c_2, \ldots$$

The stationarity condition ensures that impulse responses die out (weak dependence).

**Expectation and variance from the MA representation:**

$$\mu = E(y_t) = \frac{\delta}{1 - \theta_1 - \theta_2 - \ldots - \theta_p} = \frac{\delta}{\theta(1)}$$

$$\gamma_0 = V(y_t) = \left(1 + c_1^2 + c_2^2 + c_3^2 + \ldots\right)\sigma^2$$

---

### Example: AR(2) Models

The AR(2) characteristic equation:

$$\theta(z) = 1 - \theta_1 z - \theta_2 z^2 = 0$$

With solutions (for $\theta_2 \neq 0$):

$$z_1 = \frac{-(-\theta_1) + \sqrt{(-\theta_1)^2 - 4(-\theta_2) \cdot 1}}{2(-\theta_2)}, \quad z_2 = \frac{-(-\theta_1) - \sqrt{(-\theta_1)^2 - 4(-\theta_2) \cdot 1}}{2(-\theta_2)}$$

The **stationarity region** for $(\theta_1, \theta_2)$ in the AR(2) model:

$$\theta_1 + \theta_2 < 1, \quad \theta_2 - \theta_1 < 1, \quad |\theta_2| < 1$$

---

## 6. ARMA Modelling, Estimation, and Model Selection

### ARMA Models

The **ARMA($p$, $q$)** model combines AR and MA components:

$$y_t - \theta_1 y_{t-1} - \ldots - \theta_p y_{t-p} = \delta + \varepsilon_t + \alpha_1\varepsilon_{t-1} + \ldots + \alpha_q\varepsilon_{t-q}$$

$$\theta(L)y_t = \delta + \alpha(L)\varepsilon_t$$

The class of ARMA models is very flexible and can replicate most patterns of autocovariances seen in actual data.

### Unit Roots and ARIMA Models

A root (or inverse root) at one, $\phi_1 = 1$, is called a **unit root**. If there is a unit root, we can factorize:

$$\theta(L) = (1 - L)\theta^*(L) = \theta^*(L)\Delta$$

and write the model as: $\theta^*(L)\Delta y_t = \alpha(L)\varepsilon_t$

An ARMA($p$,$q$) model for $\Delta^d y_t$ is denoted an **ARIMA($p$,$d$,$q$)** model for $y_t$.

---

### Estimation of ARMA Models

The natural estimator is **maximum likelihood**.

**For the AR(1) model**, conditioning on $y_0$ and assuming Gaussian errors:

$$\log L_T(\delta, \theta, \sigma^2) = -\frac{T}{2}\log(2\pi\sigma^2) - \sum_{t=1}^T \frac{(y_t - \delta - \theta y_{t-1})^2}{2\sigma^2}$$

**For the MA(1) model**, we recursively compute residuals:

$$\varepsilon_1 = y_1 - \mu, \quad \varepsilon_2 = y_2 - \mu - \alpha\varepsilon_1, \quad \varepsilon_3 = y_3 - \mu - \alpha\varepsilon_2, \ldots$$

The likelihood $\log L_T(\mu, \alpha, \sigma^2) = -\frac{T}{2}\log(2\pi\sigma^2) - \sum_{t=1}^T \frac{\varepsilon_t^2}{2\sigma^2}$ is then maximized.

---

### Model Selection

**Information criteria** balance fit against model complexity (should be **minimized**):

$$AIC = \log\hat{\sigma}^2 + \frac{2k}{T}$$

$$HQ = \log\hat{\sigma}^2 + \frac{2k\log(\log(T))}{T}$$

$$BIC = \log\hat{\sigma}^2 + \frac{k\log(T)}{T}$$

where $k = p + q + 1$ is the number of parameters.

**General-to-Specific (GETS) principle**: Start with a large model and reduce. The opposite (specific-to-general) is dangerous, as estimators in misspecified models are not consistent. Always be aware of **cancelling roots** when applying GETS to ARMA models.

---

## 7. Forecasting

### Optimal Forecasts

The **optimal predictor** (in mean squared error sense) is the conditional expectation, given the information set $\mathcal{I}_T = \{y_{-\infty}, \ldots, y_{T-1}, y_T\}$:

$$y_{T+k \mid T} = E(y_{T+k} \mid \mathcal{I}_T)$$

### Forecasting with ARMA(1,1)

For $y_t = \theta y_{t-1} + \varepsilon_t + \alpha\varepsilon_{t-1}$, with estimated residuals $\hat{\varepsilon}_1, \ldots, \hat{\varepsilon}_T$ and $\hat{\varepsilon}_{T+1} = \hat{\varepsilon}_{T+2} = \ldots = 0$:

**One-step-ahead forecast:**
$$\hat{y}_{T+1 \mid T} = \hat{\theta}y_T + \hat{\alpha}\hat{\varepsilon}_T$$

**Two-step-ahead forecast:**
$$\hat{y}_{T+2 \mid T} = \hat{\theta}\hat{y}_{T+1 \mid T}$$

---

### Forecast Comparison: Diebold-Mariano Test

Given two competing forecast series $\{f_{1,t}\}$ and $\{f_{2,t}\}$ for $\{y_t\}$, define squared forecast errors:

$$e_{1,t} = (y_t - f_{1,t})^2 \quad \text{and} \quad e_{2,t} = (y_t - f_{2,t})^2$$

The forecasts are equally good if:

$$H_0: E[d_t] = 0, \quad \text{where } d_t = e_{1,t} - e_{2,t}$$

The **Diebold-Mariano test statistic**:

$$t_{H_0} = \frac{\bar{d}}{\widehat{s.e.}(\bar{d})}$$

where $\bar{d} = T^{-1}\sum_{t=1}^T d_t$. Since $d_t$ is typically autocorrelated, $\widehat{s.e.}(\bar{d})$ should use a **heteroskedasticity and autocorrelation consistent (HAC)** variance estimator.

Under $H_0$, with $d_t$ stationary and weakly dependent, $t_{H_0} \xrightarrow{d} N(0,1)$ as $T \to \infty$.

**Implementation**: Simply regress $d_t$ on a constant.

> Alternative loss functions can also be used, e.g. absolute error $e_{1,t} = |y_t - f_{1,t}|$.
