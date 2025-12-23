+++
title = "(Un)biased Point Estimation"
tags = ["statistics"]
date = "2024-11-12"
description = "This article explores how to estimate the maximum parameter $(\\theta)$ of a uniform distribution from sample data, deriving the Maximum Likelihood Estimator (MLE), identifying its bias, and constructing an unbiased estimator by adjusting the MLE"
+++

## Problem Setup

Suppose that $X$ has a uniform distribution on the interval $[0, \theta]$, where $\theta$ is unknown and $X$ could be reaction time to a stimulus or volumes of rocks, for example.[^1]

{{< info-purple >}}
One goal could be to estimate $\theta$. That is, you have a random sample $(X_1, X_2, \ldots, X_n)$ from a uniform distribution on the interval $[0, \theta]$, where $\theta$ is the unknown parameter to be estimated.
{{< /info-purple >}}

### Likelihood Function
The probability density function (PDF) of a single observation $X_i$ from a uniform distribution on $[0, \theta]$:
$$
f(x_i; \theta) = 
\begin{cases} 
\frac{1}{\theta} & \text{if } 0 \leq x_i \leq \theta \\\
0 & \text{otherwise}
\end{cases}
$$
Given that the sample is independent and identically distributed (i.i.d.), the joint likelihood function for the entire sample is the product of the individual PDFs:

$$
L(\theta; X_1, X_2, \ldots, X_n) = \prod_{i=1}^{n} f(x_i; \theta) = \prod_{i=1}^{n} \frac{1}{\theta} \cdot \mathbf{1}_{\{0 \leq x_i \leq \theta\}}
$$

Here, $\mathbf{1}_{\{0 \leq x_i \leq \theta\}}$ is an indicator function that equals 1 if $(0 \leq x_i \leq \theta)$ for all $i$, and 0 otherwise. This simplifies to:

$$
L(\theta; X_1, X_2, \ldots, X_n) = \frac{1}{\theta^n} \cdot \mathbf{1}_{\{\max(X_i) \leq \theta\}}
$$

where $\max(X_1, X_2, \ldots, X_n)$ is the maximum of the observed sample values.

### Finding the Maximum Likelihood Estimator (MLE)
The MLE of $\theta$ is the value of $\theta$ that maximizes the likelihood function.

$$
L(\theta; X_1, X_2, \ldots, X_n) = 
\begin{cases} 
\frac{1}{\theta^n} & \text{if } \theta \geq \max(X_i) \\\
0 & \text{if } \theta < \max(X_i)
\end{cases}
$$

To maximize $L(\theta)$, we want the smallest possible value of $\theta$ that still satisfies the condition $\theta \geq \max(X_1, X_2, \ldots, X_n)$. Notice that since $L(\theta) = \frac{1}{\theta^n}$, $L(\theta)$ decreases as $\theta$ increases. The smallest possible $\theta$ (which maximizes the likelihood and where $L(\theta) > 0$) is $\theta = \max(X_1, X_2, \ldots, X_n)$.

{{< info-blue >}}
Thus, the MLE for $\theta$ is:
$$
\hat{\theta} = \max(X_1, X_2, \ldots, X_n)
$$
{{< /info-blue >}}

### Biased Solution

For example, given a random sample of $n$ reaction times, $(X_1, X_2, \ldots, X_n)$, consider the estimator: $\hat\theta = \max(X_1, X_2, \ldots, X_n)$. This might seem like a reasonable choice but consider that this estimator will never overestimate $\theta$ since the largest value in the sample can never exceed the maximum of the distribution from which it came (i.e., $\theta$). Generally, in order for the estimator to be "unbiased", some samples wil yield estimates that exceed $\theta$ and other samples will yield estimates smaller than $\theta$. Estimates that evenly hover around the true value is what we might expect from an unbiased estimator. A principal in statistics to keep in mind is the *Principal of Unbiased Estimation*.

{{< info-blue >}}
<b>Principal of Unbiased Estimation</b><br>When choosing among several different estimators of $\theta$, select one that is unbiased.
{{< /info-blue >}}

### Calculating Bias and Finding Unbiased Estimator

We already have evidence to claim that the MLE estimate $\left(\hat{\theta} = \max(X_1, X_2, \ldots, X_n)\right)$ is biased. Now we could ask how biased it is and whether there is hope in making the estimator unbiased. Put more formally, a point estimator $\hat\theta$ is said to be an unbiased estimator of $\theta$ is $\mathbb{E}[\hat\theta] = \theta$. Furthermore, the bias is the difference: $\mathbb{E}[\hat\theta] - \theta$. Of course, in order to find these expressions, we need to calculate the expected value of the estimor $\left(\hat{\theta} = \max(X_1, X_2, \ldots, X_n)\right)$. In order to do that, we first need to go through steps of calculating CDF and PDF of the MLE estimator.

---

{{< centerb >}}
Step 1: CDF of the Maximum
{{< /centerb >}}

Let $Y = \hat{\theta} = \max(X_1, X_2, \ldots, X_n)$.

The cumulative distribution function (CDF) of $ Y $ is:
$$P(Y \leq y) = P(\max(X_1, X_2, \ldots, X_n) \leq y)$$
Since the $X_i$ are independent and uniformly distributed on $[0, \theta]$:
$$
P(Y \leq y) = P(X_1 \leq y) \cdot P(X_2 \leq y) \cdots P(X_n \leq y) = \left(\frac{y}{\theta}\right)^n
$$
for $ 0 \leq y \leq \theta $.

Thus, the CDF of $ Y $ is:
$$
F_Y(y) = \left(\frac{y}{\theta}\right)^n
$$
for $ 0 \leq y \leq \theta $.

---

{{< centerb >}}
Step 2: PDF of the Maximum
{{< /centerb >}}

The probability density function (PDF) of $ Y $ can be found by differentiating the CDF:
$$
f_Y(y) = \frac{d}{dy} F_Y(y) = \frac{d}{dy} \left(\frac{y}{\theta}\right)^n = \frac{n}{\theta} \left(\frac{y}{\theta}\right)^{n-1}
$$
for $ 0 \leq y \leq \theta $.

---

{{< centerb >}}
Step 3: Expectation of $Y$
{{< /centerb >}}

The expected value of $ Y $ is:
$$
\mathbb{E}[Y] = \int_0^{\theta} y \cdot f_Y(y) \, dy = \int_0^{\theta} y \cdot \frac{n}{\theta} \left(\frac{y}{\theta}\right)^{n-1} dy
$$

This simplifies to:
$$
\mathbb{E}[Y] = \frac{n}{\theta^n} \int_0^{\theta} y^n \, dy
$$
We can compute the integral:
$$
\int_0^{\theta} y^n \, dy = \frac{y^{n+1}}{n+1} \Big|_0^{\theta} = \frac{\theta^{n+1}}{n+1}
$$
Thus:
$$
\mathbb{E}[Y] = \frac{n}{\theta^n} \cdot \frac{\theta^{n+1}}{n+1} = \frac{n \theta}{n+1}
$$

{{< info-blue >}}
So, the expected value of $\hat{\theta}$ is:
$$
\mathbb{E}[\hat{\theta}] = \frac{n}{n+1} \cdot \theta
$$
{{< /info-blue >}}

---

### Conclusion
The expectation result above reveals that $\frac{n}{n+1} < 1$. This means that $\mathbb{E}[\hat{\theta}]$ is slightly less than $\theta$. This result indicates that the MLE, $\left(\hat{\theta} = \max(X_1, X_2, \ldots, X_n)\right)$, is a biased estimator for $\theta$, with the bias shrinking as the sample size $n$ gets large. The final task is to calculate the bias of the MLE estimator and find the unbiased estimator:

{{< info-green >}}
$$
\begin{align}
\text{bias} &= \mathbb{E}[\hat\theta] - \theta \\\
&= \frac{n}{n+1} \cdot \theta - \theta \\\
&= -\frac{\theta}{n+1}
\end{align}
$$
{{< /info-green >}}

$$
\text{since: } \mathbb{E}\left[ \frac{n+1}{n} \cdot \max(X_1, X_2, \ldots, X_n) \right] = \frac{n+1}{n} \cdot \mathbb{E}\left[\max(X_1, X_2, \ldots, X_n) \right] = \frac{n+1}{n} \cdot \frac{n}{n+1} \cdot \theta = \theta
$$

{{< info-green >}}

$$
\text{(unbiased estimator)}\ \ \ \ \hat{\theta}_u = \frac{n + 1}{n} \cdot \max(X_1, X_2, \ldots, X_n)
$$
{{< /info-green >}}

This new estimator, $\hat{\theta}_u$, will overestimate and underestimate $\theta$ depending on the sample but will do so in an unbiased way.

## references
[^1]: Devore, Jay L., Kenneth N. Berk, and Matthew A. Carlton. Modern mathematical statistics with applications. Vol. 285. New York: Springer, 2012. 