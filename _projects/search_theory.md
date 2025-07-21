---
layout: default
title: "Probabilistic Search Theory for Randomly Moving Targets"
---
# Probabilistic Search Theory for Randomly Moving Targets

## Motivation

Search problems are common in both military and civilian domains—from rescuing missing persons, pets or wreckage like MH370 (non-evasive randomly moving targets), to tracking fugitives or foraging animals (evasive randomly moving targets). Unfortunately, many traditional methods are limited in adaptability and struggle in dynamic or uncertain environments. **Figure 1a and 1b** below showcase the real-world examples illustrating these challenges, often resorting to predetermined or exhaustive sweeps.

<div class="image-pair">
  <div class="image-box">
    <img src="/assets/lawnmower.jpeg" alt="Lawnmower trajectory">
    <div class="caption">
      Figure 1a. Lawnmower trajectory used to search for the missing F-35B fighter jet. 
      <a href="https://x.com/flightradar24/status/1703827299412455459?lang=en">Image source</a>
    </div>
  </div>
  <div class="image-box">
    <img src="/assets/image-9.png" alt="MH370 search">
    <div class="caption">
      Figure 1b. Searching for the debris of MH370. 
      <a href="https://mh370.radiantphysics.com/2025/03/31/update-on-the-search-for-mh370/">Image source</a>
    </div>
  </div>
</div>


### Existing research 
Previous work in probabilistic search has several limitations:

- <a href="#ref1">Phelps et al. [2014]</a> considers only uncertainty in the initial target location, neglecting uncertainty in its motion;
- <a href="#ref2">Hellman [1972]</a> focuses on optimizing search trajectories, but ignores dynamic feasibility of searchers;
- <a href="#ref3">Ohsumi [1991]</a> introduces dynamic programming for optimal control, but is computationally intensive and impractical for complex models;


## Modeling Target Behavior

We model the motion of a target \( x(t) \in \mathbb{R}^d \) using a stochastic differential equation (SDE):

\[
dx(t) = a(x(t), t)dt + B(x(t), t)dW(t)
\]

- **Non-evasive targets** follow natural stochastic motion (e.g., diffusion).
- **Evasive targets** modify behavior based on searcher proximity, intentionally avoiding detection.
- The belief over target location is encoded in a probability density function \( p(x, t) \).

## Adaptive Observation: The Crux

The interaction between the searchers and the environment is fundamentally informational. Searchers adapt their motion not merely to explore, but to maximize information gain.

This leads to the formulation of a **forced Fokker–Planck equation (fFPE)** that governs the PDF of the target:

\[
\frac{\partial p}{\partial t} = -\nabla \cdot (a(x, t) p) + \nabla \cdot \left(D(x, t) \nabla p\right) - \text{Observation Term}
\]

Here, the last term represents the suppression of probability mass near searchers due to observation.

## Our Approach: Structured and Collaborative Search

Rather than relying on greedy or random search:

- We **optimize time-periodic orbits** for search vehicles to create persistent, structured coverage.
- Use **collaborative control** to ensure joint performance across multiple agents.

The searchers are modeled as nonholonomic unicycles, and we apply adjoint-based gradient optimization to tune their paths with respect to discovery rate objectives.

## Ongoing Work

We are extending the framework to:
- Account for dynamically changing ROIs,
- Integrate sensor heterogeneity,
- Design hybrid strategies blending exploration and exploitation.

Stay tuned for updates as we apply this framework to real-world scenarios and more challenging target dynamics.

## References

<ol>
  <li id="ref1">
    Chris Phelps, Qi Gong, Johannes O. Royset, Claire Walton, and Isaac Kaminer. <em>Consistent approximation of a nonlinear optimal control problem with uncertain parameters</em>. <a href="https://www.sciencedirect.com/science/article/pii/S0005109814004063">Automatica</a>, 50(12):2987–2997, 2014. <a href="#cite1">↩</a>
  </li>
  <li id="ref2">
    Olavi Hellman. <em>On the optimal search for a randomly moving target.</em> <a href="https://www.jstor.org/stable/2099690">SIAM Journal on Applied Mathematics</a>, 22(4):
    545–552, 1972.
  </li>
  <li id="ref3">
    Akira Ohsumi. <em>Optimal search for a markovian target.</em> <a href="https://onlinelibrary.wiley.com/doi/abs/10.1002/1520-6750%28199108%2938%3A4%3C531%3A%3AAID-NAV3220380407%3E3.0.CO%3B2-L">Naval Research Logistics (NRL)</a>, 38(4):531–554, 1991.
  </li>
  <li id="ref4">
    M. Zhao and T. Bewley, <em>Probabilistic search for randomly moving targets using optimized time-periodic orbits</em>, submitted to Automatica, 2025.
  </li>
</ol>
