# Introduction

## Getting Started

Start by cloning this repo.

```
git clone https://github.com/wfullmer/MFIX-Exa_Tutorials.git
```

This is instruction, not code.
So go ahead and run your cases directly in here and don't worry about
maintaining it as a repo. If you screw something up, nuke it and start over.
As you become familiar with MFIX-Exa and start developing your own cases,
you might start from one of these simple cases, but you should maintain those
inputs separately (best practice would be in your own versioning system,
but that's up to you).


## Preliminaries

* <ins>Building the code:</ins> I am not going to cover building the code in these tutorials.
If you are using an ubuntu machine that you have `sudo` access to, I have put
[build instructions](https://mfix.netl.doe.gov/forum/t/building-and-running-mfix-exa-on-an-ubuntu-laptop/5367)
on the user forum. Please consult the documentation for
[general build instructions](https://mfix.netl.doe.gov/doc/mfix-exa/guide/latest/user_guide/quick_start/BuildingMFIX.html).
There are also some (now outdated)
[machine-specific build instructions](https://mfix.netl.doe.gov/doc/mfix-exa/guide/latest/references/hpc.html)
that may also be of use.
* <ins>Running the code:</ins> When I say, "run it," I'm going to assume you have
an executable (or simlink to an executable) named mfix in the local
directory named mfix that can be called by `./mfix inputs` or
`mpirun -np # ./mfix inputs`.
* <ins>General workflow:</ins> Speaking of *local* directory... Each case should be contained in a `run` subdir.
You should copy this before adding in your executable and running anything. You
should probably make these descriptive, e.g., `cp -r run/ init` but, to be honest,
I am lazy and my subdirs look like `run1`, `run2`, `run2b`, etc. The point is that
when you change something, e.g., mesh resolution, you should run this in a new
location so that it's easy to compare changes. Additionally, when I say something like
"from our previous inputs," I mean the last inputs that were run. Suppose we have a
fourth iteration using my lazy naming convention above, I would do something like
`cp -r run run3` and `cp run2b/inputs run3/`or equivalent.
* <ins>Additional software:</ins> We will use some "peripheries" in these tutorials, e.g., paraview, *hypre*, and OpenSCAD.
But this is not a tutorial on any of those additional pieces of software.
Users who are unfamiliar with these codes should look at their specific user guides, tutorials, etc.
* <ins>Resources:</ins> MFIX-Exa is an HPC code. It was built to run on GPUs, many GPUs, or many many CPUs.
But I would hate for someone to spend time working through a tutorial only to find out that the case is
run on hundreds of CPUs and you only have access to a handful. So if a case needs more
than 4 CPUs to run effectively, there will be a warning at the top of the tutorial.
* The MFIX-Exa development team will be starting to work on a GUI in FY26. So these
cases very likely to be superseded in the not-too-distant future.


Ok. With all that being said, let's begin! I would suggest starting with the
[lid-driven cavity](fluid/lid-driven_cavity/README.md),
but if you you're only interested in granular flow, jump straight to
[normal collisions](granular/normal_collisions/README.md).



Just checking what these look like:

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.

