# Concepts

## Stochastic - aiming or guessing  

### Sigma Algebra
A $\sigma$-algebra $\mathcal{F}$ on a set $\Omega$ is a collection of subsets that include the empty set, is closed under complement and closed under union. 

### Measure
A measure assigns a non-negative value to a set, an example of a measure would be the cardinality of a finite set (and infinite if you allow the ascribing of infinite number of elements to infinite sets). It must also hold that the measure of of a countable union of disjoint sets is the sum of the measure on each set (countable additivity). 

### Probability Measure 
This is just a measure that satisfies that measure of the whole space is equal to 1.

### Random Variable
A random variable (RV) is a function with random input. 

### Probability Distribution
The Probability Distribution of an RV is a probability measure on the value space of the variable. It ascribes a value in [0,1] on the outcomes of the RV

### Stochastic Process
A Stochastic Process is a collection of random variables indexed by some set, generally time. 

### Statistic
A statistic is a function or transformation of data such as the sample mean. The Neyman-Fischer factorization theorem says that if we can factor the density function into one function of the statistic, which depends on the parameter and another function which does not depend on the parameter. If $T$ is our statistic, $f$ our density and $g$ and $h$ functions:

$$
f_\theta(x) = g_\theta(T(x))h(x)
$$

### Sufficient statistic
A sufficient statistic is a statistic that tells us as much about the distributions parameter that the data possibly can. A minimal sufficient statistic is a sufficient statistic that cannot be further reduced. One way of seeing this is that for other sufficient statistics the minimal can be obtained by a transformation of them.

For example if we have data drawn from a uniform distribution:

$$
X_i \sim U(0,\theta)
$$
then one sufficient statistic is $2\bar X$ but it is not a minimal sufficient statistic. A minimal sufficient statistic for this sample is the the sample max:

$$
T = max(X_i)
$$

---
## Discrete Markov Chain
A discrete Markov Chain is a stochastic function, i.e there are many possible outputs for a given input, with the property that only the the left closest value to the current value influences the functions value at the current value.  

More precisely:

$P(X_n = t | X_{n-1}, X_{n-2},... , X_{0}) = P(X_n = t | X_{n-1})$

Less precisely, only the previous state influences the current probability and knowing the previous state, knowledge of earlier states than that provide no information for the current probability. 

We say that a chain is positive recurrent if there is a state with finite return time and recurrent if there is a state with definite return:

$P(\sigma_s < \infty)$

$E[\sigma_s]< \infty $

We say that a chain has an invariant probability distribution $\pi$ if $\pi P = \pi$ where $\pi $ is a row vector of probabilities and $P$ is the transition matrix of the chain.

---
## Characteristic function

The characsteristic function $\varphi$ of a random variable $X$ is simply the Fourier transform of the distribution of $X$.

$\quad\quad$ $\varphi_X(t) = E[e^{itX}], \quad t\in \mathbb{R} $

It uniquely determines the distribution of $X$ and satisfy the following property for id variables $X,Y$:

$\quad\quad$ $\varphi_{X+Y}(t) =\varphi_{X}(t)\varphi_{Y}(t) $

We also have: 

$\quad\quad$ $\varphi_{X}(-t) = \overline{\varphi_{X}(t)}$

$\quad\quad$ $\varphi_{X}'(0) = iE[X] $

$\quad\quad$ $\varphi_{X}''(0) = -E[X^2] $


$\quad\quad$ $\varphi_{aX+b}(t) = e^{itb}\varphi_{X}(at) $

Exampe for $X \sim N(\mu, \sigma^2$):

$\quad\quad$ $\varphi_{X}(t) = e^{i\mu t - \frac{1}{2}\sigma^2t^2} $

---

## Likelihood
The likelihood paradigm is to assess how likely data is under a given model with the presumption that a model which estimates the data as more likely is a more fitting model.

The likelihood ratio for models $P$ and $Q$ is given by:

$L(X)  = \frac{P(X)}{Q(X)}$  

And for two hypothezised parameters $\theta_0$ and $\theta_1$ under a function $f$:

$\Lambda(\theta | X) = \frac{f(X;\theta_1)}{f(X;\theta_0)}$

But we often work with the log of the likelihood as often in statistics the log makes things easier to handle in that we can talk about sums where we would otherwise have products. And as the log is a strictly increasing function maximizing and convex arguments apply to it.

If we have iid data $X_i$ with density function $f$ the likelihood function becomes: 

$L(\theta|X) = \displaystyle \prod_{i=1}^{n} f(x_i;\theta) $

And the log likelihood turns this into:

$\ell(\theta|X)= \displaystyle \sum_{i=1}^{n} \log f(x_i;\theta)$


### The MLE
One of the most common uses for the likelihood function is to obtain an estimator for a parameter with maximum likelihood under the data. This is with the help of the log-likelihood by simply derivating and setting the derivative of the log-likelihood to zero and solving for the parameter. The obtained estimator is denoted $\hat\theta_{MLE}$.


## Error estimates
Error, deviation, difference, loss, cost or inaccuracy are ways to denote the discrepancy between what a model predicts and observations of data.

### Mean Squared Error (MSE)
The Mean Squared Error is a modification of the mean error which penalizes larger error and favours smaller error. It's defined as, for target values $y$, input $x_i$ and model $f$:

$$
MSE(f) = \displaystyle \frac{1}{n}\sum_{i=1}^{n}(y_i-f(x_i))^2
$$



## Distributions and transformations

### Parametric family
A parametric family is a group of distributions described by a finite-dimensional parameter with the same support.

### Exponential family
The exponential family is a parametric family of distributions and is the collection of distributions with density function that can be written on the following form:

$$
f(x|\theta) = h(x)e^{\eta(x)^\mathsf{T}T(x)-A(\theta)}
$$
Where $T$ a sufficient statistic $\eta$ a reparametrization of $\theta$ and $A$ is the log-partition function necessary to normalize the distribution. It cannot have support that it dependent on the parameter

Some examples:

* The Poisson distribution, Poisson($\lambda$) with density $f$:
$$
f = \frac{\lambda^xe^{-\lambda}}{x!}, \quad x\in\mathbb{N_0}
$$
$$
= \frac{1}{x!}e^{xlog\lambda-\lambda}
$$
$\quad$ where $h(x)=\frac{1}{x!}, T(x) = x, \eta(\theta) = log(\theta), A(\theta) = \theta$
* The normal distribution $N(\mu,\sigma) $ with density:
$$
\frac{1}{2\pi\sigma^2}e^{-\frac{(x-\mu)^2}{2\sigma^2}}, \quad x\in \mathbb{R}
$$
$$
= e^{-log(\frac{1}{2\pi\sigma^2})-\frac{(x-\mu)^2}{2\sigma^2}}
$$
$$
= e^{-log(\frac{1}{2\pi\sigma^2})-\frac{(x^2- 2\mu x + \mu^2)}{2\sigma^2}}
$$

$\quad$ where: 
$$
\begin{aligned}
    h(x) &= 1,\\
  T_1(x) &= x,\quad T_2(x)=x^2,\\
  \eta_1(\theta) &= \frac{\mu}{\sigma^2},\quad
  \eta_2(\theta) = \frac{1}{2\sigma^2},\\
  A(\theta) &= \frac{\mu^2}{2\sigma^2} + \frac{1}{2}\log(2\pi\sigma^2).
\end{aligned}
$$


## Importance sampling
Importance sampling is a trick for estimation when we want to sample rare events from a distribution that in itself is hard to draw form. Instead of sampling from such a distribution we sample from an easier one and reweigh the samples according to the ratio between the desired and easier distribution.

One algorithm that makes the importance sampling more effective is where we update the proposal distribution according to the weighted samples so which lets us sample even more effectively and help us not get stuck in an ineffective proposal.

## Transformers 

## Kolmogorov Complexity
The kolmogorov complexity of a some unit $x$ is the smallest size of all programs $p$ that can output $x$. It is not computable. Proof by contradiction:

* Consider a program Q that takes input n and computes Kolmogorov complexities $K(s_i)$ of strings $s_i$ and ouputs and halts once its larger than n. This program can is described with a constant size and n can be encoded in log n bits. We then have $n \lt K(s_i) \lt  log(n)+C $. This does not hold for large enough $n$ and our assumption was wrong.

## Simulation of random numbers

### Linear Congruential Generator (LCG)
This is a random number generator where we generate numbers according to the following recurrence formula:

$$
X_{n+1} = aX_n+b \quad(mod \space m)
$$
Where m and b are coprime, $X_0$ is called the seed and determines where we start in the sequence and m is prime. It has period m.

### Inverse Transform Method
The inverse transform method generates uniform samples and puts these through the inverse cdf of the desired RV:

> ***Algorithm Inverse-Transform***:
>
> Generate $U_i = U(0,1)$
>
> Set $X_i = F(U_i)$

### Acceptance-Rejection Method
When we have an unknown distribution f that we are not sure how to sample from, but we have a secondary distribution g such that $cg\geq f$ we can sample from g instead and only accept samples that fall under f.

## Tests of simulated random numbers

### Kolmogorov-Smirnov (KS) test
The Kolmogorov Smirnov test says that the largest absolute difference between the empirical cdf and the theoretical cdf of simulated values should scale like the square root of the number of samples and converge to a Kolmogorov random variable K. The null that the simulated values are from the theoretical distribution is rejected at level $\alpha$ when this difference divided by the square root of the number of samples is greater then the corresponding quantile of K. The quantiles are tabulated.

### Q-Q plot
Here we sort the simulated values and compare them to the theoretical quantiles. 

### $\chi^2$-test
In the $\chi^2$-test we use the statistic 
$
\sum_i \frac{(O_i-E_i)^2}{E_i}
$
where $O_i$ is the number of observations of an event and $E_i$ the theoretical expected value of the number of such observations. We then test this statistic against a $\chi^2_{f-1-p}$ distribution with $f-1-p$ degrees of freedom where $f$ is the number of categories or the size of the sample space  and $p$ is the number of estimated parameters.

### Gap test 
Here we test that the gaps between elements in a sequence of uniform RVs have a geometric distribution.

### Serial test 
The serial test groups a sequence of uniform RVs into vectors of size d and checks if they are now uniform on $[0,1)^d$
