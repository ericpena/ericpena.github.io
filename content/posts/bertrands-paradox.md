+++
title = "Bertrand's Paradox"
tags = ["statistics", "estimation", "asymptotics"]
date = "2025-01-05"
description = "What’s the probability that a random chord in a circle is longer than the side of an inscribed triangle? Surprisingly, the answer is 1/4… or 1/3… or 1/2. All are correct. Bertrand’s Paradox reveals why “random” is not a mathematical concept until you define the underlying probability measure — and why hidden modeling assumptions shape every simulation you run."
draft = false
+++

---

# Bertrand’s Paradox: When “Random” Isn’t a Real Answer

In 1889, the French mathematician **Joseph Bertrand** posed what looked like a harmless geometry question:

{{< info-blue >}}
Pick a chord at random in a circle.  
What is the probability that it is longer than the side of the equilateral triangle inscribed in the circle?
{{< /info-blue >}}

It sounds clean. Precise. Mathematical. But there is no single correct answer. Depending on how you interpret “at random,” the probability is: $\frac{1}{4}$, $\frac{1}{3}$, or $\frac{1}{2}$. And all three answers can be derived rigorously.

---

## Who Was Bertrand?

{{< info-blue >}}
Joseph Bertrand (1822–1900) was a French mathematician known for his work in probability, number theory, and thermodynamics. He was deeply interested in the foundations of probability — especially in how symmetry and “uniform randomness” are often invoked without careful definition. Bertrand’s chord problem was not just a puzzle. It was a critique. He was exposing a subtle flaw in the way people casually use the word “random.”

{{< /info-blue >}}

---

## What Is the Problem Exactly?


{{< info-green >}}
1. Draw a circle.
2. Inscribe an equilateral triangle inside it.
3. Select a chord “at random.”
4. Ask:

$$
P(\text{chord length} > \text{triangle side}) = \text{ ?}
$$

At first glance, symmetry suggests there *must* be a single answer. But the phrase “random chord” does not uniquely define a probability distribution over all possible chords. **And that is the heart of the paradox.**

{{< /info-green >}}

---

## Why This Matters

Bertrand’s paradox reveals something interesting: Probability does not live in geometry alone. It lives in:

$$
(\text{sample space}) + (\text{a probability measure})
$$

If you do not specify the measure — how chords are generated — the problem is incomplete. Different generation methods impose different probability distributions. Different distributions produce different answers. No contradiction or mistake, just different assumptions.

---

## Why Should We Care

Bertrand’s paradox shows up anytime someone says:

- “We sampled uniformly.”
- “We ran random simulations.”
- “We chose random test cases.”

Uniform over what? Random with respect to which measure? Those hidden modeling choices shape conclusions. Bertrand’s paradox forces us to confront an uncomfortable truth: **There is no such thing as neutral randomness.** There are only assumptions — explicit or implicit. And once you make them explicit, the paradox disappears.

# Okay, But Which Method Is “Right”?

Now that we’ve seen three different answers — $\frac{1}{3}$, $\frac{1}{2}$, and $\frac{1}{4}$ — your brain probably wants closure.

So let’s slow down and examine what actually changed.

The **geometry didn’t change.**  
The **circle didn’t change.**  
The **triangle didn’t change.**

Only the *procedure* changed. And the procedure *is the probability distribution*.

---

# Let’s Make the Geometry Explicit

Assume the circle has radius $R$. The side length of the inscribed equilateral triangle is:

$$
s = \sqrt{3} R
$$

Now consider a chord whose midpoint is a distance $r$ from the center. The length of that chord is:

$$
\ell = 2\sqrt{R^2 - r^2}
$$

We want:

$$
\ell > \sqrt{3} R
$$

Substitute:

$$
2\sqrt{R^2 - r^2} > \sqrt{3} R
$$

Square both sides:

$$
4(R^2 - r^2) > 3R^2
$$

$$
4R^2 - 4r^2 > 3R^2
$$

$$
R^2 > 4r^2
$$

$$
r < \frac{R}{2}
$$

So the chord is longer than the triangle side **exactly when its midpoint lies within a circle of radius $R/2$.** That’s the geometric heart of the puzzle. Everything now depends on how we distribute midpoints.

---

# Why the Three Answers Happen

### Case 1: Uniform Midpoints in the Disk

If midpoints are uniformly distributed in area:

- Total area = $\pi R^2$
- Favorable area = $\pi (R/2)^2$

So:

$$
P = \frac{\pi (R/2)^2}{\pi R^2} = \frac{1}{4}
$$

---

### Case 2: Uniform Distance Along a Radius

If we:
- Choose a random direction,
- Then choose $r$ uniformly in $[0, R]$,

Then:

$$
P = \frac{R/2}{R} = \frac{1}{2}
$$

Because now we’re weighting radius *linearly*, not by area.

Notice something subtle: Uniform in area means density proportional to $r$. Uniform in radius means density constant in $r$. Those are different measures.

---

### Case 3: Uniform Endpoints on Circumference

This implicitly induces yet another distribution on $r$.

If you derive it carefully, the density of $r$ becomes:

$$
f(r) = \frac{2}{\pi \sqrt{R^2 - r^2}}
$$

Integrating over $r < R/2$ gives:

$$
P = \frac{1}{3}
$$

Different mechanism. Different induced measure.

Same geometry.

---

# The Core Insight

“Random chord” is not a well-defined object.

It is shorthand for:

> A chord drawn according to some probability measure on the space of chords.

Different parameterizations create different uniformity assumptions.

Uniform in:
- angle
- radius
- midpoint area
- endpoints

are all different probability spaces.

---

# The Deeper Mathematical Issue

Probability is not invariant under reparameterization.

If:

- $X$ is uniform in $[0,1]$,
- and $Y = X^2$,

then $Y$ is **not** uniform.

Uniformity is coordinate-dependent.

Bertrand’s paradox is what happens when you say:

> “Uniform” — but fail to specify in which coordinates.

---

# A Mental Model That Helps

Think of it this way.

Imagine three robots:

- Robot A picks two random edge points.
- Robot B picks a random radius and distance.
- Robot C picks a random midpoint in area.

You press “run simulation.”

All three claim:

> “We generated 10 million random chords.”

They disagree on the answer. But none are incorrect. They just implemented different measures.

---

# Why This Matters Beyond Geometry

This puzzle shows up anytime someone says:

- “We sampled uniformly.”
- “We ran unbiased simulations.”
- “We chose random test cases.”

Those words are meaningless without a measure.

Uniform over:
- parameters?
- exposure?
- physical space?
- time?
- scenarios weighted by frequency?

Each choice encodes assumptions. Bertrand’s paradox is the geometry version of:

{{< info-purple >}}
Your model assumptions are doing more work than you think.
{{< /info-purple >}}

---

# So How Do We Decide Which Is Correct?

We impose a physical principle.

For example:

- If chords are created by dropping random sticks onto a circle, midpoint-uniform may be justified.
- If chords arise from random angles, endpoint-uniform may be justified.
- If chords are constructed by choosing random radius offsets, then radius-uniform applies.

The “correct” answer depends on the *generative process*. No generative process → no unique probability.

---

# A Slightly Philosophical Ending

Bertrand’s paradox teaches a powerful lesson:

{{< info-purple >}}
**Mathematics does not choose your probability model. You do.**

And if you don’t choose explicitly, you still chose — implicitly.
{{< /info-purple >}}