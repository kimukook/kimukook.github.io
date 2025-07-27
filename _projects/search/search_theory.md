---
layout: project
title: "Probabilistic Search for Randomly Moving Targets"
read_time: 15–18 minutes
permalink: /projects/search-theory/
category: main
summary: Advancing and optimizing adaptive control strategies to rapidly locate randomly moving targets, whether non-evasive or evasive
---
# Overview

This project focuses on adaptive control of autonomous agents searching for randomly moving targets. This project proposes computational frameworks that iteratively confine control strategies balancing the information gathering and agents mobility. As such, we present three complementary developments: (i) <a href="#part1">a continuous-discrete observation framework</a>, (ii) <a href="#part2">a time-periodic search strategy tailored for non-evasive targets</a>, and (iii) <a href="#part3">a collaborative search approach for tracking evasive targets</a>.

**Keywords:** Probabilistic search theory · Stochastic dynamics · PDE-constrained optimization · Adjoint analysis

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
    <img src="/assets/search_MH370.png" alt="MH370 search">
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

<div class="section-divider"></div>

# Methodology and Numerical Results

The crux of this project is <em><strong>adaptive observation</strong></em>, a framework that couples estimation and control. The estimation task involves modeling the moving target’s likely position as a stochastic process, accounting for the uncertainty in both its initial location and dynamics. The control task involves decision-making and coordination of searchers as they scan their surroundings to locate the target. Crucially, these two components are organically coupled: searchers’ observations not only inform the evolving estimate of the target’s location, but also respond to it, forming a “feedback loop” that iteratively drives both estimation and control tasks. This idea is illustrated in Figure 3 below.
<div class="center">
  <div class="image-full">
    <img src="/assets/Search_flowchart_math.svg" alt="Search flowchart" width="600px">
    <div class="caption">
      Figure 3. Discrete-time flow chart of <em>search process</em>. Note that the discrete-time flow is for illustration purposes only; the actual work is conducted in continuous-time.
    </div>
  </div>
</div>

We simply show numerical results in this general page, for more mathemetical background, inter alia, the model setup for randomly moving targets using stochastic differential equation, the probability density function of target position, and the optimal control problem formulation, click the sub-titles in blue below to see more detailed info. 
<a id="part1"></a>

## [Part 1 Probabilistic search with continuous-discrete observation]({{ site.baseurl }}/projects/search-theory/part1)

We first consider a hybrid search framework in which the target's motion evolves continuously in time, while observations are made at discrete time steps. The core challenge lies in optimizing searcher controls under uncertainty while accounting for the evolving probability density function (PDF) of the target’s position.

### Numerical results
<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/hybrid_traj.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray;">
    <strong>Figure 4.</strong> Real-time animation of two autonomous searchers performing hybrid search. The searcher trajectories are shown in <span style="color:rgb(0, 114, 189);">blue</span> and <span style="color:rgb(217, 83, 25);">orange</span>, with planned trajectories in lighter dotted lines in the horizon. The grayscale background illustrates the evolving probability density function (PDF) of the target’s location: darker regions indicate lower probability (suppressed by proximity to searchers), while lighter regions represent areas of higher uncertainty and likelihood of target presence. The adaptive control strategy drives the searchers to iteratively explore and shape the PDF landscape in pursuit of the hidden target.
  </figcaption>
</figure>

<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/hybrid_control.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray;">
    <strong>Figure 5.</strong> Time evolution of control inputs for the two autonomous searchers. The top and bottom panels correspond to Agent 1 and Agent 2, respectively. Solid curves represent the executed control inputs $\mathrm{u}_1$, $\mathrm{u}_2$ applied over time, while the lighter dashed lines indicate the planned control trajectories within each predictive horizon. These results illustrate how hybrid search dynamically adjusts control strategies in response to updated PDF of target position.
  </figcaption>
</figure>

<a id="part2"></a>
## [Part 2 Probabilistic search using optimized periodic orbits]({{ site.baseurl }}/projects/search-theory/part2)

Inspired by the periodic-like trajectories obtained from optimizing hybrid search strategy as shown in Figure 4 above, <a href="#ref7">Zhao and Bewley \[2025\]</a> investigates a periodic search strategy for randomly moving targets. By optimizing the controls—and thus periodic trajectories—of multiple autonomous agents, the approach efficiently shapes the long-term probability landscape to maximize detection rate under uncertainty.

### Numerical results
<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/periodic_opt.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray;">
    <strong>Figure 6.</strong>  Results of optimized periodic search strategy with three autonomous agents. Top-left: optimized periodic trajectories of the searchers in <span style="color:rgb(0, 114, 189);">blue</span>, <span style="color:rgb(217, 83, 25);">orange</span>, and <span style="color:rgb(237, 177, 32);">yellow</span>. Top-right: convergence of the objective functional, and periodic constraint over iterations, indicating successful adjoint-based optimization. Bottom-left: optimized control inputs $u_1$ and $u_2$ for each agent across one period. Bottom-right: validation of time-periodicity using the trajectory mismatch metric $\gamma(t)$, along with its time-averaged integral. The dashed traces represent previous iterations, and the red horizontal line marks the convergence target. These results demonstrate the effectiveness of time-periodic orbit design for persistent probabilistic search.
  </figcaption>
</figure>

<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/periodic_traj.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray;">
    <strong>Figure 7.</strong> Three autonomous searchers executing periodic search trajectories, shown in <span style="color:rgb(0, 114, 189);">blue</span>, <span style="color:rgb(217, 83, 25);">orange</span>, and <span style="color:rgb(237, 177, 32);">yellow</span>. The grayscale background depicts the evolving probability density function (PDF) of the target’s location: darker regions represent suppressed likelihood due to nearby searchers, while lighter regions indicate higher probability areas where the target is more likely to reside. The coordinated periodic motion helps maintain spatial coverage and adaptively sculpts the uncertainty landscape over time.
  </figcaption>
</figure>

<a id="part3"></a>
## [Part 3 Probabilistic search and collaborative search strategy]({{ site.baseurl }}/projects/search-theory/part3)
Under construction

## Part 4 Probabilistic search for grid-based Bayesian estimation exploiting sparsity
Theory and code under development...

# Conclusion
This project presents principled frameworks for designing optimized time-periodic search trajectories for autonomous agents operating under uncertainty. By formulating the search task as a PDE-constrained optimization problem, we derive trajectories that repeatedly traverse the domain in a manner that minimizes uncertainty about a target's location over time. The resulting orbits are not only dynamically feasible but also information-optimal, balancing spatial coverage with control efficiency. Numerical results demonstrate fast convergence of the objective and control inputs, as well as successful periodicity enforcement via adjoint-based gradient optimization. This approach is particularly well-suited for long-duration, passive monitoring tasks such as rescue-and-save missions, persistent surveillance, and environmental monitoring.

**References**

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
    Communications in Statistics-Theory and Methods (2025): 1-26.
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
    under review at Automatica since Feb. 2025.
  </li>
</ol>
