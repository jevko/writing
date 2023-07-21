---
author: Darius J Chuck
title: "[DRAFT] Terse canonical name-, paren-, and space-free syntaxes for lambda calculus"
subtitle: "[SUMMARY-ONLY]"
date: 2023-07-21
---

<style>
@media screen {
  html {
    /* todo: use for publishing a dark-mode draft: */
    filter: invert(1);
  }
}
@media print {
  .pagebreak { page-break-before: always; }
}
</style>

<div class="pagebreak"> </div>

# Summary

[[N.G. de Bruijn 1972]](#debruijn) introduced a way to eliminate names from the syntax of lambda calculus, making it much simpler and "easy to handle in metalingual discussion" and "easy for the computer and for the computer programmer". 

[[J. Tromp 2023]](#tromp) incorporated and expanded upon this idea in his Binary Lambda Calculus (BLC) syntax, which also eliminates the notion of significant parentheses and spaces.

BLC makes for a very good binary canonical representation of lambda calculus terms.

In this article I define text-based equivalents which retain the desirable properties of BLC.

Going futher, I propose ways to also remove repetition from the syntax.

I also show how various syntax modifications and variants can be mixed-and-matched and combined to reintroduce human-readability while retaining the ease of processing.

I introduce a loose labelling scheme for lambda calculus syntax variants, with LCλ<sup>2</sup>τ<sub>0</sub>α<sup>2</sup> denoting the most terse text-based variant of the syntax.

Compare a few well-known combinators:

<table>
<tr>
  <th>combinator</th>
  <th>conventional</th>
  <th>de Bruijn</th>
  <th>LCλ<sup>2</sup>τ<sub>0</sub>α<sup>2</sup></th>
</tr>
<tr>
  <th>I</th>
  <td>λx.x</td>
  <td>λ 0</td>
  <td>λτ<sub>0</sub></td>
</tr>
<tr>
  <th>K</th>
  <td>λx.λy.x</td>
  <td>λ λ 1</td>
  <td>λ<sup>2</sup>τ<sub>1</sub></td>
</tr>
<tr>
  <th>U</th>
  <td>λx.x x</td>
  <td>λ 0 0</td>
  <td>λατ<sub>0</sub>τ<sub>0</sub></td>
</tr>
<tr>
  <th>W</th>
  <td>λx.λy.x y y</td>
  <td>λ λ 1 0 0</td>
  <td>λ<sup>2</sup>α<sup>2</sup>τ<sub>1</sub>τ<sub>0</sub>τ<sub>0</sub></td>
</tr>
<tr>
  <th>S</th>
  <td>λx.λy.λz.x z (y z)</td>
  <td>λ λ λ 2 0 (1 0)</td>
  <td>λ<sup>3</sup>α<sup>2</sup>τ<sub>2</sub>τ<sub>0</sub>ατ<sub>1</sub>τ<sub>0</sub></td>
</tr>
<tr>
  <th>Ω</th>
  <td>(λx.x x) (λx.x x)</td>
  <td>(λ 0 0) (λ 0 0)</td>
  <td>αλατ<sub>0</sub>τ<sub>0</sub>λατ<sub>0</sub>τ<sub>0</sub></td>
</tr>
</table>

To get the LCλ<sup>2</sup>τ<sub>0</sub>α<sup>2</sup> syntax:

1. Eliminate significant parentheses from de Bruijn syntax by changing application to use the prefix-operator *α* (alpha) instead of juxtaposition.

3. Eliminate significant spaces by transforming each de Bruijn index *n* into *τ<sub>n</sub>*. E.g.
  * *0* becomes *τ<sub>0</sub>*,
  * *5* becomes *τ<sub>5</sub>*,
  * etc.

2. Use superscripts to run-length encode more than one consecutive lambda and alpha. E.g.:
  * *λ λ λ* becomes *λ<sup>3</sup>*, 
  * *α α α α α* becomes *α<sup>5</sup>*, 
  * etc.

<!-- todo: make these labels uniform thru the document -- make sure they are not messed up -->

The LCλ<sup>2</sup>τ<sub>0</sub>α<sup>2</sup> label signifies that the syntax: 

* uses λ as the prefix abstraction operator, with run-length encoding (<sup>2</sup>),
* uses τ as the prefix for de Bruijn indices, indexing from 0 (<sub>0</sub>), making it name-free and space-free, 
* uses α as the prefix application operator (making it paren-free), with run-length encoding (<sup>2</sup>).

For an example of how this syntax can be combined with the conventional one, the Y combinator, i.e.:

$$λf.(λx.f (x x)) (λx.f (x x))$$

can be rendered as:

$$
\begin{aligned}
Y = \lambda_f \alpha \\
& \lambda \alpha \,\tau_f\,(\alpha \tau_0 \tau_0) \\
& \lambda \alpha \,\tau_f\,(\alpha \tau_0 \tau_0)
\end{aligned}
$$

naming the *f* variable ($\lambda_f$) and then using $\tau_f$ rather than $\tau_1$ to refer to it. Also, redundant parens and formatting are added for clarity.

The described syntaxes may be useful:

* as a tool of thought, 
* for learning and teaching lambda calculus, 
* for communicating through papers and articles, 
* for use in software such as parsers, generators, translators, 
* for handwritten notes.

And for a bit of humor, here is how to encode UWU:

$$UWU = α^2λατ_0τ_0λ^2τ_1τ_0τ_0λατ_0τ_0$$

# References

1. <a name="debruijn"></a> [de Bruijn, Nicolaas Govert](https://en.wikipedia.org/wiki/Nicolaas_Govert_de_Bruijn) (1972). ["Lambda Calculus Notation with Nameless Dummies: A Tool for Automatic Formula Manipulation, with Application to the Church-Rosser Theorem"](http://alexandria.tue.nl/repository/freearticles/597619.pdf) (PDF). [Indagationes Mathematicae](https://en.wikipedia.org/wiki/Indagationes_Mathematicae). 34: 381–392. ISSN [0019-3577](https://www.worldcat.org/issn/0019-3577). [Archived](https://web.archive.org/web/20110520163316/http://alexandria.tue.nl/repository/freearticles/597619.pdf) (PDF) from the original on 2011-05-20.

3. <a name="tromp"></a> [Tromp, John](https://en.wikipedia.org/wiki/John_Tromp) (2023). ["Functional Bits: Lambda Calculus based
Algorithmic Information Theory"](https://tromp.github.io/cl/LC.pdf) (PDF).
