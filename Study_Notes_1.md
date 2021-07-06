# Study Notes of Time Series

## Part 1: Basic Descriptive Techniques

### 1.1 $~$ Types of Variations

*Seasonal Variations*

- annual in period

- e.g. sales figure, temperature reading

- can readily be estimated if directly interested

- can be removed from the data if not directly interested

*Other Cyclic Variations*

- variatons at fixed period $~~~$ e.g. daily temperature

- variation not at fixed period, but still predictable $~~~$ e.g. business cycles of 3 to 4 years or more than 10 years

*Trend*

- 'long term change in the mean level'

- need to take into account the number of observation available and make a subjective assessment of what 'long term'  means

- e.g. climate variables: data of 50 years we may see a cyclic variation; while data of 20 years we may only see a trend

*Other irregular fluctuation (Residual)*

- after trends and cyclic variations are removed from the data, we will observe the residual that may or may not be 'random'

- need to analyze if there is any cyclic variation left to be extract, or

- any irregular variations may be explained in terms of probablity models, such as moving average (MA) or autoregressive (AR)

### 1.2 $~$ Stationary Time Series

**Stationary:** A time series is stationary if there is no systematic change in mean (no trend, if there is no systematic change in variance and if stricly periodic variations has been removed.

- Many theories are concerned with stationary time series. So **transform** to statsionary if neccessary.

### 1.3 $~$ Transformations

####*1. To stablize the variance*

Suggested if: (1) there is a trend; (2) variance is increasing with the mean

- If the standard deviation is directly proportional to the mean, **a logarithm transform is indicated**.

- If the variance changes through time without a trend being present, then a transformation will not help. In such cases, a model that allows for changing variance should be considered.

####*2. To make the seasonal effect additive*

Suggested if: (1) there is a trend; (2) seasonal effect is increasing with mean

- if so, suggested to make the seasonal effect constant from year to year. This is refer to as **additive seasonal effect**.

- **Multiplicative seasonal effect** if directly proportional to the mean.

- A **logarithm transformation** is suggested to make it additive

- However, this transform will only stablize the variance if error term is also thought to be multiplicative (see later)

####*3. To make the data normally distributed*

- Model building and forecasting are usually carried out on the assumption
that the data are normally distributed.

- Difficult. Necessary to model the data using a different 'error' distribution

**BOX-COX transformation**:

logarithm and square-root are special cases of BOX-COX. Given a time series $\{x_t\}$ and a transformation parameter $\lambda$, the transformed series is given by:

\[
   y_t= \begin{cases}
        (x_t^\lambda-1)/\lambda, & \text{if}\ \lambda \neq 0\\
        log \ x_t, & \text{if}\ \lambda = 0 \end{cases}
\]

**Problems in practice:**

1. Experiments found little in improvement with BOX-COX transformation

2. Cannot achieve all of the above requirements

3. Hard to 'transform back'

### 1.4 $~$ Analyzing Series WITH Trend and NO Seasonal Variations

Simplest type of trend, 'linear model + noise': an observaton at time $t$ is a random variable $X_t$

\[
X_t = \alpha + \beta \ t + \epsilon \tag{1.1}
\]

- (1.1) is a deterministic function of time and is sometimes called **global** linear trend, and is generally not practical.

- More emphasis on models that is **locally** linear. One possibility is to fit a **piecewise linear** model.

- To solve the unsmoothing points in pieceise linear model, we could assume that $\alpha$ and $\beta$ evolve stochastically, leading to a **Stochastic Trend**.

**General Approaches:**

#### *1.4.1 $~$ Curve fitting*

-  ** for future updates **

#### *1.4.2 $~$ Filtering*

**Moving Average**

Basic Formula:

\[
y_t = \sum^{+s}_{r = -q} a_r x_{t+r} \\
s.t.  \sum a_r = 1
\]

- Simplest example: $Sm(x) = \frac{1}{2q+1}\sum_{r = -q}^{q} x_{t+r} $. Help to removing seasonal variation.
- **Symmetric coefficient**: $(\frac{1}{2} + \frac{1}{2})^{2q}$. When q gets large, approximates to normal curve.

- **Spenser's 15-point** moving average: used for mortality stats

- **Henderson** moving average: cubic polynomial trend without distortion.

**end-effects problem**: happens when symmetric filter is chosen. $Sm(x)$ can only calculate from $ t=q+1$ to $t = N-q$. In forecasting, it is particularly important to calculate smooth values up to $t=N$.

- **Exponential Smoothing**:
$$Sm(x) = \sum^\infty_{j=0} \alpha(1-\alpha)^j \  x_{t-j} $$

  where $0 < \alpha < 1$. Note that $\alpha(1-\alpha)^j$ decreases geometrically with j.

Once we have extimated the trend, we calculate the residual:

\[ \begin{aligned}
  Res(x_t) &= \text{residual from smmothed value} \\
   &= x_t - Sm(x_t) \\
  &= \sum^{s}_{r=-q} b_r \ x_{t+r}
\end{aligned}\]

- This is also a linear filter with $b_0 = 1 - a_0$ and $b_r = -a_r$ for $r\neq0$.
- If $\sum a_r = 1$ then $\sum b_r = 0$