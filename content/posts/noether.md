+++
title = "Lagrangian Mechanics (WIP)"
tags = ["physics", "mathematics"]
date = '2024-11-09'
description = "Overview of Lagrangian Mechanics and how it relates to conserved quantities in physical systems"
draft = true
+++

## Table of Contents

0. [Overview](#overview)
1. [Equation of Motion](#equation-of-motion)
2. [Principle of Least Action](#principle-of-least-action)
3. [Euler-Lagrange Equation](#euler-lagrange-equation)
4. [Example](#example)

## Overview

{{< info-green >}}

Lagrangian mechanics offers a powerful and elegant framework for understanding the dynamics of physical systems. Developed by Joseph-Louis Lagrange in the 18th century, it reformulates Newtonian mechanics to focus on energy principles rather than forces. At its core, the Lagrangian approach introduces a function called the Lagrangian, defined as the difference between the kinetic energy and potential energy of a system. This method is particularly useful for analyzing complex systems with constraints, such as pendulums, planetary motion, or even modern robotics, as it simplifies calculations and generalizes easily to multiple dimensions. By applying the principle of least action, Lagrangian mechanics allows us to derive equations of motion that reveal the underlying behavior of a system with remarkable clarity. In this article, we’ll explore the foundational concepts of this framework, aiming to make it accessible to anyone curious about the mathematical elegance of physics.

{{< /info-green >}}

## Equation of Motion

The equations of motion are foundational to our understanding of physics, describing how systems evolve over time under the influence of forces. In classical mechanics, Newton’s second law, $F=ma$, provides a straightforward yet powerful framework: it relates the motion of an object to the forces acting upon it, allowing us to predict trajectories and dynamics from the motion of planets to the flight of a baseball. However, as our understanding of physics deepened, the equations of motion took on even greater significance, revealing connections between seemingly disparate phenomena and embodying deeper principles about the universe.

At their core, the equations of motion are more than just tools for prediction; they embody the fundamental symmetries and conservation laws that govern nature. For instance, Lagrangian mechanics reframes the equations of motion not in terms of forces but through energy $––$ specifically, the difference between kinetic and potential energy, known as the Lagrangian whose details are provided below. This perspective is far more general, providing a bridge to more advanced areas of physics, including quantum mechanics and relativity. In this framework, the equations of motion are derived elegantly from the principle of least action, a profound idea that suggests the paths taken by physical systems are those for which a quantity called "action" is minimized or *stationary*.

This shift in perspective underscores the deeper importance of the equations of motion. They are not merely equations to solve; they reveal how the universe inherently organizes itself. Whether describing the deterministic motion of classical objects or the probabilistic evolution of quantum systems, the equations of motion encapsulate the predictive power and universality of physical laws. By understanding these equations, we gain not only the ability to describe how things move but also a glimpse into the fundamental principles—such as the principle of least action—that reflect the elegance and simplicity of nature.

## Principle of Stationary Action

The principle of stationary action is a profound and unifying idea in physics that reveals how nature operates efficiently. It states that the motion of a physical system between two points in time follows a path for which the action is stationary—typically minimized—compared to all other conceivable paths.[^1] This principle applies universally, from the orbits of planets in celestial mechanics to the behavior of quantum particles, making it one of the most fundamental concepts in science. What makes it extraordinary is its ability to derive the equations of motion for systems in a way that highlights the intrinsic elegance of physical laws, emphasizing energy relationships rather than forces. Erwin Schrödinger himself was even inspired by this work which led to the development of the Schrödinger equation $--$ the equation which governs how probabilistic wave functions of quantum particles evolve through time.

The action is a scalar quantity, defined mathematically as the integral of the Lagrangian over time. The Lagrangian, $\mathcal{L}$, represents the difference between a system's kinetic energy $(T)$ and potential energy $(U)$:

$$\mathcal{L} = T - U$$

The action, $S$, is then given by:

$$S \equiv \int_{t_1}^{t_2} \mathcal{L}(q(t), \dot q(t), t) dt$$

Here, $t_1$ and $t_2$ represent the initial and final times of the system, $\mathcal{L}$ encapsulates the system's dynamics at every instant within this interval, and $q(t)$ is the *equation of motion*. Integrals like the one above are called *functionals*, and $S$ is sometimes denoted as $S[q(t)]$. This notation tries to make clear that $S$ depends on, not a number, but rather the entire trajectory, $q(t)$. This kind of mathematics is referred to as calculus of variations (or variational calculus). The principle of stationary action asserts that the physical trajectory of the system is the one that makes $S$ stationary. In practical terms, this means that small variations in the path around the true trajectory do not significantly change $S$, leading to the **Euler-Lagrange** equations, which govern the motion of the system and what we'll touch on in the next section.

What makes this principle so powerful is its generality. In classical mechanics, it reproduces Newton’s laws of motion. In optics, it relates to Fermat’s principle, where light takes the path of least time. In quantum mechanics, it lays the foundation for Feynman’s path integral formulation, where every possible path contributes to the behavior of particles, weighted by their action. Therefore, the principle of stationary action serves as a unification, revealing that the laws of physics are deeply rooted in optimization and symmetry.[^2]

For example, consider a ball dropped from rest, and consider the function $y(t)$ for $0 \le t \le 1$. Assume $y(0) = 0$ and $y(1) = -g/2$ (which comes from $y = -gt^2/2$).

![least-action](/images/coord/least-action.png)

A number of different trajectories can be considered and each can be given a scalar value (i.e., action). We have tools to help us determine which trajectory yields a stationary value $--$ ultimately giving us the desired equation of motion.

## Euler-Lagrange Equation

The following theorem allows us to connect the principle of stationary action to the aforementioned **Euler-Lagrange** equations:

{{< info-blue >}}

Theorem

If the function $x_0(t)$ yields a stationary value (that is, a local minimum, maximum, or saddle point) of $S$, then

$$\frac{\partial \mathcal{L}}{\partial x_0}=\frac{d}{dt}\frac{\partial \mathcal{L}}{\partial \dot{x}_0}$$

We consider the class of functions whose endpoints are fixed. That is, $x(t_1) = x_1$ and $x(t_2) = x_2$.

{{< /info-blue >}}

Now, we can essentially replace Newton's Second Law of Motion, $F=ma$, by the following principle

{{< info-blue >}}

Hamilton's Principle

The path of a particle is the one that yields a stationary value of the action, $S$.

{{< /info-blue >}}

This says if and only if we have a stationary value, then the Euler-Langrage equations hold and the E-L equations are essentially the same as $F=ma$. We will see examples of describing a system in terms of its energy instead of forces which allows the search for the equation of motion.[^3]

## Example

If what has been written so far seems vague or a bit generalized, it is because this was
intended to be more of a reminder than an introduction. Let's finish this overview with
the relationship between the Newtonian and Lagrangian formulations. 
The equations that are obtained by these methods must be equal; physics does not change
depending on the language we use to describe it; they really are one and the same. Just because
Newton's laws are usually explicitly written in terms of force doesn't mean we
can't express it in terms of another quantity like momentum for example:
$$F = ma = m\dot{v} = \dot{p}$$
Let's not forget how related force and energy really are:

$$\Delta T = T\_2 - T\_1 = \int_{1}^{2}\textbf{F} \cdot d\textbf{r}$$

$$U(\textbf{r}) = -\int_{r_0}^r F(\textbf{r}') \cdot d\textbf{r}'$$
To relate Lagrangian and Newtonian methods more directly:

## Euler-Lagrange Equation

$$\frac{\partial \mathcal{L}}{\partial q_i}=\frac{d}{dt}\frac{\partial \mathcal{L}}{\partial \dot{q}_i}$$
$$\frac{\partial \mathcal{L}}{\partial q_i} = F_i\ \ \ and\ \ \ \frac{\partial \mathcal{L}}{\partial \dot{q}_i} \equiv p_i$$
These are referred to as generalized forces and generalized momenta. We may start our discussion of generalized ignorable coordinates and conservation laws now!

## Generalized Coordinates
Generalized momenta and generalized forces are not the same thing as the familiar
force and momentum we are used to. We can still relate momentum and force in the
usual manner:
$$F_i = \frac{d}{dt}p_i$$
except these are understood to be defined using generalized coordinates. The fact that
*generalized force* $=$ *rate of change of generalized momentum* should not be surprising.
A direct way to think of generalized coordinates is to describe the complete
motion of a system in the fewest number of coordinates. Consider a pendulum bob for one
moment (yes, another pendulum).

![Pendulum](/images/coord/pendulum.png)

We have a choice of using Cartesian coordinates to describe the motion of this
bob or any other coordinate system we can dream up. The downside of using
Cartesian coordinates $(x,y)$, is that $x$ and $y$ must constantly compensate one another to assure the length L remains constant. We can imagine all the combinations of values that satisfy $x^2+y^2-L^2=0$. Long story short, spherical (or polar) coordinates $(r, \theta, \phi)$ are the most appropriate for this problem for
obvious symmetrical advantages and can be considered the generalized coordinates that define our system.

Now that we have mentioned what generalized coordinates are, we can gain more insight
on what generalized momenta is. Ordinary momentum by definition is $p = mv$ where $v$ is
one time derivative away from a position variable: $p = m (\dot{x}+\dot{y}+\dot{z})$.
So we can easily see that generalized momenta is simple the mass of an object times the
time derivative of its generalized position vectors! Simple! Generalized force can be found the same way except with two time derivatives. $F_t$ in the Figure 1 is the
generalized force of the pendulum system. This pendulum can escape from the x-y grid universe and be thought of as moving along one generalized coordinate, $\theta(t)$. (The length of the pendulum, L, if fixed but if it weren't, $r(t)$ could be another generalized coordinate used to describe the system).

## Cyclic Coordinates
When the Lagrangian of a system is independent of a generalized coordinate $q_i$, that
coordinate is sometimes called a *cyclic* or *ignorable* coordinate.
Saying the Lagrangian is independent of a particular variable is exactly what it
sounds like, neither the kinetic nor the potential energy depend on this quantity.
This leads directly to the fact that there exists a conserved quantity!

We can generally express a Lagrangian that is independent of some generalized
coordinate $q_2$ as:
$$\mathcal{L}=\mathcal{L}(q_1, q_3, q_4, \cdots, \dot{q}_1, \dot{q}_2, \dot{q}_3, \dot{q}_4, \cdots, t)$$

What this means exactly, is that the generalized momentum that corresponds to $q_2$ is
conserved. This can be written as:
$$\frac{d}{dt}\frac{\partial \mathcal{L}}{\partial \dot{q}_2} = \frac{\partial \mathcal{L}}{\partial q_2} = 0$$
$$\frac{\partial \mathcal{L}}{\partial \dot{q}_2} = \kappa$$ where $\kappa$ is constant. We can say that this system exhibits conservation of angular momentum!


This makes solving equations of motion using Lagrangian even easier than before!

Let's take advantage of this property by examining the $\mathcal{L}$ of a standard classical mechanics
problem (one of which never gets old). It is stated as follows:
 
**Problem** *A mass $m$ is free to slide on a frictionless table and is connected, via a string that passes through a hole in the table, to a mass $M$ that hangs below. Assume that $M$
moves in a vertical line only, and assume that the string always remains taut. Figure 2 shows a moment in time of this situation.*

![Table](/images/coord/table.png)

The Lagrangian is as follows:
$$\mathcal{L}=T-U$$
$$\mathcal{L}=\frac{1}{2}M \dot{r}^2+\frac{1}{2}m(\dot{r}^2+r^2\dot{\theta}^2)+Mg(l-r)$$
The important thing to notice about this expression is that there is no $\theta$ variable
in it anywhere. The Lagrangian is said to be invariant under variations of the generalized
coordinate $\theta$. The important conclusion to take away from this is that the momentum that corresponds to $\theta$ is conserved or in
this case, the angular momentum $mr^2\dot{\theta}$. Therefore without much investigating we can quickly see that $\frac{d}{dt}(mr^2\dot{\theta})=0$. This comes directly from the *Euler-Langrange* equation obtained by varying $\theta$:

$$\frac{\partial \mathcal{L}}{\partial \theta}=\frac{d}{dt}\frac{\partial \mathcal{L}}{\partial \dot{\theta}}$$
$$0 = \frac{d}{dt}(mr^2\dot{\theta})$$

The *E-L* equation that comes from varying $r$ is:
$$\frac{\partial \mathcal{L}}{\partial r}=\frac{d}{dt}\frac{\partial \mathcal{L}}{\partial \dot{r}}$$
$$(M+m)\ddot{r}=mr\dot{\theta}^2-Mg$$

## Conservation of Energy
Energy is also another quantity that is often conversed in these types of mechanical problems. We will introduce an important claim that touches on this conservation law. First let's give a definition of *energy* in terms of the *Lagrangian*:
$$E \equiv (\sum_{i=1}^{N} \frac{\partial \mathcal{L}}{\partial \dot{q}_i} \dot{q}_i) - \mathcal{L}$$
This may seem random to define the energy in such a way but don't worry too much about it for now. Without going into too much detail, this result is far from random. In fact, there is a rigorous mathematical reason, called the theory of Legendre transforms, that explains why energy can be written in this form. You see this often in Hamiltonian mechanics since the Hamiltonian is simply the total energy of the system: $T+U$.

Now we may introduce the claim mentioned earlier:


*If $\mathcal{L}$ has no explicit time dependence (that is, if $\frac{\partial \mathcal{L}}{\partial t} = 0$), then E is conserved (that is, $\frac{dE}{dt} = 0$), assuming that the motion obeys the E-L equations.*

Without proving it, the following relation summarizes this claim:
$$\frac{dE}{dt}=-\frac{\partial \mathcal{L}}{\partial t}.$$

## Applications
I programmed this nonlinear double pendulum with Mathematica (Wolfram Language)
![](/images/coord/doublependulum_5.gif)

## Practice Problem

![Falling Sticks](/images/coord/sticks.png)

Here is a fun problem you can practice with.

Two massless sticks of length $2r$, each with a mass $m$ fixed at its middle, are hinged at an end. One stands on top of the other, as shown in above. The bottom end of the lower stick is hinged at the ground. They are held such that the lower stick is vertical, and the upper one is tilted at a small angle $\epsilon$ with respect to the vertical. They are then released. At this instant, what are the angular accelerations of the two sticks? Work in the approximation where $\epsilon$ is very small.

### References

[^1]: Principle of stationary action is sometimes called principle of "least" action but this is a misnomer since it is not always the case that the stationary value is a minimum. For example, the harmonic oscillator with $\mathcal{L} = \frac{1}{2}m \dot{x}^2 - \frac{1}{2}k x^2$ is a sometimes a minimum and sometimes a saddle point depending on the situation.
[^2]: There are more that can be said with respect to symmetry in terms of Noether's theorem but I'll save this for another note.
[^3]: There also exists a Hamiltonian formulation of Classical Mechanics that takes advantage of its own coordinate system called *Canonical Coordinates*.
[^3]: Morin, David. Introduction to classical mechanics: with problems and solutions. Cambridge University Press, 2008.