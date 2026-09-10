+++
title = "Freedom of Model Building"
tags = ["statistics"]
date = "2026-09-09"
description = "How do scientists decide which model to use when several can fit the same data? This post follows that question through the assumptions and creative choices behind scientific models, and looks at how physical reasoning and experiments help us decide which ones deserve our confidence."
draft = false
+++

---

# Who Gets to Choose the Curve?
*On the strange freedom of building scientific models*

{{< info-green >}}

There is a moment in learning physics that has always made me uncomfortable. We collect data, plot the points, and draw a curve through them. Someone announces that the relationship is exponential, logarithmic, or a power law, and the lesson moves on. But I am still looking at the graph, wondering who decided that. Why this curve? Why not another one that passes just as close to the measurements? Somewhere between observation and explanation, a person has made a choice. I wanted to understand what gave that choice its authority.

{{< /info-green >}}

This made physical models feel arbitrary to me, and it turns out others have thought about the same concern for a long time. Poincaré, Einstein, and other thinkers worried about the same gap. Philosophers call one version of it *underdetermination*: the evidence can be compatible with several different models. A finite collection of measurements does not uniquely specify a curve. Multiple functions can agree where we have measured and disagree where we have not.

Henri Poincaré explored almost exactly this problem in *Science and Hypothesis* in 1902. He asked why, when connecting experimental points, we favor regular curves over extravagant zigzags. We bring expectations about simplicity and smoothness to the graph, even though those expectations are not themselves measurements. Poincaré then confronted the awkward question underneath: we may need simplicity to generalize, but what entitles us to expect nature to cooperate? An ordinary graph turns out to contain both observations and assumptions about how the world should behave. [Read “Hypotheses in Physics.”](https://brocku.ca/MeadProject/Poincare/Poincare_1905_10.html)

Einstein, in his 1933 lecture “On the Method of Theoretical Physics,” argued that the fundamental concepts and principles of a theory cannot simply be extracted from experience through logical deduction. They require invention. Experience guides our choices and judges their consequences, but it does not write the theory for us. Einstein recognized the uncertainty this introduces and expressed confidence that mathematical simplicity could nevertheless lead toward understanding nature. Even he had to consider what supported his way of thinking. [Read the lecture in Appendix B.](https://www.informationphilosopher.com/books/einstein/Einstein.pdf#page=402)

To see how invention becomes a testable proposal, consider exponential decay. We might choose an exponential because it resembles our data, but we could also begin with a physical assumption: the quantity loses a constant fraction of what remains per unit time. That assumption gives the equation $dy/dt=-ky$, whose solution is $y(t)=y_0e^{-kt}$. The curve now follows from a proposed rule about the system. We can investigate whether the fractional rate remains constant or whether changing conditions undermine the assumption. Still, different mechanisms can produce exponential behavior, so a successful fit does not uniquely reveal its cause.

Richard Feynman described the practical process plainly: guess a law, calculate its consequences, and compare them with experiment. The guess earns credibility through what happens next. If an exponential and a power law both describe our measurements, we might observe much later, where their predictions separate, or change the experimental conditions. This offers an answer to my original question about authority. Anyone can propose a curve; confidence depends on reasons others can examine, including explicit assumptions, reproducible observations, and successful new predictions. Sometimes the evidence cannot distinguish the candidates, and recognizing that is itself progress. [Watch “Seeking New Laws.”](https://videos.cern.ch/record/1048168)

![least-action | 100](/images/models/points.png)

Pierre Duhem adds a complication. A prediction depends on more than the proposed law: it also involves assumptions about instruments, starting conditions, and the surrounding environment. When an experiment disagrees with a prediction, it may not identify which assumption failed. Perhaps our decay model is inadequate, or perhaps the detector drifted. In *The Aim and Structure of Physical Theory*, Duhem explains why scientific judgment remains necessary even after the measurements arrive. Researchers can agree about an observation while disagreeing about what should be revised. [Read “Physical Theory and Experiment.”](https://joelvelasco.net/teaching/5330/Duhem_physical_theory_experiment%28curd_cover%29.pdf)

A modern version of this caution appears in Richard McElreath’s *Statistical Rethinking*, under the memorable name “The Scourge of Histomancy.” It describes choosing a probability distribution by gazing at a histogram. His objection is specific: regression assumptions concern outcomes conditional on predictors, while a pooled histogram can conceal those relationships. But the broader temptation is familiar. We recognize a shape and feel we have understood something. Similar caution motivates Clauset, Shalizi, and Newman’s work on power-law distributions, which emphasizes careful fitting and comparison with alternatives. A convincing graph can suggest a model without establishing it. [Read McElreath’s passage on page 282](https://civil.colorado.edu/~balajir/CVEN6833/bayes-resources/RM-StatRethink-Bayes.pdf) and the [power-law paper](https://arxiv.org/abs/0706.1062).

I no longer think “arbitrary” captures what bothered me about models. There is freedom in constructing them, alongside real constraints: independent evidence, physical reasoning, and predictions that survive new measurements. When I look at a fitted curve now, I still wonder who put it there, but I also ask what assumptions support it, what alternatives remain possible, and what experiment would make them disagree. The uneasiness has become useful. It gives me a reason to keep asking questions after the curve has been drawn.

---