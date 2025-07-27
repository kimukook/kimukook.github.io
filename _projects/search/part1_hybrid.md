---
layout: project
title: "Part 1: Hybrid Search"
read_time: 5
permalink: /projects/search-theory/part1
---

## Modeling Framework
Readers familiar with stochastic (or search) theory can safely omit this section, and jump to results part below. 

In the existing literature, such as <a href="#ref1">Phelps et al. \[2014\]</a>, the target is typically modeled with an uncertain initial position but deterministic motion. In these formulations, the initial state is explicitly characterized by a probability density function (PDF), while the subsequent motion follows a known differential equation.

In contrast, we model the target motion as a <em>stochastic process</em> $\lbrace \mathrm{x}(t) \mid t \in \[0, t_f\]\rbrace$. The evolution of $\mathrm{x}(t)$ is described by a stochastic differential equation (SDE) \[see (1) below\]. Figure 3 provides a representative comparison between traditional target modeling approaches and the method proposed in this work.

<div style="text-align: center;">
  $$ \mathrm{d}\mathrm{x}(t) = \mathrm{v}(\mathrm{x}, t)\, \mathrm{d}t + D(\mathrm{x}, t)\, \mathrm{d} \omega(t), \tag{1} $$
</div>

here $\omega(t)$ is a vector Brownian motion process. Examples of the drift term $\mathrm{v}(\mathrm{x}, t)$ and diffusion term $D(\mathrm{x}, t)$ can be found in <a href="#ref7"> Zhao and Bewley \[2025\]</a> and are thus omitted here. 

<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/target_motion.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray;">
    <strong>Figure 2.</strong> Animated illustration of target motion and searcher trajectories. The red and blue curves represent the searchers, while the yellow, purple, and green paths denote the traditional, non-evasive, and evasive targets, respectively.
  </figcaption>
</figure>

It is well known that the PDF of a target whose motion is governed by a SDE satisfies Fokker-Planck equation <a href="#ref5"> Jazwinski \[2013\]</a>. In this work, we extend this classical result by proposing a <em><strong>forced Fokker-Planck equation</strong></em> that captures the time evolution of PDF under the influence of search \[see (2) below\]. The derivation of (2) follows the approach outlined in Theorem 1 of <a href="#ref6">Hellman \[1970\]</a>.
<div style="text-align: center;">
  $$ \frac{\partial p}{\partial t} - \nabla\cdot\big(D\cdot\nabla p + p\, \nabla\cdot D - \mathrm{v}\,p\big) = p\, \bigg(\int_\Omega \phi\, p\,\mathrm{d}\mathrm{x} - \phi\bigg), \tag{2} $$
</div>
here $\phi(\mathrm{x}, t)$ is the instantaneous search density function \[see <a href="#ref7"> Zhao and Bewley \[2025\]</a>]. Finally, we conclude this section by highlighting the core assumption made regarding the target dynamics in <a href="#ref7"> Zhao and Bewley \[2025\]</a>.

**Assumption**
In the absence of searchers, the PDF of target's position is statistically stationary.
