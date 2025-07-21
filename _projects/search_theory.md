---
layout: default
title: "Search Theory for Moving Targets"
permalink: /projects/search-project/
---

# Search Theory for Moving Targets

## Motivation

In a range of applications — from wildlife tracking to search-and-rescue to defense — autonomous agents are tasked with locating targets moving in uncertain ways. Unfortunately, many traditional methods are limited in adaptability and struggle in dynamic, cluttered, or ambiguous environments. Below are real-world examples illustrating these challenges:

<!-- Add your image links -->
<center>
  <img src="/assets/img/animal_tracking_example.jpg" width="70%" alt="Tracking in the wild"><br>
  <em>Example: Inefficient coverage in wildlife tracking with static patrol routes.</em>
</center>

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
