# Econometrics II | Department of Economics, University of Copenhagen | Spring 2026

## Hand-In Assignment #3: A Dynamic Model for U.S. House Prices

### Context

Housing is the single most important asset for many households and the housing market plays a central role in the macroeconomy. A fundamental question in housing economics is whether house prices are aligned with economic fundamentals or whether they exhibit bubble-like behavior. The user cost model of housing provides a theoretical framework for this question. In this model, the cost of owning a home should, in equilibrium, be tied to the rental price of housing.

More specifically, the equilibrium purchase price of a house equals the present discounted value of future rents, where the discount rate depends on the mortgage rate.

Hence, with $h$, $r$ and $m$ the log of a house price index, the log of a rent index and the mortgage rate, respectively, the relationship between the three variables may in the long run be given by:

$$h = \alpha + \beta_1 r + \beta_2 m \tag{3.1}$$

for some constants $\alpha$, $\beta_1$ and $\beta_2$.

**Economic theory predictions:**
- $\beta_1 > 0$ (higher rents are associated with higher house prices)
- $\beta_2 < 0$ (higher mortgage rates, all else equal, reduce house prices through the user cost channel)

Under the strict user cost model, the rent elasticity satisfies $\beta_1 = 1$, which is a testable restriction.

**Reference:** A.K. Anundsen (2019), "Detecting Imbalances in House Prices: What Goes Up Must Come Down?", *The Scandinavian Journal of Economics*, 121(4), 1587–1619.

**Purpose:** The purpose of this assignment is to test the empirical validity of the theoretical relationship in equation (3.1).

---

## The Data

The data file `Assignment_3.xlsx` contains monthly observations from January 2000 – December 2024 of the following variables:

| Variable | Definition |
|----------|-----------|
| **HousePrice** | S&P/Case-Shiller U.S. National Home Price Index, Seasonally Adjusted |
| **Rent** | CPI for Rent of Primary Residence (1982–84 = 100), Seasonally Adjusted |
| **MortgageRate** | 30-Year Fixed Rate Mortgage Average (%) |
| **h** | log(HousePrice) |
| **r** | log(Rent) |
| **m** | MortgageRate |

### Data Sources

All data were retrieved from the [FRED Database](https://fred.stlouisfed.org/).

- **S&P/Case-Shiller index:** A widely used measure of U.S. residential house prices (FRED series identifier: CSUSHPISA)
- **CPI rent measure:** Tracks the cost of renting a primary residence, compiled by the Bureau of Labor Statistics (FRED series identifier: CUSR0000SEHA)
- **Mortgage rate:** The average 30-year fixed rate compiled by Freddie Mac (FRED series identifier: MORTGAGE30US)

---

## The Assignment

Conduct an empirical analysis for the period **January 2012 – December 2023** to determine if a long-run relationship as in equation (3.1) exists between house prices, rents, and the mortgage rate. If you find such a relationship, investigate how the corresponding equilibrium is sustained.

---

## Hints

1. **Graphical analysis:** For the graphical analysis, use any transformations of the variables you find relevant.

2. **Statistical tools:** You can use any tool from the toolbox for co-integrated variables that you find relevant.

3. **Assumptions:** Discuss which assumptions are required to derive the behavior of the estimator and explain if these assumptions are fulfilled or not empirically.

4. **Statistical testing:** Be precise about the statistical tests you use for testing various hypotheses. Explain which null hypotheses you test, how you test them, and what your conclusions are.

5. **CVAR approach** (if used):
   - It is fine if you carry out the analysis with an unrestricted constant – similar to the approach applied in the problem set. Hence, you may ignore the term with $\alpha$ in equation (3.1). Think about the interpretation of the unrestricted constant.
   - Note that your conclusions about co-integration may be sensitive to the choice of lag-length in the VAR model. Likewise, your conclusion may be sensitive to the sample period. Hence, you may want to investigate and comment on the robustness of your results.

6. **Robustness analysis:** The dataset includes observations before and during the housing bubble and the financial crisis (i.e., before 2012). You may investigate whether your empirical findings are robust against including observations from this time period.

---

## Formal Requirements

1. **Report structure:** You must hand in a report that:
   - Presents your graphical analysis
   - Describes the econometric model
   - Outlines the modeling progress (e.g., the approach you have taken, the alternative models you have tried, etc.)
   - Presents your preferred model including interpretation and statements on economic and statistical significance
   - Discusses the potential weaknesses of the model

2. **Length and format:**
   - Maximum of 12,000 characters including spaces (corresponding to 5 normal pages of text) plus 2 pages with output in the form of tables and graphs
   - Written in English
   - Handed in as a PDF document
   - See Absalon for details

3. **Group work:** You are allowed to work in groups of up to three persons (not necessarily in the same exercise class). Assessment criteria are given on the course page on Absalon.

4. **Anonymity:** Please do not write any names, student IDs, or exam numbers in your hand-in.
