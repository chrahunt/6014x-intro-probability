---
type: lecture
num: 15
unit: 6
title: Linear models with normal noise
---

# Lecture 15: Linear models with normal noise

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
$\newcommand{\Th}{\Theta}$
$\newcommand{\th}{\theta}$
$\newcommand{\Thh}{\widehat{\Theta}}$
$\newcommand{\thh}{\widehat{\theta}}$
$\newcommand{\map}{\text{MAP}}$
$\newcommand{\lms}{\text{LMS}}$

## Overview

We will look at a special case of continuous parameter, continuous observation problem where the parameters are independent normal r.v.s.

\[
X_i = \sum_{j=1}^m a_{ij}\Th_j + W_i
\]

with $W_i, \Th_j$ independent normal random variables.

* $\Th_j$ represents the variables to uncover and $W_i$ is just noise
* Very common and convenient model
* $X_i$ are normal because they are the sum of normal r.v.s
* LMS and MAP are the same (peak of normal is at mean) and given by linear functions
* Nice analytic properties
* Long example of estimating trajectory given noisy sensor readings

## Recognizing normal PDFs

Recall Normal r.v.s have the form

![](unit7lec15-linear-models-w-normal-noise\15fbcf9f0cad93331d71b554346c87da.png)

going from specific fns to parameters of normal

easy case:

![](unit7lec15-linear-models-w-normal-noise\49032291edb1fd9f337b877541306d28.png)

pdf has to die out, so exponent must be negative (assume so from now on)

derivation of parameters of PDF

![](unit7lec15-linear-models-w-normal-noise\50189ee9345f739d36b6294cb00da314.png)

this shows us that a distribution of this form is normal.

for the mean we know that's where the distance is maximal, or the part $\alpha x^2 + \beta x + \gamma$ is minimal, which is where its derivative is 0, which is exactly where it is indicated in the box.

## Normal unknown and additive noise

Simple first, complex later.

Additive normal noise. Let $X = \Th + W$ with $\Th, W \sim N(0, 1)$ and independent.

Since they are both cts, we use the appropriate bayes rule

\[
\cpdf{\Th}{X}{\cnd{\th}{x}} = \frac{ \color{blue}{\pdf{\Th}{\th}} \color{red}{\cpdf{X}{\Th}{\cnd{x}{\th}}} }{\color{green}{\pdf{X}{x}}}\\
\pdf{X}{x} = \int \iint{\pdf{\Th}{\th} \cpdf{X}{\Th}{\cnd{x}{\th}} }{\th}
\]

We start by finding the parts of our eqn. Given $\th$,

\[
\color{red}{\cpdf{X}{\Th}{\cnd{x}{\th}}}: X = \th + W
\]

which (since $W$ is standard normal) implies that $X \sim N(\th, 1)$. $\Th$ is standard normal, so we know its pdf.

Using these,

\[
\begin{align}
\cpdf{\Th}{X}{\cnd{\th}{x}} &= \color{green}{\frac{1}{\pdf{X}{x}}} \color{blue}{c_1 e^{-\frac{1}{2}\th^2}} \color{red}{c_2 e^{-\frac{1}{2}(x - \th)^2}}\\
&= c(x)e^{-g(\th)}
\end{align}
\]

where $g(\th)$ is just some quadratic fn of $\th$. Fixing $x$, we can see that this is also normal by previous work.

As discussed previously, a normal r.v. gives us $\thh_\map = \thh_\lms = \cex{\Th}{X = x}$. To find it's value we want to see where $\cpdf{\Th}{X}{\cnd{\th}{x}}$ is maximal, which means we want to minimize $g(\th)$. $g(\th)$ is quadratic and has a positive leading term, so we can just find the $\th$ for which $g^\prime(\th) = 0$. Combining terms gives us

\[
\begin{align}
\frac{\d}{\d\th}\left[g(x)\right] &= \frac{\d}{\d\th}\left[\frac{1}{2}\th^2 + \frac{1}{2}(x - \th)^2\right]\\
&= \th + (\th - x)
\end{align}
\]

Setting that equal to 0 gives us $\th = \frac{x}{2}$. For the estimator we get $\Thh_\map = \cex{\Th}{X} = \frac{X}{2}$.

How special is this example?  
It's not. It also works for general means and variances.
working it out on your own helps determine that the posterior is normal, so the LMS and MAP coincide and the estimators are linear, of the form $\Thh = aX + b$.

Recall:
$N(a, b) + N(c, d) = N(a + c, b + d)$

$Y = aX+b \implies Y \sim N(a\mu + b, a^2\sigma^2)$

then we can accept that $X$ is normal, but what is its estimator?

it will be where the sum of the exponents on $\pdf{\Th}{\th}$ and $\cpdf{X}{\Th}{\cnd{X}{\th}}$ are equal to 0. Given $X = a\Th + bW$ and conditioned on $\Th = \th$, we have $X \sim N(b\mu_W + a\th, b^2\sigma_W^2)$. Let $\Th \sim N(\mu_\Th, \sigma_\Th^2)$ then we have

\[
-(\th - \mu_\Th)^2\cdot\frac{1}{2\sigma_\Th^2} + -(x - (b\mu_W + a\th))^2\cdot\frac{1}{2\sigma+W^2}
\]
