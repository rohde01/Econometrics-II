# Assignment 1 Polish Plan — Forecasting Economic Growth and Growth-at-Risk

## Context

The current Assignment 1 report ([assignment1.tex](Assignment1/assignment1.tex), compiled [assignment1.pdf](Assignment1/assignment1.pdf)) is already a competent, end-to-end answer: AR(2) is selected by GETS/BIC, misspecification is discussed, DM and GaR coverage tests are reported, and the conclusion engages honestly with the COVID episode. The aim is **not** a rewrite but a targeted polish so the report unambiguously meets every formal assessment criterion and addresses the concrete issues raised in [received_peer_feedback_snips.md](Assignment1/received_peer_feedback_snips.md).

Three classes of gap are driving the edits:

1. **Formal-theory completeness** (Assessment Criteria §2): the report relies on a Wald *t*-statistic for coefficients and an LR statistic for GETS reductions but never states either formally with its asymptotic distribution. Stationarity is asserted for AR(2) using $\hat{\phi}_1+\hat{\phi}_2<1$ alone, which is necessary but not sufficient (the AR(2) triangle requires three conditions, see [02_DynamicModels_s2026.md:288-290](course_notes/02_DynamicModels_s2026.md)).
2. **Reader clarity** (peer feedback): the introduction lacks a one-sentence motivation; "low-order AR" is asserted without anchoring it in the ACF/PACF pattern; "LB lag-8" is ambiguous; Figure 2's caption promises dashed bands that should be verified; Table 1 makes the reader hunt for best values; the Gaussian-GaR caveat is stated without explanation.
3. **In-scope only**: the report must stay within material covered up to Assignment 1 (lectures L1–L9 per [econometrics-ii-course-plan.md](econometrics-ii-course-plan.md): likelihood, AR/MA/ARMA, GETS, IC, misspecification, forecasting, DM test, QMLE). No quantile regression, ARCH/GARCH, VAR, unit roots, or rolling re-estimation — all later in the course.

User decisions taken at planning time:
- **Preferred model stays plain AR(2)** (no in-model GFC dummy; dummy retained only as JB-robustness diagnostic as currently done).
- **Candidate set unchanged**: AR(1)–AR(4) and ARMA(1,1).
- **Length budget**: edits must be **character-neutral** relative to the current body text; every addition requires a matching cut listed below.

## Files modified

- [Assignment1/assignment1.tex](Assignment1/assignment1.tex) — the report itself; **the only source-of-truth file edited**.
- [Assignment1/tables/table1_selection.tex](Assignment1/tables/table1_selection.tex) — bold best value per criterion column.
- [Assignment1/main.ipynb](Assignment1/main.ipynb) — only if Figure 2 regeneration is needed (see §5 of edits); otherwise leave untouched.

No new figures, no new tables, no new estimations. All numerical results in the report (LR p-values, BIC values, DM, coverage *t*, tick loss) already exist and stand.

---

## Edits (in document order)

### 1. Introduction — add motivation, sharpen the question (character-neutral)

Peer feedback: "not totally clear what the main question is", "include a sentence or two about why you would want to forecast GDP growth".

Replace the first paragraph of §1 with three short sentences that explicitly cover the four [TipsforWriting.md:73-78](TipsforWriting.md) elements (question, motivation, method, conclusion):

- **Motivation** (new, ~1 sentence): GDP growth forecasts are inputs to monetary, fiscal and prudential policy; GaR additionally quantifies downside risk used by central banks (cite the Adrian et al. 2019 / Nationalbanken footnotes already in the assignment brief).
- **Main question** (sharpened): *Can a parsimonious univariate model for U.S. GDP growth deliver one-step-ahead point forecasts and 10% GaR estimates that outperform naive benchmarks over 2010Q1–2024Q4?*
- **Method + headline result**: keep current AR(2)/BIC + DM/coverage-test sentences.

**Compensating cut**: drop the standalone "Overall, the results support…" sentence — that conclusion is restated in §6 already.

### 2. Econometric Theory — fill the gaps the peers flagged

§3 currently states the ARMA equation and OLS/MLE estimation but is missing four items the assessment criteria demand: a precise stationarity statement, the *t*-statistic for individual coefficients, the LR statistic, and the conditional-likelihood subtlety. Add them compactly.

#### 2a. Stationarity stated precisely in lag-polynomial form

Replace the current one-line "Stationarity requires that all roots of the AR polynomial lie outside the unit circle" with:

> Writing $\theta(L) = 1 - \phi_1 L - \cdots - \phi_p L^p$, the AR($p$) process is stationary and weakly dependent iff all roots $z_j$ of $\theta(z)=0$ satisfy $|z_j|>1$, equivalently $|\phi_j^{-1}|<1$ for the inverse roots. For AR(2) this reduces to the triangle $\phi_1+\phi_2<1$, $\phi_2-\phi_1<1$, $|\phi_2|<1$ ([02_DynamicModels_s2026.md:288-290](course_notes/02_DynamicModels_s2026.md)).

This directly fixes the peer comment that $\hat\phi_1+\hat\phi_2<1$ is not sufficient.

#### 2b. Define the *t*-statistic for individual coefficients

Add a single equation after the asymptotic-normality statement in §3.1 ("Estimation"):

$$H_0:\phi_j=0,\quad t_{\phi_j}=\frac{\hat\phi_j}{\widehat{\mathrm{s.e.}}(\hat\phi_j)}\xrightarrow{d} N(0,1),$$

with one sentence noting this is the Wald form from [01_LikelihoodAnalysis_s2026.md:398-415](course_notes/01_LikelihoodAnalysis_s2026.md) and is what Table 2 reports.

#### 2c. Define the LR statistic used for GETS reductions

Add (one line plus one sentence):

$$\xi_{\mathrm{LR}}=-2\bigl(\log L(\tilde\theta_T)-\log L(\hat\theta_T)\bigr)\xrightarrow{d}\chi^2(j),$$

where $j$ is the number of restrictions. Note explicitly that LR is non-robust to QMLE-type misspecification, motivating the BIC cross-check later.

#### 2d. One line on conditional vs. exact likelihood

Acknowledge that the Gaussian log-likelihood shown is *conditional on $y_1,\ldots,y_p$* (standard in the lecture notes, [01_LikelihoodAnalysis_s2026.md:138-181](course_notes/01_LikelihoodAnalysis_s2026.md)). Two short clauses suffice.

**Compensating cuts for 2a–2d**: tighten §3.3 (Forecasting) — the DM derivation can be one equation plus one sentence instead of the current paragraph (the result $t_{\mathrm{DM}}\to N(0,1)$ under HAC is enough; the "regress $d_t$ on a constant" sentence can go since it duplicates §4.4). Tighten §3.4 (GaR) wording — the boxed equation already carries the substance.

### 3. Empirical §4.1 (Model Selection) — fix the "low-order AR" claim, fix Figure 2, highlight Table 1

#### 3a. Anchor "low-order AR" in the data

Peer feedback: "Citing 'motivating the use of a low-order autoregressive model' — Why is this the case?". Replace that clause in §2 (Data) with a clause tied to evidence: "…motivating an autoregressive specification, with order to be determined from the ACF/PACF in §4.1." Then in §4.1, the existing ACF-decays / PACF-cuts-at-2 sentence does the actual justification — make sure §2 simply forward-references rather than asserting.

#### 3b. Figure 2 caption ↔ figure consistency

Peer feedback: "'Dashed lines indicate 95% confidence bands' but there are no such dashed lines". **First verify by opening [Assignment1/figures/fig2_acf_pacf.pdf](Assignment1/figures/fig2_acf_pacf.pdf).** Two cases:
- If bands are present but solid/colored: change caption wording to match ("Horizontal bands indicate the $\pm 1.96/\sqrt{T}$ 95% confidence interval").
- If bands are missing: regenerate the figure in [Assignment1/main.ipynb](Assignment1/main.ipynb) (statsmodels `plot_acf`/`plot_pacf` already draws them — most likely they were hidden by an alpha=0 or `vlines` override). This is the only notebook touch required.

#### 3c. Table 1 readability

Edit [Assignment1/tables/table1_selection.tex](Assignment1/tables/table1_selection.tex) to **bold the minimum AIC, minimum BIC, minimum $\hat\sigma$, and the LB column entry that is *not* rejected at 5% for AR(1)**. This is a one-line `\textbf{}` change per cell, no recomputation. Addresses "highlight the 'best' model for each criteria".

#### 3d. Disambiguate "LB lag-8"

Peer feedback: "what does the lag-8 refer to?". In §4.2, replace "Ljung-Box lag-8" with "Ljung-Box test at $h=8$ lags (referred to $\chi^2(h-p)=\chi^2(6)$ under the AR(2) null)". One sentence; no number changes.

### 4. Empirical §4.3 (Estimates) — fix the stationarity statement

Replace the current sentence "$\hat\phi_1+\hat\phi_2=0.847<1$ confirms stationarity" with a check against all three AR(2) triangle conditions from §3 (point 2a above), then state the roots ("complex conjugates, modulus ≈ 0.72, hence damped oscillations"). The modulus number is already in the report; we are just citing the *correct* sufficient condition.

### 5. §4.5 (GaR) — explain *why* Gaussian GaR can mis-calibrate

Peer feedback: "Maybe elaborate on why this is the case." Add one sentence: "Under residual excess kurtosis the true 10%-quantile lies further below $\mu_t$ than $\sigma\Phi^{-1}(0.10)$, so Gaussian GaR systematically understates risk; conversely, with positive skew the lower tail can be over-stated." Tie this back to the JB rejection in §4.2.

**Compensating cut**: the parenthetical in §5 (Discussion) that already gestures at this point ("Gaussian GaR can be too optimistic or too conservative…") becomes redundant — shorten it.

### 6. §5 (Discussion) — tighten, do not expand

The three-limitation structure is good. Just trim the COVID-paragraph by one sentence (already restated in conclusion) to free characters for the new theory additions in §2.

### 7. Notation / consistency sweep

- Ensure $\phi$ is used everywhere for AR coefficients in §3 and §4 (lecture notes use $\theta$; the report has standardized on $\phi$ — verify the new edits stick to $\phi$).
- The intercept symbol $\delta$ vs. the unconditional mean $\mu$ is used correctly; do not introduce $\theta(L)$ in two different senses (it's used for the AR polynomial in lecture notes but the report already uses $\phi$ for coefficients — write the polynomial as $\phi(L)=1-\phi_1 L-\cdots$ to stay consistent).

---

## Out of scope (explicitly excluded)

- Adding a rolling/expanding window for re-estimation (forecasting design is fixed by the assignment brief: estimate on 1990–2009, forecast 2010–2024).
- Quantile regression / non-parametric GaR (not in the AR/ARMA model class the brief permits, and quantile regression is not in L1–L9).
- ARCH/GARCH conditional-variance modeling (covered in L20+, after Assignment 1).
- Unit-root testing (L13+).
- A multivariate or factor-augmented specification.
- Any new figures or new estimation runs.

---

## Verification

After the edits, in order:

1. **Compile**: rebuild [assignment1.pdf](Assignment1/assignment1.pdf) and visually verify the four figures, the four tables, and (especially) Figure 2's confidence bands now match the caption.
2. **Character count**: run `pdftotext -layout Assignment1/assignment1.pdf - | awk '/^References/{exit} 1' | wc -m` and confirm the body-text count is **not greater** than the pre-edit count (currently ≈ 17k including all captions/tables; the actual 12,000-char body excludes the table-page material — the deliverable check is that no new net characters land in body prose).
3. **Cross-reference each peer-feedback item** in [received_peer_feedback_snips.md](Assignment1/received_peer_feedback_snips.md) against the edited PDF: confirm each is addressed (introduction motivation, dynamic-model / stationarity in equation form, AR(2) sufficient condition, *t*-statistic definition, LR-statistic definition, low-order AR justification, Figure 2 caption, "lag-8" clarification, Table 1 highlighting, Gaussian-GaR elaboration).
4. **Cross-reference assessment criteria** in [AssessmentCriteria.md](AssessmentCriteria.md): theory section now contains (i) precise model definition + properties (stationarity triangle, MA(∞) reference), (ii) precise estimator with assumptions (OLS=MLE under Gaussianity; QMLE sandwich), (iii) precise null + test statistic + asymptotic distribution for *t*-test, LR-test, DM-test, and coverage test.
5. **No-regression check**: the four headline numbers — BIC = −542.33, DM *t* = 1.186 (*p* = 0.236), AR(2) GaR violation rate 0.150, mean tick losses 0.0046/0.0040 — must be unchanged (these come from the notebook; the LaTeX edits do not touch them).
