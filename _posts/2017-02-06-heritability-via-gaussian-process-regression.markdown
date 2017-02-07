---
layout: post
title:  "Explaining Missing Heritability Using Gaussian Process Regression (Reader's Digest)"
date:   2017-02-06
category: statistics
tags: [mixed model]
---

<script type="text/javascript" async
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

### Summary

The paper "Explaining Missing Heritability Using Gaussian Process Regression" by Sharp et al.
tries to tackle the problem of missing heritability and the detection of higher-order interaction
effects through Gaussian process regression, a technique widely used in the machine learning community.
The authors obtained estimates of broad-sense heritability for a number of mice and yeast
phenotypes using a RBF kernel that models higher-order interactions, and found these estimates
significantly larger than the narrow-sense heritability of these phenotypes. The authors also
deteced several loci displaying interaction effects.

### Background

#### Heritability

In genetics, phenotypes are modeled by the following equation
\\[ y_i = f(x_i) + u_i + \epsilon_i, \\]
where \\( y_i \\) is the phenotype measurement of the i-th individual, \\( x_i \\) the genotype vector,
\\( u_i \\) a random effect term that captures relatedness among individuals, and \\( \epsilon_i \\)
the environmental noise. Here, \\( f(\cdot) \\) is a function that maps the genotype vector into
a real number. Under this model, heritability is defined the proportion of variance in \\( y_i \\)
that is due to variation of \\( f(x_i) \\),
\\[ \text{heritability} = {{\text{Var}(f(x))} \over {\text{Var}(y)}} \\]

Different flavors of heritability exist based on the complexity of the \\( f(\cdot) \\) function
and the input that goes into \\( f(\cdot) \\). In general geneticists work with four types of heritability,
as listed below.

- Broad-sense heritability (\\( H^2 \\))
