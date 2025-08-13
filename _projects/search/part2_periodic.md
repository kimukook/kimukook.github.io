---
layout: project
title: "Part 2: Periodic Search"
read_time: 5
permalink: /projects/search-theory/part2
---
Under development! 

### Problem formulation
We solve the following optimal control problem:
- The searchers dynamics is still described by the differential equation as shown in <a href="#part1">Part 1</a>.
- The evolution of target position's PDF is described by (2) above.
- We impose the periodic constraint on searchers' state vector
<div style="text-align: center;">
$$
\phi(\mathrm{q}_{m}(t_f), \mathrm{q}_{m}(0)) \triangleq \frac1{t_f}\bigl( \mathrm{q}_m(t_f) - \mathrm{q}_m(0)\bigr), \quad \phi(\mathrm{q}_{m}(t_f), \mathrm{q}_{m}(0)) = 0.
$$
</div>
- We minimize the objective functional which is a measure of maximizing the probability of finding the target during the period.
<div style="text-align: center;">
$$
J = \frac1{t_f} \int_0^{t_f} \bigl[ \sum_{m=1}^M \mathrm{u}_m^T\, R_m\, \mathrm{u}_m - \int_\Omega p(\mathrm{x}, t)\, \phi(\mathrm{x}, t)\, \mathrm{d}\mathrm{x}\bigr]\,\mathrm{d} t.
$$
</div>
