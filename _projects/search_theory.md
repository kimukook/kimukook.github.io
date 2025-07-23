---
layout: project
title: "Probabilistic Search for Randomly Moving Targets"
---
# Introduction

This project addresses the <em>probabilistic search</em> of uncertain, mobile targets by leveraging continuous-time modeling and advanced control strategies. We present three complementary developments: (i) a continuous-discrete observation framework, (ii) a time-periodic search strategy tailored for non-evasive targets, and (iii) a collaborative search approach for tracking evasive targets.

**Keywords:** Probabilistic search theory · Stochastic dynamics · PDE-constrained optimization · Adjoint analysis

The crux of this project is <em>adaptive observation</em>, a framework that couples estimation and control. The estimation task involves modeling the moving target’s likely position as a stochastic process, accounting for the uncertainty in both its initial location and dynamics. The control task involves decision-making and coordination of searchers as they scan their surroundings to locate the target. Crucially, these two components are organically coupled: searchers’ observations not only inform the evolving estimate of the target’s location, but also respond to it, forming a “feedback loop” that iteratively drives both estimation and control tasks. This idea is illustrated in Figure 1 below.
<div class="center">
  <div class="image-full">
    <img src="/assets/flow_chart_search.svg" alt="Search flowchart" width="600px">
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
    <img src="/assets/image-9.png" alt="MH370 search">
    <div class="caption">
      Figure 2b. Searching for the debris of MH370. 
      <a href="https://mh370.radiantphysics.com/2025/03/31/update-on-the-search-for-mh370/">Image source</a>
    </div>
  </div>
</div>


## Existing research
Previous state-of-the-art work in probabilistic search has several limitations:

- <a href="#ref1">Phelps et al. \[2014\]</a> considers only uncertainty in the target's initial location, neglecting uncertainty in its motion;
- <a href="#ref2">Hellman \[1972\]</a> focuses on optimizing search trajectories, but ignores dynamic feasibility of searchers;
- <a href="#ref3">Ohsumi \[1991\]</a> introduces dynamic programming for optimal control, but is computationally intensive and impractical for complex models;

In contrast, this project develops novel and efficient mathematical frameworks for the control of multiple autonomous
searchers tasked with locating an unseen, randomly moving target, whose motion may be <em>non-evasive</em>, or even <em>evasive</em>.

## Model on target motion
In existing study <a href="#ref1">Phelps et al. \[2014\]</a>, the target is typically modeled with an uncertain initial position but deterministic motion. In their formulation, accordingly, the initial state is explicitly represented by a probability density function, while the subsequent motion is governed by a known differential equation.

In contrast, we model the target motion as a <em>stochastic process</em> $\{\mathrm{x}(t) \mid t \in [0, t_f]\}$. The evolution of $\mathrm{x}(t)$ is described by a stochastic differential equation \[see (1) below\]. Figure 3 illustrates a representative example highlighting the difference between target modeling in existing approaches and our proposed method. 

<div style="display: flex; justify-content: space-between; align-items: center;">
  <div>
    $$ \mathrm{d}\mathrm{x}(t) = \mathrm{v}(\mathrm{x}, t)\, \mathrm{d}t + D(\mathrm{x}, t)\, \mathrm{d} \omega(t) $$
  </div>
  <div style="margin-left: 1em;">(1)</div>
</div>

An example of the drift term $\mathrm{v}(\mathrm{x}, t)$ and diffusion term $D(\mathrm{x}, t)$ can be found in <a href="#ref5"> Zhao and Bewley \[2025\]</a> and thus omitted here. We simply bring up the assumption made on target dynamics in <a href="#ref5"> Zhao and Bewley \[2025\]</a>.

**Assumption**
In the absence of searchers, the probability density function of target is statistically stationary.

<div class="section-divider"></div>

# Results

## Part 1 Hybrid search 
under construction
<div class="section-divider"></div>

## Part 2 Probabilistic Search using optimized periodic orbits

## Part 3 Collaborative search strategy


# References

<ol>
  <li id="ref1">
    Chris Phelps, Qi Gong, Johannes O. Royset, Claire Walton, and Isaac Kaminer. 
    <a href="https://www.sciencedirect.com/science/article/pii/S0005109814004063" target="_blank">
      <em>Consistent approximation of a nonlinear optimal control problem with uncertain parameters</em>
    </a>. 
    Automatica, 50(12):2987–2997, 2014. <a href="#cite1">↩</a>
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
    <a href="http://robotics.ucsd.edu/pubs/ZB_periodic_search.pdf">
    M. Zhao and T. Bewley, 
    <em>Probabilistic search for randomly moving targets using optimized time-periodic orbits</em></a>, 
    submitted to Automatica, 2025.
  </li>
</ol>

