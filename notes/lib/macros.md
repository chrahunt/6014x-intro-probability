<!--
Most commands have a conditional form with a "c" prefix.
pr - probability
ex - expected value
pmf - probability mass function
pdf - probability density function

Symbols:
Th - big theta
th - theta
Thh - big theta hat
thh - little theta hat
-->
<div display="none">\[
\newcommand{\cnd}[2]{\left.#1\,\middle|\,#2\right.}
\newcommand{\pr}[1]{\mathbf{P}\!\left(#1\right)}
\newcommand{\cpr}[2]{\pr{ \cnd{#1}{#2} } }
\newcommand{\ex}[1]{\mathbf{E}\left[#1\right]}
\newcommand{\cex}[2]{ \ex{ \cnd{#1}{#2} } }
\newcommand{\abs}[1]{ \left|#1\right| }
\newcommand{\unfrm}[2]{ \mathcal{U}\left( #1, #2 \right) }
\newcommand{\setst}[2]{\left\{#1\,\middle|\,#2\right\}}
\newcommand{\var}[1]{\text{var}\left(#1\right)}
\newcommand{\cvar}[2]{ \var{\cnd{#1}{#2}} }
\newcommand{\pmf}[2]{p_{#1}\left(#2\right)}
\newcommand{\cpmf}[3]{ \pmf{ \cnd{#1}{#2} }{#3} }
\newcommand{\pdf}[2]{f_{#1}\left(#2\right)}
\newcommand{\cpdf}[3]{ \pdf{ \cnd{#1}{#2} }{ #3 } }
\newcommand{\cdf}[2]{ F_{ #1 }\left( #2 \right) }
\newcommand{\if}{\text{if }}
\newcommand{\d}{\text{d}}
\newcommand{\iint}[2]{\!#1\,\d#2}
\newcommand{\exp}{\text{exp}}
\DeclareMathOperator{\exp}{exp}
\newcommand{\norm}{\mathcal{N}}
\newcommand{\norml}[1]{\norm\!\left(#1\right)}
\DeclareMathOperator{\cov}{cov}
\newcommand{\ninfty}{{-\infty}}
\newcommand{\Th}{\Theta}
\newcommand{\th}{\theta}
\newcommand{\Thh}{\widehat{\Theta}}
\newcommand{\thh}{\widehat{\theta}}
\newcommand{\map}{\text{MAP}}
\newcommand{\lms}{\text{LMS}}
$\newcommand{\toip}{\stackrel{\text{i.p.}}{\to}}$
\]</div>
