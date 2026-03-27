# Measuring Geopolitical Risk

**Authors:** Dario Caldara and Matteo Iacoviello  
**Publication:** American Economic Review, 2022, 112(4): 1194–1225  
**DOI:** https://doi.org/10.1257/aer.20191823

## Abstract

We present a news-based measure of adverse geopolitical events and associated risks. The geopolitical risk (GPR) index spikes around the two world wars, at the beginning of the Korean War, during the Cuban Missile Crisis, and after 9/11. Higher geopolitical risk foreshadows lower investment and employment and is associated with higher disaster probability and larger downside risks. The adverse consequences of the GPR index are driven by both the threat and the realization of adverse geopolitical events. We complement our aggregate measures with industry- and firm-level indicators of geopolitical risk. Investment drops more in industries that are exposed to aggregate geopolitical risk. Higher firm-level geopolitical risk is associated with lower firm-level investment. (JEL C43, E32, F51, F52, G31, H56, N40)

---

## 1. Introduction

Entrepreneurs, market participants, and central bank officials view geopolitical risks as key determinants of investment decisions and stock market dynamics. The Bank of England includes geopolitical risk, together with economic and policy uncertainty, among an "uncertainty trinity" that could have significant adverse economic effects. In recent years, the European Central Bank, the International Monetary Fund, and the World Bank have routinely highlighted and monitored the risks to the outlook posed by geopolitical tensions. In a 2017 Gallup survey of more than 1,000 investors, 75 percent of respondents expressed worries about the economic impact of various military and diplomatic conflicts happening around the world.

From the standpoint of many economic models, adverse geopolitical events and threats can impact macroeconomic variables through several channels, such as loss of human life, destruction of capital stock, higher military spending, or increased precautionary behavior. However, the importance of geopolitical factors in shaping macroeconomic outcomes has not been the subject of systematic empirical analysis. The main limitation has been the lack of an indicator that is consistent over time, and that measures real-time geopolitical tensions as perceived by the press, the public, global investors, and policymakers. This is the perspective we adopt here.

We construct newspaper-based indices of geopolitical risk (GPR), daily and monthly, global and country-specific, and examine their evolution since 1900. Using aggregate macroeconomic data, we then show that higher GPR increases the probability of an economic disaster and predicts lower investment and employment. Using firm-level data, we document that the adverse implications of geopolitical risk are stronger for firms in more exposed industries, and that high firm-level GPR is associated with lower firm-level investment.

The construction of our index consists of definition, measurement, and validation.

---

## 2. Construction of the GPR Indices

### 2.1 Definition of Geopolitical Risk

Formally, geopolitics is the study of how geography affects politics and the relations among states. By contrast, the popular usage of the term geopolitics is more complex and contested, ranging from narrow to broad definitions of what constitutes geography and who the relevant political actors are. In A Dictionary of Human Geography, Rogers, Castree, and Kitchin (2013) state that the media often refer to geopolitical concerns to describe the impact of international crises and international violence. This is the perspective we adopt here.

**We define geopolitical risk as the threat, realization, and escalation of adverse events associated with wars, terrorism, and any tensions among states and political actors that affect the peaceful course of international relations.**

Two considerations about our definition are in order:

1. **Historical foundation:** Our definition of geopolitical risk builds on the historical usage of the term—to describe the practice of states to control and compete for territory. However, in line with recent assessments of modern international relations, our definition also includes power struggles that do not involve acts of violence and competition over territories, such as the Cuban Missile Crisis or recent tensions between the United States and Iran, or the United States and North Korea. Our definition also includes terrorism. In recent decades, terrorist acts have generated political tensions among states and, in some instances, have led to full-fledged wars.

2. **Scope of "risk":** Our definition of geopolitical risk captures—with a slight abuse of the word "risk"—a wide range of adverse geopolitical events, from their threat, to their realization, to their escalation. This choice is dictated by journalistic practices and measurement considerations. We break the headline index into separate "acts" and "threats" components, so that interested researchers can choose their preferred components for downstream empirical applications.

### 2.2 Measurement

Our sample is the text contained in about 25 million news articles published in the print edition of leading English-language newspapers from 1900 through the present, corresponding to about 30,000 and 10,000 articles per month in the recent and historical sample, respectively.

**Recent GPR Index (1985–present):** The recent GPR index is based on automated text-searches on the electronic archives of 10 newspapers:
- Chicago Tribune
- Daily Telegraph
- Financial Times
- Globe and Mail
- Guardian
- Los Angeles Times
- New York Times
- USA Today
- Wall Street Journal
- Washington Post

This selection of six newspapers from the US, three from the United Kingdom, and one from Canada reflects our intention to capture events that have global dimension and repercussions.

**Historical GPR Index (1900–present):** Based on searches of the historical archives of:
- Chicago Tribune
- New York Times
- Washington Post

#### 2.2.1 Dictionary-Based Method

We construct the GPR index using a **dictionary-based method**, specifying a dictionary of words whose occurrence in newspaper articles is associated with coverage of geopolitical events and threats. Such a method organizes prior information about how features of a text map into the outcome of interest.

**How we specify the dictionary:**

1. We build directly on the definition of geopolitical risk adopted in this paper, selecting words that closely align with our definition.

2. We use information from two geopolitical textbooks and from the Corpus of Historical American English to isolate themes more likely to be associated with geopolitical events or words more likely to be used in conjunction with war-related words.

3. We organize the search around high-frequency words and their synonyms more likely to appear in newspapers on days of high geopolitical tensions. For instance, the word "crisis" has a relative term frequency of 0.25 percent on days of high geopolitical tensions compared to 0.04 percent on an average day.

#### 2.2.2 Search Query Structure

Our goal is to provide an index that can highlight distinct aspects of geopolitical risk and can be sliced conceptually and geographically. These considerations lead to our search query, which specifies **two words or phrases whose joint occurrence likely indicates adverse geopolitical events**.

The query is organized in eight categories:

**Threats (Categories 1–5):**
1. War threats
2. Peace threats
3. Military buildup
4. Nuclear threats
5. Terrorist threats

**Acts (Categories 6–8):**
6. Beginning of war
7. Escalation of war
8. Terrorist acts

For six of our categories, we run proximity searches (searching for terms appearing within two words of each other). For two categories, we search for either two words appearing in the same article or for one bigram and one word appearing in the same article.

**Core Topic Words include:**
- War, conflict, hostilities, revolution, uprising, revolt, coup, geopolitical
- Military, troops, missiles, weapons, bombs, warheads
- Nuclear terms (nuclear war, atomic war, nuclear missile, etc.)
- Terror, guerrilla, hostage
- Peace, truce, armistice, treaty, parley

**Core Threat/Act Words include:**
- Threat, warn, fear, risk, concern, danger, doubt, crisis, trouble, dispute, tension, imminent, inevitable, menace, brink, scare, peril
- Begin, start, declare, begun, began, outbreak, broke out, breakout, proclamation, launch
- Advance, attack, strike, drive, shell, offensive, invasion, invade, clash, raid, launch
- Attack, act, bomb, kill, strike, hijack

**Exclusion words** filter out false positives related to movies, films, museums, anniversaries, obituaries, memorials, arts, books, memoirs, price wars, games, stories, history, veterans, tributes, sports, music, racing, cancer, real estate, mafia trials, and taxes.

#### 2.2.3 Index Construction

The index counts, each month, the number of articles discussing rising geopolitical risks, divided by the total number of published articles.

---

## 3. The Recent GPR Index (1985–2020)

Figure 1 presents the GPR index from 1985 through 2020. The index is characterized by several spikes corresponding to key adverse geopolitical events:

- **April 1986:** Terrorist escalation leading to US bombing of Libya
- **1990–1991:** Iraq invasion of Kuwait and subsequent Gulf War
- **Beginning of 1993:** Escalating tensions between the United States and Iraq
- **2001:** Surge after 9/11 events
- **2003:** Invasion of Iraq
- **2011:** Military intervention in Libya
- **2014:** Russian annexation of Crimea
- **2015:** Paris terrorist attacks
- **2017–2018:** North Korea crisis

The index displays a break in its mean after 2001. The 9/11 terrorist attacks saw a shift in news coverage of geopolitical events, driven by increased reporting on terrorist threats and the war on terror.

---

## 4. The Daily and Historical GPR Index

### 4.1 Daily GPR Index

Figure 2 shows the GPR index at daily frequency. The daily index is noisier than its monthly counterpart but provides a detailed view of larger episodes, including those that may seem to be missed by the monthly index. For instance:
- August 1991: Ethnic violence escalation in former Yugoslavia and attempted coup in Soviet Union
- March 1999: NATO air strikes in Kosovo

The daily GPR index illustrates three scenarios of how geopolitical tensions unfold:

1. **Protracted buildup:** A protracted buildup in tensions leads to a defining event causing a big spike, as in the case of the Gulf War.

2. **Climactic event:** One climactic event causes a large spike in daily geopolitical risk followed by readings persistently higher than average, as in the aftermath of 9/11.

3. **Slow-moving tensions:** Slow-moving geopolitical tensions persistently remain in the news cycle, averaging out to elevated values in the monthly GPR (e.g., Syrian Civil War, 2017–2018 North Korea crisis).

### 4.2 Historical GPR Index (1900–2020)

Figure 3 displays the historical GPR index from 1900 onward. The historical index closely mimics the recent index during 1985–2020 (correlation of 0.95) and is higher on average during the first half of the twentieth century.

**Major historical spikes:**
- **WWI and WWII:** Highest readings coincide with both world wars
- **Post-WWII:** Index declines rapidly but rises again during Korean War
- **1950s–1980s:** Multiple crises including Suez Crisis, Cuban Missile Crisis, Six-Day War, Falklands War, Afghan Invasion
- **2000s onwards:** Terrorism, Iraq War, and rising bilateral tensions dominate

---

## 5. Geopolitical Threats vs. Geopolitical Acts

We construct two components of the GPR index:

**Geopolitical Threats (GPT):** Searches articles including phrases related to threats and military buildups (categories 1–5 in the search query)

**Geopolitical Acts (GPA):** Searches phrases referring to the realization or escalation of adverse events (categories 6–8)

The GPT and GPA indices have a correlation of 0.59 over the full sample and 0.45 from 1985 onward. Independent variation highlights when threats emerge without immediate realization or when acts occur without prior threat buildup.

**Historical patterns:**
- **WWI:** GPA index elevated while GPT subdued at outbreak, though spike in threats when US severs diplomatic relations precedes American entry
- **WWII:** GPT index rises amid coverage of war risk (annexation of Czechoslovakia), while GPA spikes at beginning of war, Pearl Harbor, D-Day
- **1960s:** International crises captured by GPT spikes (Berlin Crisis, Cuban Missile Crisis) without leading to wars
- **Gulf War:** GPT surges in run-up; GPA spikes after initiation
- **Recent:** GPT high during US-North Korea and Iran tensions

---

## 6. Validation of the Index

### 6.1 Plausibility Tests

#### 6.1.1 Largest Spikes in Historical Index

The five largest geopolitical shocks over 120 years are:
1. Beginning of WWII (September 1939)
2. Beginning of WWI (August 1914)
3. Pearl Harbor (December 1941)
4. 9/11 (September 2001)
5. Korean War onset (July 1950)

These captures well-known episodes of sizable increases in war, terrorism, and international crisis risks.

#### 6.1.2 Narrative GPR Index

As validation, we construct a "narrative" index by manually reading and scoring 44,000 front pages of the New York Times (1900–2019). Each day is scored 0, 1, 2, or 5 depending on whether:
- 0: No headline features rising or existing geopolitical tensions
- 1: One headline (not lead) features GPR
- 2: Lead headline (not banner) features GPR
- 5: Banner headline features GPR

**Result:** The automated and narrative indices have a **correlation of 0.86**, sharing very similar spikes during world wars, Korean War, Gulf War, and 9/11. This high correlation bolsters confidence that the automated index accurately measures geopolitical risks.

#### 6.1.3 Country-Specific Measures

We construct country-specific GPR indices by counting joint occurrences of geopolitical terms and country names. This enables granular assessment showing:
- Most countries share exposure to common events (world wars, Gulf War, Iraq War)
- Some spikes isolated to specific regions (UK's Suez Crisis and Falklands War, Germany's Berlin Wall crisis, Japan/Russia/China regional wars, Mexico/Korea US-involved wars)

### 6.2 Comparison with Related Economic and Geopolitical Data

#### 6.2.1 Military Spending News

The GPR index correlates with Ramey's (2011) measure of military expenditure news (correlation of 0.29). The GPR index is above historical mean in 15 of 16 instances where military spending news exceeds 5% of GDP. However, the indices show independent variation:
- GPR spikes during both world wars, Korean War, post-9/11 not matched by military spending news
- Suggests GPR captures important geopolitical information beyond military spending

#### 6.2.2 War Deaths

The GPR index is positively correlated with worldwide deaths from conflicts (correlation of 0.82):
- GPA (acts) correlates more with war deaths (0.83) than GPT (threats) (0.46)
- Correlation weakens after 1950s
- GPR level permanently higher post-WWII compared to interwar period despite lower death tolls (reflects increased attention to conflict risks)

#### 6.2.3 Financial and Economic Uncertainty

Compared to VIX (financial volatility) and EPU (Economic Policy Uncertainty) index:
- **Simultaneity periods:** Both indices rise during Gulf War (1990–1991) and after 9/11 (2001)
- **Independent variation:** GPR unaffected by economic/financial distress or presidential elections; EPU/VIX unaffected by Crimea annexation or most terrorist events
- **Causality:** GPR-to-VIX/EPU direction plausible; reverse direction less plausible
- **Granger causality:** Macroeconomic, financial, and uncertainty developments do NOT Granger cause GPR

### 6.3 Additional Accuracy Checks

#### 6.3.1 Human Audit

An extensive human audit of over 7,000 randomly sampled newspaper articles yields:
- **Correlation with manual coding:** Annual frequency correlation of 0.93 between automated and "human" index
- **Lower error rates:** GPR index has lower Type I error rate relative to alternative search specifications

#### 6.3.2 Sensitivity to Newspaper Selection

- Recent index (10 newspapers) and historical index (3 newspapers) have **correlation of 0.95** for overlapping period
- **Non-US vs. US newspapers:** Correlation of 0.88
- **Cronbach alpha:** 0.96 (excellent internal consistency across ten newspapers)

#### 6.3.3 Language Change Over Time

Extensive analysis confirms the index neither ignores nor over-relies on words used more in certain periods:
- Words like "terrorism," "blockade," "invasion," "war," "crisis," "troops," "threat" have odds of appearing 5+ times higher on high-geopolitical-risk days
- Index includes both early twentieth-century words ("menace," "peril") and recent words ("risk," "tension")
- **Excluded words filter:** Prevents upward bias from increased arts/sports/entertainment coverage

#### 6.3.4 Media Attention vs. Underlying Risk

The index is robust to media attention artifacts:
- Not prone to spurious fluctuations from other newsworthy events (natural disasters, inflation, Olympics, elections)
- Not impacted by newspaper political orientation
- High correlation between occurrence of murders, hijackings, nuclear tests and media coverage (suggests media coverage aligned with actual events)

---

## 7. VAR Evidence on Macroeconomic Effects

### 7.1 Aggregate Economic Effects

We examine macroeconomic consequences using a structural VAR model with quarterly data (1986:I–2019:IV). Eight variables included:
1. Log of GPR index
2. VIX
3. Log of real business fixed investment per capita
4. Log of private hours per capita
5. Log of S&P 500 index
6. Log of WTI price of oil
7. Yield on 2-year US Treasuries
8. Chicago Federal Reserve's National Financial Conditions Index (NFCI)

**Identification:** Cholesky decomposition ordering GPR index first (contemporaneous correlations reflect GPR effects on economic variables rather than reverse).

**Impulse Response to 2 Standard Deviation GPR Shock:**

- **GPR:** Rises persistently, remains elevated for nearly two years
- **VIX:** Short-lived increase in financial uncertainty
- **Stock prices:** Decline (peak effect ≈ 5%)
- **Oil prices:** Decline (peak effect ≈ 10%)
- **Two-year yield:** Modest decrease
- **Fixed investment:** Gradually declines, bottoming at −1.5% after ~1 year, then slowly reverts to trend
- **Hours worked:** Decline 0.6% one year after shock
- **GDP:** Drops 0.3% over first year (when GDP included in specification)

**Interpretation:** Decline in investment and hours consistent with models emphasizing:
- Contractionary effects of negative news about the future (Beaudry and Portier 2006; Jaimovich and Rebelo 2009)
- Recessions driven by shocks with negative first moment and positive second moment (Bloom et al. 2018)

### 7.2 Acts vs. Threats

Modified VAR replacing GPR with GPA and GPT indices using Cholesky ordering: GPA, then GPT.

**Key findings:**

- **Acts shock:** Sharp, significant increase in threats (acts can prompt contemporaneous threats), induces similar decline in investment/hours as full GPR shock
- **Threats shock:** Small, short-lived increase in acts

**Counterfactual analysis:** Holding threats constant in response to acts, or vice versa, shows:
- Both acts and threats in isolation produce contractionary effects
- If threats remained unchanged after acts shock, investment/hours decline would be smaller
- Decline in activity associated with increased threats (acts held constant) confirms unrealized threats about future events have contractionary effects

**Theoretical support:** Results support models where agents:
- Form expectations using worst-case probability (Ilut and Schneider 2014)
- Reassess macroeconomic tail risks in response to threats (Kozlowski, Veldkamp, and Venkateswaran 2018)

**Caveat:** Most adverse geopolitical events in sample did not directly hit US (except 9/11). Countries experiencing wars on their soil suffer very large activity drops (Barro 2006; Glick and Taylor 2010).

---

## 8. Tail Effects of Geopolitical Risk

### 8.1 Effects on Disaster Probability

**Model:** Probability of economic disaster in country i in year t:

Di,t = αi + β·GPRt + γ·GPRCi,t + δ·ΔGDPi,t−1 + controls + ui,t

Where:
- Di,t = zero/one dummy for economic disaster
- αi = country fixed effect
- GPR = global index
- GPRC = country-specific index
- ΔGDP = real GDP growth

**Sample:** 26 countries, 1900–2019

**Key Results:**

| Specification | Global GPR Effect | Country GPR Effect |
|---|---|---|
| Simple (no FE) | +18 pp | — |
| With country FE | — | +9 pp |
| With WWII dummies | Not significant | +8 pp** |
| With spikes | +17 pp** | +8 pp** |
| With military spending control | +2 pp | +6.6 pp** |

**Interpretation:**
- One standard deviation increase in global GPR → 18 percentage point increase in disaster probability
- One standard deviation increase in country-specific GPR (after controlling for global) → 9 percentage point increase
- Many disasters occur during world wars, but geopolitical risks and consequences materialize across history and countries
- **Disaster onset:** One standard deviation country GPR increase brings probability from 2.2% to 9% (6.8 pp increase)
- **Disaster ending:** High GPR reduces probability of disaster end, though effects smaller and less precise

### 8.2 Quantile Regression Effects

**Model:** Quantile regression of GDP growth, TFP growth, and military spending on country-specific GPR

**Results at different quantiles (q10, q50, q90):**

| Variable | OLS | q10 | q50 | q90 |
|---|---|---|---|---|
| **GDP growth** | −0.35% | −1.44%** | −0.24% | +0.30% |
| **TFP growth** | −0.22% | −1.86%** | −0.04% | +1.53%** |
| **Military exp. (% GDP)** | +2.15% | +0.16% | +0.63% | +7.08%** |

**Key insights:**
- Left tail (q10) GDP decline **4× larger** than OLS effect (implies tail risk concentration)
- Right tail (q90) GDP slightly increases (suggests some heterogeneity in conflict outcomes)
- TFP distribution shows higher uncertainty (both positive and negative tail events more likely)
- Military spending right tail disproportionately affected (elevated GPR predicts large military buildup risk)

---

## 9. Geopolitical Risk and Firm-Level Investment

### 9.1 Measuring Firm-Level Geopolitical Risk

**Three components:**

GPRi,t = GPRt + GPRt × Λk + Zi,t

Where:
- First term: Aggregate GPR
- Second term: Aggregate GPR interacted with industry exposure Λk (captures disproportionate effects on exposed industries)
- Third term: Idiosyncratic firm-level GPR Zi,t (firm-specific risks not reflected at aggregate/industry level)

#### 9.1.1 Industry Exposure

Regression of daily portfolio returns in 49 Fama-French industry groups on daily GPR changes:

Rk,t = αk + βk·ΔGPRt + εk,t

Sample: 1985–2019

**Exposure ranking (sample industries):**
- **Negative exposure (defensive/gain from GPR):** Precious metals, petroleum, defense
- **Positive exposure (hurt by GPR):** Shipping, transportation

For empirical application: Λk = dummy variable = 1 for above-median exposure industries, 0 otherwise.

#### 9.1.2 Firm-Level Geopolitical Risk from Earnings Calls

Following Hassan et al. (2019), text analysis of quarterly earnings call transcripts of US-listed firms (2005:I–2019:IV):

**Firm-level GPR:** Count joint occurrences of "risk" words within 10 words of "geopolitical" words, normalized by total transcript word count.

**Example words:**
- Geopolitical: war, military, terror, conflict, coup, embargo
- Risk: risk, potential, danger, dispute, incident, attack

**Validation:** Aggregate firm-level index correlated with newspaper GPR index at correlation of 0.19 (positive correlation, though short sample, validates investor-press alignment).

**Isolation of idiosyncratic component:** Include sector-by-quarter dummies in regressions to absorb aggregate and industry-specific components.

### 9.2 Dynamic Effects of Industry-Specific Geopolitical Risk

**Specification (local projections approach):**

log(iki,t+h) = αi,h + βh·(Λk × Δ log GPRt) + dh·Xi,t + εi,t+h

Where:
- h ≥ 0 indexes current and future quarters
- Λk = industry exposure dummy
- Xi,t = controls (firm cash flows, Tobin's Q, lagged investment)

**Result:** Firm in high-exposure industry experiences ~1 percentage point larger investment decline than non-exposed counterpart in first year after two standard deviation GPR shock.

**Interpretation:** Negative repercussions of GPR on investment vary by industry exposure; stock market effects partly drive differential investment responses.

### 9.3 Dynamic Effects of Firm-Specific Geopolitical Risk

**Specification:**

log(iki,t+h) = αi,h + αk,t,h + γh·Zi,t + dh·Xi,t + εi,t+h

Where:
- αi = firm fixed effects
- αk,t = sector-by-quarter dummies (absorb aggregate/industry components)
- Zi,t = firm-level GPR from earnings calls
- h ≥ 0 indexes quarters ahead

**Result (Figure 11, bottom panel):** Firms gradually reduce investment over two quarters after increase in firm-level GPR (two standard deviations):
- Investment declines >1% at trough
- Remains below baseline for up to one year

### 9.4 Summary of Firm-Level Evidence

**Table 5 Summary (horizon = 2 quarters ahead):**

| Specification | Coefficient | Standard Error |
|---|---|---|
| Δ GPR × industry exposure (sample 1) | −0.63 | (0.29) |
| Δ GPR × industry exposure (sample 2) | −0.64 | (0.27) |
| Firm-level GPR | −0.67 | (0.30) |
| Political risk (Hassan et al.) | −0.75 | (0.25) |

**Key findings:**
- Investment responds more to GPR changes in above-average exposure industries
- Firm-level GPR negatively associated with firm-level investment
- Similar magnitude to firm-level political risk response, validating the geopolitical risk measure
- Changes in geopolitical risks → heterogeneous firm investment effects depending on industry and firm-specific risks
- Link between GPR and firm activity is significant, economically meaningful, persistent

---

## 10. Conclusions

We propose and implement indicators of geopolitical risk measuring threat, realization, and escalation of adverse geopolitical events. Three main contributions:

1. **New measure of adverse geopolitical events:** GPR index shares some spikes with military spending news, conflict human costs, EPU index, and financial volatility, but also captures important geopolitical information not reflected in these indicators.

2. **Distinguishing threats from realizations:** Methodology pinpoints timing of different geopolitical event types, enabling measurement of distinct effects.

3. **Systematic evidence on geopolitical events and business cycles:** Using quarterly VARs, cross-country historical data, and firm-level data, we document:
   - **Aggregate effects:** GPR shock induces persistent investment and employment declines
   - **Disaster risk:** Higher GPR associated with increased probability of economic disaster
   - **Downside risk:** Elevated GPR correlates with higher downside risks to GDP growth
   - **Firm heterogeneity:** Adverse implications stronger for exposed industries; high firm-level GPR associated with lower investment

### Future Research Directions

1. **Additional measurement sources:** Extend using foreign-language publications, country reports, parliamentary debate transcripts
2. **International ramifications:** Investigate impact on asset prices, capital flows, trade flows, global supply chains
3. **Endogeneity of geopolitical risk:** Complement analysis of geopolitical risk as a business cycle driver with understanding of conflict causes and interstate warfare determinants

---

## References

Alfaro, Ivan, Nicholas Bloom, and Xiaoji Lin. 2018. "The Finance Uncertainty Multiplier." *NBER Working Paper* 24571.

Baker, Scott R., Nicholas Bloom, and Steven J. Davis. 2016. "Measuring Economic Policy Uncertainty." *Quarterly Journal of Economics* 131 (4): 1593–1636.

Barro, Robert J. 2006. "Rare Disasters and Asset Markets in the Twentieth Century." *Quarterly Journal of Economics* 121 (3): 823–66.

Barro, Robert J., and José F. Ursúa. 2012. "Rare Macroeconomic Disasters." *Annual Review of Economics* 4 (1): 83–109.

Bazzi, Samuel, and Christopher Blattman. 2014. "Economic Shocks and Conflict: Evidence from Commodity Prices." *American Economic Journal: Macroeconomics* 6 (4): 1–38.

Beaudry, Paul, and Franck Portier. 2006. "Stock Prices, News, and Economic Fluctuations." *American Economic Review* 96 (4): 1293–1307.

Bergeaud, Antonin, Gilbert Cette, and Rémy Lecat. 2016. "Productivity Trends in Advanced Countries between 1890 and 2012." *Review of Income and Wealth* 62 (3): 420–44.

Berger, David, Ian Dew-Becker, and Stefano Giglio. 2019. "Uncertainty Shocks as Second-Moment News Shocks." *Review of Economic Studies* 87 (1): 40–76.

Berkman, Henk, Ben Jacobsen, and John B. Lee. 2011. "Time-Varying Rare Disaster Risk and Stock Returns." *Journal of Financial Economics* 101 (2): 313–32.

Blattman, Christopher, and Edward Miguel. 2010. "Civil War." *Journal of Economic Literature* 48 (1): 3–57.

Bloom, Nicholas. 2009. "The Impact of Uncertainty Shocks." *Econometrica* 77 (3): 623–85.

Bloom, Nicholas, Max Floetotto, Nir Jaimovich, Itay Saporta-Eksten, and Stephen J. Terry. 2018. "Really Uncertain Business Cycles." *Econometrica* 86 (3): 1031–65.

Caldara, Dario, Cristina Fuentes-Albero, Simon Gilchrist, and Egon Zakrajšek. 2016. "The Macroeconomic Impact of Financial and Uncertainty Shocks." *European Economic Review* 88 (C): 185–207.

Caldara, Dario, and Matteo Iacoviello. 2022. "Replication Data for: Measuring Geopolitical Risk." *American Economic Association* [publisher], Inter-university Consortium for Political and Social Research [distributor]. https://doi.org/10.3886/E154781V1.

Carney, Mark. 2016. "Uncertainty, the Economy and Policy." Speech, Bank of England, London, June 30.

Dijkink, Gertjan. 2009. "Geopolitics and Religion." In *International Encyclopedia of Human Geography*, edited by Rob Kitchin and Nigel Thrift, 453–57. Oxford: Elsevier.

Fama, Eugene F., and Kenneth R. French. 1997. "Industry Costs of Equity." *Journal of Financial Economics* 43 (2): 153–93.

Flint, Colin. 2016. *Introduction to Geopolitics*. Oxfordshire: Routledge.

Foster, John Bellamy. 2006. "The New Geopolitics of Empire." *Monthly Review* 57 (8): 1–18.

Gentzkow, Matthew, Bryan Kelly, and Matt Taddy. 2019. "Text as Data." *Journal of Economic Literature* 57 (3): 535–74.

Glick, Reuven, and Alan M. Taylor. 2010. "Collateral Damage: Trade Disruption and the Economic Impact of War." *Review of Economics and Statistics* 92 (1): 102–27.

Gourio, Francois. 2008. "Disasters and Recoveries." *American Economic Review* 98 (2): 68–73.

Hassan, Tarek A., Stephan Hollander, Laurence van Lent, and Ahmed Tahoun. 2019. "Firm-Level Political Risk: Measurement and Effects." *Quarterly Journal of Economics* 134 (4): 2135–2202.

Ilut, Cosmin L., and Martin Schneider. 2014. "Ambiguous Business Cycles." *American Economic Review* 104 (8): 2368–99.

Jackson, Matthew O., and Massimo Morelli. 2011. "The Reasons for Wars: An Updated Survey." In *The Handbook on the Political Economy of War*, edited by Christopher Coyne and Rachel Mathers, 34–57. Cheltenham, England: Edward Elgar Publishing Limited.

Jaimovich, Nir, and Sergio Rebelo. 2009. "Can News about the Future Drive the Business Cycle?" *American Economic Review* 99 (4): 1097–1118.

Jorda, Oscar. 2005. "Estimation and Inference of Impulse Responses by Local Projections." *American Economic Review* 95 (1): 161–82.

Kozlowski, Julian, Laura Veldkamp, and Venky Venkateswaran. 2018. "The Tail that Keeps the Riskless Rate Low." *NBER Working Paper* 24362.

Ludvigson, Sydney C., Sai Ma, and Serena Ng. 2021. "Uncertainty and Business Cycles: Exogenous Impulse or Endogenous Response?" *American Economic Journal: Macroeconomics* 13 (4): 369–410.

Nakamura, Emi, Jón Steinsson, Robert Barro, and José Ursúa. 2013. "Crises and Recoveries in an Empirical Model of Consumption Disasters." *American Economic Journal: Macroeconomics* 5 (3): 35–74.

Pindyck, Robert S., and Neng Wang. 2013. "The Economic and Policy Consequences of Catastrophes." *American Economic Journal: Economic Policy* 5 (4): 306–39.

Ramey, Valerie A. 2011. "Identifying Government Spending Shocks: It's All in the Timing." *Quarterly Journal of Economics* 126 (1): 1–50.

Ramey, Valerie A., and Sarah Zubairy. 2018. "Government Spending Multipliers in Good Times and in Bad: Evidence from US Historical Data." *Journal of Political Economy* 126 (2): 850–901.

Rogers, Alisdair, Noel Castree, and Rob Kitchin. 2013. *A Dictionary of Human Geography*. Oxford: Oxford University Press.

Rosenthal, Jack. 2004. "The Public Editor; What Belongs on the Front Page of The New York Times." *New York Times*, August 22.

Roser, Max, and Mohamed Nagdy. 2013. "Military Spending." *Our World in Data*. https://ourworldindata.org/military-spending.

Saiz, Albert, and Uri Simonsohn. 2013. "Proxying for Unobservable Variables with Internet Document-Frequency." *Journal of the European Economic Association* 11 (1): 137–65.

Sherwin, Martin J. 2012. "The Cuban Missile Crisis at 50: In Search of Historical Perspective." *Prologue Magazine* 44 (3): 6–16.

Stein, Arthur A., and Bruce Russett. 1980. "Evaluating War: Outcomes and Consequences." In *Handbook of Political Conflict: Theory and Research*, edited by Ted Robert Gurr, 399–422. New York: Free Press.

---

## Appendix: Key Figures and Tables

### Figure 1: Recent GPR Index from 1985
Shows monthly index with major geopolitical events labeled (US bombing Libya, Gulf War, 9/11, Iraq War, Crimea annexation, North Korea tensions, etc.)

### Figure 2: Daily Geopolitical Risk
Timeline of daily GPR from 1985–2020 with detailed event annotations including specific dates and events

### Figure 3: Historical GPR Index from 1900
Shows index from 1900–2020 with major historical events labeled (World Wars, Korean War, Cuban Missile Crisis, etc.)

### Figure 4: Geopolitical Threats and Geopolitical Acts
Dual-panel figure showing separate threats (red) and acts (black) indices with detailed historical breakouts

### Figure 5: Narrative GPR Index
Comparison of automated GPR index with manually scored New York Times front pages (0, 1, 2, or 5 scoring), showing 0.86 correlation

### Figure 6: Country-Specific Geopolitical Risk
Nine subplots showing country-specific indices for US, UK, Japan, Russia, Germany, Korea, Mexico, and China with relevant historical events labeled

### Figure 7: Comparisons with Military Spending News and War Deaths
Top panel: Quarterly GPR vs. military spending news (Ramey 2011)
Bottom panel: Annual GPR vs. worldwide deaths from conflicts, showing 0.82 correlation

### Figure 8: Comparison with Financial and Economic Uncertainty
Top panel: GPR vs. VIX (financial volatility)
Bottom panel: GPR vs. EPU index (economic policy uncertainty)

### Figure 9: Impact of Increased Geopolitical Risk
Eight subplots showing impulse responses to 2 standard deviation GPR shock:
- GPR, VIX, Private fixed investment, Hours
- S&P 500, Oil price, Two-year yield, NFCI index

### Figure 10: Impact of Increased Geopolitical Risk: Acts versus Threats
Two panels (A and B) showing responses to GPA and GPT shocks respectively, with counterfactuals

### Figure 11: Response of Firm-Level Investment to Geopolitical Risk
Top panel: Industry response to aggregate GPR exposure
Bottom panel: Idiosyncratic firm-level GPR response with 90% confidence intervals

### Table 1: Search Query for the GPR Index
Detailed specification of eight search categories, topic/threat/act word sets, and excluded words

### Table 2: Largest Geopolitical Shocks since 1900
Lists ranking of largest shocks by GPR index overall, threats component, and acts component with events and dates

### Table 3: Geopolitical Risk and Economic Disasters
Multiple regression specifications showing disaster probability effects of global and country-specific GPR (1900–2019, 26 countries)

### Table 4: Quantile Regression Effects of Country-Specific Geopolitical Risk
Shows OLS and quantile (q10, q50, q90) effects on GDP growth, TFP growth, and military expenditures

### Table 5: Geopolitical Risk and Firm-Level Investment
Four specifications showing industry and firm-level geopolitical risk effects on firm investment (2-quarter horizon)

---

**Updated data on geopolitical risk available at:** https://www.matteoiacoviello.com/gpr.htm

**Replication materials:** Caldara and Iacoviello (2022) at https://doi.org/10.3886/E154781V1
