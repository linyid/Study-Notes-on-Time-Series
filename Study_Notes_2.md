# Study Notes of Time Series

## Part 2: Some Linear Time Series models

### 2.1  $~$ Stochastic Processes and Their Property

**Stochastic Process** can be described as ‘a statistical phenomenon that evolves in time according to probabilistic laws’. a.k.a 'random process'.

Examples:

- length of a queue
- the number of accidents in a particular town in successive months
- the air temperature at a particular site on successive days

Mathematically, **Stochastic Process** is a collection of random variable that are ordered in time and defined at a set of time points, which may be continuous or discrete.

- denote $X(t)$ at time t if continuous ($-\infty <t < \infty$)
- denote $X_t$ at time t if discrete ($t = 0, \pm 1, \pm 2, .. $)

**IMPORTANT property of time series:** At most one observation at a given time.

This is not usually the case of all stochastic processces.

- **Ensemble:** the infinite set of time series that might have been observed.

- **Realization:** every member of the ensemble.

- The observed time series can be thought as one particular realization (and the **only** one that we will ever observe).

- Denote $x(t)$ if continuous, $x_t$ if descrete.

A useful way of describing a stochastic process is to give the *moments* of a process, particularly the first and second moments are called **mean** and **autocovariance funcition** (acv. f.)

These definition is analagous to the discrete case:

***Mean.***  $~~~$ The mean function $\mu(t)$ is defined for all $t$ by
$$ \mu(t) = E[X(t)]$$

***Variance.*** $~~~$ The variance function $\sigma^2(x)$ is defined for all $t$ by
$$\sigma^2(x) = Var[X(t)] = E[(X(t) - \mu(t))^2]$$

***Autocovariance.*** $~~~$ The acv.f. $\gamma(t_1, t_2)$ is the covariance of $X(t_1)$ with $X(t_2)$, i.e.

$$\gamma(t_1, t_2) = E\{ [X(t_1) - \mu(t_1)][X(t_2) - \mu(t_2)] \}$$

Note: Variance function is a special case of acv.f. when $t_1 = t_2$

### 2.2 $~$ Stationary Processes

***Definition.*** $~$ A time series is said to be **strictly stationary** if the joint distribution of $X(t_1), ..., X(t_k)$ is the same as the joint distribution of $X(t_1 + \tau), ..., X(t_k + \tau)$ for all $t_1, ..., t_k, \tau$

Notes:
- Shifting the time origin by an amount $\tau$ has no effect on the joint distributions, which must therefore depend only on the interval $t_1, t_2, .., t_k$.

- If $k=1$, the definition implies that the distribution of $X(t)$ is the same for all $t$. Provided the first two moments are finite, we have
$$ \mu(t) = \mu \\
\sigma^2(t) = \sigma^2$$

  are both constants

- If $k=2$, the joint distribution of $X(t_1)$ and $X(t_2)$ depends only on $t_2 - t_1 = \tau$, which is calledd the **lag**. Then $\gamma(t_1, t_2)$ can be written as $\gamma(\tau)$, and
$$ \begin{aligned} \gamma(\tau) &= E\{ [X(t) - \mu][X(t+\tau) - \mu] \} \\
                                &= Cov[X(t), X(t+\tau)] \end{aligned}$$

  is called the acv coefficient at lag $\tau$

***Definition.*** $~$ **Autocorrelation function** (ac.f.) is defined by

$$ \rho(\tau) = \gamma(\tau) / \gamma(0)$$

Note:
- The size of an $\gamma$ depends on the units in which $X(t)$ is measured. Thus ac.f. is helpful to standardize the acv.f.
- This quantity measures the correlation between $X(t)$ and $X(t+\tau)$.

***Definition.*** $~$ A process is **second-order stationary** (or **weakly stationary**) if its mean is constant and its acv.f. depends only the lag, so that
$$ E[X(t)] = \mu $$

and $$ Cov[X(t), X(t+\tau)] = \gamma(\tau) $$

Notes:

- By letting $\tau=0$, we note that the form of a stationary acv.f. implies that the variance, as well as the mean, is consant.
- The definition implies that both the variance and the mean must be finite.

The weaker definition of stationary will be used from now on.

### 2.3 $~$  Properties of the Autocorrelation Function

Suppose a stationary stochastic process $X(t)$ has mean $\mu$, variance $\sigma^2$, acv.f. $\gamma(\tau)$ and ac.f. $\rho(\tau)$. Then

$$ \rho(\tau) = \gamma(\tau) / \gamma(0) = \gamma(\tau) / \sigma^2$$

Note that $\rho(0) = 1$.

***Property 1:*** $~$ The ac.f. is an even function of the lag, so that $\rho(\tau) = \rho(-\tau)$.

*Proof.* $~$ $$ \begin{aligned}
\gamma(\tau) &= Cov[X(t), X(t+\tau)] \\
&= Cov[X(t - \tau), X(t) \ \ \ \ \ \ \text{Since $X(t)$ is stationary.} \\
&= \gamma(-\tau)
\end{aligned} $$

Notes:
- This property simply says that the correlation between $X(t)$ and $X(t+\tau)$ is the same as that between $X(t-\tau)$ and $X(t)$.

***Property 2:*** $~$ $| \rho(\tau) | \leq 1$

Notes:
- This indicates that the correlatiion coefficient is standardized acv.f., and the value of $\rho(\tau)$ does not depend on the units in which the time series is measured.

***Property 3:*** $~$ The ac.f. does not uniquely identify the underlying model.

Notes:
- We know that a given stochastic process has a unique covariance structure, but the converse is not in general true.
- We will see that, a requirement called the invertibility condition is needed to ensure uniquess in both directions.
