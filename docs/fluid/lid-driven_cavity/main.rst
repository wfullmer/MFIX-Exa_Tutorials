.. _LidDrivenCavity:

Lid-driven Cavity
-----------------

The following inputs are defined using the ``fluid`` prefix.

+--------------------------------------------+-------------------------------------------------------------+--------+----------+
|                                            | Description                                                 |  Type  | Default  |
+============================================+=============================================================+========+==========+
| solve                                      | Specify the name of the fluid or set to ``None`` to disable | String | ``None`` |
|                                            | the fluid solver. The name assigned to the fluid solver is  |        |          |
|                                            | used to specify fluid properties and initial and boundary   |        |          |
|                                            | conditions.                                                 |        |          |
+--------------------------------------------+-------------------------------------------------------------+--------+----------+


The root prefix for the following inputs use the name defined using the ``fluid.solve`` keyword. For example, if the fluid solver
is named ``myfluid``, then the following keywords are preceded with ``myfluid`` and a period. Currently, MFIX-Exa only supports
a single fluid; therefore, it is common to name the fluid ``fluid``. This is illustrated later in example input snippets.

.. |Sutherland_Eq| replace:: :math:`\mu(T) = \mu_{ref}\left(\frac{T}{T_{ref}}\right)^{3/2}\frac{T_{ref} + S}{T+S}`

.. |Reid_4parm_Eq| replace:: :math:`\mu(T) = Ae^{\left(\frac{B}{T} + CT + DT^2 \right)}`

.. |Sato_Eq| replace:: :math:`\mu_{pit} = C d_s \rho \left|\boldsymbol{u} - \boldsymbol{u_s}\right|`

.. |eff_visc| replace:: :math:`\mu_{eff} = \mu_{mol} + \mu_{eddy} + \mu_{susp} + \mu_{pit}`

.. |mix_Eq| replace:: :math:`\mu_{mix} = \sum_{\alpha=1}^{N} \frac{X_{\alpha} \mu_{\alpha}}{\sum_{\beta} X_{\beta} \phi_{\alpha \beta}}`

Here is a quick inline eq test for |Sato_Eq|. What does this look like? What if we don't use the replace feature and just
put the in-line eq like so $Re = \rho_g U L / \mu_g$?

Or what about a separate eq like this: 


   
$$\mu_{mix} = \sum_{\alpha=1}^{N} \frac{X_{\alpha} \mu_{\alpha}}{\sum_{\beta} X_{\beta} \phi_{\alpha \beta}}$$




Incompressible fluid
^^^^^^^^^^^^^^^^^^^^

Here's a bash code block test: 

.. code-block:: bash
   :caption: Snippet of inputs defining a simple incompressible fluid. This is not a complete input file.

   mfix.constraint = IncompressibleFluid

   mfix.advect_density  = 0
   mfix.advect_enthalpy = 0
   mfix.solve_species   = 0


   # Fluid model settings
   # -----------------------------------------------------------------------
   fluid.solve = fluid0

   fluid0.viscosity.molecular = constant
   fluid0.viscosity.molecular.constant = 1.8e-5


   # Initial Conditions
   # -----------------------------------------------------------------------
   ic.regions = full-domain

   ic.full-domain.fluid0.volfrac   =  1.0
   ic.full-domain.fluid0.density   =  1.0

   ic.full-domain.fluid0.velocity  =  0.0  0.0  0.0


   # Boundary Conditions
   # -----------------------------------------------------------------------
   bc.regions = inlet  outlet

   bc.inlet = mi
   bc.inlet.fluid0.volfrac  =  1.0
   bc.inlet.fluid0.density  =  1.0

   bc.inlet.fluid0.velocity =  1.0e-8  0.0  0.0

   bc.outlet = po
   bc.outlet.fluid0.pressure =  0.



   
Check this formatted table. 

+------------------------------------------+----------------------------------------------------------+--------+----------+
|                                          | Description                                              |  Type  | Default  |
+==========================================+==========================================================+========+==========+
| newton_solver.absolute_tol               | Define absolute tolerance for the Newton solver          |  Real  |  1.e-8   |
+------------------------------------------+----------------------------------------------------------+--------+----------+
| newton_solver.relative_tol               | Define relative tolerance for the Newton solver          |  Real  |  1.e-8   |
+------------------------------------------+----------------------------------------------------------+--------+----------+
| newton_solver.max_iterations             | Define max number of iterations for the Newton solver    |  int   |  500     |
+------------------------------------------+----------------------------------------------------------+--------+----------+



