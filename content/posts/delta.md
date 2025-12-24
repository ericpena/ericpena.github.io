+++
title = "Estimators and the Delta Method"
tags = ["statistics", "estimation", "asymptotics"]
date = "2025-01-05"
description = "A pedagogical introduction to estimators and the Delta Method, focusing on intuition, derivation via Taylor series, practical examples, and connections to test-set variance and modern statistical practice."
draft = false
+++

## Why Estimators Deserve Your Attention

In statistics and machine learning, we almost never observe the quantity we truly care about.  
Instead, we **estimate** it.

Whether it’s a population mean, a regression coefficient, a risk metric, or a model performance score, the object of interest is typically an unknown parameter $\theta$. An **estimator** is a rule—usually a function of data—that produces an approximation of this unknown quantity.

{{< info-purple >}}
Understanding *how estimators behave*—especially their variability—is just as important as computing their point values.
{{< /info-purple >}}

This article focuses on one of the most powerful tools for studying estimators:

> **The Delta Method**

It allows us to approximate the variance (and distribution) of *functions* of estimators, using little more than calculus and asymptotics.

---

## Estimators: A Quick Refresher

Let $X_1, \dots, X_n \sim P_\theta$ be i.i.d. data from a distribution indexed by an unknown parameter $\theta$.

An **estimator** is a function
$\hat{\theta}_n = g(X_1, \dots, X_n)$
designed to approximate $\theta$.

Common properties we care about:
- **Consistency**: $\hat{\theta}_n \to \theta$
- **Bias**: $\mathbb{E}[\hat{\theta}_n] - \theta$
- **Variance**: $\mathrm{Var}(\hat{\theta}_n)$
- **Asymptotic distribution**: how $\hat{\theta}_n$ behaves as $n \to \infty$

Many classical estimators satisfy

$$
\sqrt{n}(\hat{\theta}_n - \theta)
\xrightarrow{d}
\mathcal{N}(0, \sigma^2)
$$

But what happens if we care about **a function of $\theta$**?

---

## The Core Problem the Delta Method Solves

Suppose:
- $\hat{\theta}_n$ estimates $\theta$
- You care about $h(\theta)$ for some smooth function $h$

Examples:
- $\theta = \sigma^2$, but you want $\sigma$
- $\theta = p$, but you want $\log(p / (1-p))$
- $\theta$ is a vector, but you want a nonlinear risk or performance metric

You compute:
$h(\hat{\theta}_n)$

**Question:**  
What is the variance (or distribution) of this transformed estimator?

---

## Intuition: Everything Is a Taylor Expansion

The Delta Method is nothing more than a **first-order Taylor approximation**.

Expand $h(\hat{\theta}_n)$ around the true value $\theta$:
$$
h(\hat{\theta}_n)
\approx
h(\theta) + h'(\theta)(\hat{\theta}_n - \theta)
$$

Subtract $h(\theta)$ and rescale:
$$
\sqrt{n}\left(h(\hat{\theta}_n) - h(\theta)\right)
\approx
h'(\theta)\sqrt{n}(\hat{\theta}_n - \theta)
$$

If
$$
\sqrt{n}(\hat{\theta}_n - \theta)
\xrightarrow{d}
\mathcal{N}(0, \sigma^2),
$$

then
$$
\sqrt{n}\left(h(\hat{\theta}_n) - h(\theta)\right)
\xrightarrow{d}
\mathcal{N}\left(0, [h'(\theta)]^2 \sigma^2\right)
$$

{{< info-purple >}}
The Delta Method says: *propagate uncertainty through a nonlinear function using its derivative.*
{{< /info-purple >}}

---

## The Delta Method (Formal Statement)

Let:
- $\hat{\theta}_n \xrightarrow{p} \theta$
- $\sqrt{n}(\hat{\theta}_n - \theta) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$
- $h$ is differentiable at $\theta$

Then:
$$
\sqrt{n}\big(h(\hat{\theta}_n) - h(\theta)\big)
\xrightarrow{d}
\mathcal{N}\left(0, [h'(\theta)]^2 \sigma^2\right)
$$

Equivalently:
$$
\mathrm{Var}\big(h(\hat{\theta}_n)\big)
\approx
\frac{[h'(\theta)]^2 \sigma^2}{n}
$$

---

## Example 1: Estimating the Standard Deviation

Suppose:

$$
\hat{\sigma}^2 \approx \mathcal{N}\left(\sigma^2, \frac{2\sigma^4}{n}\right)
$$

You want $\hat{\sigma} = \sqrt{\hat{\sigma}^2}$.

Define:

$$
h(x) = \sqrt{x}, \quad h'(x) = \frac{1}{2\sqrt{x}}
$$

Apply the Delta Method:

$$
\mathrm{Var}(\hat{\sigma})
\approx
\left(\frac{1}{2\sigma}\right)^2 \cdot \frac{2\sigma^4}{n}
=\frac{\sigma^2}{2n}
$$

Even though $\hat{\sigma}$ is nonlinear, its uncertainty is tractable.

---

## Example 2: Log-Odds Transformation

Let $\hat{p}$ estimate a Bernoulli probability:

$$
\sqrt{n}(\hat{p} - p) \xrightarrow{d} \mathcal{N}(0, p(1-p))
$$

Define:

$$
h(p) = \log\!\left(\frac{p}{1-p}\right)
\quad\Rightarrow\quad
h'(p) = \frac{1}{p(1-p)}
$$

Then:

$$
\mathrm{Var}(h(\hat{p}))
\approx
\frac{1}{n\,p(1-p)}
$$

This underlies logistic regression inference and confidence intervals.

---

## Multivariate Delta Method (Briefly)

If $\hat{\theta} \in \mathbb{R}^k$ and

$$
\sqrt{n}(\hat{\theta} - \theta)
\xrightarrow{d}
\mathcal{N}(0, \Sigma),
$$

and $h:\mathbb{R}^k \to \mathbb{R}$,

then:

$$
\mathrm{Var}(h(\hat{\theta}))
\approx
\frac{1}{n}
\nabla h(\theta)^\top
\Sigma
\nabla h(\theta)
$$

This is essential for:
- Risk metrics
- Composite performance scores
- Safety or reliability functions
- Post-model transformations

---

## Connection to Test-Set Variance

Many evaluation metrics are **functions of sample averages**:
- Accuracy
- Error rates
- Mean loss
- Calibration metrics

Example:

$$
\hat{R} = \frac{1}{n}\sum_{i=1}^n \ell(Y_i, \hat{f}(X_i))
$$

Often we then apply:
- Logs
- Ratios
- Square roots
- Normalizations

{{< info-purple >}}
The Delta Method explains why test-set uncertainty scales like $1/n$ and how nonlinear metrics amplify or dampen noise.
{{< /info-purple >}}

This is especially important when:
- Comparing models
- Setting thresholds
- Reporting confidence intervals
- Making deployment decisions

---

## When the Delta Method Works (and When It Doesn’t)

**Works well when:**
- $n$ is large
- $h$ is smooth
- The estimator is asymptotically normal

**Be careful when:**
- $h'(\theta) = 0$
- The estimator is biased or unstable
- The distribution is heavy-tailed
- You are near boundaries (e.g. $p \approx 0$ or $1$)

In those cases:
- Higher-order Delta Methods
- Bootstrap
- Subsampling  
may be more appropriate.

---

## Why This Matters

The Delta Method is the bridge between:
- Estimation and inference
- Calculus and probability
- Raw metrics and decision-making

It teaches a deep lesson:

> **Uncertainty propagates through models exactly the way sensitivity does.**

Once you see that, you start to think differently about estimators, metrics, and confidence.

---

## Key Takeaways

- Estimators are random variables, not just numbers
- The Delta Method approximates the variance of transformed estimators
- It is derived from a first-order Taylor expansion
- It underpins confidence intervals for nonlinear quantities
- It explains variance in test-set metrics and derived scores

If you understand the Delta Method, you understand how *uncertainty flows* through your entire modeling pipeline.