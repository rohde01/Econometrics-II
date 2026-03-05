# Hand-In Assignment #1: Forecasting Economic Growth and Growth-at-Risk

**Econometrics II | Department of Economics, University of Copenhagen | Spring 2026**

---

A central theme in macroeconomics and central banking is understanding the distribution of future GDP growth. From a policy or regulatory standpoint, it is useful to assess how present circumstances relate to future growth outcomes and to what extent they help predict those outcomes. Recent research has explored ways to measure growth vulnerability and its underlying drivers, see, e.g., Adrian et al. (2019)[^1]. One common approach is Growth-at-Risk (GaR), defined as a specific quantile of the conditional distribution of future GDP growth. GaR can be estimated using methods such as quantile regression[^2] or various dynamic time-series models[^3]. The methodology is occasionally applied by the IMF[^4] and has also been examined by the Danish Central Bank[^5].

Recent findings indicate that, when it comes to producing accurate GaR estimates, data-rich or machine-learning-based models do not systematically outperform simple univariate time-series approaches.[^6]

The purpose of this assignment is two-fold: We first seek to propose a univariate model for GDP growth. Based on this model, we subsequently seek to evaluate its (relative) forecasting accuracy and its ability to quantify GaR.

[^1]: Adrian, T., N. Boyarchenko, and D. Giannone, 2019, "Vulnerable Growth", *American Economic Review*, vol. 109, pp. 1263–1289.
[^2]: E.g., Plagborg-Møller, M., G. Ricco, L. Reichlin, and T. Hasenzagl, 2020, "When is growth at risk?", *Brookings Papers on Economic Activity*, pp. 167–229.
[^3]: E.g., Brownlees, C. and A.B.M. Souza, 2021, "Backtesting global Growth-at-Risk", *Journal of Monetary Economics*, vol. 118, 312–330.
[^4]: https://www.imf.org/en/Publications/WP/Issues/2019/02/21/Growth-at-Risk-Concept-and-Application-in-IMF-Country-Surveillance-46567
[^5]: https://www.nationalbanken.dk/en/news-and-knowledge/publications-and-speeches/archive-publications/2022/evaluating-the-macroprudential-stance-in-a-growth-at-risk-framework
[^6]: Adrian, T., H. Chen, M.-S. Dovi, and J.H. Lee, 2025, "Machine-learning Growth-at-Risk", https://arxiv.org/html/2506.00572v1

---

## The Data

The data file `Assignment_1.xlsx` contains quarterly data for the period 1990(1) to 2024(4), for the following variables:

- **GDPC1**: U.S. Real Gross Domestic Product (seasonally adjusted)
- **y**: log(GDPC1_t) − log(GDPC1_{t−4})

The GDPC1 series was retrieved from the FRED Database[^7]. Note that y_t quantifies the yearly GDP growth rate.

In addition, the file contains the series `forecast_naive`, which contains (one-period) forecasts of y for the period 2010(1) to 2024(4). Specifically, `forecast_naive` is the simple historical average of y from 1990(1) to 2009(4). Lastly, the file contains the series `GaR_np` which are one-period GaR estimates at risk level 10% for each quarter in the period 2010(1) to 2024(4). The series is constant and given by the sample (unconditional) 10%-quantile of y based on data for the period 1990(1) to 2009(4).

[^7]: https://fred.stlouisfed.org/series/GDPC1

---

## The Assignment

Estimate a univariate time series model for the GDP growth y_t or a suitable transformation of this variable for the period 1990(1) to 2009(4). Based on your preferred model, produce one-period forecasts for the later development in y_t from 2010(1) to 2024(4) (60 forecast observations in total). Compare your forecasts with the forecast series `forecast_naive` and the actual data series for y_t. In addition, use the model to produce one-period GaR estimates at risk level 10% from 2010(1) to 2024(4), and compare the estimates with the `GaR_np` series and the actual data series for y_t.

You are only required to assess stationarity of the variables based on a graphical inspection. You are allowed to consider the class of autoregressive models, AR(p) models, or the class of combined ARMA(p,q) models.

---

## Hints

1. For the graphical analysis, use any transformations of the variable you find relevant.
2. When using the OLS or ML estimator, carefully discuss which assumptions are required for deriving the estimator and explain if these assumptions are fulfilled, or not, empirically. If not, what are the consequences for your estimation results? Can you improve on this?
3. If you come up with several model specifications, select the one that seems the most relevant and justify your decision. Remember that in most cases, the simpler the better.
4. Be precise about the statistical tests you use for testing various hypotheses. Explain which null hypotheses you test, how you test them, and what your conclusions are. You do not have to explain the misspecification tests.
5. Consider how to formally compare competing forecasts.
6. For details about Growth-at-Risk, we refer to the Appendix below.

---

## Formal Requirements

1. You must hand in a report that (i) presents your graphical analysis, (ii) describes the econometric model, (iii) outlines the modeling progress (e.g., the approach you have taken, the alternative models you have tried, etc.), (iv) presents your preferred model including interpretation and statements on economic and statistical significance, and (v) discusses the potential weaknesses of the model.
2. The report must be a maximum of 12,000 characters including spaces (corresponding to 5 normal pages of text) plus 2 pages with output in the form of tables and graphs. The report must be written in English. It must be handed in as one pdf document. See Absalon for details.
3. You are allowed to work in groups of up to three persons (not necessarily in the same exercise class). The assessment criteria are given on the course page on Absalon.
4. Please do not write any names, student IDs, or exam numbers in your hand-in.

---

## Appendix: Details about Growth-at-Risk

### Preliminaries

Let Z be a standard normal random variable, N(0, 1), with CDF given by:

$$P(Z \leq x) = \Phi(x) := \int_{-\infty}^{x} \frac{1}{\sqrt{2\pi}} \exp\!\left(-\frac{y^2}{2}\right) dy, \quad x \in \mathbb{R}.$$

Let Φ⁻¹(α) denote the inverse CDF of Z, with α ∈ (0, 1). For instance, for α = 0.1, Φ⁻¹(0.1) ≈ −1.282 is the 10-percentile (or 10%-quantile) of N(0, 1).

For constants μ ∈ ℝ and σ ∈ (0, ∞), define:

$$X = \mu + \sigma Z.$$

With α ∈ (0, 1), the α-quantile (or 100α percentile) of X, denoted x_α, is defined by:

$$P(X \leq x_\alpha) = \alpha.$$

In particular, we have that:

$$\alpha = P(X \leq x_\alpha) = P\!\left(\frac{X - \mu}{\sigma} \leq \frac{x_\alpha - \mu}{\sigma}\right) = P\!\left(Z \leq \frac{x_\alpha - \mu}{\sigma}\right) = \Phi\!\left(\frac{x_\alpha - \mu}{\sigma}\right),$$

such that:

$$\frac{x_\alpha - \mu}{\sigma} = \Phi^{-1}(\alpha),$$

and, consequently, the α-quantile is given by:

$$x_\alpha = \mu + \sigma \Phi^{-1}(\alpha).$$

---

### Conditional Quantiles (Growth-at-Risk) for Univariate Time Series Models

Consider a univariate time series model:

$$y_t = \mu_t + \varepsilon_t, \quad t = 1, 2, \ldots, T,$$

where (ε_t)_{t=1,…,T} is an i.i.d. process with ε_t ~ N(0, σ²), and μ_t denotes the conditional mean of y_t, that is, μ_t = E[y_t | y_{t−1}, ε_{t−1}, …]. For instance, if y_t is given in terms of an AR(1) model, then μ_t = φ + φ₁y_{t−1}, and if y_t follows an ARMA(1,1) model, then μ_t = φ + φ₁y_{t−1} + θ₁ε_{t−1}. Note that μ_t is the best forecast of y_t given past observations I_{t−1} = (y_{t−1}, ε_{t−1}, …).

If y_t is the GDP growth rate for period t, the one-period Growth-at-Risk at risk level α ∈ (0, 1), denoted GaR^α_t, is given by:

$$P\!\left(y_t \leq \text{GaR}^\alpha_t \mid \mathcal{I}_{t-1}\right) = \alpha, \quad \text{GaR}^\alpha_t \in \mathcal{I}_{t-1},$$

that is, GaR^α_t is the α-quantile of the conditional distribution of GDP growth (y_t) given the information set I_{t−1}. Using that ε_t is independent of I_{t−1}, and that μ_t ∈ I_{t−1}, by derivations similar to those given in the previous section:

$$\text{GaR}^\alpha_t = \mu_t + \sigma \Phi^{-1}(\alpha).$$

---

### Evaluating GaR Estimates

When evaluating the accuracy of GaR estimates (GaR^α_t)_{t=1,…,T}, one may count how often the actual realized GDP growth was worse than the GaR. Let:

$$\text{hit}_t = \begin{cases} 1 & \text{if } y_t < \text{GaR}^\alpha_t \\ 0 & \text{if } y_t \geq \text{GaR}^\alpha_t \end{cases}, \quad t = 1, \ldots, T.$$

Then the frequency of GaR "violations" is given by:

$$\hat{p}_T = \frac{1}{T} \sum_{t=1}^{T} \text{hit}_t.$$

Under correct model specification, (hit_t)_{t=1,…,T} is an i.i.d. Bernoulli(α) process, and one may test the hypothesis of correct coverage:

$$E[\text{hit}_t] = \alpha,$$

using a simple t-test or likelihood ratio test (ignoring any estimation uncertainty arising from estimating μ_t and σ).

The variable hit_t does not capture how much y_t deviates from GaR^α_t. Instead one may look at the so-called "tick" loss function given by:

$$\mathcal{T}_\alpha(y_t, \text{GaR}^\alpha_t) := (\alpha - \text{hit}_t)(y_t - \text{GaR}^\alpha_t).$$

This loss function is particularly tailored for evaluating quantile forecasts such as GaR.[^8] Since α < 1, the function is asymmetric in the sense that negative deviations (y_t < GaR^α_t) are given more weight than positive deviations (y_t ≥ GaR^α_t).

[^8]: Giacomini, R., and I. Komunjer, 2005, "Evaluation and combination of conditional quantile forecasts", *Journal of Business & Economic Statistics*, vol. 23, pp. 416–431.
