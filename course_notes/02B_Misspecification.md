# Model Formulation and Misspecification Testing
**Econometrics II**
*Rasmus Søndergaard Pedersen*

---

## Model Formulation

- In practice, the correct model is unknown. We search for regressors, lag-length, model type, etc.
- Given that the true model is nested in the estimation model (and under regularity conditions), $\hat{\beta}$ is consistent for any true value $\beta_0$, also $\beta_0 = 0$. This suggests a **general-to-specific (GETS)** principle.
- Estimators in misspecified models are not consistent, in general. The opposite **specific-to-general** principle is dangerous.
- With GETS in ARMA models, always be aware of cancelling roots.
- We can never prove that a model is correctly specified. But we can conduct **misspecification tests** to ensure that the main dynamic properties (of interest) are accounted for.

---

## The Statistical Models

We consider different statistical models:

**1. The linear regression model:**

$$y_t = x_t'\beta + \epsilon_t \tag{*}$$

Estimated by MLE (= OLS if $\epsilon_t$ is assumed Gaussian).

**2. The ARMA model:**

$$y_t - \theta_1 y_{t-1} - \ldots - \theta_p y_{t-p} = \delta + \epsilon_t + \alpha_1 \epsilon_{t-1} + \ldots + \alpha_q \epsilon_{t-q} \tag{**}$$

Estimated by MLE.

Throughout:
- $\epsilon_t$ is assumed Gaussian or to follow some other distribution.
- **Misspecification testing** is based on the estimated residuals, $\{\hat{\epsilon}_t\}_{t=1}^T$.

---

## Test for No-Autocorrelation, (*)

A test for no-autocorrelation is based on the **auxiliary regression**:

$$\hat{\epsilon}_t = x_t'\delta + \gamma_1 \hat{\epsilon}_{t-1} + \ldots + \gamma_h \hat{\epsilon}_{t-h} + u_t$$

and the hypothesis:

$$H_0 : \gamma_1 = \ldots = \gamma_j = \ldots = \gamma_h = 0 \quad \text{vs.} \quad H_A : \text{some } \gamma_j \neq 0$$

where $x_t$ is included because it may be correlated with $\epsilon_{t-1}, \ldots, \epsilon_{t-h}$.

The **Breusch-Godfrey LM statistic** is given by:

$$\xi_{\text{auto}} = T \cdot R^2 \quad \text{with} \quad \xi_{\text{auto}} \xrightarrow{d} \chi^2(h) \text{ under } H_0$$

$\text{cov}(\hat{\epsilon}_t, x_t) = 0$ and any explanatory power is due to $\hat{\epsilon}_{t-1}, \ldots, \hat{\epsilon}_{t-h}$.

---

## Portmanteau Test for No-Autocorrelation, (*) and (**)

A simpler test is based on the autocorrelations:

$$\rho_j = \frac{\sum_{t=j+1}^{T} (\hat{\epsilon}_t - \bar{\epsilon})(\hat{\epsilon}_{t-j} - \bar{\epsilon})}{\sum_{t=1}^{T} (\hat{\epsilon}_t - \bar{\epsilon})^2}, \quad \text{with} \quad \bar{\epsilon} = T^{-1} \sum_{t=1}^{T} \hat{\epsilon}_t$$

The **Portmanteau** or **Ljung-Box statistic** is given by:

$$\xi_{LB} = T^2 \sum_{j=1}^{h} \frac{\rho_j^2}{T - j}$$

Under the null, $\xi_{LB} \xrightarrow{d} \chi^2(h - p)$, where $p$ is the number of AR+MA terms in the original model.

---

## Test for No-Heteroskedasticity, (*)

To test the assumption of no-heteroskedasticity we use the **auxiliary regression**:

$$\hat{\epsilon}_t^2 = \psi_0 + x_{1t}\psi_1 + \ldots + x_{kt}\psi_k + x_{1t}^2\delta_1 + \ldots + x_{kt}^2\delta_k + u_t$$

The null hypothesis is unconditional homoskedasticity:

$$H_0 : \psi_1 = \ldots = \psi_k = \delta_1 = \ldots = \delta_k = 0$$

and the alternative is that the variance of $\epsilon_t$ depends on $x_{it}$ or the squares $x_{it}^2$.

The test is based on the LM statistic:

$$\xi_{\text{het}} = T \cdot R^2, \quad \text{with} \quad \xi_{\text{het}} \xrightarrow{d} \chi^2(2k) \text{ under } H_0$$

We may also include non-redundant cross terms, $x_{it} \cdot x_{jt}$.

---

## Test for No-ARCH, (*) and (**)

To test the assumption of no **autoregressive conditional heteroskedasticity (ARCH)**, known as volatility clustering, we use the auxiliary regression:

$$\hat{\epsilon}_t^2 = \gamma_0 + \gamma_1 \hat{\epsilon}_{t-1}^2 + \gamma_2 \hat{\epsilon}_{t-2}^2 + \ldots + \gamma_h \hat{\epsilon}_{t-h}^2 + u_t$$

The null hypothesis is conditional homoskedasticity:

$$H_0 : \gamma_1 = \cdots = \gamma_h = 0$$

and the alternative is volatility clustering, $\gamma_j \neq 0$.

The test is based on the LM statistic:

$$\xi_{\text{ARCH}} = T \cdot R^2, \quad \text{with} \quad \xi_{\text{ARCH}} \xrightarrow{d} \chi^2(h) \text{ under } H_0$$

---

## Test for Correct Functional Form, (*)

To test for the functional form, the so-called **RESET test** can be used. The idea is to consider the auxiliary regression model:

$$\hat{\epsilon}_t = x_t'\delta + \gamma_1 \hat{y}_t^2 + \gamma_2 \hat{y}_t^3 + u_t \tag{1}$$

where $\hat{y}_t = x_t'\hat{\beta}$ is the predicted value of the original regression.

- The null hypothesis of correct specification is $\gamma_1 = \gamma_2 = 0$.
- The alternative is that a squared or cubic term of $x_{it}$ is omitted.

The test statistic is given by:

$$\xi_{\text{reset}} = T \cdot R^2, \quad \text{with} \quad \xi_{\text{reset}} \xrightarrow{d} \chi^2(2) \text{ under } H_0$$

---

## Test for Normality, (*) and (**)

- To check normality, we can plot the residuals and a histogram for visual inspection.
- If residuals fall outside the 'expected' interval, it indicates an extraordinary event. Misspecification tests are sensitive to outliers.
- We may include an **intervention dummy** for outliers: $d_t = \mathbb{I}(t = T_0)$.

A formal test is based on estimated **skewness** (S) and **kurtosis** (K):

$$S_T = T^{-1} \sum_{t=1}^{T} e_t^3 \quad \text{and} \quad K_T = T^{-1} \sum_{t=1}^{T} e_t^4$$

where $e_t = (\hat{\epsilon}_t - \bar{\epsilon})/\hat{\sigma}$ denotes the standardized residual, with $\bar{\epsilon} = T^{-1}\sum_{t=1}^T \hat{\epsilon}_t$ and $\hat{\sigma}^2 = T^{-1}\sum_{t=1}^T (\hat{\epsilon}_t - \bar{\epsilon})^2$.

The Gaussian distribution has $S \equiv E[(\epsilon_t/\sigma)^3] = 0$ (symmetry) and $K \equiv E[(\epsilon_t/\sigma)^4] = 3$. $K - 3$ is known as **excess kurtosis**.

Under normality (i.e., $S = 0$ and $K = 3$):

$$\sqrt{T}(S_T - S) \xrightarrow{d} N(0,6) \quad \text{and} \quad \sqrt{T}(K_T - K) \xrightarrow{d} N(0, 24 \cdot T^{-1})$$

such that:

$$\xi_S = \frac{T}{6} \cdot S_T^2 \xrightarrow{d} \chi^2(1) \quad \text{and} \quad \xi_K = \frac{T}{24} \cdot (K_T - 3)^2 \xrightarrow{d} \chi^2(1)$$

Because $\xi_S$ and $\xi_K$ are asymptotically independent, the joint test for $H_0 : S = (K-3) = 0$ can be based on:

$$\xi_{JB} = \xi_S + \xi_K, \quad \text{with} \quad \xi_{JB} \xrightarrow{d} \chi^2(2) \text{ under } H_0$$

Known as the **Jarque-Bera test**.

---

## Example: Danish House Prices, 1972(1)–2004(2)

| | AR(3) | AR(2) | AR(1) | Preferred |
|---|---|---|---|---|
| Constant | 0.0009332 (0.462) | 0.0009436 (0.47) | 0.0009752 (0.487) | 0.001113 (0.607) |
| Dlog(KP/PCP)_1 | 0.5306 (5.96) | 0.5309 (5.99) | 0.5475 (7.41) | 0.5042 (7.38) |
| Dlog(KP/PCP)_2 | 0.02437 (0.242) | 0.0302 (0.341) | . | . |
| Dlog(KP/PCP)_3 | 0.01096 (0.123) | . | . | . |
| I:1983(2) | . | . | . | 0.07577 (3.59) |
| I:1987(1) | . | . | . | 0.08063 (3.88) |
| $\hat{\sigma}$ | 0.02289 | 0.02281 | 0.02273 | 0.02071 |
| Log-lik. | 308.560 | 308.552 | 308.493 | 321.589 |
| AIC | -4.686 | -4.701 | -4.715 | -4.886 |
| HQ | -4.650 | -4.674 | -4.697 | -4.850 |
| SC/BIC | -4.597 | -4.635 | -4.671 | -4.798 |
| No autocorr. 1–5 | [0.13] | [0.19] | [0.18] | [0.11] |
| No hetero. | [0.05] | [0.02] | [0.04] | [0.05] |
| Normality | [0.00] | [0.00] | [0.00] | [0.28] |
| T | 130 | 130 | 130 | 130 |
