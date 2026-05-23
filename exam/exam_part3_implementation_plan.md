# Plan: Econometrics II 2026 Exam — Part 3 (Additional Assignment)

## Context

Part 3 is a **purely theoretical** assignment with 7 questions covering material the two empirical hand-ins do not cover: the algebra of VAR(1) impulse responses, OLS consistency under conditional heteroskedasticity, an ARCH-with-exogenous-regressor model (modified ARCH(1) where the conditional variance of $y_t$ depends on $x_{t-1}^2$), the joint conditional log-likelihood and separability of estimation, multi-step volatility forecasts, and QMLE/GMM under non-Gaussian innovations. The course curriculum already covers everything needed: VAR algebra (course_notes2/Vector_Autoregressive_Models.md), ARCH/GARCH (course_notes3/08_ARCH_s2026.md), conditional models / likelihood factorization (course_notes/03_ConditionalModels_s2026.md, 01_LikelihoodAnalysis_s2026.md), and GMM (course_notes3/GMM_Estimation_Lecture_Notes.md). The graders explicitly state Part 3 questions are "specific and do not attempt to trick you" and that the standard for a top grade is **precision** — correct statements, correct notation, clear assumptions, full derivations, no hand-waving. There is **no character limit** but the instructor explicitly recommends being brief and to the point.

**Deliverable:** A self-contained derivation-style write-up appended to `exam/exam.tex`, compiled into the single PDF that the user submits alongside Parts 1 and 2. **LaTeX only — no notebook, no figures, no data analysis.** Part 3 is purely theoretical.

## Files to Modify

- **Modify:** `exam/exam.tex` — fill out the `\section{Part 3 - The Additional Assignment}` body with 7 numbered subsections, one per question. 12pt, 1.5 line spacing (already set in scaffold). Match notation of `exam/Econometrics_Exam_Part3.md` verbatim ($\Phi$, $\phi_1,\phi_2,\phi_3$, $\omega_{ij}$, $\psi$, $\mathcal{I}_t$, $\sigma_t^2$).

## Question-by-Question Solution Outline

For each question below: state the result, then sketch the derivation. The write-up should mirror this structure with full intermediate steps.

### Q1(a) — $\Phi^{(k)}_{12}$ for $\phi_1\neq\phi_3$
- $\Phi$ is upper-triangular ⇒ eigenvalues are $\phi_1,\phi_3$ and $\Phi^k$ is upper-triangular with diagonal $(\phi_1^k,\phi_3^k)$.
- **Recommended approach:** induction on $k$. Base case $k=1$: $\Phi^{(1)}_{12}=\phi_2$, matches $\phi_2(\phi_1-\phi_3)/(\phi_1-\phi_3)=\phi_2$. Step: $\Phi^{k+1}=\Phi\,\Phi^k$, so $\Phi^{(k+1)}_{12}=\phi_1\Phi^{(k)}_{12}+\phi_2\Phi^{(k)}_{22}=\phi_1\,\phi_2\frac{\phi_1^k-\phi_3^k}{\phi_1-\phi_3}+\phi_2\phi_3^k=\phi_2\frac{\phi_1^{k+1}-\phi_3^{k+1}}{\phi_1-\phi_3}$.
- (Alternative: spectral decomposition $\Phi=V\Lambda V^{-1}$, with $V$ the eigenvector matrix — give as a brief remark.)

### Q1(b) — Special case $\phi_1=\phi_3$
- The $0/0$ form in (5.4) is resolved by L'Hôpital w.r.t. $\phi_3$ (treating $\phi_1$ as the limit): $\Phi^{(k)}_{12}=\phi_2\,k\,\phi_1^{k-1}$.
- Or derive directly: by induction $\Phi^{(k)}_{12}=\phi_2\sum_{j=0}^{k-1}\phi_1^{k-1}=\phi_2\,k\,\phi_1^{k-1}$.

### Q1(c) — Cumulated IRF $\sum_{k=0}^\infty \Phi^{(k)}_{12}$
- $\Phi^{(0)}=I$ contributes 0 to the $(1,2)$ slot. For $k\geq 1$:
$$\sum_{k=1}^\infty \phi_2\frac{\phi_1^k-\phi_3^k}{\phi_1-\phi_3}=\frac{\phi_2}{\phi_1-\phi_3}\!\left[\frac{\phi_1}{1-\phi_1}-\frac{\phi_3}{1-\phi_3}\right]=\frac{\phi_2}{(1-\phi_1)(1-\phi_3)}.$$
- Convergence requires $|\phi_1|<1, |\phi_3|<1$ (already assumed). Identify with the $(1,2)$-element of $(I-\Phi)^{-1}$.

### Q2 — OLS consistency when $\varepsilon_t=H_t^{1/2}u_t$
- **Yes, equation-by-equation OLS is consistent.** Argument has two ingredients:
  1. Regressor–error orthogonality at the population level. Since $H_t^{1/2}\in\mathcal{I}_{t-1}$ and $u_t$ is i.i.d. mean-zero independent of $\mathcal{I}_{t-1}$, $E[\varepsilon_t\mid\mathcal{I}_{t-1}]=H_t^{1/2}E[u_t]=0$. Hence $E[Z_{t-1}\varepsilon_t']=0$.
  2. A LLN/ergodic theorem applies because $\{(Z_t,\varepsilon_t)\}$ is stationary (assumed) and weakly dependent: $\frac{1}{T}\sum Z_{t-1}Z_{t-1}' \xrightarrow{p} E[Z_{t-1}Z_{t-1}']$ (PD), and $\frac{1}{T}\sum Z_{t-1}\varepsilon_t' \xrightarrow{p}0$.
- Together, $\hat\Phi_{\text{OLS}}=\Phi+\big(\tfrac{1}{T}\sum Z_{t-1}Z_{t-1}'\big)^{-1}\tfrac{1}{T}\sum Z_{t-1}\varepsilon_t'\xrightarrow{p}\Phi$.
- **Caveat to mention** (this is what graders reward): OLS is **no longer efficient**, the usual MLE-equals-OLS equivalence breaks because the Gaussian likelihood is misspecified, and asymptotic variance must use heteroskedasticity-robust (sandwich) standard errors. Cite the parallel result for ARCH-type regressions in [08_ARCH_s2026.md §3].

### Q3 — Unconditional variance of $\varepsilon_t$ in the ARCH-X model
- By the law of iterated expectations and stationarity: $E[\varepsilon_t^2]=E[\sigma_t^2]=\omega+\alpha E[\varepsilon_{t-1}^2]+\gamma E[x_{t-1}^2]$.
- $\{x_t\}$ is a stationary AR(1) with $|\phi_3|<1$ and Gaussian innovation, so $E[x_t]=0$ and $E[x_t^2]=\sigma_\eta^2/(1-\phi_3^2)$.
- Solving for $E[\varepsilon_t^2]$ yields (5.8).
- **Conditions for well-defined and strictly positive:** $\omega>0$, $\alpha\geq 0$, $\gamma\geq 0$, $\sigma_\eta^2>0$, $|\phi_3|<1$, and crucially $0\leq\alpha<1$. Numerator is positive; denominator $1-\alpha>0$.
- **Comparison to standard ARCH(1)** ($\gamma=0$): reduces to $\omega/(1-\alpha)$. The extra term $\gamma\sigma_\eta^2/[(1-\alpha)(1-\phi_3^2)]$ is the contribution from the persistent exogenous regressor $x_{t-1}^2$; persistence in $x_t$ amplifies the unconditional variance of $\varepsilon_t$.

### Q4 — Conditional joint density and log-likelihood
- **Independence ⇒ factorization.** Since $z_t \perp \eta_t$ and both are independent of $\mathcal{I}_{t-1}$, the conditional distributions are independent: $f(y_t,x_t\mid\mathcal{I}_{t-1})=f(y_t\mid\mathcal{I}_{t-1})\,f(x_t\mid\mathcal{I}_{t-1})$.
- $f(y_t\mid\mathcal{I}_{t-1})=\frac{1}{\sqrt{2\pi\sigma_t^2}}\exp\!\big(-\tfrac{(y_t-\phi_1 y_{t-1}-\phi_2 x_{t-1})^2}{2\sigma_t^2}\big)$, with $\sigma_t^2=\omega+\alpha(y_{t-1}-\phi_1 y_{t-2}-\phi_2 x_{t-2})^2+\gamma x_{t-1}^2$ (note: $\varepsilon_{t-1}^2$ is a function of past $y$'s, $x$'s and $\theta_y$, hence measurable w.r.t. $\mathcal{I}_{t-1}$ given the parameters).
- $f(x_t\mid\mathcal{I}_{t-1})=\frac{1}{\sqrt{2\pi\sigma_\eta^2}}\exp\!\big(-\tfrac{(x_t-\phi_3 x_{t-1})^2}{2\sigma_\eta^2}\big)$.
- **Log-likelihood:** $\log L(\psi)=\sum_{t=1}^T \log f(y_t\mid\mathcal{I}_{t-1};\theta_y)+\sum_{t=1}^T \log f(x_t\mid\mathcal{I}_{t-1};\theta_x)$ with $\theta_y=(\phi_1,\phi_2,\omega,\alpha,\gamma)$ and $\theta_x=(\phi_3,\sigma_\eta^2)$. Write out both sums explicitly.
- **Separability:** YES, the parameters can be estimated separately. Reason: parameter spaces $\theta_y$ and $\theta_x$ are **variation-free** and appear in disjoint summands, so $\arg\max_\psi \log L = (\arg\max_{\theta_y}\log L_y,\,\arg\max_{\theta_x}\log L_x)$. Cite the conditional/marginal cut argument in [03_ConditionalModels_s2026.md].
- (Optional polish: note that for finite-sample MLE we treat $\varepsilon_0,y_0,x_0$ as given initial conditions, in line with the conditional likelihood convention in the lecture notes.)

### Q5(a) — One- and two-step volatility forecasts
- **$\sigma_{T+1\mid T}^2$:** $\sigma_{T+1}^2=\omega+\alpha\varepsilon_T^2+\gamma x_T^2$, and all three RHS variables are in $\mathcal{I}_T$ ($\varepsilon_T=y_T-\phi_1 y_{T-1}-\phi_2 x_{T-1}$ is a deterministic function of $\mathcal{I}_T$ given $\theta$). Hence $\sigma_{T+1\mid T}^2=\omega+\alpha\varepsilon_T^2+\gamma x_T^2$.
- **$\sigma_{T+2\mid T}^2$:** $\sigma_{T+2\mid T}^2 = \omega+\alpha E[\varepsilon_{T+1}^2\mid\mathcal{I}_T]+\gamma E[x_{T+1}^2\mid\mathcal{I}_T]$. By LIE, $E[\varepsilon_{T+1}^2\mid\mathcal{I}_T]=E[\sigma_{T+1}^2 z_{T+1}^2\mid\mathcal{I}_T]=\sigma_{T+1\mid T}^2$ (since $z_{T+1}\perp\mathcal{I}_T$, $E[z_{T+1}^2]=1$). For the $x$-term: $x_{T+1}=\phi_3 x_T+\eta_{T+1}$, so $E[x_{T+1}^2\mid\mathcal{I}_T]=\phi_3^2 x_T^2+\sigma_\eta^2$. Putting together:
$$\sigma_{T+2\mid T}^2=\omega+\alpha\,\sigma_{T+1\mid T}^2+\gamma(\phi_3^2 x_T^2+\sigma_\eta^2).$$

### Q5(b) — Convergence as $h\to\infty$
- Recursion for $h\geq 2$: $\sigma_{T+h\mid T}^2=\omega+\alpha\sigma_{T+h-1\mid T}^2+\gamma\,E[x_{T+h-1}^2\mid\mathcal{I}_T]$.
- $E[x_{T+h-1}^2\mid\mathcal{I}_T]\to \sigma_\eta^2/(1-\phi_3^2)$ as $h\to\infty$ because AR(1) forecasts of $x_t^2$ converge to the unconditional mean (under $|\phi_3|<1$).
- The recursion is then asymptotically $\sigma_{T+h\mid T}^2=\omega+\alpha\sigma_{T+h-1\mid T}^2+\gamma\sigma_\eta^2/(1-\phi_3^2)+o(1)$, a contraction with rate $\alpha<1$, whose fixed point is exactly (5.8).
- Conclude: $\sigma_{T+h\mid T}^2\to E[\varepsilon_t^2]$ at exponential rate $\alpha$ (with a transient at rate $\phi_3^2$ from the $x$-side).

### Q6 — GMM under non-Gaussian $z_t$
- **Step 1: Verify conditional moments at $\psi_0$.**
  - $E[\varepsilon_t\mid\mathcal{I}_{t-1}]=\sigma_t E[z_t]=0$ (since $\sigma_t\in\mathcal{I}_{t-1}$ and $z_t\perp\mathcal{I}_{t-1}$, $E[z_t]=0$).
  - $E[\varepsilon_t^2-\sigma_t^2\mid\mathcal{I}_{t-1}]=\sigma_t^2(E[z_t^2]-1)=0$.
- **Step 2: Build unconditional moments via instruments.** Standard course device: any function of $\mathcal{I}_{t-1}$ is a valid instrument. Five parameters $(\phi_1,\phi_2,\omega,\alpha,\gamma)$ require at least 5 moments.
  - **Mean-equation moments (2):** $g_t^{(1)}(\theta_y)=\varepsilon_t(\theta_y)\cdot(y_{t-1},x_{t-1})'$, with $E[g_t^{(1)}(\theta_{y,0})]=0$ by LIE.
  - **Variance-equation moments (3):** $g_t^{(2)}(\theta_y)=(\varepsilon_t^2-\sigma_t^2)\cdot(1,\varepsilon_{t-1}^2,x_{t-1}^2)'$ (or equivalently $(1,y_{t-1}^2,x_{t-1}^2)'$), with $E[g_t^{(2)}(\theta_{y,0})]=0$.
- **Step 3: Estimator.** Stack $g_t(\theta_y)=(g_t^{(1)\,\prime},g_t^{(2)\,\prime})'\in\mathbb{R}^5$; define $g_T(\theta_y)=\tfrac{1}{T}\sum_{t=1}^T g_t(\theta_y)$. Then $\hat\theta_y^{GMM}=\arg\min_{\theta_y} g_T(\theta_y)'W_T g_T(\theta_y)$.
- Just-identified case: choice of $W_T$ does not affect the estimator; over-identification (extra instruments) allows efficiency gains via $W_T^{opt}=\hat S^{-1}$ and yields an over-identification ($J$) test. Cite [GMM_Estimation_Lecture_Notes.md] for the $V=(D'WD)^{-1}D'WSWD(D'WD)^{-1}$ sandwich.
- **Why GMM, not Gaussian MLE:** without $z_t\sim N(0,1)$, the Gaussian likelihood is misspecified; QMLE remains consistent (sandwich variance) but the conditional moment restrictions (5.9) are the *minimal* assumptions and motivate GMM as the natural estimator.

### Q7 — Test $H_0:\gamma=0$
- Under regularity, $\sqrt{T}(\hat\theta_y-\theta_{y,0})\xrightarrow{d} N(0,V)$ with $V$ from the GMM sandwich. Let $\hat V$ be a consistent estimator (use HAC if needed, but in this i.i.d.-in-$z_t$ setting the standard sample-analog estimator suffices).
- **Wald test:** With selection vector $R=(0,0,0,0,1)$ picking $\gamma$ out of $\theta_y$:
$$\xi_W=T\,(R\hat\theta_y)'(R\hat V R')^{-1}(R\hat\theta_y)=T\,\frac{\hat\gamma^2}{\hat V_{\gamma\gamma}}\xrightarrow{d}\chi^2(1)\quad\text{under }H_0.$$
- Equivalent t-statistic: $\sqrt{T}\hat\gamma/\sqrt{\hat V_{\gamma\gamma}}\xrightarrow{d}N(0,1)$. Reject for large $|t|$.
- **One-sentence boundary caveat:** since the model imposes $\gamma\geq 0$, $H_0:\gamma=0$ puts the parameter on the boundary; a strictly correct one-sided test uses a 50:50 mixture of $\chi^2(0)$ and $\chi^2(1)$ (analogous to testing for ARCH effects at the boundary). Include this as one trailing sentence after the Wald derivation — not a full re-derivation.

## Style and Formatting Conventions

- 12pt, 1.5 line-spacing already in `exam/exam.tex`. Use `amsmath` `align`/`equation` environments, number key equations.
- Match exam notation precisely: $\Phi^{(k)}_{12}$, $\mathcal{I}_{t-1}$, $\psi$, $\theta$, $\sigma_t^2$. Avoid introducing new symbols where the exam already names them.
- Sub-section per question: `\subsection*{Question (1)}`, etc.
- Lead each question with a one-line statement of the result before the derivation. End with a one-line interpretation/comment where it adds value (Q1c, Q3 comparison, Q5b, Q7 boundary).
- Cite course material lightly (e.g., "by the QMLE result in §4 of the ARCH notes"); the exam is closed-book in the formal sense but the lecture notes are the natural reference and graders expect alignment with course conventions.

## Verification

1. **LaTeX compiles cleanly.** `cd exam && pdflatex exam.tex` produces a PDF with no unresolved references and reasonable typesetting.
2. **Spot-check formulas algebraically.** For Q1(a), verify the induction step on paper for $k=2,3$. For Q3, plug $\gamma=0$ into (5.8) and confirm it collapses to $\omega/(1-\alpha)$. For Q5(b), check the fixed point of the recursion equals (5.8) by direct substitution.
3. **Proofread pass.** Every parameter restriction stated; every conditional moment computation justified by a one-line invocation of LIE / independence / stationarity. No "approximately correct" claims (graders flag this explicitly in the criteria).
4. **Cross-check against curriculum.** Q2 mirrors the OLS-vs-MLE discussion in §3 of the ARCH notes; Q4 mirrors §3 of the Conditional Models notes; Q5 mirrors the GARCH forecasting recursion in §5; Q6–Q7 mirror the conditional-moment-to-GMM construction in the GMM lecture notes. If any answer drifts from these reference treatments, revise to align.
