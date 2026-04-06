---
title: The likelihood principle
slug: likelihood-principle
date: 2026-04-05
draft: false
subtitle: What the data say about the parameter—and what they do not
tags:
  - Statistics
notebook_url: "https://github.com/alexwangjiaqi/alex-blog/blob/main/notebooks/likelihood-principle.ipynb"
---

These are notes I keep coming back to when I want to separate *what the data actually say* from the extra baggage of *how* we decided to collect them.

## Two likelihoods, same inference

Suppose we observe data $x$ and agree on a model: the law of $x$ given parameter $\theta$ has density (or mass) $p(x \mid \theta)$. The **likelihood function** is that expression read as a function of $\theta$ with $x$ fixed:

$$
L(\theta \mid x) \propto p(x \mid \theta).
$$

Any positive constant in $x$ that does not depend on $\theta$ can be dropped; likelihoods are only defined up to proportionality.

The **likelihood principle (LP)** says, informally: if two experiments produce proportional likelihoods for the same $\theta$, they carry the *same* evidential content about $\theta$. Your inferences—if they are to be driven only by this model and this realised dataset—should not depend on which of the two experiments “happened,” once $L(\theta \mid x)$ is fixed.

A sharp consequence: the **stopping rule** of a sequential experiment, if it does not enter the likelihood, should not change inference. For example, in a Bernoulli model, observing nine successes in twelve trials can arise from “sample twelve” or “sample until nine successes”; if the likelihood for $\theta$ is the same in both cases, LP says treat them the same. That clashes with some classical frequentist intuitions about “optional stopping,” which is one reason the principle is both powerful and controversial.

## Birnbaum and the formal story

Birnbaum (1962) gave a much-discussed argument that **the conditionality principle** and the **sufficiency principle** together imply a general version of LP. Not everyone accepts the premises or the step from “plausible principles” to LP; the literature is full of careful counterarguments and refinements. I am not trying to settle that here—only to flag that LP is not an arbitrary slogan; it sits in the middle of foundational debates about what probability *means* for inference.

## What LP does *not* say

- It does **not** tell you which prior to use, or whether you must be Bayesian. It constrains how **likelihood-shaped** information should be used once a model is fixed.
- It does **not** absolve you of modelling choices: misspecify $p(x\mid\theta)$ and the likelihood is misleading in the ordinary sense.
- It does **not** forbid caring about design, loss functions, or frequentist risk—only that those concerns are layered *on top of* (or beside) the evidential message in $L(\theta\mid x)$, not smuggled in as if they changed the likelihood itself.

## Why I care

When I write down a model and see two procedures that depend on the same $L(\theta\mid x)$ but give different “answers,” I want to know *exactly* what extra input entered—often it is a convention about coverage, or a rule tied to the sampling scheme rather than to the realised likelihood. The likelihood principle is a clean diagnostic for that: it asks you to be honest about what is in the data, and what you added yourself.

---

*If you are new to this: a standard reference is Berger & Wolpert (1988),* The Likelihood Principle *; for the philosophical heat map, see Mayo’s and others’ responses to Birnbaum-style arguments.*
