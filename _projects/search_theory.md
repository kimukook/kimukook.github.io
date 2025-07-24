---
layout: project
title: "Probabilistic Search for Randomly Moving Targets"
---
# Overview

This project focuses on adaptive control of autonomous agents searching for randomly moving targets. This project proposes computational frameworks that iteratively confine control strategies balancing the information gathering and agents mobility. As such, we present three complementary developments: (i) <a href="#part1">a continuous-discrete observation framework</a>, (ii) <a href="#part2">a time-periodic search strategy tailored for non-evasive targets</a>, and (iii) <a href="#part3">a collaborative search approach for tracking evasive targets</a>.

**Keywords:** Probabilistic search theory · Stochastic dynamics · PDE-constrained optimization · Adjoint analysis

The crux of this project is <em><strong>adaptive observation</strong></em>, a framework that couples estimation and control. The estimation task involves modeling the moving target’s likely position as a stochastic process, accounting for the uncertainty in both its initial location and dynamics. The control task involves decision-making and coordination of searchers as they scan their surroundings to locate the target. Crucially, these two components are organically coupled: searchers’ observations not only inform the evolving estimate of the target’s location, but also respond to it, forming a “feedback loop” that iteratively drives both estimation and control tasks. This idea is illustrated in Figure 1 below.
<div class="center">
  <div class="image-full">
    <img src="/assets/Search_flowchart_math.svg" alt="Search flowchart" width="600px">
    <div class="caption">
      Figure 1. Discrete-time flow chart of <em>search process</em>. Note that discrete-time flow is for illustration purposes   only; the actual work is conducted in continuous-time.
    </div>
  </div>
</div>

## Motivation

Search problems are common in both military and civilian domains—from rescuing missing persons, pets or wreckage like MH370 (non-evasive randomly moving targets), to tracking fugitives or foraging animals (evasive randomly moving targets). Unfortunately, many traditional methods are limited in adaptability and struggle in dynamic or uncertain environments. Figure 2a and 2b below showcase the real-world examples illustrating these challenges, often resorting to predetermined or exhaustive sweeps.

<div class="image-pair">
  <div class="image-box">
    <img src="/assets/lawnmower.jpeg" alt="Lawnmower trajectory">
    <div class="caption">
      Figure 2a. Lawnmower trajectory used to search for the missing F-35B fighter jet. 
      <a href="https://x.com/flightradar24/status/1703827299412455459?lang=en">Image source</a>
    </div>
  </div>
  <div class="image-box">
    <img src="/assets/searh_MH370.png" alt="MH370 search">
    <div class="caption">
      Figure 2b. Searching for the debris of MH370. 
      <a href="https://mh370.radiantphysics.com/2025/03/31/update-on-the-search-for-mh370/">Image source</a>
    </div>
  </div>
</div>

## Key challenges
Previous state-of-the-art work in probabilistic search has several limitations:

- <a href="#ref1">Phelps et al. \[2014\]</a> considers only uncertainty in the target's initial location, neglecting uncertainty in its motion;
- <a href="#ref2">Hellman \[1972\]</a> focuses on optimizing search trajectories, but ignores dynamic feasibility of searchers;
- <a href="#ref3">Ohsumi \[1991\]</a> introduces dynamic programming for optimal control, but is computationally intensive and impractical for complex models;

In contrast, this project develops novel and efficient mathematical frameworks for the control of multiple autonomous
searchers tasked with locating an unseen, randomly moving target, whose motion may be <em>non-evasive</em>, or even <em>evasive</em>.

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
  <figcaption style="color: gray; font-style: italic;">
    <strong>Figure 3.</strong> Animated illustration of target motion and searcher trajectories. The red and blue curves represent the searchers, while the yellow, purple, and green paths denote the traditional, non-evasive, and evasive targets, respectively.
  </figcaption>
</figure>

It is well known that the PDF of a target whose motion is governed by a SDE satisfies Fokker-Planck equation <a href="#ref5"> Jazwinski \[2013\]</a>. In this work, we extend this classical result by proposing a <em><strong>forced Fokker-Planck equation</strong></em> that captures the time evolution of PDF under the influence of search \[see (2) below\]. The derivation of (2) follows the approach outlined in Theorem 1 of <a href="#ref6">Hellman \[1970\]</a>.
<div style="text-align: center;">
  $$ \frac{\partial p}{\partial t} - \nabla\cdot\big(D\cdot\nabla p + p\, \nabla\cdot D - \mathrm{v}\,p\big) = p\, \bigg(\int_\Omega \phi\, p\,\mathrm{d}\mathrm{x} - \phi\bigg), \tag{2} $$
</div>
here $\phi(\mathrm{x}, t)$ is the instantaneous search density function \[see <a href="#ref7"> Zhao and Bewley \[2025\]</a>]. Finally, we conclude this section by highlighting the core assumption made regarding the target dynamics in <a href="#ref7"> Zhao and Bewley \[2025\]</a>.

**Assumption**
In the absence of searchers, the PDF of target's position is statistically stationary.

<div class="section-divider"></div>

# Methodology and Numerical Results
<a id="part1"></a>
## Part 1 Probabilistic search with continuous-discrete observation
We consider a hybrid search framework in which the target's motion evolves continuously in time, while observations are made at discrete time steps. The core challenge lies in optimizing searcher controls under uncertainty while accounting for the evolving probability density function (PDF) of the target’s position.
### Problem formulation
This hybrid system is governed by:
- A Fokker-Planck equation modeling the time evolution of the PDF $p(\mathrm{x}, t)$,
<div style="text-align: center;">
$$
\frac{\partial p}{\partial t} - \nabla\cdot\big(D\cdot\nabla p + p\, \nabla\cdot D - \mathrm{v}\,p\big) = 0,
$$
</div>
- Searchers' dynamics $\dot{\mathrm{q}}_m(t) = \mathrm{g}_m(\mathrm{q}_m, \mathrm{u}_m)$, for $m=1,\ldots,M$,
- A Bayesian rule updating the information collected by searchers at each observation time $t_k$,
<div style="text-align: center;">
$$
\phi({\bf x},\, t_k) = \prod_{m=1}^M\phi_m({\bf x},\, t_k), \quad \phi_m({\bf x},\, t_k) = 1 - \alpha_m\, \exp\big(-\beta_m\, \| {\bf x} - E_m\, {\bf q}_m(t_k)\|^2 \big),
$$
</div>
- An objective functional that maximizes the probability of finding the target while penalizing control efforts
<div style="text-align: center;">
$$
J = \left( \int_\Omega \bigl[ p^+({\bf x},\, t_f) \bigr]^2\, \mathrm{d}{\bf x} \right)^{\frac12} + \int_0^{t_f} \sum_{m=1}^M {\bf u}_m^T\, R_m\, {\bf u}_m\, \mathrm{d}t
$$
</div>

### Numerical results
<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/hybrid_traj.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray; font-style: italic;">
    <strong>Figure 4.</strong> Animated illustration of hybrid search, searchers' trajectories and evolution of PDF.
  </figcaption>
</figure>

<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/hybrid_control.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray; font-style: italic;">
    <strong>Figure 4.</strong> Animated illustration of hybrid search, searchers' control inputs.
  </figcaption>
</figure>

<a id="part2"></a>
## Part 2 Probabilistic search using optimized periodic orbits
<a id="part3"></a>
## Part 3 Probabilistic search and collaborative search strategy


# References

<ol>
  <li id="ref1">
    Chris Phelps, Qi Gong, Johannes O. Royset, Claire Walton, and Isaac Kaminer. 
    <a href="https://www.sciencedirect.com/science/article/pii/S0005109814004063" target="_blank">
      <em>Consistent approximation of a nonlinear optimal control problem with uncertain parameters</em>
    </a>. 
    Automatica, 50(12):2987–2997, 2014.
  </li>

  <li id="ref2">
    Olavi Hellman. 
    <a href="https://www.jstor.org/stable/2099690" target="_blank">
      <em>On the optimal search for a randomly moving target</em>
    </a>. 
    SIAM Journal on Applied Mathematics, 22(4):545–552, 1972.
  </li>

  <li id="ref3">
    Akira Ohsumi. 
    <a href="https://onlinelibrary.wiley.com/doi/abs/10.1002/1520-6750%28199108%2938%3A4%3C531%3A%3AAID-NAV3220380407%3E3.0.CO%3B2-L" target="_blank">
      <em>Optimal search for a Markovian target</em>
    </a>. 
    Naval Research Logistics (NRL), 38(4):531–554, 1991.
  </li>

  <li id="ref4">
    B. L. Hanson, M. Zhao and T. R. Bewley, 
    <a href="https://www.tandfonline.com/doi/full/10.1080/03610926.2024.2439999">
    <em>An extensible framework for the probabilistic search of stochastically-moving targets characterized by generalized Gaussian distributions or experimentally-defined regions of interest</em></a>, 
    submitted to Automatica, 2025.
  </li>

  <li id="ref5">
    Jazwinski, Andrew H, 
    <em>Stochastic processes and filtering theory.</em>, 
    Courier Corporation, 2013.
  </li>

   <li id="ref6">
    Hellman, Olavi, 
    <a href="[https://www.tandfonline.com/doi/full/10.1080/03610926.2024.2439999](https://projecteuclid.org/journals/annals-of-mathematical-statistics/volume-41/issue-5/On-the-Effect-of-a-Search-Upon-the-Probability-Distribution/10.1214/aoms/1177696816.full)">
    <em>On the effect of a search upon the probability distribution of a target whose motion is a diffusion process.</em></a>, 
    The Annals of Mathematical Statistics 41.5 (1970): 1717-1724.
  </li>
  
  <li id="ref7">
    M. Zhao and T. Bewley, 
    <a href="http://robotics.ucsd.edu/pubs/ZB_periodic_search.pdf">
    <em>Probabilistic search for randomly moving targets using optimized time-periodic orbits</em></a>, 
    submitted to Automatica, 2025.
  </li>
</ol>
