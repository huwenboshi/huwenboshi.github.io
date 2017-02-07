---
layout: post
title:  "Explaining Missing Heritability Using Gaussian Process Regression (reader's digest)"
date:   2017-02-06
category: statistics
tags: [mixed model]
---

<script type="text/javascript" async
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

### Abstract

This post talks about linear mixed model -- what it is, how it's fit, and
how it's used in genetics.

### Definition

A linear mixed model is a linear model that contains both fixed effects and
random effects, and is expressed as
\\( \textbf{y} = \textbf{X}\mathbf{\beta} + \textbf{Z}\textbf{u} + \mathbf{\epsilon} \\),
where \\( \textbf{y} \\) is the response, \\( \textbf{X} \\) design matrix for
the fixed effects \\( \mathbf{\beta} \\), \\( \textbf{Z} \\) design matrix for
the random effects \\( \textbf{u} \\), and \\( \mathbf{ϵ} \\) random noise.

### Fitting algorithms

### Applications in genetics

#### Heritability estimation

#### Genome-wide association studies
