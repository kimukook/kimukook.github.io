---
layout: default
title: "Probabilistic Search Theory for Randomly Moving Targets"
---
# Search Theory for Moving Targets

## Motivation

Search problems are common in both military and civilian domains—from rescuing missing persons, pets or wreckage like MH370 (non-evasive randomly moving targets), to tracking fugitives or foraging animals (evasive randomly moving targets). Unfortunately, many traditional methods are limited in adaptability and struggle in dynamic or uncertain environments. **Figure 1a and 1b** below showcase the real-world examples illustrating these challenges:

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
The search problem has been widely studied [^1].


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
[1^] Chris Phelps, Qi Gong, Johannes O. Royset, Claire Walton, and Isaac Kaminer. Consistent approximation of a nonlinear optimal control problem with uncertain parameters. Automatica, 50(12):2987–2997, 2014.
