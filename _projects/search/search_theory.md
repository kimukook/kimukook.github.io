---
layout: project
title: "Probabilistic Search for Randomly Moving Targets"
read_time: 8–10 minutes
permalink: /projects/search-theory/
category: main
spotlight_order: 1
spotlight: true
summary: This project develops a novel and efficient mathematical framework for the control of multiple autonomous searchers tasked with locating an unseen, random moving target, whose movement may be non-evasive or evasive. At the core of this approach is the concept of \emph{Adaptive Observation}, a closed-loop probabilistic search strategy that comprises two intertwined components, estimation (of where the object may be) and control (of the trajectory of searchers). The estimation task involves modeling the moving target's likely position as a stochastic process, using a forced Fokker-Planck formulation, accounting for uncertainty in both the target's initial position and its assumed limitations on its dynamics. The control task involves decision-making and coordination of multiple searchers as they scan their surroundings to locate the target.
media: /assets/search/periodic_traj.mp4
---
<h1 class="highlight">Overview</h1>
This project aims to optimize controls of autonomous agents searching for randomly moving targets (non-evasive and evasive). Computational frameworks are proposed to iteratively confine control strategies, balancing the information gathering and agents mobility. We present three complementary developments: (i) <a href="#part1">a continuous-discrete observation framework</a>, (ii) <a href="#part2">a time-periodic search strategy tailored for non-evasive targets</a>, and (iii) <a href="#part3">a collaborative search approach for tracking evasive targets</a>. An example of probabilistic search, on finding the lost pet, is shown in Figure 1 below.
<div class="center">
  <div class="image-full">
    <img src="/assets/search/Search_project_scenario.svg" alt="Search flowchart" width="600px">
    <div class="caption">
      Figure 1. An illustration of the probabilistic search problem. A drone acts as the searcher, actively observing the environment while moving. The target, a lost pet whose position is unknown to the drone, moves randomly in the field. The searcher's actions adapt based on observations made along its path to infer the target's location.
    </div>
  </div>
</div>
**Keywords:** Probabilistic search theory · Stochastic dynamics · PDE-constrained optimization · Adjoint analysis

## Motivation
Search problems are common in both military and civilian domains—from rescuing missing persons, pets or wreckage like MH370 (non-evasive randomly moving targets), to tracking fugitives or foraging animals (evasive randomly moving targets). Unfortunately, many traditional methods are limited in adaptability and struggle in uncertain environments. Figure 2a and 2b below showcase the real-world challenges, even just for a stationary target shown in Figure 2a, often resorting to predetermined or exhaustive sweeps.
<div class="image-pair">
  <div class="image-box">
    <img src="/assets/search/lawnmower.jpeg" alt="Lawnmower trajectory">
    <div class="caption">
      Figure 2a. Lawnmower trajectory used to search for the missing $109M F-35B fighter jet in 2023. 
      <a href="https://x.com/flightradar24/status/1703827299412455459?lang=en">Image source</a>
    </div>
  </div>
  <div class="image-box">
    <img src="/assets/search/search_MH370.png" alt="MH370 search">
    <div class="caption">
      Figure 2b. Searching for the debris of MH370. 
      <a href="https://mh370.radiantphysics.com/2025/03/31/update-on-the-search-for-mh370/">Image source</a>
    </div>
  </div>
</div>

## Key challenges in theory
Previous state-of-the-art work in probabilistic search has several limitations:

- <a href="#ref1">Phelps et al. \[2014\]</a> considers only uncertainty in the target's initial location, neglecting uncertainty in its motion;
- <a href="#ref2">Hellman \[1970\]</a> focuses on optimizing search trajectories, but ignores dynamic feasibility of searchers;
- <a href="#ref3">Ohsumi \[1991\]</a> introduces dynamic programming for optimal control, but is computationally intensive and impractical for complex models;

In contrast, the computational frameworks developed in this project will not only tackle the aforementioned challenges, but will also propose modeling for non-evasive target, or even <em>evasive</em>.
<div class="section-divider"></div>

# Methodology and Numerical Results
The crux of this project is <em><strong>adaptive observation</strong></em>, a framework that couples estimation and control. The estimation task involves modeling the moving target’s likely position as a stochastic process, accounting for the uncertainty in both its initial location and dynamics. The control task involves decision-making and coordination of searchers as they scan their surroundings to locate the target. Crucially, these two components are organically coupled: searchers’ observations not only inform the evolving estimate of the target’s location, but also respond to it, forming a “feedback loop” that iteratively drives both estimation and control tasks. This idea is illustrated in Figure 3 below.
<div class="center">
  <div class="image-full">
    <img src="/assets/search/Search_flowchart_math.svg" alt="Search flowchart" width="600px">
    <div class="caption">
      Figure 3. Schematic of the <em>search process</em> in discrete time. The <span style="color: red;">red</span> lines highlights the core feedback loop: searchers’ observations inform the estimate (i.e., the probability density function of the target), which in turn updates searchers' controls (and consequently, the trajectories). This project developed the result in continuous-time, while the diagram is shown in discrete-time for illustration purposes only.
    </div>
  </div>
</div>
In this homepage, we focus on showcasing numerical results. For detailed mathematical background—including the modeling of the target's motion via stochastic differential equations, the evolution of the target’s probability density function (PDF) using Fokker-Planck equation, and the formulation of the optimal control problem—please click the blue section titles below for more details.

<h2  class="highlight"><a href="/projects/search-theory/part1">Part 1 Continuous-discrete observation</a></h2>
We first consider a hybrid search framework in which the target's motion evolves continuously in time, while observations are made at discrete time steps. The core challenge lies in optimizing searcher controls under uncertainty while accounting for the evolving probability density function (PDF) of the target’s position.

<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/search/hybrid_traj.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray; text-align: left;">
    <strong>Figure 4.</strong> Real-time animation of two autonomous searchers performing hybrid search. The searcher trajectories are shown in <span style="color:rgb(0, 114, 189);">blue</span> and <span style="color:rgb(217, 83, 25);">orange</span>, with planned trajectories in lighter dotted lines in the horizon. The grayscale background illustrates the evolving probability density function (PDF) of the target’s location: darker regions (close to searchers) indicate lower probability (suppressed by searchers' observation), while lighter regions (far from searchers) represent areas of higher uncertainty and likelihood of target presence. The adaptive control strategy drives the searchers to iteratively explore and shape the PDF landscape (exploring lighter regions) in pursuit of the hidden target.
  </figcaption>
</figure>

<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/search/hybrid_control.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray; text-align: left;">
    <strong>Figure 5.</strong> Time evolution of control inputs for the two autonomous searchers. The top and bottom panels correspond to Agent 1 and Agent 2, respectively. Solid curves represent the executed control inputs $\mathrm{u}_1$, $\mathrm{u}_2$ applied over time, while the lighter dashed lines indicate the planned control trajectories within each predictive horizon. These results illustrate how hybrid search dynamically adjusts control strategies in response to updated PDF of target position.
  </figcaption>
</figure>

<h2 class="highlight"><a href="/projects/search-theory/part2">Part 2 Optimized periodic orbits</a></h2>
Inspired by the periodic-like trajectories obtained from optimizing hybrid search strategy as shown in Figure 4 above, <a href="#ref4">Zhao and Bewley \[2025\]</a> investigates a periodic search strategy for randomly moving targets. By optimizing the controls—and thus periodic trajectories—of multiple autonomous agents, the approach efficiently shapes the long-term probability landscape to maximize detection rate under uncertainty.

<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/search/periodic_opt.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray; text-align: left;">
    <strong>Figure 6.</strong>  Results of optimized periodic search strategy with three autonomous agents. Top-left: optimized periodic trajectories of the searchers in <span style="color:rgb(0, 114, 189);">blue</span>, <span style="color:rgb(217, 83, 25);">orange</span>, and <span style="color:rgb(237, 177, 32);">yellow</span>. Top-right: convergence of the objective functional, and periodic constraint over iterations, indicating successful adjoint-based optimization. Bottom-left: optimized control inputs $u_1$ and $u_2$ for each agent across one period. Bottom-right: validation of time-periodicity using the trajectory mismatch metric $\gamma(t)$, along with its time-averaged integral. The dashed traces represent previous iterations, and the red horizontal line marks the convergence target. These results demonstrate the effectiveness of time-periodic orbit design for persistent probabilistic search.
  </figcaption>
</figure>

<figure style="text-align: center">
  <video autoplay loop muted playsinline width="600">
    <source src="/assets/search/periodic_traj.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <figcaption style="color: gray; text-align: left;">
    <strong>Figure 7.</strong> Three autonomous searchers executing periodic search trajectories, shown in <span style="color:rgb(0, 114, 189);">blue</span>, <span style="color:rgb(217, 83, 25);">orange</span>, and <span style="color:rgb(237, 177, 32);">yellow</span>. The grayscale background depicts the evolving probability density function (PDF) of the target’s location: darker regions near searchers represent suppressed likelihood due to the search effect, while lighter regions indicate higher probability areas where the target is more likely to reside. The coordinated periodic motion helps maintain spatial coverage and adaptively sculpts the uncertainty landscape over time.
  </figcaption>
</figure>

<a id="part3"></a>
## [Part 3 Collaborative search strategy]({{ site.baseurl }}/projects/search-theory/part3)
Under construction

## Part 4 Probabilistic search for grid-based Bayesian estimation exploiting sparsity
Theory and code under development...
<div class="section-divider"></div>

# Conclusion
We presents principled frameworks for optimizing controls of autonomous agents searching for randomly movingtargets. This project concludes:
- The proposed framework can efficiently locate the unseen target even under mobile uncertainty;
- There is enough control authority for optimizing searchers controls (and thus, trajectories), and the proposed adjoint analysis can guide the control synthetics;
- The proposed periodic and collaborative search strategy can efficiently find the evasive target, balancing the spatial coverage with control efficiency.

Numerical results demonstrate fast convergence of the objective and control inputs, as well as successful periodicity enforcement via adjoint-based gradient optimization. This approach is particularly well-suited for long-duration, passive monitoring tasks such as rescue-and-save missions, persistent surveillance, and environmental monitoring.

## References
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
    <a href="https://projecteuclid.org/journals/annals-of-mathematical-statistics/volume-41/issue-5/On-the-Effect-of-a-Search-Upon-the-Probability-Distribution/10.1214/aoms/1177696816.full">
      <em>On the effect of a search upon the probability distribution of a target whose motion is a diffusion process</em>
    </a>. 
    The Annals of Mathematical Statistics 41.5 (1970): 1717-1724.
  </li>
  
  <li id="ref3">
    Akira Ohsumi. 
    <a href="https://onlinelibrary.wiley.com/doi/abs/10.1002/1520-6750%28199108%2938%3A4%3C531%3A%3AAID-NAV3220380407%3E3.0.CO%3B2-L" target="_blank">
      <em>Optimal search for a Markovian target</em>
    </a>. 
    Naval Research Logistics (NRL), 38(4):531–554, 1991.
  </li>
  
  <li id="ref4">
    Muhan Zhao and Thomas R. Bewley, 
    <a href="http://robotics.ucsd.edu/pubs/ZB_periodic_search.pdf">
    <em>Probabilistic search for randomly moving targets using optimized time-periodic orbits</em></a>, 
    under review at Automatica since Feb. 2025.
  </li>
</ol>
