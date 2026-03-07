# A Model-Based Approach to Hypothesis Testing

**Econometrics II | Department of Economics, Copenhagen | Rasmus S. Pedersen**

---

Consider a time series process $\{x_t\}_{t=1,\ldots,T}$ with $T = 100$. A realization of the time series is given in the data set `x_series.xlsx`.

Let $\mu = E[x_t]$ denote the mean of $x_t$ (for all $t$). Based on the data we seek to test the hypothesis

$$H_0 : \mu = 10$$

against the two-sided alternative $H_A : \mu \neq 10$. To do so, we consider two different statistical models for testing $H_0$, both relying on maximum likelihood estimation. The first model is the **Gaussian location model** and the second is the **AR(1) model**.

---

## Model 1: The Gaussian Location Model

As you may recall from the lectures, the Gaussian location model is given by

$$x_t = \mu + \varepsilon_t, \quad t = 1, \ldots, T,$$

with $\varepsilon_t \sim i.i.d.\, N(0, \sigma^2)$ and $\mu \in \mathbb{R}$ and $\sigma^2 > 0$. Recall also that the MLE for $\mu$ is

$$\hat{\mu}_T = \frac{1}{T} \sum_{t=1}^{T} x_t,$$

and with $\mu_0$ and $\sigma_0^2$ denoting the true values of $\mu$ and $\sigma^2$, respectively, it holds that as $T \to \infty$

$$\sqrt{T}(\hat{\mu}_T - \mu_0) \xrightarrow{d} N(0, \sigma_0^2).$$

This result suggests that a $t$-test for $H_0$ can be carried out by computing the $t$-statistic

$$t_{H_0} = \frac{\hat{\mu}_T - 10}{\sqrt{\hat{\sigma}^2_T / T}},$$

and compare $|t_{H_0}|$ with the critical value $1.96$ (testing at a 5% nominal level). Here $\hat{\sigma}^2_T$ is the maximum likelihood estimate of $\sigma^2$ given by

$$\hat{\sigma}^2_T = \frac{1}{T} \sum_{t=1}^{T} (x_t - \hat{\mu}_T)^2,$$

and $\sqrt{\hat{\sigma}^2_T / T}$ is the estimated standard error of $\hat{\mu}_T$.

### Questions

**(1)** Based on the provided data set, compute $\hat{\mu}_T$ and $\sqrt{\hat{\sigma}^2_T / T}$:

> **Hint:** In PcGive, choose "Models for time-series data" (Category) and "Single-equation Models" (Model class). Then estimate a linear regression model for $x_t$ with a constant being the only regressor. The estimation method is OLS, and $\sqrt{\hat{\sigma}^2_T / T}$ is simply the "Standard" standard error.

**(2)** Carry out the test for $H_0$ based on $t_{H_0}$ as described above. What is your conclusion about the hypothesis?

---

## Model 2: The AR(1) Model

Next, consider the AR(1) model for $x_t$ given by

$$x_t = \alpha + \rho x_{t-1} + \varepsilon_t, \quad t = 1, \ldots, T,$$

with $\varepsilon_t \sim i.i.d.\, N(0, \sigma^2)$ and $\alpha \in \mathbb{R}$ and $\sigma^2 > 0$, and $x_0 = 10$ (fixed). Assume throughout that $|\rho| < 1$ (the stationarity region for the model). In this case, it holds that $x_t$ is stationary with

$$E[x_t] = \frac{\alpha}{1 - \rho}.$$

Recall that the MLE for $(\alpha, \rho)$ is simply given by the OLS estimator from regressing $x_t$ on $(1, x_{t-1})$, and testing $H_0$ can be done by testing the non-linear hypothesis $\alpha/(1-\rho) = 10$.

We will make a shortcut and reformulate the model in terms of $\mu$. In particular, using that $\alpha = \mu(1-\rho)$, we have that

$$x_t = \mu(1 - \rho) + \rho x_{t-1} + \varepsilon_t. \tag{M.1}$$

The model (M.1) can be estimated by maximum likelihood. Assuming that the true value $|\rho_0| < 1$, it holds that the MLE for $(\mu, \rho, \sigma^2)$, denoted $(\hat{\mu}_{T,ML}, \hat{\rho}_{T,ML}, \hat{\sigma}^2_{T,ML})$ is asymptotically normal, and a $t$-test for $H_0$ can be carried out by computing the $t$-statistic

$$\tilde{t}_{H_0} = \frac{\hat{\mu}_{T,ML} - 10}{s.e.(\hat{\mu}_{T,ML})},$$

and compare $|\tilde{t}_{H_0}|$ with the critical value $1.96$ (again testing at a 5% nominal level). Here $s.e.(\hat{\mu}_{T,ML})$ is an estimate of the standard error of $\hat{\mu}_{T,ML}$ (which may be derived from the information matrix; see lecture notes for details).

### Questions

**(1)** Based on the provided data set, compute $(\hat{\mu}_{T,ML}, \hat{\rho}_{T,ML}, \hat{\sigma}^2_{T,ML})$:

> **Hint:** In PcGive, choose "Models for time-series data" (Category) and "ARFIMA Models" (Model class). Estimate the AR(1) model. Remember to fix the parameter $d$ at 0 (zero) when formulating the model. Lastly, choose "Maximum Likelihood" as the estimation method. The estimate of the "Constant" in the output is $\hat{\mu}_{T,ML}$.

**(2)** Use the reported standard error of $\hat{\mu}_{T,ML}$ to carry out the $t$-test based on $\tilde{t}_{H_0}$. What is your conclusion?

**(3)** The hypothesis $H_0$ is true. In fact, the data-generating process of $x_t$ is given by (M.1) with $(\mu_0, \rho_0, \sigma_0^2) = (10, 0.9, 1)$.

Why — do you think — is the hypothesis rejected when using Model 1, but not rejected based on Model 2? Briefly consider how the use of misspecification tests could (potentially) have prevented you from drawing a false conclusion about $H_0$.
