---
layout: post
title:  "Estimating regional SNP-heritability using HESS"
date:   2018-05-10
category: heritability
tags: [summary statics]
---

<script type="text/javascript" async
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

### Summary

A recent [preprint](https://www.biorxiv.org/content/early/2018/05/10/318618)
by Benner et al. compared the performance between BOLT-REML, FINEMAP, and HESS
in estimating regional SNP-heritability, and showed that HESS was severely
biased under various simulation settings. In this blog post, I hope to explain
why HESS yielded biased estimates under simulations outlined by Benner et al.,
and highlight best practices for running HESS.

### Brief overview of HESS

HESS is a method to estimate regional SNP-heritability using GWAS summary statistics
under the fixed-effect model, \\( y = \mathbf{x}^T\mathbf{\beta} + \epsilon\\),
where the true effect size vector \\( \mathbf{\beta} \\) is treated as a fixed
constant. Under the fixed-effect model, heritability is defined as
\\( \mathbf{\beta}^T \mathbf{V} \mathbf{\beta} \\), where \\( \mathbf{V} \\)
is the LD matrix. In the simple scenario, where there is only one region HESS
estimates region SNP-heritability as
\\[
    \
\\]

### Conclusion
