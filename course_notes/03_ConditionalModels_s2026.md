# Conditional Models for Stationary Time Series
**Econometrics II**  
*Rasmus Søndergaard Pedersen*

---

## Outline

1. The autoregressive distributed lag (ADL) model.
2. Dynamic and long-run multipliers in the ADL model.
3. The general case.
4. The error correction model (ECM).
5. Empirical example: GDP and stock market returns.

---

## 1. The ADL Model

We want to model the relationship between variables $y_t$ and $x_t$ and **assume the direction of causality**:

$$x_t \rightsquigarrow y_t$$

We are interested in the conditional mean, and assume linearity and a given lag-length. Then:

$$E(y_t \mid y_1, \ldots, y_{t-1}, x_1, \ldots, x_{t-1}, x_t) = \delta + \theta y_{t-1} + \phi_0 x_t + \phi_1 x_{t-1}$$

This can also be written as a linear regression:

$$y_t = \delta + \theta y_{t-1} + \phi_0 x_t + \phi_1 x_{t-1} + \epsilon_t$$

with $E(\epsilon_t \mid y_{t-1}, x_t, x_{t-1}) = 0$. Called the **autoregressive distributed lag (ADL) model**.

We may write the model using lag polynomials as:

$$\theta(L)y_t = \delta + \phi(L)x_t + \epsilon_t$$

with $\theta(L) = 1 - \theta L$ and $\phi(L) = \phi_0 + \phi_1 L$.

The model can easily be extended, e.g.:

$$y_t = \delta + \sum_{i=1}^{k_y} \theta_i y_{t-i} + \sum_{i=0}^{k_x} \phi_i x_{t-i} + \sum_{i=0}^{k_z} \xi_i z_{t-i} + \epsilon_t$$

**Stationarity condition:** $y_t$ is stationary if (1) $x_t$ is stationary and (2) the AR polynomial is invertible, i.e. $|\theta| < 1$.

### Interpretation

Interpretations of coefficients is somewhat complicated — there is no natural *ceteris paribus* experiment. Key interpretable aspects:

1. **Contemporaneous impact** $\frac{\partial y_t}{\partial x_t}$
2. **Long-run / steady-state / equilibrium** solution
3. **Speed of adjustment** towards equilibrium
4. **Dynamic multipliers**: $\frac{\partial y_t}{\partial x_t},\ \frac{\partial y_{t+1}}{\partial x_t},\ \frac{\partial y_{t+2}}{\partial x_t},\ \ldots$

---

## 2. Dynamic and Long-Run Multipliers

### Dynamic Multipliers

From successive period equations we can find the dynamic multipliers as derivatives:

$$\frac{\partial y_t}{\partial x_t} = \phi_0$$

$$\frac{\partial y_{t+1}}{\partial x_t} = \theta\phi_0 + \phi_1$$

$$\frac{\partial y_{t+2}}{\partial x_t} = \theta(\theta\phi_0 + \phi_1)$$

$$\frac{\partial y_{t+3}}{\partial x_t} = \theta^2(\theta\phi_0 + \phi_1)$$

$$\vdots$$

$$\frac{\partial y_{t+k}}{\partial x_t} = \theta^{k-1}(\theta\phi_0 + \phi_1)$$

Due to stationarity $|\theta| < 1$, shocks have **transitory effects**.

Writing $\theta(L)y_t = \delta + \phi(L)x_t + \epsilon_t$, the solution is:

$$y_t = \theta^{-1}(L)\delta + \theta^{-1}(L)\phi(L)x_t + \theta^{-1}(L)\epsilon_t$$

where $\theta^{-1}(L)\delta = \frac{\delta}{1-\theta}$ and the dynamic multipliers come from:

$$\frac{\phi(L)}{\theta(L)}x_t = \phi_0 x_t + \sum_{i=1}^{\infty} \theta^{i-1}(\theta\phi_0 + \phi_1)\, x_{t-i}$$

### Long-Run Solution and Long-Run Multiplier

Defining the **steady state** as $y_t = y_{t-1}$, $x_t = x_{t-1}$, $\epsilon_t = 0$:

$$y_t = \frac{\delta}{1-\theta} + \frac{\phi_0 + \phi_1}{1-\theta}\, x_t$$

This is the **long-run solution**. The **long-run multiplier** is:

$$\frac{\partial E(y_t)}{\partial E(x_t)} = \frac{\phi_0 + \phi_1}{1-\theta} = \frac{\phi(1)}{\theta(1)}$$

This also equals the sum of all accumulated short-run effects:

$$\sum_{k=0}^{\infty} \frac{\partial y_{t+k}}{\partial x_t} = \frac{\phi_0 + \phi_1}{1 - \theta}$$

---

## 3. The General Case

Consider the general two-variable case, **ADL$(p, q)$**:

$$\theta(L)y_t = \delta + \phi(L)x_t + \epsilon_t$$

where:

$$\theta(L) = 1 - \theta_1 L - \theta_2 L^2 - \ldots - \theta_p L^p$$
$$\phi(L) = \phi_0 + \phi_1 L + \phi_2 L^2 + \ldots + \phi_q L^q$$

The solution is:

$$y_t = \frac{\delta}{\theta(1)} + \sum_{i=0}^{\infty} c_i\, x_{t-i} + \sum_{i=0}^{\infty} d_i\, \epsilon_{t-i}$$

The coefficients $c_0, c_1, c_2, \ldots$ are the **dynamic multipliers** or **lag-weights** (with $c_0 = \phi_0$, $d_0 = 1$).

The **long-run solution** is:

$$y_t = \frac{\delta}{\theta(1)} + \frac{\phi(1)}{\theta(1)}\, x_t = \mu + \beta x_t$$

The **long-run multiplier** is:

$$\frac{\partial E(y_t)}{\partial E(x_t)} = \frac{\phi(1)}{\theta(1)} = \beta = \frac{\phi_0 + \phi_1 + \ldots + \phi_q}{1 - \theta_1 - \theta_2 - \ldots - \theta_p}$$

---

## 4. The Error Correction Model (ECM)

Starting from the ADL model:

$$y_t = \delta + \theta y_{t-1} + \phi_0 x_t + \phi_1 x_{t-1} + \epsilon_t$$

Rearranging yields the **ECM**:

$$\Delta y_t = \delta + \underbrace{(\theta - 1)}_{\gamma_1} y_{t-1} + \phi_0\,\Delta x_t + \underbrace{(\phi_0 + \phi_1)}_{\gamma_2} x_{t-1} + \epsilon_t \tag{*}$$

or alternatively:

$$\Delta y_t = \phi_0\,\Delta x_t - \underbrace{(1-\theta)}_{\text{speed}} \left(y_{t-1} - \underbrace{\frac{\delta}{1-\theta}}_{\mu} - \underbrace{\frac{\phi_0 + \phi_1}{1-\theta}}_{\beta}\, x_{t-1}\right) + \epsilon_t \tag{**}$$

$\Delta y_t$ reacts to deviations from the long-run solution $y_t^* = \mu + \beta x_t$ (the **attractor**):

$$y_t - y_t^* = y_t - \mu - \beta x_t$$

The model **error-corrects** (or **equilibrium-corrects**).

---

## 5. Empirical Example: GDP and Stock Market Returns

**Research question:** Is the stock market helpful in predicting GDP?

**Data:** Quarterly US GDP ($Y$) and Standard & Poor's stock market index ($S$).

For stationarity, use growth rates:

$$\text{Dy}_t = \log(Y_t) - \log(Y_{t-1}), \quad \text{Ds}_t = \log(S_t) - \log(S_{t-1})$$

**Assumed causal direction:** $\text{Ds}_t \rightsquigarrow \text{Dy}_t$

**General ADL model** (starting point):

$$\text{Dy}_t = \delta + \sum_{i=1}^{4} \theta_i\,\text{Dy}_{t-i} + \sum_{i=0}^{4} \phi_i\,\text{Ds}_{t-i} + \epsilon_t$$

potentially augmented with dummy variables for outliers.

### Preferred Simplified Model

Estimation sample: 1951:2–2018:4.

| Variable   | Coefficient  | Std. Error | t-value |
|------------|-------------|------------|---------|
| Dy_1       | 0.195947    | 0.05366    | 3.65    |
| Dy_2       | 0.146804    | 0.05204    | 2.82    |
| Constant   | 0.00380486  | 0.0006438  | 5.91    |
| Ds         | 0.0141974   | 0.005630   | 2.52    |
| Ds_1       | 0.0222467   | 0.005696   | 3.91    |
| Ds_2       | 0.0256934   | 0.005811   | 4.42    |
| I:1952(4)  | 0.0254186   | 0.007089   | 3.59    |
| I:1958(1)  | −0.0260818  | 0.007171   | −3.64   |
| I:1978(2)  | 0.0343161   | 0.007104   | 4.83    |
| I:1980(2)  | −0.0256373  | 0.007111   | −3.61   |

### Misspecification Tests

| Test           | Statistic               | p-value   |
|----------------|-------------------------|-----------|
| AR 1–5         | F(5, 256) = 0.72688     | [0.6038]  |
| ARCH 1–4       | F(4, 263) = 3.2441      | [0.0128]* |
| Normality      | Chi²(2) = 0.55136       | [0.7591]  |
| Hetero         | F(10, 256) = 0.85798    | [0.5733]  |
| Hetero-X       | F(20, 246) = 0.67201    | [0.8521]  |
| RESET23        | F(2, 259) = 0.29218     | [0.7469]  |

The model appears to be reasonably well specified.

### Long-Run Solution

| Parameter      | Coefficient | Std. Error | t-value |
|----------------|-------------|------------|---------|
| Constant       | 0.00578907  | 0.0007219  | 8.02    |
| Ds             | 0.0945418   | 0.01597    | 5.92    |
| Long-run sigma | 0.0107385   |            |         |

where:

$$\mu = \frac{\delta}{1 - \theta_1 - \theta_2} = \frac{0.00380486}{1 - 0.195947 - 0.146804} = 0.005786$$

$$\beta = \frac{\phi_0 + \phi_1 + \phi_2}{1 - \theta_1 - \theta_2} = \frac{0.0141974 + 0.0222467 + 0.0256934}{1 - 0.195947 - 0.146804} = 0.09454$$

Standard errors are computed via the $\Delta$-method (functions of the covariance matrix).

### Lag Structure

| Variable  | Lag 0  | Lag 1  | Lag 2  | Sum    | SE(Sum)  |
|-----------|--------|--------|--------|--------|----------|
| Dy        | −1     | 0.196  | 0.147  | −0.657 | 0.0609   |
| Constant  | 0.0038 | 0      | 0      | 0.0038 | 0.000644 |
| Ds        | 0.0142 | 0.0222 | 0.0257 | 0.0621 | 0.00954  |

### Speed of Adjustment

$$(1 - \theta_1 - \theta_2) = 1 - 0.196 - 0.147 = 0.657$$

About **66% of any deviation from equilibrium is removed each period**. The profile of dynamic adjustment is described by the dynamic multipliers / lag-weights.
