+++
title = "Connecting Distributions"
tags = ["statistics"]
date = "2025-12-21"
description = "This short note builds intuition for how several core distributions—Poisson, Exponential, Gamma, Beta, Binomial, Chi Square, Dirichlet, Multinomial—are tightly connected. Rather than treating them as isolated formulas, we view them as different lenses on the same random process: events happening in time or within the same family."
+++

## A guided tour of a tightly connected family

This article builds both a **high-level conceptual map** and a **low-level algebraic understanding** of how the following distributions are not isolated objects, but different faces of a small number of underlying stochastic mechanisms:

- Poisson (counts in time or space)
- Exponential (inter-arrival times)
- Gamma (waiting time for multiple events; conjugate to Poisson)
- Chi-squared (special case of Gamma)
- Beta (normalized ratio of Gammas; probability on \([0,1]\))
- Beta-prime and F (ratios and scaled ratios of Gammas)
- Binomial (fixed-\(n\) Bernoulli trials)
- Multinomial (categorical counts)
- Dirichlet (multivariate generalization of Beta)

The unifying idea is simple but powerful:

{{< info-purple >}}
**Events happen. We either count them, wait for them, sum their waiting times, or normalize competing rates.**
{{< /info-purple >}}

Once this is internalized, most distributional relationships stop feeling arbitrary. Instead of memorizing PDFs and CDFs, we learn a small set of **transforms, sums, ratios, and conjugacy rules** that generate almost everything we see in applied statistics.

{{< info-purple >}}
**Big picture map**

- **Poisson ↔ Exponential ↔ Gamma** form a time–count–sum triad.
- **Beta and Dirichlet** arise by *normalizing independent Gammas*.
- **Binomial and Multinomial** are discrete count analogs and are conjugate to **Beta and Dirichlet**.
- **Chi-square, F, Beta-prime** are reparameterizations or ratios of Gammas.
- Many hypothesis tests ultimately reduce to **Gamma algebra + Beta CDFs**.
{{< /info-purple >}}

---

## 1 — From events to counts to times

Start with the most primitive object:  
**events occur randomly in time at a constant average rate \(\lambda\)**.

This assumption alone already implies a remarkable amount of structure.

### Poisson: counting events in a window

Let \(K(t)\) be the number of events observed in a time window of length \(t\). Then

$$
K(t) \sim \mathrm{Poisson}(\lambda t), \qquad 
\mathbb{P}(K = k) = \frac{(\lambda t)^k e^{-\lambda t}}{k!}.
$$

Interpretation:
- The Poisson distribution answers **“how many?”**
- The parameter \(\lambda t\) is *expected count = rate × exposure*.
- Independence and stationarity are baked in: counts in disjoint intervals are independent.

This is the natural model for:
- crashes per mile
- failures per hour
- arrivals per minute
- defects per batch

---

### Exponential: waiting for the next event

Instead of asking *how many events occur*, ask:

{{< info-purple >}}
**How long until the next one happens?**
{{< /info-purple >}}

Let \(T\) be the waiting time to the next event. Then

$$
T \sim \mathrm{Exponential}(\lambda), \qquad 
f_T(t) = \lambda e^{-\lambda t}, \quad t > 0.
$$

Key intuition:
- The Exponential distribution answers **“how long do I wait?”**
- It is **memoryless**:
  $$
  \mathbb{P}(T > s+t \mid T > s) = \mathbb{P}(T > t)
  $$
- Memorylessness uniquely characterizes the exponential distribution.

This property is why Exponentials dominate:
- survival analysis
- reliability theory
- queueing systems
- hazard-rate reasoning

---

### Gamma: waiting for multiple events

Now ask a slightly richer question:

{{< info-purple >}}
**How long until the \(k\)-th event occurs?**
{{< /info-purple >}}

Let \(T_1, \dots, T_k\) be iid Exponential(\(\lambda\)) waiting times. Their sum

$$
S_k = \sum_{i=1}^k T_i
$$

has a Gamma distribution:

$$
S_k \sim \mathrm{Gamma}(k, \lambda)
$$

with density (shape–rate parameterization)

$$
f(x;\alpha,\beta)
= \frac{\beta^{\alpha}}{\Gamma(\alpha)} x^{\alpha-1} e^{-\beta x}, \quad x>0.
$$

Interpretation:
- **Exponential**: waiting for *one* event
- **Gamma**: waiting for *many* events
- **Poisson**: counting how many events fit into a time window

These are not three different stories — they are three views of the *same process*.

**Mental model to keep:**

- Poisson counts events
- Exponential times a single event
- Gamma times multiple events

---

## 2 — Gamma, Chi-squared, and F: special cases and ratios

### Chi-squared is just a Gamma

The Chi-squared distribution is not new; it is a Gamma in disguise.

If

$$
Z \sim \chi^2_{\nu}
$$

then

$$
Z \sim \mathrm{Gamma}\left(\frac{\nu}{2}, \frac{1}{2}\right)
$$

(shape, rate).

This explains why Chi-squared appears everywhere in:
- variance estimation
- likelihood ratio tests
- goodness-of-fit tests

All of these are ultimately about **sums of squared Gaussian noise**, which collapses into Gamma structure.

---

### Ratios of Gammas → Beta-prime and Beta

Let

$$
X \sim \mathrm{Gamma}(a, 1), \quad 
Y \sim \mathrm{Gamma}(b, 1),
$$

independent.

#### Ratio: Beta-prime

The ratio

$$
R = \frac{X}{Y}
$$

has a **Beta-prime** distribution:

$$
f_R(r) = \frac{r^{a-1}}{B(a,b)} (1+r)^{-a-b}, \quad r>0.
$$

This appears naturally when comparing **rates or intensities**.

---

#### Normalized ratio: Beta

Now normalize instead:

$$
U = \frac{X}{X+Y} \in (0,1).
$$

Then

$$
U \sim \mathrm{Beta}(a,b)
$$

with density

$$
f(u) = \frac{1}{B(a,b)} u^{a-1} (1-u)^{b-1}.
$$

This single transformation explains why Beta distributions dominate probability modeling.

---

### F distribution as scaled Gamma ratios

If

$$
X \sim \chi^2_{d_1}, \quad 
Y \sim \chi^2_{d_2},
$$

then

$$
F = \frac{(X/d_1)}{(Y/d_2)} \sim F_{d_1,d_2}.
$$

Under the hood:
- \(X\) and \(Y\) are Gammas
- Their ratio reduces to a Beta CDF after reparameterization

This is why:
- F CDFs
- t-tests
- likelihood ratio tests

all collapse to **incomplete Beta functions** numerically.

---

## 3 — From Gamma to Beta and Dirichlet: normalization is everything

Let

$$
X_i \sim \mathrm{Gamma}(\alpha_i, \beta), \quad i=1,\dots,K,
$$

independent with the *same rate*.

Define normalized components

$$
p_i = \frac{X_i}{\sum_j X_j}.
$$

Then

$$
(p_1,\dots,p_K) \sim \mathrm{Dir}(\alpha_1,\dots,\alpha_K)
$$

with density

$$
f(\mathbf p) = \frac{1}{B(\boldsymbol\alpha)} 
\prod_{i=1}^K p_i^{\alpha_i-1}.
$$

Interpretation:
- **Gamma**: raw, unnormalized “mass”
- **Dirichlet**: proportions of that mass
- **Beta**: Dirichlet with \(K=2\)

This is one of the most important constructions in Bayesian statistics.

---

## 4 — Binomial / Multinomial and conjugate priors

### Binomial + Beta

Binomial likelihood:

$$
\mathbb{P}(k \mid n,p) = \binom{n}{k} p^k (1-p)^{n-k}.
$$

Beta prior:

$$
p \sim \mathrm{Beta}(a,b).
$$

Posterior:

$$
p \mid k \sim \mathrm{Beta}(a+k, b+n-k).
$$

Interpretation:
- successes add to \(a\)
- failures add to \(b\)
- conjugacy = bookkeeping

---

### Multinomial + Dirichlet

Multinomial likelihood:

$$
\mathbf{k} \sim \mathrm{Multinomial}(n,\mathbf p).
$$

Dirichlet prior:

$$
\mathbf p \sim \mathrm{Dir}(\boldsymbol\alpha).
$$

Posterior:

$$
\mathbf p \mid \mathbf k \sim \mathrm{Dir}(\boldsymbol\alpha + \mathbf k).
$$

Same algebra, higher dimension.

{{< info-purple >}}
**Conjugacy checklist**

- Poisson + Gamma → Gamma
- Binomial + Beta → Beta
- Multinomial + Dirichlet → Dirichlet
{{< /info-purple >}}

---

## 5 — How to move around the web (recipes)

1. **Counts ↔ times**  
   Poisson ⇔ Exponential ⇔ Gamma

2. **Rates → probabilities**  
   Normalize Gammas → Beta / Dirichlet

3. **Comparing rates**  
   Ratio of Gammas → Beta-prime / F

4. **Discrete counts**  
   Binomial / Multinomial with Beta / Dirichlet priors

---

## 6 — Worked mini-example

Observe \(E=5\) events in exposure \(t=2\). Prior:

$$
\lambda \sim \mathrm{Gamma}(\alpha_0,\beta_0).
$$

Posterior:

$$
\lambda \mid E \sim \mathrm{Gamma}(\alpha_0+E,\beta_0+t).
$$

With $(\alpha_0=0.5,\beta_0=0)$:

$$
\lambda \mid E \sim \mathrm{Gamma}(5.5,2),
$$

posterior mean $(= 2.75)$.

Everything here is just **Gamma updating Poisson exposure**.

---

## 7 — What to take away

### High-level
These distributions form a **single connected system**, not a list.

### Low-level moves
- Sum → Gamma
- Normalize → Beta / Dirichlet
- Count + exposure → Poisson / Gamma
- Ratio → Beta-prime / F

{{< info-green >}}
**Implementation notes**

- Always check Gamma parameterization (rate vs scale).
- Use regularized incomplete Beta for numerical stability.
- Prefer log-space for large parameters.
{{< /info-green >}}

---

## Further reading

- Devore, Berk, Carlton — *Modern Mathematical Statistics*
- Gelman et al. — *Bayesian Data Analysis*

This note aims to replace memorization with a map:
**events → times → sums → ratios → proportions → conjugate updates**.