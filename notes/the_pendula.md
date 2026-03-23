---
layout: page
title: The Pendula
date: 2026-03-23
permalink: /notes/the_pendula/
---

<script>
document.addEventListener("DOMContentLoaded", function () {
  window.MathJax = {
    tex: {
      inlineMath: [['$', '$'], ['\\(', '\\)']],
      displayMath: [['$$','$$']]
    },
    svg: {
      fontCache: 'global'
    }
  };

  var script = document.createElement("script");
  script.src = "https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js";
  script.async = true;
  document.head.appendChild(script);
});
</script>



The pendulum is one of the simplest mechanical systems, but its phase space
structure already shows nonlinear behavior.

Here we will study:

- equation of motion
- phase space
- exact solution
- numerical solution

This is a test inline equation: \( E = mc^2 \)

This is a displayed equation:

$$
\ddot{\theta} + \frac{g}{l} \sin\theta = 0
$$
