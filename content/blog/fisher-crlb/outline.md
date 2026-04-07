# Fisher Information, Curvature, and the Cramér–Rao Lower Bound
## Detailed blog post outline

---

## Working title options

- **Fisher Information: Curvature, Uncertainty, and the Cramér–Rao Bound**
- **Why Curvature of the Likelihood Tells You About Estimation Precision**
- **Fisher Information and the Geometry of Statistical Uncertainty**
- **From Likelihood Curvature to the Cramér–Rao Lower Bound**

---

## Big-picture goal of the post

This post should explain, in a conceptually honest but still intuitive way, why Fisher information is connected to estimation precision, why curvature of the log-likelihood matters, and what the Cramér–Rao lower bound is really saying.

The post should assume that the reader already understands:

- what a statistical model is,
- what the likelihood and log-likelihood are,
- what the maximum likelihood estimator is.

That material was handled in the previous blog post, so here we pick up from there.

The main conceptual arc is:

1. define Fisher information carefully,
2. explain its equivalent forms,
3. show why curvature matters,
4. explain why information adds across i.i.d. data,
5. introduce the Cramér–Rao lower bound,
6. explain why achieving the bound is a big deal,
7. give a concrete example where the bound is achieved.

The post should feel like a natural sequel to the likelihood/MLE post.

---

# Suggested structure

---

## 0. Opening: where we are in the story

### Goal of section
Bridge from the previous blog post.

### Content
Open by reminding the reader:

- In the last post, we introduced the likelihood as a random function of the parameter.
- We saw that the MLE chooses the parameter value that maximises that function.
- But that raises the natural next question:

> How much uncertainty should we expect in that estimator?

Say that Fisher information is one of the central objects that answers this question.

### Tone
Motivating and transitional, not technical yet.

### Suggested closing sentence
> Fisher information is the quantity that turns the shape of the likelihood into a statement about how precisely a parameter can be estimated.

---

## 1. Fisher information: first definitions

### Goal of section
State Fisher information cleanly in the scalar and multivariate settings.

### Structure

#### 1.1 Scalar definition
Let \(X \sim f(\cdot,\theta)\), with scalar parameter \(\theta\in\Theta\subseteq\mathbb{R}\).

Define the score:
\[
S(\theta) = \frac{\partial}{\partial\theta}\log f(X,\theta).
\]

Then define the Fisher information:
\[
I(\theta) = \mathbb{E}_\theta\!\left[S(\theta)^2\right].
\]

Under regularity conditions, also state the equivalent form:
\[
I(\theta) = -\mathbb{E}_\theta\!\left[\frac{\partial^2}{\partial\theta^2}\log f(X,\theta)\right].
\]

Make clear that this is for **one observation**.

Then for i.i.d. data \(X_1,\dots,X_n\),
\[
I_n(\theta)=n I_1(\theta).
\]

#### 1.2 Multivariate definition
Now let \(\theta\in\mathbb{R}^p\).

Define the score vector:
\[
S(\theta)=\nabla_\theta \log f(X,\theta).
\]

Define the Fisher information matrix:
\[
I(\theta)=\mathbb{E}_\theta\!\left[S(\theta)S(\theta)^\top\right].
\]

Under regularity conditions:
\[
I(\theta)= - \mathbb{E}_\theta\!\left[\nabla^2_\theta \log f(X,\theta)\right].
\]

For i.i.d. data:
\[
I_n(\theta)=nI_1(\theta).
\]

### Important points to stress
- In one dimension, Fisher information is a scalar.
- In higher dimensions, it becomes a matrix because parameter uncertainty has different directions and interactions.
- The matrix version is not just a technicality; it encodes how information behaves in different parameter directions.

### Appendix hook
Say something like:

> The equivalence of these forms is standard under regularity assumptions. I’ve placed the proof in the appendix, following Rajen Shah’s notes.

Also mention that the additivity/tensorisation for i.i.d. samples is proved in the appendix too.

---

## 2. What Fisher information is measuring

### Goal of section
Give a conceptual interpretation before diving into curvature.

### Content
Explain that Fisher information measures the **sensitivity of the model to changes in the parameter**.

If changing \(\theta\) slightly causes the distribution \(f(\cdot,\theta)\) to change a lot, then the data should be informative about \(\theta\).

If changing \(\theta\) barely changes the distribution, then the data should not tell us much about \(\theta\).

This can be phrased in two equivalent ways:

- Fisher information is the variance of the score,
- Fisher information is the expected negative curvature of the log-likelihood.

Then say that the second interpretation is especially geometrically intuitive, which motivates the next section.

### Tone
Conceptual. Avoid proving anything here.

### Key sentence
> Fisher information measures how sharply the statistical model reacts, on average, to small changes in the parameter.

---

## 3. Why curvature matters

### Goal of section
This is the central intuition section of the post.

This is where the single figure does almost all the work.

### Opening idea
Remind the reader:

- the log-likelihood is a random curve,
- the MLE is its maximiser,
- the shape of that curve near its maximum should affect how much the estimator moves from sample to sample.

Then introduce the key intuitive claim:

> Sharper log-likelihood \(\Rightarrow\) more local information about the parameter \(\Rightarrow\) lower estimator variance.

---

## 4. Central figure: simulated log-likelihoods under different variances

### Goal of figure
This should visually connect:

- sharper curvature,
- less spread in MLEs,
- higher Fisher information.

### Figure concept
Use the Gaussian location model with known variance:

\[
X_1,\dots,X_n \sim N(\theta,\sigma^2),
\]
with true value \(\theta=0\).

Choose:

- \(n=20\),
- \(m=10\) replicated samples,
- compare two cases:
  - \(\sigma_1^2 = 1\),
  - \(\sigma_2^2 = 10\).

For each replicate sample, compute and plot the log-likelihood as a function of \(\theta\).

### What the figure should show

#### Left panel
- 10 realised log-likelihood curves for samples from \(N(0,1)\).
- These curves should be relatively sharply curved.
- Their maximisers should be closer together.

#### Right panel
- 10 realised log-likelihood curves for samples from \(N(0,10)\).
- These curves should be flatter.
- Their maximisers should be more spread out.

### Main visual message
The figure should make the following two facts visible:

1. The log-likelihood curves are sharper when variance is smaller.
2. The corresponding MLEs vary less across repeated samples.

### Caption suggestion
> Log-likelihoods from repeated samples in the Gaussian location model with known variance. When the observation variance is smaller (left), the log-likelihood is more sharply curved and the MLEs are less variable across samples. When the observation variance is larger (right), the log-likelihood is flatter and the MLEs are more spread out.

### What to say in the text around the figure

Explain carefully:

- In the known-variance Gaussian location model,
  \[
  \ell_n(\theta) = -\frac{1}{2\sigma^2}\sum_{i=1}^n (X_i-\theta)^2 + C,
  \]
  so the curvature is
  \[
  \ell_n''(\theta) = -\frac{n}{\sigma^2}.
  \]

- Thus smaller \(\sigma^2\) means more negative second derivative in magnitude, i.e. sharper curvature.
- Also, the MLE is \(\hat\theta=\bar X\), whose variance is
  \[
  \operatorname{Var}(\hat\theta)=\frac{\sigma^2}{n}.
  \]

So in this model we can see everything explicitly:
- sharper curvature corresponds to smaller estimator variance,
- flatter curvature corresponds to larger estimator variance.

### Important subtlety to state explicitly
This figure is an **intuition builder**, not a proof of the general theory.

The post should say clearly:

- here we are looking at realised log-likelihoods,
- Fisher information is an expected quantity,
- but this figure gives a concrete picture of why curvature should be related to precision.

This distinction is crucial. Otherwise the post risks conflating observed curvature with Fisher information.

---

## 5. From observed curvature to Fisher information

### Goal of section
Bridge from the figure to the formal definition.

### Content
Explain:

The figure shows realised log-likelihood curves. But Fisher information is not defined as the curvature of one realised curve. It is the **expected** negative curvature:

\[
I(\theta) = -\mathbb{E}_\theta\!\left[\frac{\partial^2}{\partial\theta^2}\log f(X,\theta)\right].
\]

So Fisher information is the average local sharpness that the model tends to produce at parameter value \(\theta\).

Phrase it like this:

- observed curvature = sample-dependent,
- Fisher information = model-level average of this curvature.

This is the right moment to say that in practice one often also uses **observed information**, but that the theoretical object in the CRLB is Fisher information.

### Key message
> The figure explains why curvature should matter; Fisher information formalises this by averaging curvature over repeated samples from the model.

---

## 6. Why information adds for i.i.d. samples

### Goal of section
State the tensorisation/additivity result and give intuition.

### Content
For i.i.d. observations:
\[
\ell_n(\theta)=\sum_{i=1}^n \log f(X_i,\theta),
\]
so the score adds:
\[
S_n(\theta)=\sum_{i=1}^n S_i(\theta).
\]

Then Fisher information adds:
\[
I_n(\theta)=nI_1(\theta).
\]

### Intuition
Independent observations contribute independent pieces of evidence about the parameter, so information accumulates linearly.

Possible phrasing:

> If one observation gives you a certain amount of local information about the parameter, then \(n\) independent observations should give you \(n\) such pieces of information.

In the multivariate case:
\[
I_n(\theta)=n I_1(\theta)
\]
still holds, but now for matrices.

### Appendix hook
Say that the proof is straightforward from independence and is included in the appendix following Rajen’s notes.

### Nice optional note
This is one reason why variances of efficient estimators typically scale like \(1/n\): information grows like \(n\), so uncertainty shrinks like \(1/n\).

---

## 7. The Cramér–Rao lower bound: first scalar form

### Goal of section
Introduce the simplest form first.

### Content
State:

If \(\hat\theta\) is an unbiased estimator of scalar parameter \(\theta\), then under regularity conditions
\[
\operatorname{Var}_\theta(\hat\theta)\ge \frac{1}{I_n(\theta)}.
\]

Or equivalently, in the i.i.d. case,
\[
\operatorname{Var}_\theta(\hat\theta)\ge \frac{1}{nI_1(\theta)}.
\]

### Emphasis
This is a lower bound on the variance of **any unbiased estimator**.

It says:
- no unbiased estimator can have variance smaller than the reciprocal of the information.

### Tone
Simple and punchy.

### Suggested explanatory sentence
> The Cramér–Rao bound turns Fisher information into a hard limit: if the model contains only a certain amount of information about the parameter, then no unbiased estimator can beat that limit.

---

## 8. More general forms of the Cramér–Rao bound

### Goal of section
State broader versions without derailing the flow.

### Structure

#### 8.1 Function-of-parameter version
If estimating \(g(\theta)\) instead of \(\theta\), then for unbiased estimator \(T\) of \(g(\theta)\),
\[
\operatorname{Var}_\theta(T)\ge \frac{(g'(\theta))^2}{I_n(\theta)}.
\]

#### 8.2 Multivariate version
If \(\theta\in\mathbb{R}^p\), then for unbiased estimators under suitable regularity assumptions, covariance matrices satisfy a matrix lower bound of the form
\[
\operatorname{Cov}_\theta(T)\succeq \nabla g(\theta)^\top I_n(\theta)^{-1} \nabla g(\theta)
\]
in the appropriate formulation.

You may want to keep this section relatively light and say that in higher dimensions the inverse Fisher information matrix plays the role of the canonical lower bound on covariance.

### Advice on presentation
Do not overburden the main body with too many technical variants. The point is to show the reader that the scalar formula is the simplest face of a broader principle.

### Appendix hook
Put the proofs in the appendix.

---

## 9. Intuition behind the Cramér–Rao lower bound

### Goal of section
Explain what the bound means geometrically/statistically.

### Content
This section should be more reflective.

Explain:

- If the likelihood is flat, then many nearby parameter values are hard to distinguish.
- In that situation, it is impossible for an unbiased estimator to concentrate too tightly around the truth.
- If the likelihood is sharp, then the data distinguish nearby parameter values more effectively, so lower variance becomes possible.

Then connect back:

- Fisher information quantifies local distinguishability.
- The CRLB says that distinguishability imposes a lower bound on estimator variance.

### Important nuance
The bound does **not** say every estimator attains it.
It only says no unbiased estimator can go below it.

### Good phrasing
> The Cramér–Rao bound is not a recipe for constructing an estimator. It is a statement about what is fundamentally achievable in the model.

---

## 10. Why achieving the CRLB matters

### Goal of section
Explain the UMVU consequence.

### Content
Say:

If an unbiased estimator achieves the Cramér–Rao lower bound, then it must have the minimum possible variance among all unbiased estimators.

So it is automatically a **uniformly minimum-variance unbiased estimator** (UMVU), at least within the class covered by the theorem’s assumptions.

This is because:
- it is unbiased by construction,
- the CRLB says no unbiased estimator can have smaller variance.

### Suggested phrasing
> Achieving the Cramér–Rao lower bound is a certificate of optimality: among unbiased estimators, there is nowhere left to improve.

### Important caveat
You may want one sentence noting that unbiasedness is a restriction, and some biased estimators can outperform unbiased ones under other criteria. But do not linger here unless you want to foreshadow later posts.

---

## 11. Worked example: Bernoulli model

### Goal of section
Give a complete concrete example where all the ideas come together.

### Model
Let
\[
X_1,\dots,X_n \overset{\text{i.i.d.}}{\sim} \operatorname{Bern}(\theta),
\qquad \theta\in(0,1).
\]

### Steps to include

#### 11.1 Likelihood and MLE
The likelihood is
\[
L_n(\theta)=\theta^{\sum X_i}(1-\theta)^{n-\sum X_i}.
\]

The log-likelihood is
\[
\ell_n(\theta)=\left(\sum X_i\right)\log\theta + \left(n-\sum X_i\right)\log(1-\theta).
\]

Differentiating and solving gives
\[
\hat\theta_{\text{MLE}} = \bar X.
\]

You can be brief here since MLE mechanics were covered in the previous post.

#### 11.2 Fisher information
For one observation,
\[
\ell(\theta;X)=X\log\theta+(1-X)\log(1-\theta),
\]
so
\[
\frac{\partial^2}{\partial\theta^2}\ell(\theta;X)
=
-\frac{X}{\theta^2}
-\frac{1-X}{(1-\theta)^2}.
\]

Taking expectation:
\[
I_1(\theta)=\frac{1}{\theta(1-\theta)}.
\]

Therefore
\[
I_n(\theta)=\frac{n}{\theta(1-\theta)}.
\]

#### 11.3 CRLB
So the Cramér–Rao lower bound is
\[
\frac{1}{I_n(\theta)}=\frac{\theta(1-\theta)}{n}.
\]

#### 11.4 Variance of the MLE
But
\[
\operatorname{Var}(\bar X)=\frac{\theta(1-\theta)}{n}.
\]

So the MLE achieves the bound exactly.

### Conclusion of example
Therefore the MLE \(\bar X\):

- is unbiased,
- achieves the Cramér–Rao lower bound,
- is therefore UMVU.

### Why this example is good
It is clean, familiar, and everything works exactly rather than asymptotically.

You can mention that this is Example Sheet 1 Question 1 in Rajen’s course materials.

---

## 12. Optional short remark: what happens in higher dimensions?

### Goal of section
A brief forward-looking remark.

### Content
Say that in higher dimensions:

- uncertainty is directional,
- Fisher information becomes a matrix,
- the inverse information matrix plays the role of the covariance lower bound,
- this also explains why asymptotic normality of the MLE is expressed with covariance approximately \(I(\theta_0)^{-1}\).

Do not develop this too much unless you want the post to become substantially longer.

---

## 13. Conclusion

### Goal of section
Tie the story together.

### Points to recap
- Fisher information can be defined through the score or expected curvature.
- Curvature matters because sharper likelihoods make nearby parameter values easier to distinguish.
- Fisher information adds linearly across i.i.d. observations.
- The Cramér–Rao lower bound says no unbiased estimator can have variance below the reciprocal of the information.
- If an unbiased estimator attains the bound, it is optimal among unbiased estimators.
- In the Bernoulli model, the MLE does exactly that.

### Suggested closing line
> Fisher information is the mathematical object that converts the geometry of likelihood into a precise statement about the limits of estimation.

---

# Appendix plan

This should be explicitly referenced in the main post.

## Appendix A. Equivalence of the two definitions of Fisher information
Following Rajen Shah’s notes:
- score variance form,
- negative expected Hessian / second derivative form.

## Appendix B. Additivity / tensorisation under i.i.d. sampling
Show:
\[
I_n(\theta)=nI_1(\theta).
\]

## Appendix C. Proof of the scalar Cramér–Rao lower bound
Likely via covariance with the score and Cauchy–Schwarz.

## Appendix D. Equality condition in the Cramér–Rao bound
State the condition under which an unbiased estimator attains the bound.

## Appendix E. Multivariate statement of the CRLB
Give the matrix form cleanly.

---

# Notes on style

## What to keep explicit
Be extremely explicit about the difference between:

- **observed curvature** of a realised log-likelihood,
- **Fisher information**, which is an expected quantity.

This is the conceptual place where readers most often get misled.

## What not to do
- Do not pretend that “the second derivative of one likelihood curve is the variance of the MLE.” That is false.
- Do not introduce too many regularity assumptions in the main post. Mention them lightly and push details to the appendix.
- Do not overload the post with too many figures. The Gaussian log-likelihood comparison is enough if used well.

## Tone target
The post should feel:

- rigorous enough for a serious mathematics/statistics student,
- intuitive enough for someone who knows MLEs but has not internalised Fisher information,
- cleaner and more honest than a typical “stats intuition” post.

---

# Figure production notes

## Single figure layout
Use a 1x2 panel layout.

### Left panel
- title: `Known variance σ² = 1`
- x-axis: `θ`
- y-axis: `log-likelihood`
- 10 curves, one per sample

### Right panel
- title: `Known variance σ² = 10`
- x-axis: `θ`
- y-axis: `log-likelihood`
- 10 curves, one per sample

### Design notes
- Use the same x-axis range across both panels.
- Use the same y-axis scale if possible, or explain if not.
- Mark the maximiser of each curve with a small dot if visually clean.
- True parameter \(\theta=0\) can be shown with a faint vertical dashed line.
- The left panel should visually look “tighter” and “steeper”.
- The right panel should visually look more spread out and flatter.

## Optional annotation
You could annotate one curve in each panel with text like:
- “sharper curvature”
- “flatter curvature”

But do this only if it does not clutter the image.


---

# Final recommended flow in one sentence

> Define Fisher information carefully, interpret it as expected curvature and local distinguishability, use the Gaussian figure to make curvature and estimator variance visually tangible, then introduce the Cramér–Rao lower bound as the formal variance limit implied by that information, and close with the Bernoulli MLE as a concrete estimator that attains the bound.