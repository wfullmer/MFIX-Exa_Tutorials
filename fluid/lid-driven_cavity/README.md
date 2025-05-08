# Lid-driven Cavity

TODO

lid-driven cavity -- give it out so it doesn't work. first, show that the p0 from initial projection is expected 9.87...e+32. that's an identifier for developers, I.e., to easily identify if an initial pressure isn't applied somewhere. so that one's fine. but in the next line, step 1 we see velocities of order +32 as well. this is not ok. the solution has diverged before it has even begun. the problem is that the initial iterations don't see the boundary velocity and take the largest possible step, 1.+14 which, as soon as fluid motion is felt diverges instantly. There are several ways to deal with this, we will cover two methods below.
First, as mentioned, the problem is that a too large time step is taken. We could reduce the time step of the initial iterations by a user supplied factor keyword but this feature was developed to scale dt by 2 or 3, maybe 10, not 10^17. It's easier to control the actual simulation time step. even though this is a steady state problem, we still have access to limit dt through the mfix.dt_max keyword. so first, remove the initial iterations by setting mfix.initial_iterations = 0  in the inputs (note to self, this should already be in the inputs and set to 3). let's go ahead and run this now. you see that initial iterations are skipped, we get into the pseudo-time advancement and again diverge right away, again because we start with a dt of 1e+14 and just can't recover as soon as the eb BC affects the fluid. so now let's limit the max dt so we don't start with such a ridiculous first step. I'm going to use mfix.dt_max = 0.001 . now your case should run.
A second method is to key the time stepping algorithm in on the fact that we expect velocities on the order of 1m/s in the domain. Instead of using a single full-domain homogeneous IC, let's add a second, small IC close to the wall that has $u$ = 1 m/s. first we need to add this new IC to the regions list, let's call it
## post processing
### visualizing
Paraview to see u and v contours
### analysis
fextract & compare to ghia ghia & shen
## higher reynolds number
decreasing viscosity. can you increase u and get the same result?
## resolution
--- increase to to 64^2
--- parallel, set the grid to 32 x 32 and run on 4 CPUs
--- increase to 128^2
--- base 2 grids
As you know, MFIX-Exa uses AMReX under the hood. Even though we rarely use AMR capabilities, AMReX (and MFIX-Exa by extension) is a multi-level, multigrid block-structured AMR framework. The MLMG Algo has a strong preference for nice power-of-two grids. so if we want an odd number to truly get centerline data, rather than setting n_cells to 129, let's keep n_cells = 128 128 32 and either shrink the box or grow the domain. In this case, i'll choose to grow the domain, (oof this is going to be an ugly number) (edited) 


wdf - This is the diff from the file I was running from what's in your 
mfix-exa-stuff repo plus the first change to get it to run. 

14c14
< amr.blocking_factor = 4
---
> amr.blocking_factor = 16
29d28
< #amr.n_cell =  32  32  8
104c103
< mfix.regions = full-domain  top-wall  near-wall
---
> mfix.regions = full-domain  top-wall
112,114d110
< regions.near-wall.lo    =  0.0125   0.0875  0.0
< regions.near-wall.hi    =  0.0875   0.1     0.025
< 
120c116
< ic.regions = full-domain  near-wall
---
> ic.regions = full-domain
127c123
< ic.full-domain.fluid.pressure  =  0.0
---
> ic.full-domain.fluid.pressure  = 101.325e+3
129,133d124
< 
< ic.near-wall.fluid.volfrac   =  1.0
< ic.near-wall.fluid.density   =  1.0
< ic.near-wall.fluid.pressure  =  0.0
< ic.near-wall.fluid.velocity  =  1.0  0.0  0.0
