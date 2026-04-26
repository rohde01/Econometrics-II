

## Plan: Assignment 3 Top-Grade Within Scope

Deliver a concise, reproducible, course-aligned co-integration analysis of U.S. house prices, rents, and mortgage rates for 2012M1-2023M12, using methods taught in Econometrics II (unit-root testing, VAR lag selection, CVAR rank testing, equilibrium/error-correction interpretation, misspecification checks, and targeted robustness only).

**Steps**
1. Define scope and report backbone (no estimation yet)  
   - Fix research question exactly as assignment asks: whether a long-run relation in equation (3.1) exists and, if yes, how equilibrium is sustained.  
   - Lock report structure in `assignment3.tex`: Introduction, Data, Econometric Theory, Empirical Analysis, Discussion, Conclusion (already scaffolded).  
   - Set explicit scope boundary: primary method = CVAR/VECM; optional compact robustness via Engle-Granger and/or pre-2012 sample sensitivity only.  
   - *Blocks all later steps: this determines what outputs are required.*

2. Build the reproducible analysis pipeline in notebook (data + exports)  
   - Implement in `main.ipynb`: data load from `Assignment_3.xlsx`, sample filter to 2012M1-2023M12, variable checks (`h`, `r`, `m`), plotting and table export paths.  
   - Reuse prior assignment conventions for export-ready artifacts (LaTeX tables in `tables/`, PDF figures in `figures/`).  
   - Keep a fixed naming scheme to match writing flow: table1...table6 and fig1...fig4.  
   - *Depends on step 1; can run in parallel with drafting prose placeholders in step 7.*

3. Data and preliminary time-series evidence  
   - Produce figure set for levels/transformations to motivate non-stationarity and co-movement (house prices, rents, mortgage rate).  
   - Produce compact descriptive statistics table (focus on relevant moments only).  
   - State data source and sample clearly (FRED-based series through assignment file).  
   - *Depends on step 2.*

4. Integration order and dynamic specification choices  
   - Run ADF-style unit-root tests consistent with course notes (in levels and first differences where relevant).  
   - Select VAR lag length with information criteria and/or LR sequence using course-consistent logic.  
   - Decide deterministic specification for CVAR (start with unrestricted constant, as hinted in assignment).  
   - *Depends on steps 2-3; blocks rank testing.*

5. Core CVAR analysis to answer assignment question  
   - Estimate CVAR for `X_t = (h_t, r_t, m_t)'`.  
   - Determine co-integration rank via trace sequence and stop at smallest non-rejected rank.  
   - For preferred rank, report normalized co-integrating relation (on `h`) and error-correction loadings (`alpha`) to explain how equilibrium is sustained.  
   - Test theory-relevant restrictions in scope: rent elasticity restriction `beta_r = 1` (strict user-cost benchmark), and discuss sign/magnitude of mortgage-rate effect (`beta_m < 0` prediction).  
   - *Depends on step 4; central decision point for final conclusion.*

6. Misspecification and compact robustness (required before strong inference claims)  
   - Run residual diagnostics for the preferred dynamic specification (autocorrelation, normality, heteroskedasticity/ARCH-style checks as applicable to your software outputs).  
   - If diagnostics fail materially, adjust lag/deterministic choice minimally and re-evaluate rank/restrictions.  
   - Run one bounded robustness extension only (to avoid overdoing): include pre-2012 period OR alternative lag length window; report whether conclusions change.  
   - *Depends on step 5; feeds directly into Discussion and limitations.*

7. Write the report to maximize grade under strict length constraints  
   - Introduction: main question, motivation, method, previewed conclusion.  
   - Theory section: model first, then estimator logic/assumptions, then test hypotheses and asymptotic distributions in course notation.  
   - Empirical section: present process (not only final model), show model-selection path, diagnostics before final hypothesis conclusions, then economic interpretation.  
   - Discussion: limitations (sample, lag sensitivity, deterministic specification, potential regime changes) and robustness takeaway.  
   - Keep text <=12,000 characters including spaces; move detail density into high-information tables/figures (max 2 pages output).  
   - *Can partially run in parallel with steps 5-6 once early outputs exist; finalized after step 6.*

8. Final integration and submission-quality checks  
   - Insert all selected tables/figures into `assignment3.tex` with consistent numbering/captions and in-text references.  
   - Verify every reported test includes: null, statistic, reference distribution/critical value basis, and conclusion.  
   - Verify anonymity and formatting constraints (English, no identifiers, page/character limits).  
   - Compile PDF and perform final coherence pass: question -> method -> evidence -> conclusion.

**Relevant files**
- `/Users/user/Projects/Econometrics-II/Assignment3/Assignment_3_s2026.md` — primary task definition, period, theory expectations, robustness options.
- `/Users/user/Projects/Econometrics-II/AssessmentCriteria.md` — grading rubric for writing, theory, model selection, diagnostics, conclusions.
- `/Users/user/Projects/Econometrics-II/TipsforWriting.md` — structure and presentation rules that map directly to rubric.
- `/Users/user/Projects/Econometrics-II/reading_plan.md` — course scope boundary (cointegration/CVAR toolbox weeks).
- `/Users/user/Projects/Econometrics-II/course_notes3/06_Cointegration_s2026.md` — Engle-Granger logic, unit-root-on-residuals, ECM interpretation.
- `/Users/user/Projects/Econometrics-II/course_notes3/CointegratedVAR_Lecture.md` — CVAR rank testing, alpha/beta interpretation, restriction testing.
- `/Users/user/Projects/Econometrics-II/course_notes2/Vector_Autoregressive_Models.md` — lag-length logic, VAR diagnostics/inference backbone.
- `/Users/user/Projects/Econometrics-II/Assignment3/main.ipynb` — full empirical workflow and export generation.
- `/Users/user/Projects/Econometrics-II/Assignment3/tables/` — LaTeX tables for main/robustness results.
- `/Users/user/Projects/Econometrics-II/Assignment3/figures/` — exported figures for data, diagnostics, and robustness visuals.
- `/Users/user/Projects/Econometrics-II/Assignment3/assignment3.tex` — final write-up integration and submission PDF.

**Verification**
1. Re-run notebook from top to bottom without manual intervention; confirm all expected artifacts are regenerated in `tables/` and `figures/`.
2. Confirm at least one complete model-selection path is documented: lag choice -> rank choice -> restriction testing -> preferred model.
3. Confirm diagnostics are presented before final inferential claims on co-integration/restrictions.
4. Cross-check reported signs/restrictions with theory: `beta_r > 0`, `beta_m < 0`, and explicit test of `beta_r = 1`.
5. Character-count audit of textual sections to stay within 12,000 characters (including spaces) and output pages within 2-page cap.
6. Compile `assignment3.tex` successfully and verify all captions, numbering, and in-text references are consistent.

**Decisions**
- Included scope: CVAR-centered analysis with standard course diagnostics and one compact robustness extension.
- Excluded scope (to prevent overdoing): SVAR/IRFs, structural-break/threshold cointegration, expanding variable set beyond `h, r, m`, advanced non-course methods.
- Preferred strategy: prioritize a clean, defensible empirical chain over multiple alternative models.

**Further Considerations**
1. Primary robustness choice recommendation: use pre-2012 sample extension (economic relevance from bubble/crisis period) rather than many lag permutations.
2. If mortgage-rate integration properties look borderline in short sample, keep CVAR treatment but explicitly note this as a limitation and robustness sensitivity point.
3. If CVAR rank is weakly identified, include a compact Engle-Granger residual-based check as supporting evidence (not as a second full main model).
