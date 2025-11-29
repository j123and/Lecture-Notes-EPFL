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
One of the most common uses for the likelihood function is to obtain an estimator for a parameter with maximum likelihood under the data. This is with the help of the log-likelihood done in the following way:


