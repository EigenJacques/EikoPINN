# EikoPINN: Physics informed neural network implementation to solve the Eikonal equations for fluid simulation.

Turbulence closure models for Reynolds averaged Navier Stokes (RANS) simulations require the calculation of normal distance from wall boundary conditions. 
In particular, Prandtl's mixing length theory defines the turbulent viscosity $\mu_t$ as:
$$ \mu_t(x) = \rho(l_m(x))^2\sqrt{G(x)} $$
where $l_m$ is the mixing length and $G$ is the modulus of the mean squared strain-rate-tensor. 
Various formulations of the mixing length are possible, but all are a function of the normal wall distance. One example is the formulation by an NVIDIA team, Henningh et al. 
$$ l_m(x) = min[0.419d(x) , 0.09d_{max}]$$
This can be an expensive calculation when following a naive approach such as a brute force nearest point calculation. This is especially true when the domain is discretised with a large number of evaluation points. 
Instead, modern fluid dynamic solvers follow an alternative approach by solving an Euler like transport equation on the computational domain. The transport equation and boundary conditions are formulated such that the solution approximates the true normal wall distance. This is a particularly elegant solution since almost no additional complexity is introduced as a fluid dynamic solver already has all the tools implemented to perform this calculation. 

# The Eikonal equations
The mixing length lm is a function of the normal distance from the
nearest wall d. A signed distance function representation of the wall
distance was computed by solving a Poisson-type equation on the same
simulation domain, as proposed by Spalding [84]. A level set function
L was found using the Poisson equation

# Preliminaries


# Example 


# References
J. D. Smith, K. Azizzadenesheli and Z. E. Ross, "EikoNet: Solving the Eikonal Equation With Deep Neural Networks," in IEEE Transactions on Geoscience and Remote Sensing, vol. 59, no. 12, pp. 10685-10696, Dec. 2021, doi: 10.1109/TGRS.2020.3039165.
keywords: {Mathematical model;Training;Receivers;Neural networks;Computational modeling;Position measurement;Deep learning;Geophysics;partial differential equations (PDEs);ray tracing;travel time},

Hennigh, O., Narasimhan, S., Nabian, M.A., Subramaniam, A., Tang-
sali, K., Fang, Z., Rietmann, M., Byeon, W. and Choudhry, S.: NVIDIA
SimNetTM: An AI-Accelerated Multi-Physics Simulation Framework.
Lecture Notes in Computer Science (including subseries Lecture Notes in Ar-
tificial Intelligence and Lecture Notes in Bioinformatics), vol. 12746 LNCS,
pp. 447–461, 2021. ISSN 16113349. 2012.07938.

