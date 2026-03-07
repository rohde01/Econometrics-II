# Econometrics II | Department of Economics, Copenhagen | Rasmus S. Pedersen

# Problem Set #2
## Univariate Time Series Models

During this exercise class, you are asked to work with univariate time series models. First, Exercise #2.1 asks you to estimate univariate time series models for some Danish time series. Secondly, Exercise #2.2 contains an example of an exam question about ARMA processes.

Next, Exercise #2.3 is optional. It considers a first-order moving average model and asks you to derive the unconditional mean, variance, and autocovariances. This is very close to what is done in the lecture notes. Finally, the optional Exercise #2.4 considers a first-order autoregressive model and asks you to derive the moving average representation and use it to discuss the properties of the model. Again, this is very close to what is done in the lecture notes.

---

## #2.1 ARIMA Models for Danish Macro Time Series

The file `TimeSeries.oxdata` contains the following quarterly time series for the Danish economy covering 1971:1 – 2018:3:

| Variable | Description |
|----------|-------------|
| EFKRKS | Effective (nominal) exchange rate index |
| ENL | Current account (current prices) |
| FIPMXE | Business machinery investments (constant prices) |
| FY | Total GDP (constant prices) |
| IBZ | Bond yield (pro anno yield in ratio) |
| KP | House price index |
| PCP | Consumption deflator |
| UNR | Unemployment rate (ratio) |
| TT | Terms of trade, export price/import price |

**(1)** Select the time series you want to analyze. It could be a raw series or a transformation, such as the real house price or the (ex post) real interest rate. Discuss if it is preferable to analyze the log of your chosen time series.

**(2)** Draw a graph of your chosen time series. If the time series does not look stationary from a visual inspection, take first differences and construct a new graph.

**(3)** Draw the autocorrelation function, ACF, and the partial autocorrelation function, PACF, for your time series. What does that suggest about the dynamic properties of the time series?

> **Hint:** To draw the ACF and PACF, choose **[Graphics]** from the **[Model]** menu in OxMetrics, select your variable, press **[All plot types]** and select ACF or PACF under **[Time-series properties]**.

**(4)** Now estimate the relevant candidate AR or ARMA model. You can select which class of models you prefer to consider.

> **Hint:** To estimate an AR model, select the **[Models for time-series data]** and choose the **[Single-Equation Dynamic Modelling using PcGive]** in the **[Model class]** menu. In the data selection window, include the number of lagged variables. To estimate an ARMA model, select the **[Models for time-series data]** and choose the **[ARFIMA models using PcGive]** in the **[Model class]** menu. In the data selection window, include the time series with no lags and a constant term and press OK. In the model settings window, specify the AR order and MA order. Under Fractional parameter, choose to fix *d* at 0, and estimate the model with maximum likelihood.
>
> To be able to automatically construct general-to-specific likelihood ratio tests in OxMetrics, you should estimate the general model before the specific models.

**(5)** Choose **[Progress]** in the menu to get a table with information criteria and other relevant information. Which model do you prefer?

**(6)** Reestimate the preferred model and look at graphical output for the residuals, e.g. residual ACF, PACF, and histogram/density. Also calculate the available misspecification tests. What do you conclude concerning the fit of the model?

**(7)** Finally reestimate the model but retain 24 observations for forecasts. Forecast the 24 periods and compare the forecasts with the actual values.

In your own words, characterize the nature of a univariate time series forecast. What do you conclude regarding the forecast performance of the model?

---

## #2.2 ARMA Processes (Example of an Exam Question)

**(1)** Consider the model given by

$$\phi(L)y_t = \psi_t \tag{2.1}$$

$$\phi(L)\psi_t = \varepsilon_t \tag{2.2}$$

where $\phi(L)$ and $\theta(L)$ are lag polynomials of degrees $p$ and $q$, respectively, and $\varepsilon_t$ and $\psi_t$ are mutually independent and distributed as i.i.d.(0,1). Assume that both polynomials are invertible, and show that these equations imply an autoregressive structure,

$$\Pi(L)y_t = \varepsilon_t \tag{2.3}$$

Give the order of the polynomial $\Pi(L)$.

Now assume that $p = q = 1$ with

$$\phi(L) = 1 - \phi L \quad \text{and} \quad \theta(L) = 1 - \theta L \tag{2.4}$$

Find an explicit expression for $\Pi(L)$ in this case and write the corresponding AR equation for $y_t$.

**(2)** Now consider a new process

$$y_t = x_t + \varepsilon_t + \varepsilon_{t-1} \tag{2.5}$$

where $\varepsilon_t$ and $x_t$ are mutually independent and both are i.i.d. $N(0, 1)$. We may think of (2.5) as a moving-average process with an explanatory variable (MA-X).

Find the mean, variance and auto-covariances of $y_t$ and suggest an ARMA model with the same number of non-zero auto-covariances.

Next consider the standard MA(1) process of the form

$$z_t = u_t + \theta u_{t-1}, \quad u_t \overset{d}{=} N(0, \sigma_u^2) \tag{2.6}$$

with $|\theta| < 1$. Give expressions for $\theta$ and $\sigma_u^2$ such that the processes $y_t$ and $z_t$ are observationally equivalent, in the sense that they have the same unconditional mean, variance and auto-covariances.

Calculate the parameters in the equation for $z_t$ for the case $\alpha = 0.5$.

---

## #2.3 The First-Order Moving Average Model (optional)

Consider the first-order moving average, MA(1), model,

$$z_t = \mu + \varepsilon_t + \theta\varepsilon_{t-1}, \quad t = 1, 2, \ldots, T, \quad \varepsilon_0 \text{ given} \tag{2.7}$$

where the error term, $\varepsilon_t$, is assumed to be independently and identically distributed with mean zero and variance $\sigma^2$. We write that $\varepsilon_t$ is i.i.d.$(0, \sigma^2)$ and we refer to such a process as a white noise process.

To characterize the properties of the stochastic process for $z_t$, we derive the unconditional mean, variance, and autocovariances. In particular, we are interested in whether the MA(1) process is (weakly) stationary.

**(1)** Derive the unconditional mean $E(z_t)$.

**(2)** Derive the unconditional variance $V(z_t)$.

**(3)** Show that the first autocovariance, $\gamma_1$, is given by:

$$\gamma_1 = \text{cov}(z_t, z_{t-1}) = E((z_t - E(z_t))(z_{t-1} - E(z_{t-1}))) = \theta\sigma^2$$

and derive the second autocovariance,

$$\gamma_2 = \text{cov}(z_t, z_{t-2}) = E((z_t - E(z_t))(z_{t-2} - E(z_{t-2})))$$

**(4)** Explain whether the MA(1) process is weakly stationary.

---

## #2.4 The First-Order Autoregressive Model (optional)

Consider the AR(1) model,

$$y_t = \mu + \phi y_{t-1} + \varepsilon_t, \quad t = 1, 2, \ldots, T \tag{2.8}$$

where the error term, $\varepsilon_t$, is i.i.d.$(0, \sigma^2)$, and the initial value $y_0$ is given.

To characterize the properties of the stochastic process for $y_t$, we are interested in deriving the unconditional mean, variance, and autocovariances. In the previous exercise, we could derive these directly for the MA(1) process as the process only depended on the innovations $\varepsilon_t$. For the AR(1) process, we first derive the moving average representation for $y_t$ and use the moving average representation to derive the properties of the stochastic process for $y_t$.

**(1)** Derive the moving average representation of $y_t$ by recursive substitution.

> **Hint:** Start from equation (2.8). On the right-hand side, insert the expression for $y_{t-1}$ as given by the model. Next, insert an expression for $y_{t-2}$, and continue, until you have expressed $y_t$ in terms of the initial value $y_0$, the constant term, $\mu$, and the sequence of shocks, $\varepsilon_1, \varepsilon_2, \ldots, \varepsilon_t$.

**(2)** Assuming that the coefficient $\phi$ satisfies the condition $|\phi| < 1$, use the moving average representation to explain what happens to the effect of the initial value $y_0$ on $y_t$ as $t \to \infty$.

Still assuming that $|\phi| < 1$, explain what happens to the effect of past shocks, say $\varepsilon_1$, on $y_t$ as $t \to \infty$. Do the shocks have a transitory or permanent effect on $y_t$? Would the effects of the initial value and the innovations be the same if $\phi = 1$?

Use the moving average representation of $y_t$ to derive the conditional mean $E(y_t | y_0)$.

**(3)** Now, assume that the process $y_t$ started in the infinite past instead of at $t = 0$. That abstract assumption allows us to continue the recursive substitution in Question (2.8) infinitely back in time, which is equivalent to assuming that the initial value $y_0$ can be represented as:

$$y_0 = (1 + \phi + \phi^2 + \cdots)\mu + \sum_{i=0}^{\infty} \phi^i \varepsilon_{-i}$$

Insert this expression for the initial value $y_0$ in the moving average representation for $y_t$ to derive the solution for $y_t$ in terms of the innovations $\varepsilon_t, \varepsilon_{t-1}, \ldots, \varepsilon_1, \varepsilon_0, \varepsilon_{-1}, \ldots$ and the constant term $\mu$:

$$y_t = (1 + \phi + \phi^2 + \phi^3 + \cdots)\mu + \varepsilon_t + \phi\varepsilon_{t-1} + \phi^2\varepsilon_{t-2} + \cdots + \phi^t\varepsilon_0 + \phi^{t+1}\varepsilon_{-1} + \cdots$$

$$= \sum_{i=0}^{\infty} \phi^i \mu + \sum_{i=0}^{\infty} \phi^i \varepsilon_{t-i}$$

We refer to this solution as the **infinite moving average representation**.

**(4)** Assume that the stationarity condition, $|\phi| < 1$, is satisfied.

Use the infinite moving average representation to derive the unconditional mean $E(y_t)$.

Explain why the condition $|\phi| < 1$ is necessary for the stochastic process $y_t$ to be stationary. What would happen to the unconditional mean $E(y_t)$ if $\phi = 1$?

**(5)** Show that the unconditional variance of $y_t$ is given by:

$$\gamma_0 = V(y_t) = E((y_t - E(y_t))^2) = \frac{\sigma^2}{1 - \phi^2}$$

**(6)** Show that the first and second autocovariances, $\gamma_1$ and $\gamma_2$, are given by:

$$\gamma_1 = \text{cov}(y_t, y_{t-1}) = E\left((y_t - E(y_t))(y_{t-1} - E(y_{t-1}))\right) = \phi\gamma_0$$

$$\gamma_2 = \text{cov}(y_t, y_{t-2}) = E\left((y_t - E(y_t))(y_{t-2} - E(y_{t-2}))\right) = \phi^2\gamma_0$$

The autocorrelation function (ACF) is defined as:

$$\rho_k = \frac{\gamma_k}{\gamma_0}$$

Explain how the autocorrelation function depends on the parameters of the AR(1) model. What happens to $\rho_k$ as $k$ increases?

**(7)** Autoregressive models are often used to create forecasts and forecast variances of future observations. For example, we can use the model for $y_t$ for $t = 1, 2, \ldots, T$ in (2.8) to create the out-of-sample forecast and forecast variance of $y_{T+1}$. Despite the simplicity of autoregressive models, they have the advantage of requiring only past observations of the time-series of interest, they serve as a good benchmark for forecasts based on more sophisticated models, and they have shown hard to beat in practice.

Given the AR(1) model in (2.4), the optimal point forecast of $y_{T+1}$ is given by the conditional expectation $E(y_{T+1} | \mathcal{I}_T)$, where $\mathcal{I}_T = \{y_0, y_1, \ldots, y_T\}$ is the information set available at time $T$, i.e. at the end of the sample.

Derive the out-of-sample forecast of $y_{T+1}$ given by $E(y_{T+1} | \mathcal{I}_T)$.

In addition to the optimal point forecast, we are always interested in the variance of the forecast. For example, we can use the forecast variance to derive a confidence interval for our forecast, which is more relevant to report than the point forecast alone.

The forecast variance is given by the conditional variance:

$$V(y_{T+1} | \mathcal{I}_T) = E\left((y_{T+1} - E(y_{T+1} | \mathcal{I}_T))^2 \,\big|\, \mathcal{I}_T\right)$$

As $y_{T+1} - E(y_{T+1} | \mathcal{I}_T)$ is the forecast error, the forecast variance $V(y_{T+1} | \mathcal{I}_T)$ equals the conditional variance of the forecast error.

Derive the forecast variance given by $V(y_{T+1} | \mathcal{I}_T)$.
