# Plan: Exam Part 2 — Improving Assignment 3 for Top-Grade Hand-In

## Context

Part 2 of the exam is the user's already-completed Assignment 3 (a CVAR/co-integration analysis of U.S. house prices, rents, and the 30-year mortgage rate, 2012M1–2023M12). The semester version is good enough to pass but contains several concrete gaps that map directly to (i) explicit assessment-criteria requirements, (ii) the assignment's hints, and (iii) peer feedback received from other students. None of these gaps requires a redesign — the structure, sample, lag choice (k=4, AIC), deterministic specification (unrestricted constant), rank decision (r=1), and diagnostic toolkit are all sound. The job is targeted polish: tighten the writing, plug missing theory items, run the one formal hypothesis test the assignment explicitly names (β_r = 1) and one bounded robustness check, and fix presentation defects.

**Current state baseline (no edits needed beyond targeted fixes):**
- Sample, lag-length (k_ar=4 → k_ar_diff=3), deterministic specification, rank decision (r=1), diagnostics, and overall structure all defensible.
- Character count of LaTeX body ≈ 10,200 / 12,000 — about **1,800 characters of headroom** for additions.
- 3 figures, 6 tables already in place; output stays within the 2-page figures-and-tables cap.

**Files in scope:**
- `Assignment3/assignment3.tex` — the report. Mostly prose edits + a few new sentences.
- `Assignment3/main.ipynb` — extend with (a) Johansen LR test of `β_r = 1`, (b) extract `stderr_alpha`/`stderr_beta` from VECM, (c) one robustness sub-sample run, (d) fix Table 1/3 export bugs.
- `Assignment3/tables/*.tex`, `Assignment3/figures/*.pdf` — regenerated via notebook.

**Explicit non-goals:** no SVAR, no IRFs, no Engle-Granger second model, no expanded variable set, no max-eigenvalue test, no overhaul of structure or sample.

---

## Improvements

### A. Theory section — fill assessment-criteria gaps (peer feedback + AssessmentCriteria.md §3)

Currently the theory section names the CVAR/VECM and the Johansen trace statistic but does **not** state nulls, test statistics, and asymptotic distributions for the tests actually used (ADF, Johansen trace, restriction LR). Add these compactly:

1. **ADF block** (add a short paragraph in the Econometric Theory section, moving the unit-root setup out of the empirical section):
   - Null `H_0: ρ = 1` in `Δy_t = (ρ-1)y_{t-1} + Σ φ_j Δy_{t-j} + c + ε_t` against `ρ < 1`.
   - Statistic is the t-ratio on `(ρ-1)`.
   - Asymptotic distribution is the **non-standard Dickey–Fuller distribution** (not N(0,1)) — must cite explicitly per assessment criterion #3.
2. **Johansen trace block** (extend the existing trace-statistic paragraph):
   - State `H_0: rank(Π) ≤ r_0` vs `H_1: rank(Π) > r_0`.
   - Note that the trace statistic has a **non-standard asymptotic distribution** depending on the deterministic specification (unrestricted constant here), with critical values from Johansen (1995).
   - State the sequential procedure starts at `r_0=0` and stops at first non-rejection (already there — leave it).
3. **LR restriction test on β** (new short paragraph, only one or two sentences):
   - Linear restriction `H_0: R'β = c` on the (normalized) co-integrating vector is tested by the LR statistic `LR = -T Σ_{i=1}^{r} log[(1-λ̃_i)/(1-λ̂_i)] ~ χ²(s)` under `H_0`, where `λ̃_i` are the restricted eigenvalues and `s` is the number of restrictions.
   - This is the standard tool for the assignment's testable restriction `β_r = 1`.
4. **One-line statement of CVAR estimator assumptions** (peer feedback #4 explicitly asks for this):
   - "The CVAR is estimated by Gaussian maximum likelihood under the assumptions of (i) correct lag length, (ii) i.i.d. Gaussian innovations, and (iii) constant parameters; rank inference is robust to non-Gaussianity but inference on coefficients relies on the latter two."

### B. Add the one hypothesis test the assignment explicitly names

The assignment statement says: *"Under the strict user cost model, the rent elasticity satisfies β₁ = 1, which is a testable restriction."* The current draft only says "the strict unit-elasticity restriction β₁=1 is not supported by the point estimate" — that is **not a formal test**. This is the single most concrete deliverable a top-grade hand-in must add.

- **Method:** Johansen LR test of the linear restriction `β_r = 1` on the normalized cointegrating vector (with `r=1`). Distribution `χ²(1)` under H_0.
- **Implementation:** estimate the restricted CVAR by parameterising the cointegrating vector as `β = (1, -1, β_m)'` (normalising on h and imposing the unit rent elasticity), recompute the restricted canonical eigenvalues from the partial-out moment matrices, and form `LR = -T·log[(1-λ̃₁)/(1-λ̂₁)]` ~ `χ²(1)` under H_0. Custom helper in the notebook (~30 lines: regress `ΔX_t` and `X_{t-1}` on lagged differences + constant to get `R_0, R_1`; compute `S_{ij}` matrices; solve the unrestricted generalised eigenproblem for `λ̂_i`; for the restricted version, replace `X_{t-1}` with `H'X_{t-1}` where `H` spans the restricted space and re-solve). Recipe in `course_notes3/CointegratedVAR_Lecture.md`.
- **Sister Wald test:** also report `β_m = 0` via `tvalues_beta[2]` (or directly using `stderr_beta`) since the point estimate (0.0085) is essentially zero and the theory predicts `β_m < 0`. Adds one row to Table 5 or Table 7.

### C. Table 5 — add standard errors for β and α (no SEs currently shown)

A long-run coefficient table with no measure of uncertainty cannot support claims like "rent elasticity is above one rather than equal to one". Extend the notebook cell that writes `table5_cvar_estimates.tex` to include `vecm_res.stderr_beta` (for `β_r`, `β_m`) and `vecm_res.stderr_alpha` (for `α_h`, `α_r`, `α_m`), and reformat the table as two columns: Estimate, Std. error (or include t-statistics where useful, e.g., for testing `α_h = 0`, which is the "no error-correction in the h equation" hypothesis that motivates the discussion of which equation does the adjustment).

### D. Robustness — one bounded extension only

The assignment hint #6 explicitly mentions investigating the pre-2012 sample. Currently the discussion only *promises* this exercise. Do it, compactly:

- Re-estimate the CVAR on the full sample 2000M1–2023M12 with the same specification (constant unrestricted, same lag-selection procedure applied to that sample) and report in a single small table: lag chosen, trace statistic at r=0 and r≤1, the normalized β_r and β_m, and whether the LR test of `β_r=1` rejects. One paragraph of commentary in the Discussion section is enough.
- Keep this to a 3- to 5-row table; not a full re-run of all diagnostics. The point is sensitivity, not duplication.

### E. Targeted prose edits driven by peer feedback

1. **Intro:** add one sentence previewing the main finding (one co-integrating relation; rent elasticity statistically above 1; mortgage coefficient near zero; adjustment carried mainly by mortgage rate) and one sentence on real-world relevance (housing market matters for macro stability). Per peers #1 and #2.
2. **Intro paragraph 2:** explicitly name "CVAR with k=4 lags and unrestricted constant, estimated by Gaussian ML" — per peer #3.
3. **Connect α to economic adjustment** right after equation `eq:cvar`: "α_h, α_r, α_m measure how house prices, rents, and mortgage rates respectively respond to disequilibrium in the long-run relation." — per peer #3.
4. **Between subsections, add brief transition sentences**: "Since all three series appear I(1), we proceed to co-integration testing." / "Having found rank r=1, we next characterise the long-run relation and test the theory restriction β_r=1." — per peer #7.
5. **Empirical Analysis §"Co-Integration Rank"**: explicitly state the Johansen null when introducing Table 4 ("`H_0: r=0` vs `H_1: r≥1`; reject if trace > 5% critical value"). — per peer #5.
6. **Empirical Analysis §"Misspecification Diagnostics"**: add a closing sentence — "These results support consistency of the rank estimate, but violations of normality and homoskedasticity imply standard errors on β and α should be interpreted with caution and asymptotic-normality based tests are at best approximate." — per peer #9.

### F. Presentation defects

1. **Table 3 (lag selection):** the LaTeX export is missing the **AIC column header** (the leftmost numeric column shows AIC values but has no header). Fix in the notebook by setting the column name explicitly or by reformatting via `to_latex` with proper column index.
2. **Table 1 (summary stats):** drop the duplicates — `m` and `MortgageRate` are the same series; show only the analysis variables `h, r, m` (the raw `HousePrice` and `Rent` add no information once `h = log(HousePrice)` and `r = log(Rent)` are reported). Keeps the table compact and information-dense.
3. **All tables should use `[H]`** for placement consistency — currently inconsistent (`table1`, `table4`, `table5`, `table6` lack `[H]`, causing the float pile-up the peer flagged). Update the notebook export helper to wrap with `\begin{table}[H]`.
4. **Anonymity check:** verify the title/preamble contains no name or student ID (currently does not — confirm after edits).

### G. Notebook — concrete code-level changes

1. **Cell 6 (summary stats):** restrict `summary_vars` to `["h", "r", "m"]`; drop the raw-level variables.
2. **Cell 12 (lag selection):** name the AIC column explicitly so `to_latex` emits the header. Wrap with `\begin{table}[H]`.
3. **Cell 15 (CVAR table):** include `vecm_res.stderr_alpha[:, 0]` and `vecm_res.stderr_beta[:, 0]` (handling the normalisation: under `normalize_on_h`, `stderr_beta[0]=0` and the remaining entries give SEs for `β_r`, `β_m`). Output as two-column Estimate/SE table.
4. **New cell after 15 — LR test of β_r = 1:** implement reduced-rank regression with imposed restriction; compute restricted λ̃₁; report `LR = -T·log[(1-λ̃₁)/(1-λ̂₁)]` and the χ²(1) p-value. If too involved, fall back to Wald `((β̂_r-1)/SE(β̂_r))² ~ χ²(1)`. Save a small table `tables/table7_restriction_test.tex`.
5. **New cell — robustness on full sample:** repeat the lag-selection / Johansen / restriction-test pipeline on `2000M1–2023M12`. Emit a single comparison table `tables/table8_robustness.tex` (columns: 2012M1–2023M12, 2000M1–2023M12; rows: lag, trace at r=0, β_r, β_m, LR(β_r=1) p-value).
6. **All `to_latex` calls** — switch the placement to `[H]` by writing the wrapper line manually (`pandas.to_latex` doesn't emit `[H]`; either post-process the string or build the LaTeX by hand for these tables).

### H. LaTeX edits in `assignment3.tex`

1. Introduce two new tables/inputs: `\input{tables/table7_restriction_test.tex}` (inside the §"Preferred CVAR and Interpretation" right after the discussion of β_r) and `\input{tables/table8_robustness.tex}` (inside the §"Discussion").
2. Rewrite the §"Preferred CVAR and Interpretation" paragraph to use the formal LR/Wald result instead of a point-estimate comparison: "The Johansen LR test of `H_0: β_r = 1` yields a test statistic of XXX (χ²(1) p-value YYY), so the strict unit-elasticity restriction is rejected/not rejected at the 5% level."
3. Add the four targeted theory paragraphs from §A above to the Econometric Theory section.
4. Add the prose edits from §E throughout.

### I. Stay within formal requirements

- Hard cap of **12,000 characters including spaces, math, formulas** for body text. Current ~10,200; additions in §A–§E total roughly 1,500 characters of new prose. **Budget margin ≈ 300 chars.** If we go over, the first trims are: (1) shrink the §A4 estimator-assumptions sentence, (2) condense the §E1 intro motivation. Run a character-count check after editing.
- Output cap of **2 pages for figures and tables**. With one figure and one new small table added (table7, table8), and table1 made smaller, the total should remain within the cap. If pressed, drop `fig3_residuals_acf.pdf` (the diagnostics table conveys the same information for the writeup).
- 12pt font, 1.5 spacing — already in the preamble.
- No names / student IDs — confirm.

---