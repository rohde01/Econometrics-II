# Problem Set #1: Maximum Likelihood Estimation

**Econometrics II | Department of Economics, Copenhagen | Heino Bohn Nielsen**

---

Welcome to the exercise classes in Econometrics II. Through the 13 weeks of exercises, you will work with 8–9 problem sets, each dealing with one of the main topics in the curriculum. In addition, there are four assignments that you hand in through the peer-feedback platform. For each of the four assignments, the exercise class takes the form of a workshop, where you can work on the assignment, discuss the material with fellow students, ask questions and get assistance.

We strongly believe that in order to learn econometrics, it is important that you read and understand the written material, but also that you work with the tools and arguments by yourself and that you apply the models to actual economic data. The problem sets and assignments are designed to encourage that and include:

**(i) Theoretical exercises.** They deal with main issues and tools presented at the lectures and are useful in order to become familiar with the econometric reasoning and to obtain a firm understanding of the mathematical structure of the models.

**(ii) Empirical exercises.** These exercises deal with real economic data and are constructed as step-by-step guides on how to perform an empirical analysis within the current topic and which problems and issues to consider in the interpretation. Later on, if you want to perform a similar analysis of a different topic, the steps in these exercises are typically helpful. Throughout, some hints are given on how to practically perform the analyses within the software package OxMetrics.

**(iii) Assignments.** These are case studies, which are loosely formulated economic hypotheses or problems that you are asked to analyze. For these case studies you are given a relevant data set and a formulation of the problem, but there are only few hints on how to proceed, and it is up to you to design the empirical analysis; you are encouraged to work in groups. It is important to realize that there is no single correct answer to these questions (!) and several different routes may be relevant as long as you can convincingly argue for the choices you make.

The work with the empirical case studies — and the fact that you write a short empirical paper for each — will give you a good background for potential empirical analyses in your B.Sc. projects or M.Sc. theses.

---

This first problem set deals with the likelihood analysis and applications to some simple models. Exercise #1.1 is a simple maximum likelihood (ML) estimation in an exponential model. Exercise #1.2 is optional. It derives the maximum likelihood estimator in a first order autoregressive model to illustrate how to deal with dependent observations. Exercise #1.3 is an empirical linear time-series regression applied to Danish consumption data.

---

## #1.1 ML Estimation in an Exponential Model

Imagine that a manufacturer of light-bulbs is interested in estimating the expected lifetime of a bulb. From an experiment he observes a sequence of $n$ independent lifetimes, $x_1, x_2, \ldots, x_n$. From experience he knows that the lifetime of an individual bulb, $x_i$, follows an exponential distribution with expectation $\lambda$, i.e. with a density function given by

$$f(x_i \mid \lambda) = \frac{1}{\lambda} \exp\left\{-\frac{x_i}{\lambda}\right\}, \quad i = 1, 2, \ldots, n, \tag{1.1}$$

where $x_i > 0$ and $\lambda > 0$.

**(1)** Present the intuition for the maximum likelihood estimation principle, and outline the basic steps in deriving the estimator and the covariance matrix of the estimates.

**(2)** Write the log-likelihood function for the set of observations, $x_1, x_2, \ldots, x_n$. Be explicit on your assumptions.

**(3)** Derive the maximum likelihood estimator, $\hat{\lambda}$.

Assume that the manufacturer has observed $n = 100$ lifetimes, $x_1, x_2, \ldots, x_{100}$, and that $\sum_{i=1}^{100} x_i = 987$. Find the maximum likelihood estimate for this case.

Explain the difference between the *estimate* and the *estimator*.

**(4)** Find the Hessian contribution as the second derivative

$$H_i(\lambda) = \frac{\partial^2 \log \ell_i(\lambda)}{\partial \lambda \, \partial \lambda},$$

where $\log \ell_i(\lambda)$ is the log of the likelihood contribution for observation $i$, and the information,

$$\mathcal{I}(\lambda) = E[H_i(\lambda)].$$

**(5)** State the conditions under which the MLE is asymptotically normal, such that

$$\sqrt{n}(\hat{\lambda} - \lambda_0) \xrightarrow{d} N\bigl(0,\, \Omega(\lambda_0)\bigr), \quad \text{with } \Omega(\lambda_0) = \mathcal{I}(\lambda_0)^{-1}.$$

Check the conditions for the current model and argue that they are satisfied.

**(6)** State the asymptotic variance of $\hat{\lambda}$ for the example above.

**(7)** Explain the Wald principle for hypotheses testing.

Construct a Wald test for the hypothesis that the expected lifetime is $11.1$ in the numerical example above. Be specific with the formulation of hypothesis, statistic, and critical value.

What do you conclude?

---

## #1.2 ML Estimation in an Autoregressive Model *(optional)*

Consider the first order autoregressive, AR(1), model

$$y_t = \phi \, y_{t-1} + \varepsilon_t, \quad t = 1, 2, \ldots, T, \tag{1.2}$$

where we assume that $\varepsilon_t \mid y_{t-1}$ is independently and identically distributed as $N(0, \sigma^2)$. Let $y_0$ denote the initial observation.

**(1)** Show how the joint density function for the time series, $y_0, y_1, \ldots, y_T$, denoted

$$f(y_0, y_1, \ldots, y_T \mid \phi, \sigma^2),$$

can be factorized into a series of conditional and marginal distributions. Discuss how to construct the likelihood function for $y_1, y_2, \ldots, y_T$ conditional on $y_0$.

How does this procedure differ from the i.i.d. case above?

**(2)** Find an expression for the likelihood contribution for $y_t \mid y_{t-1}$, denoted $\ell_t(\phi, \sigma^2)$, and state the likelihood function for $y_1, y_2, \ldots, y_T \mid y_0$.

Also write the corresponding log-likelihood function.

**(3)** Calculate the individual scores

$$s_t(\phi, \sigma^2) = \begin{pmatrix} \dfrac{\partial \log \ell_t(\phi, \sigma^2)}{\partial \phi} \\[8pt] \dfrac{\partial \log \ell_t(\phi, \sigma^2)}{\partial \sigma^2} \end{pmatrix}.$$

**(4)** State the likelihood equations as the first order conditions for maximizing the log-likelihood function.

Solve the first order conditions and find the ML estimators, $\hat{\phi}$ and $\hat{\sigma}^2$.

**(5)** How do the ML estimators compare to the OLS estimators in model (1.2)?

**(6)** Find the Hessian matrix of double derivatives,

$$H_t(\phi, \sigma^2) = \begin{pmatrix} \dfrac{\partial^2 \log \ell_t}{\partial \phi \, \partial \phi} & \dfrac{\partial^2 \log \ell_t}{\partial \phi \, \partial \sigma^2} \\[10pt] \dfrac{\partial^2 \log \ell_t}{\partial \sigma^2 \partial \phi} & \dfrac{\partial^2 \log \ell_t}{\partial \sigma^2 \partial \sigma^2} \end{pmatrix},$$

and the information matrix $\mathcal{I}(\phi, \sigma^2) = E[H_t(\phi, \sigma^2)]$.

**(7)** State the conditions under which the MLE is asymptotically normal.

Check the conditions for the current model and argue that they are satisfied.

**(8)** State the asymptotic distribution.

---

## #1.3 Time Series Regression for Private Consumption

To introduce the software package OxMetrics, we consider a data set for aggregate private consumption in Denmark for the period 1971:1–2018:3. To obtain stationary variables we transform the variables by taking first-differences and by making linear combinations, i.e. by co-integration. We treat this topic in more detail later in the course.

**(1)** Download the data from the Absalon course page to your own computer. The data in OxMetrics format is:

```
ConsumptionData.oxdata
```

Start OxMetrics, unzip the file and open the data set. The data set contains observations for the variables:

| Variable | Description |
|----------|-------------|
| `FCP` | Private sector aggregate consumption, constant prices |
| `PCP` | Deflator for private consumption, 2010 = 1 |
| `FYD_H` | Disposable income in the household sector, constant prices |
| `FWCP` | Private wealth including owner occupied housing, constant prices |
| `ARBLOS` | Expected income loss from changes in unemployment |
| `IBZ` | Average bond rate, fractions, p.a. |

All the variables, except the interest rate, are seasonally adjusted and are taken from the data base from the model MONA of the Danish Central Bank.

Have a look at the data to see how the database is organized.

**(2)** Choose **[Graphics...]** in the **[Model]** menu and construct time series graphs of the variables. Characterize the time series behavior of the variables.

**(3)** For the empirical modelling, construct the derived variables

$$c_t = \log(\text{FCP}_t)$$
$$y_t = \log(\text{FYD\_H}_t)$$
$$w_t = \log(\text{FWCP}_t)$$
$$p_t = \log(\text{PCP}_t)$$
$$\pi_t = 4 \Delta p_t = p_t - p_{t-4}$$
$$r_t = \text{IBZ}_t - \pi_t$$

where $\log(\cdot)$ denotes the natural logarithm (as always!). To make the transformations choose the **[Algebra...]** editor in the **[Model]** menu and load the algebra file `ConsumptionData.alg` located also on the home page. Run the algebra file. Take a look at the database. What variables have been constructed? Note that the file name is now followed by a `*`. What does that mean?

> **Hint:** Note that the algebra editor is case sensitive. One way to work with data files in OxMetrics is to use a data file for the original data and save an algebra file with transformations. Each time you open the data file you should run the associated algebra file to apply the transformations to the data base. Alternatively, you can save your data including the transformed variables. If you work with the data for longer periods, however, the number of variables will typically grow and it is often difficult to remember how all the transformed variables were defined.

**(4)** Draw time series graphs of the transformed variables $c_t$, $y_t$, $w_t$, $\pi_t$, $\text{IBZ}_t$, $r_t$ and $\text{ARBLOS}_t$; and discuss the economic development in Denmark over the period.

From a graphical inspection, do any of the variables appear stationary?

In the construction of time series regression models, why is it important that the included variables are stationary?

**(5)** To obtain stationary variables consider the following transformations:

$$\Delta c_t = c_t - c_{t-1}$$
$$\Delta y_t = y_t - y_{t-1}$$
$$\Delta w_t = w_t - w_{t-1}$$
$$\Delta r_t = r_t - r_{t-1}$$
$$\text{ECM}_t = c_t - 0.679423 - 0.766989 \cdot y_t - 0.122943 \cdot w_t$$

Draw time series graphs of the new variables.

From a graphical inspection, do the transformed variables appear stationary?

> **Hint:** The variable $\text{ECM}_t$ can be thought of as the deviation of consumption, $c_t$, from the equilibrium value in period $t$ and it is formally constructed using co-integration. We will return to this issue later in the course; for now just think of $\text{ECM}_t$ as an additional explanatory variable.

**(6)** When you construct an empirical model for the consumption data, do you think it is preferable to start with a simple model and then successively include more explanatory variables; or do you think it is preferable to begin with a general model and delete insignificant variables? Motivate your answer.

**(7)** Consider the following regression model

$$\Delta c_t = \beta_1 + \beta_2 \, \Delta c_{t-1} + \beta_3 \, \Delta y_t + \beta_4 \, \Delta y_{t-1} + \beta_5 \, \Delta w_t + \beta_6 \, \Delta w_{t-1} + \beta_7 \, \Delta r_t + \beta_8 \, \Delta r_{t-1} + \beta_9 \, \text{ARBLOS}_t + \beta_{10} \, \Delta\text{ARBLOS}_{t-1} + \beta_{11} \, \text{ECM}_{t-1} + \varepsilon_t,$$

for $t = 1973\text{:}3 - 2018\text{:}3$.

Estimate the parameters of the model. Interpret the signs and magnitudes of the coefficients.

> **Hint:** To run the regression, first choose the **[Model...]** item in the **[Model]** menu. Then choose the **[Models for time series data]** category and choose **[Single Equation Dynamic Modelling using PcGive]** as the relevant model class. Then formulate the model and estimate.

**(8)** Choose **[Graphic Analysis]** in the **[Test...]** item in the **[Model]** menu, and try the possibilities. Do the residuals look well behaved?

**(9)** Use OxMetrics to calculate the tests for misspecification of the model. This is done by selecting **[Test Summary]** in the **[Test]** item in the **[Model]** menu. Try to recall how the tests are constructed and how they should be interpreted.

What do you conclude regarding the specification of the model?

**(10)** Now simplify the model by removing regressors with insignificant coefficients. Begin by deleting the variable with the smallest $t$-ratio and continue until all coefficients are significant. Always retain the constant term.

Recalculate the misspecification tests.

**(11)** The process of successively simplifying the model has been automated in OxMetrics. To use this facility, choose **[Automatic Model Selection]** on the first page after formulating the model. The algorithm tries many different routes of reduction, and is in general more robust than the manual approach, where you only try one reduction path.

Compare with your own final model.

**(12)** Finally, rerun the automatic reduction based on the general model, but now let the **[Automatic Model Selection]** insert dummy variables for large outliers in the residuals. This is done by expanding the section **[Outlier and break detection]** and selecting **[Large residuals]**.

Do the included dummy variables change the results?

Could you explain why the dummies are included, i.e. if something particular happened in the Danish economy at these points in time?

**(13)** Explain under which conditions the regression analysis above is a likelihood analysis.

Explain by reference to the concept of a *quasi-maximum likelihood estimation*, why the estimates may still be consistent and asymptotically normal even if the error terms do not follow a Gaussian distribution.
