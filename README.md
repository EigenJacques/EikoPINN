# EikoPINN
![Static Badge](https://img.shields.io/badge/Paper%20-%20Paper?label=MDPI&link=https%3A%2F%2Fwww.mdpi.com%2F2297-8747%2F28%2F2%2F62)


**A Physics Informed Neural Network (PINN) implementation that solves the Eikonal equations towards wall distance function approximation in fluid simulations.**

This is a module, implimented in python for use in conjunction with [HeartPINN](https://github.com/EigenJacques/HeartPINN-2) to simulate turbulent blood flow on a 2 dimensional domain. 

## The relevance of wall distance in fluid simulation
Turbulence closure models for Reynolds averaged Navier Stokes (RANS) simulations require the calculation of normal distance from wall boundary conditions. 

For example; Prandtl's mixing length theory [1] defines the turbulent viscosity $\mu_t$ as:
```math
\mu_t(x) = \rho(l_m(x))^2\sqrt{G(x)}
``` 
where $l_m$ is the mixing length and $G$ is the modulus of the mean squared strain-rate-tensor. 

Various formulations of the mixing length are possible. One example is the formulation by an NVIDIA team, Henningh et al [2]. 
```math
l_m(x) = min[0.419d(x) , 0.09d_{max}]
``` 

This can be an expensive calculation when following a naive approach such as a brute force nearest point search. This is especially true when the domain is discretised with a large number of evaluation points. 

Instead, modern fluid dynamic solvers follow an alternative approach by solving an Euler like transport equation on the computational domain. The transport equation and boundary conditions are formulated such that the solution approximates the true normal wall distance. This is a particularly elegant solution since minimal additional complexity is introduced in the code. A fluid dynamic solver already has all the tools implemented to perform this calculation. 

## The Eikonal equation
The mixing length $l_m$ is a function of the normal distance from the nearest wall $d$. A signed distance function representation of the wall distance was computed by solving a Poisson-type equation on the same simulation domain, as proposed by Spalding [3]. A level set function $L$ was found by solving the Poisson equation
```math
\nabla^2L = Cs
```
with boundary conditions
```math
L = 0 \ \ on \ \ \partial \Omega_{wall}
```
```math
\frac{\partial L}{\partial \overline{n}} \ \ on \ \ \partial \Omega_{other}
```
where $C = -1$ and $\overline{n}$ is the boundary normal vector. The normal wall distance d is then computed as.
```math
d = \pm\sqrt{ \sum_{i=1,2}(\frac{\partial L}{x_i})^2} + \sqrt{\sum_{i=1,2}(\frac{\partial L}{x_i})^2 + 2L}
```
where $x_i$ is the $i^{th}$ spatial dimension.

## Preliminaries


## Example 


## Further reading


## References
[1] Versteeg, H.K. and Malalasekera, W.: An Introduction to Computational
Fluid Dynamics: The Finite Volume Method, chap. 3, p. 69. Pearson Educa-
tion Limited, 2007. ISBN 9780131274983.
Available at: https://books.google.co.za/books?id=RvBZ-UMpGzIC

[2] Hennigh, O., Narasimhan, S., Nabian, M.A., Subramaniam, A., Tang-
sali, K., Fang, Z., Rietmann, M., Byeon, W. and Choudhry, S.: NVIDIA
SimNetTM: An AI-Accelerated Multi-Physics Simulation Framework.
Lecture Notes in Computer Science (including subseries Lecture Notes in Ar-
tificial Intelligence and Lecture Notes in Bioinformatics), vol. 12746 LNCS,
pp. 447–461, 2021. ISSN 16113349. 2012.07938.

[3] Spalding, D.: 10th international heat transfer conference. Brighton,
UK, 1993. (unpublished).

J. D. Smith, K. Azizzadenesheli and Z. E. Ross, "EikoNet: Solving the Eikonal Equation With Deep Neural Networks," in IEEE Transactions on Geoscience and Remote Sensing, vol. 59, no. 12, pp. 10685-10696, Dec. 2021, doi: 10.1109/TGRS.2020.3039165.
keywords: {Mathematical model;Training;Receivers;Neural networks;Computational modeling;Position measurement;Deep learning;Geophysics;partial differential equations (PDEs);ray tracing;travel time},





