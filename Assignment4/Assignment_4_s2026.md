# Econometrics II | Department of Economics, U. of Copenhagen | Spring 2026

# Hand-In Assignment #4: Volatility Timing in the U.S. Stock Market

## Introduction

A key property of stock market volatility is that it is highly persistent, or clusters: high volatility over the recent past tends to be followed by high volatility in the near future. This observation, which underpins the celebrated ARCH and GARCH models, raises an important question for investors: can the predictability of volatility be exploited to improve portfolio performance?

Harvey et al. (2018) study portfolios that are designed to counter fluctuations in volatility by scaling up the portfolio at times of low volatility and scaling down at times of high volatility. Effectively, the portfolio targets a constant level of volatility—say 10% annualized—rather than a constant notional exposure. They document that such volatility targeting typically improves investment performance as measured, for instance, in terms of larger Sharpe ratios and reduced tail risk. Relatedly, Moreira and Muir (2017) show that such strategies work because changes in volatility are not offset by proportional changes in expected returns.

Both studies approximate the conditional variance by the realized variance computed from recent returns. In this Assignment, you will instead use econometric time series models to forecast the conditional variance. You will first investigate whether market returns exhibit ARCH effects and asymmetric (leverage) volatility responses. You will then use your model to construct a volatility-targeted portfolio and evaluate whether it outperforms alternative strategies.

## The Data

The data file `Assignment_4.xlsx` contains monthly data for the period July 1926 to February 2026, for the following variables:

- **mkt**: Log return on the U.S. stock market (in percent per month)
- **rf**: Risk-free rate (in percent per month)

The underlying data were retrieved from Kenneth French's website. The market return $\text{mkt}_t$ is the value-weighted return on all firms listed on the NYSE, AMEX, and NASDAQ exchanges. The risk-free rate is based on short-term U.S. Treasury Bills.

Define the log excess return as:
$$x_t = \text{mkt}_t - \text{rf}_t$$

The file also contains the precomputed variable:

- **xs_scaled_bt**: Benchmark volatility-scaled excess return (in percent per month), defined as:

$$\text{xs\_scaled\_bt} = \frac{\bar{\sigma}}{\hat{\sigma}^{\text{ew}}_t} \cdot x_t \quad (2.1)$$

where $\hat{\sigma}^{\text{ew}}_t$ is the expanding-window standard deviation of $x_t$ computed using all observations from the beginning of the sample up to and including period $t-1$. The volatility target is set to $\bar{\sigma} = 10\% / \sqrt{12}$ per month, corresponding to 10% annualized (see the appendix for further details).

## The Assignment

Using graphical methods and relevant econometric time series models, investigate whether the log excess return $x_t = \text{mkt}_t - \text{rf}_t$ exhibits ARCH effects. Moreover, investigate whether there is evidence of asymmetric volatility (leverage effects), i.e., whether negative returns have a larger impact on future volatility than positive returns of the same magnitude.

Based on your preferred estimated model, construct volatility-scaled excess returns:
$$x^*_t = \frac{\bar{\sigma}}{\hat{\sigma}_t} \cdot x_t \quad (2.2)$$

where $\hat{\sigma}_t = \sqrt{\hat{\sigma}^2_t}$ is the estimated conditional standard deviation from your econometric model, and $\bar{\sigma} = 10\% / \sqrt{12}$ as above.

Compare your volatility-scaled returns $x^*_t$ with the unscaled excess returns $x_t$ and the benchmark $\text{xs\_scaled\_bt}$, using at least one of the performance measures described in the appendix. Comment on your findings.

## Hints

1. For the graphical analysis, use any transformations of the variables you find relevant.
2. You can use any model for the conditional mean and variance that you find relevant.
3. Carefully motivate the model that you use.
4. Be precise about the statistical tests that you use for testing various hypotheses. Explain the null hypotheses, how you test them, and what your conclusions are.
5. The spanning regression (2.3) in the appendix provides a direct test of whether volatility targeting adds value.

## Formal Requirements

1. You must hand in a report that:
   - (i) presents your graphical analysis and preliminary tests
   - (ii) describes the econometric model
   - (iii) outlines the modeling progress (e.g., the approach you have taken, the alternative models you have tried, etc.)
   - (iv) presents your preferred model including interpretation and statements on economic and statistical significance
   - (v) evaluates the volatility-targeting strategy and discusses the potential weaknesses of the approach

2. The report must be a maximum of 12,000 characters including spaces (corresponding to 5 normal pages of text) plus 2 pages with output in the form of tables and graphs. The report must be written in English. It must be handed in as a PDF document. See Absalon for details.

3. If you prefer, you are allowed to work in groups of up to three persons (not necessarily in the same exercise class as yours). The assessment criteria are given on the course page on Absalon.

4. Please do not write any names, student IDs, or exam numbers in your hand-in.

---

## Appendix: Volatility Targeting and Performance Evaluation

### Volatility Targeting

Consider a monthly excess return series $\{x_t\}^T_{t=1}$. The idea of volatility targeting is to scale the return at each point in time by the ratio of a fixed volatility target $\bar{\sigma}$ to the current conditional standard deviation $\sigma_t$. The volatility-scaled return is:

$$x^*_t = \frac{\bar{\sigma}}{\sigma_t} \cdot x_t$$

where $\sigma_t = \sqrt{\mathbb{V}[x_t | \mathcal{I}_{t-1}]}$ and $\sigma_t \in \mathcal{I}_{t-1}$, i.e., the conditional standard deviation is known at the end of period $t-1$. If the volatility model is well-specified, the conditional standard deviation of the scaled return is:

$$\sqrt{\mathbb{V}[x^*_t | \mathcal{I}_{t-1}]} = \frac{\bar{\sigma}}{\sigma_t} \cdot \sigma_t = \bar{\sigma}$$

which is constant over time. In practice, we replace $\sigma_t$ with an estimate $\hat{\sigma}_t$. For the benchmark in (2.1), we use the expanding-window sample standard deviation. For the GARCH-based strategy in (2.2), we use the GARCH conditional standard deviation.

We set the annualized volatility target to $\bar{\sigma}_{\text{ann}} = 10\%$. Since the data are monthly, the corresponding monthly target is:

$$\bar{\sigma} = \frac{\bar{\sigma}_{\text{ann}}}{\sqrt{12}} = \frac{0.10}{\sqrt{12}} \approx 0.0289$$

or approximately 2.89% per month. Note that $x_t$ is measured in percent in the data file, so $\bar{\sigma}$ should be expressed as $2.89$ (percent) when computing (2.1) and (2.2).

### Performance Evaluation

The following measures can be used to compare unscaled and volatility-scaled returns:

#### Sharpe Ratio

The annualized Sharpe ratio of an excess return series $\{r_t\}$ is (assuming stationarity):

$$\text{SR} = \frac{\mathbb{E}[r_t]}{\sqrt{\mathbb{V}(r_t)}} \cdot \sqrt{12}$$

This quantity can be estimated by its sample equivalent:

$$\widehat{\text{SR}} = \frac{\bar{r}}{\hat{\sigma}_r} \cdot \sqrt{12}$$

where $\bar{r}$ and $\hat{\sigma}_r$ are the sample mean and sample standard deviation of $r_t$, respectively.

#### Spanning Regression

Following Moreira and Muir (2017), one can test whether a volatility-timed strategy improves the Sharpe ratio by estimating $(\alpha, \beta)$ by OLS in the static regression:

$$x^*_t = \alpha + \beta x_t + \varepsilon_t \quad (2.3)$$

A positive and statistically significant $\alpha$ indicates that volatility timing improves the risk-return trade-off relative to the unscaled strategy, $x_t$. When testing $H_0: \alpha = 0$, use HAC standard errors to account for potential heteroskedasticity and autocorrelation in the error term.

---

## References

Harvey, C. R., E. Hoyle, R. Korgaonkar, S. Rattray, M. Sargaison, and O. Van Hemert (2018), "The Impact of Volatility Targeting", *The Journal of Portfolio Management*, vol. 45, 14–33.

Moreira, A. and T. Muir (2017), "Volatility-Managed Portfolios", *The Journal of Finance*, vol. 72, 1611–1643.

**Data source**: Kenneth French's Data Library
https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/Data_Library/f-f_factors.html

---

### Technical Note on Data Construction

The variables were constructed as continuously compounded (log) returns. Specifically, let $R^m_t$ and $R^f_t$ denote the simple (arithmetic) market return and risk-free rate, respectively, from the Fama-French dataset (both quoted in percent). Then:

$$\text{mkt}_t = 100 \cdot \ln(1 + R^m_t / 100)$$
$$\text{rf}_t = 100 \cdot \ln(1 + R^f_t / 100)$$
