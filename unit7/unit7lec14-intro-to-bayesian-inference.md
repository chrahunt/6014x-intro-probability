$\newcommand{\cnd}[2]{\left.#1\,\middle|\,#2\right.}$
$\newcommand{\pr}[1]{\mathbf{P}\!\left(#1\right)}$
$\newcommand{\cpr}[2]{\pr{ \cnd{#1}{#2} } }$
$\newcommand{\setst}[2]{\left\{#1\,\middle|\,#2\right\}}$
$\newcommand{\ex}[1]{\mathbf{E}\left[#1\right]}$
$\newcommand{\cex}[2]{ \ex{ \cnd{#1}{#2} } }$
$\newcommand{\var}[1]{\text{var}\left(#1\right)}$
$\newcommand{\cvar}[2]{ \var{\cnd{#1}{#2}} }$
$\newcommand{\d}{ \text{d} }$
$\newcommand{\iint}[2]{ \! #1 \,\d #2 }$
$\newcommand{\pmf}[2]{ p_{ #1 }\left( #2 \right) }$
$\newcommand{\cpmf}[3]{ \pmf{ \cnd{#1}{#2} }{#3} }$
$\newcommand{\pdf}[2]{ f_{ #1 }\left( #2 \right)}$
$\newcommand{\cpdf}[3]{ \pdf{ \cnd{ #1 }{ #2 } }{ #3 } }$
$\newcommand{\cdf}[2]{ F_{ #1 }\left( #2 \right)}$
$\newcommand{\if}{\text{if }}$
$\newcommand{\exp}{\text{exp}}$
$\newcommand{\norm}{\mathcal{N}}$
$\DeclareMathOperator{\exp}{exp}$
$\DeclareMathOperator{\cov}{cov}$
$\newcommand{\ninfty}{{-\infty}}$
$\newcommand{\abs}[1]{ \left|#1\right| }$

## Overview

* The big picture
  * Motivation, applications
  * problem types
    1. hypothesis testing
    2. estimation

* The general framework
  * Bayes rule to find the posterior distribution of an unknown based on some other known value.
  * different versions depending on whether the random variable is discrete or continuous
  * get a numerical estimate of the unknown random variable (place where it is largest or the mean of the posterior, MAP, LMS)
  * measure performance of the estimate (probability of error, mean squared error)
  * lots of examples to help with discipline and confidence in application.

## Overview of some application domains

Going back to the big picture. Interence/statistics works to generate models from data. Models are then used by probability theory to do analysis.

The prevalence of data in the modern world has changed what statisticians can do.

Big:
 data
 models
 computers

Polling
Marketing, advertising - recommender systems like Netflix
Finance
Life sciences with genomic data - disease causes

Modeling/monitoring:
- the ocean
- global climate
- pollution

physics and astronomy

signal processing - reducing and accounting for noise in different applications

Regardless of the application, the approach is the same.

## Types of inference problems

Inference/statistics may be use for 2 purposes:
* model building
* inferring unobserved variables

in the latter case the model is given to us but is incomplete.

Example:
Some signal goes through a medium, has some noise added to it, and is received as $X$ by a sensor.

![](unit7lec14-intro-to-bayesian-inference\031282c085b97061bccf63e548493e42.png)

and we're given the relationship $X = aS + W$. The two questions reasonable to ask here are:

1. Given $S$ and $X$, what is the medium (i.e. find $a$) - this is model bulding
2. Given $a$, $X$, what was the original signal $S$? - this is variable estimation

The interpretation is different but the math is the same.

Hypothesis testing problems
unknown is categorical/discrete valued-answer problem - unknown has a few possible values and the idea is to make bad decisions with low probability.

Estimation problem:
- numerical unknown, e.g. linear regression
- want an estimate that is close to the truth

## The Bayesian inference framework

$\Theta$ unknown r.v.

What is the primary difference between the bayesian framework and other frameworks?  
In the bayesian framework the unknown variable is treated as a random variable instead of a constant.

What is the distribution of the unknown?  
Prior distribution, $p_\Theta$ or $f_\Theta$, our beliefs about the unknown before obtaining data.

Then we get some observation $X$ and we generate an observation model $p_{X|\Theta}$ or $f_{X|\Theta}$

![](unit7lec14-intro-to-bayesian-inference\bfd30e1c8ac6b0181d0c9760832e000c.png)

Where do we get the prior distribution?  
* symmetry argument - we can assume all possibilities are equally likely
* range - known range, behavior
* past knowledge about distribution of $\Theta$ (prior studies)
* arbitrary, statistician's choice.

What is the output of Bayesian inference?  
A posterior distribution of the form $\cpmf{\Theta}{X}{\cnd{\cdot}{x}}$ or $\cpdf{\Theta}{X}{\cnd{\cdot}{x}}$.

![](unit7lec14-intro-to-bayesian-inference\a64116d5469a038c61827341fcf2b204.png)

Example: electoral votes.

We could say simply some probability that a particular person will win, but a more complete result would look like

![](unit7lec14-intro-to-bayesian-inference\cdcc0ba6e23184a829e7493557928e84.png)

This is useful but there may also be some estimation and summarization done after the posterior is defined:
* point estimates
* error analysis

Asked to provide a single guess about what $\Theta$ is, how to proceed?
* maximum a posteriori probability rule - report the largest value

![](unit7lec14-intro-to-bayesian-inference\2928e4c3ef3b3374bc1ced17dd962d3f.png)

We find the $\theta$ over all $\Theta$ that maximizes the posterior distribution.

We may also want to give the mean of the posterior, which is the conditional expectation estimator.

![](unit7lec14-intro-to-bayesian-inference\bdaf2d3c6746ae9a05e920a14d21192b.png)
- gives you the smallest mean squared error

The number produced is an estimate. $\widehat{\theta} = g(x)$ based on the data $x$ which is processed by $g$. Given we don't know $x$, then we have what is called an **estimator**, a **random variable** on $X$, $\widehat{\Theta} = g(X)$.

Estimator may also be used to refer to the function $g$ doing the processing on the data.

Notice that these two things are different. The estimate is a number given certain data and the estimator is the rule used to process the data.

We know what it takes to calculate conditional distributions and we have 2 estimators, so we just need to do examples.

## Discrete Parameters, discrete observation

The incoming data is discrete and the outputs of the fn are discrete. The values of $\Theta$ are alternative hypotheses.

![](unit7lec14-intro-to-bayesian-inference\e381a1caf27af4e254b55a25854642d5.png)

 Refer back to bayes rule lectures for info on how to determine distribution, now just assume we have observed $X$ and already have the conditional PMF of $\Theta$.

 Suppose $\Theta$ is
 ![](unit7lec14-intro-to-bayesian-inference\c2a149807003109ced079ff9e55a147c.png)

we can stop here or come up with an estimate:

MAP rule: $\widehat{\theta} = 2$
LMS rule = $\widehat{\theta} = \cex{\Theta}{X = x} = 2.2$

We may also want to know how good an estimate is.
