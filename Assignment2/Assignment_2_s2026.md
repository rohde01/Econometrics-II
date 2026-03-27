# Econometrics II | Department of Economics, University of Copenhagen | Spring 2026

## Hand-In Assignment #2: Geopolitical Risk and Economic Activity

Geopolitical tensions, such as wars, territorial disputes, and terrorism, have been a defining element of the global economic landscape in recent years. The Russian invasion of Ukraine in 2022, together with the intensification of conflicts in the Middle East, has renewed interest in how geopolitical events influence the macroeconomy. Caldara and Iacoviello (2022) develop a newspaper-based index of geopolitical risk and show that higher levels of geopolitical risk are associated with lower investment, declining stock prices, and greater uncertainty. The purpose of this assignment is to analyze the dynamic relationship between geopolitical risk, stock market returns, and U.S. economic activity using a VAR model.

---

## The Data

The data file `Assignment_2.xlsx` contains monthly data for the period January 1985 to January 2026, for the following variables:

- **GPR**: Geopolitical Risk Index (benchmark, monthly)
- **INDPRO**: U.S. Industrial Production Index (seasonally adjusted, 2017=100)
- **Mkt**: U.S. stock market return (percent per month)

The GPR variable was constructed by Caldara and Iacoviello (2022) and can be retrieved from Matteo Iacoviello's website.[^1] The INDPRO variable was downloaded from the FRED Database[^2] and may be viewed as a proxy for economic activity. The Mkt variable is the value-weighted U.S. market return including dividends from the Fama-French data library.[^3]

### Data Transformations

Moreover, the dataset contains the following transformations:

$$g_t = \log(GPR_t)$$

$$y_t = \log(INDPRO_t) - \log(INDPRO_{t-1})$$

$$s_t = \log\left(1 + \frac{Mkt_t}{100}\right)$$

The variable $y_t$ is the monthly growth rate of industrial production, and the variable $s_t$ is the monthly continuously compounded stock market return.

---

## The Assignment

Use a VAR model to analyze the dynamic relationship between the level of geopolitical risk ($g_t$), the monthly growth rate of industrial production ($y_t$), and the monthly stock market return ($s_t$). In particular, investigate if geopolitical risk drives stock returns and economic activity, or if it is the other way around (or both). Discuss the dynamic relationship, and if there are signs of a contemporaneous relationship between the variables.

---

## Hints

1. For the graphical analysis, use any transformations of the variables you find relevant.

2. You can use any tool from the toolbox for vector autoregressions that you find relevant to characterize the relationship.

3. Carefully discuss which assumptions are required to derive the behavior of the estimator and explain if these assumptions are fulfilled or not empirically. If not, what are the consequences for your estimation results? Can you improve on this?

4. If you come up with several model specifications, select the one that seems the most relevant and justify your decision.

5. Be precise about the statistical tests you use for testing various hypotheses. Explain which null hypotheses you test, how you test them, and what your conclusions are.

6. The dataset includes observations during the COVID-19 pandemic (2020–2021), the Russian invasion of Ukraine (2022), and the escalation of conflict in the Middle East (2023–2024). You may investigate whether your empirical findings are robust against excluding observations from one or more of these time periods. Moreover, Caldara and Iacoviello (2022) note a structural break in the GPR index around September 2001 (the 9/11 attacks). You may investigate whether your results are sensitive to the choice of sample period, e.g. by restricting the estimation to the post-9/11 period.

---

## Formal Requirements

1. You must hand in a report that:
   - (i) presents your graphical analysis
   - (ii) describes the econometric model
   - (iii) outlines the modeling progress (e.g., the approach you have taken, the alternative models you have tried, etc.)
   - (iv) presents your preferred model including interpretation and statements on economic and statistical significance
   - (v) discusses the potential weaknesses of the model

2. The report must be a maximum of 12,000 characters including spaces (corresponding to 5 normal pages of text) plus 2 pages with output in the form of tables and graphs. The report must be written in English. It must be handed in as one PDF document. See Absalon for details.

3. You are allowed to work in groups of up to three persons (not necessarily in the same exercise class). The assessment criteria are given on the course page on Absalon.

4. Please do not write any names, student IDs, or exam numbers in your hand-in.

---

## References

[1] Caldara, D. and M. Iacoviello (2022): "Measuring Geopolitical Risk," *American Economic Review*, 112(4), 1194–1225.
https://www.matteoiacoviello.com/gpr_files/GPR_PAPER.pdf

---

[^1]: Link: https://www.matteoiacoviello.com/gpr.htm
[^2]: Link: https://fred.stlouisfed.org/series/INDPRO
[^3]: Link: https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html
