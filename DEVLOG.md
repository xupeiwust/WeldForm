
20220509 - Working on SOA version. Same solver response for thermal.
20220510 - Working on FSW example. Working on Thermal SOA version.
            Working on FSW example. Working on Thermal SOA version.
              Checking Johnson Cook Traction example. 
20220511 - FSW Example. Setting contact = true. Checking normals and min initial contact gap.
20220511  - 	FSW Example. Setting contact = true. Checking normals and min initial contact gap.
              Begining to add Mat3_t to flat conversions (to test soon SOA vs AOS).
20220512  -   Working on flat arrays, using Particle class. Next step is to compare with 
              Still not working. Fixed FSW example velocity.
              Working on contact Mesh update, now the update changes normals and centroids.
              Changed JC material to FSW example.
              Fixed thermal coupling. 
20220513  -   Working on FSW example. timestep 5e-8 diverging. So, now is 2.e-8, fixed.
              INITIAL GAP WAS WRONG. Fixed. 
20220519  -   Working on Compression TRIP problem. Manual TS with CFL values of 0.2 NOT CONVERGING.
              Found an error in Particles Move, ghost particles where moving BEFORE adjusting ghost velocity.
              and acceleration were not forced to zero. MoveGhost is now also fixing accel to zero.
20220520  -   Symm TRIP problem still does not work. Begining to add arrays for parallel sum (reduction)
              instead of using particle lock (slow).
20220523  -   Numerical integration. Qpplied dep/2 in Modiried verlet algorithm.
              Verlet is FAR FASTER than leapfrog. 
              XSPH. Found an ERROR (XSPH was not applied on leapfrog). 
              But not seeing results.
              RANDLES-LIBERSY 1996: Main loop updating variables order. 
              Begining to change this, alsp like fraser. Apparently allows to CFL up to 1.5
20220524  -   Working on New order update Solver. Not working.
              ERROR found in verlet, added a new kick-drift verlet-leapfrog integrator
              Error found at XSPH in leapfrog.
              Working on #271. For THE FIRST TIME IS CONVERGING WITH A CFL LARGER THAN Modified >Verlet
              A kick-drift based solver updating on different times.
              Still wrong at displacements and velocities, but not in accelerations.
              THIS SHOULD BE DONE ALSO WITH MOD VERLET IN ORDER TO ACHIEVE EVEN BETTER TIME STEP
              FIRST SOLVER FASTER THAN MODIFIED VERLET. 
              Succesful "Differential order kick-drift solver. Can solve TRIP benchmark with CFL 0.4 
              whereas mod verlet runs at 0.2 and greater is diverging.
20220525  -   Added mod euler Differential update like Kirk Fraser method.
              It also converges at cfl 0.4 but results are strange 
20220526  -   Added different untegral algortithms, all with Added MoveGhost to KickDrift.
              Added plastic deformation Neghbour update, NOW WORKING PLASTIC.
              Contact WORKING on kick-drift algorithm. Fraser compression test works ok up until 5ms.
              Then diverges. 
20220530  -   Working on Internal and Kinetic Energy. 
------------------------------------------------------
20220601  -   Found ERROR in ghost symmetry at high strains. Velocities are extremely high. (#280)
              Begining to work on allowance of more than 1 contact surface.
20220602  -  Working on 2 surface contact. DONE. WORKING OK.
             Should be corrected:
               -  Contact forces still uneven
               -  Autoadjust initial gap. 
             Added bonded contact type.
20220607  -  Added SEO contact algorithm (which looks for penetration only and not velocity direction).
             Added displacement constraint to double side contact TRIP example. 
             Found error in ID assignment of KickDrift Solver.
             Changed TRIP example to be Symmetric in Length Axis 
             Implemented higher Artif. Visc. constants on TRIP example. 
             Added XSPH on new KickDrift Solver.
20220610  -  Added some calculation time logs to KickDrift solver. 
             Begining to add a algebraic (non discrete) surface contact algorithm for calc time reduction.
20220614  -  Begining to add Full Implicit SPH.
             Add fixes in top and bottom for 2 side compression TRIP test 
20220616  -  Fixed Internal Energy calculation.
             KickDrift Solver now calculates all material models. (Strange results in Johnson Cook).
20220621  -  Solved Finally uneven contact forces, second contact algorithm seems to be even.
             FIRST CASE WITH STATIC FRICTION WORKS. Issue #275 closed.
20220622  -  Added auto time stepping to KickDrift solver.
20220623  -  Added plastic plateau to Hollomon material.
20220624  -  Added SAE 1010 Compression example. 
             Fixed hardening for Hollomon and Johnson Cook for KickDrift Integrator
             Begining to Work with generic executable input file reader.
             This should be priority, adding and compiling each example is nonsense.
20220626  -  Working with new parallel reduction without particle locking
20220627  -  Working with new parallel reduction without particle locking, flattening arrays.
             ATTENTION: ARRAYS COULD BE DIMENSIONED BY NProc
20220628  -  Fixed error in new reduction algorithm. 
             Working on Input. Added symmetry case.
20220629  -  Working with Symmetry. Cleaning old quarter mesh and adding 
             double symm (now XY symm) to input reading
----------------------------------------------------------------------------------------------------
20220704  -  Working on Input file, contact cases
20220705  -  Begining to add wang and Zhan static friction coeff criteria
             IMPORTANT. Velocity criteria is not working well.
             Try to do wag ceiteria as seo but with dist in future time: i.e. 
             Instead of xi for dist, use xi+v*dt
20220706  -  First satisfactory results in contact problem with generic friction.
             A mixed algorithm based on Wang for contact force and Zhan for
             tangential force comparison (velocity rates), comparing with 
             current velocity, leads to an acceptable algorithm.
20220707  -  Working on Contact. Found that displacement tg force criteria 
             (Wang2013) reduces displacements for same friction coeff
20220708  -  Working on reduction.FINALLY SOLVED NISHIKURA REDUCTION IN ACCEL.
             TIME IS ABOUT HALF THE TIME WITH OPENMP LOCK REDUCING IN PAIR PHASE.
             Written reduction in tensors. Resultant tensors are the same but whole results 
             Are still bad. 
20220712  -  SIGNIFICANT IMPROVEMENTS. 1. FINALLY IMPLEMENTATION OF LEAPFROG SOLVER WORKS ON 
             LARGE TIME STEPS. 2. SOLVED PARALLEL REDUCTION BY NISHIMURA ARRAYS. Is slightly
             faster than lock but the algorithm is applicable to parallel GPU.
20220713  -  FIXED GHOST PARTICLE METHOD. Equallying ghost stress, strain and density from 
             respective particles, is working. Now remains to make Wang's hybrid 
             contact-ghost symmetry method.
20220714  -  Working with CONTACT. New Leapfrog Algorithm gives Smooth Contact Forces
             with SEO Algorithm (CalcForces2), but static friction does not work.
             On the other side, original KickDFrift Solver (without second acc update cycle)
             gives smooth forces with Wang algorithm.
             MUST FIX Original KickDrift and check also with Verlet and Fraser. 
20220715  -  FIRST FRASER ALGORITHM WORKING. REINFORCED BCs before position update works.
             ALSO WORKS WITH CFL 0.7
20220721  -  Added Thermal Per Particle test (for comparing with conventional and non block)
20220725  -  Working on Slice Mesher. All ghost particles. 
---------------------------------------------------------------------------------------------
20220801  -  Slice Mesher. Corrected ghost particles at y plane. 
             Begining with MoveGhost, tangential and normal.
20220802  -  Fixed error in slice mesh generator. 
             Testing solver in slice. Errors found.
             fixed Some meshing error with z coordinate. 
             Fixed Ghost boundary conditions
             Added homogeneous cyl mesher. 
             Fixed Fraser for NONLOCK reduction.
20220805  -  Added Frictional Work to Wang contact.
             Added thermal calculation to fraser integrator.
20220809  -  Fixed frictional work.
             Added Min - Max temperatures in Fraser integration output LOG.
             Changed material of rotation compression to Johnson Cook.
20220810  -  Changed max displacement (Now only are calculated from solid particles, excluding contact ones
             Corrected position on workpiece in FSW example. 
20220816  -  Beginging to write Solid Mesh reader. 
             Added Contact Friction Work Sum  calc.
             Added Plastic Work Sum calc.
20220822  -  Working on solid SPH mesher.
             Fixed plastic work. Now it is NOT limited to thermal problems only.
             Also, value iscorrected 
             Recovering compression thermal problem.
20220823 -   Fixed thermal compression example with new Fraser Solver.
20220826 -   Corrected Nastran reader (Hexa nodes).
             Added Pyram vol elements.
             Removed (by the moment) solid (rigid) particle to increment temperature.
20220830 -   NASTRAN reader: 
              - Added element masses. 
              - Added element h
20220831 -   Fixed h calculation in nastran import. 
--------------------------------------------------------------------------------------------
20220906 -   Added solid_part_count to GenerateSPHMesh
             Fixed FSW_nastran example (surface tool was meshed with volumetric reader).
             Added move mesh feature.
             Working on calculate initial gap.
20220907 -   Added Compression Example with nastran imported mesh.
             Found 2 things with fraser integrator:
             KGC is not working (Compression example)
20220912 -   Found an CRUCIAL ERROR in Contact. 
             Now velocity results in rotation-compression are correct.
20220913 -   Adjusting FSW_reduced_test convection coeffs. 
20220914 -   Added contact heat conductance.
20220921 -   Added accumulated contact heat flux.
             Error found in heating of rigid surfaces. There was a deltat missing. 
20220923 -   Critical ERROR Corrected error in HEAT GENERATION. 
             Incorrect use of force.
20221005 -   Changed example.
             Added tangential force to output and external forces work evaluation.
20221017 -   Added things in Nastran reader.
20221206 -   Fixed frictional work. 
20221207 -   Fixed friction_hfl
------------------------------
20230125 -   Added shear stress in Wang contact Algorithm
20230126 -  Begining to add option in Contact Compression example to not use contact (only for testing)
20230131 -  Added plastic strain dissipation per unit volume output
         -  FIXED ERRORS DUE TO PARALLEL (NOT ATOMIZED)
         --  FIXED PLASTIC DISSIPATION SUM
         -   FIXED CONTACT FRICTION SUM 
         
         - FIXED COMPRESSION 1010 input file
20230201 - Working on input file, now reading contact (with errors).
20230202 - CONTACT FIRST TIME WORKING. 
         - Fixed Contact Compression example.
20230203 - Nishimura reductions is changed to if instead of preprocessor.
         - Addded reduction type to input file readinig
         - Added a correction to locking sum in case of gradient correction (not yet ready)
         - Changed input to read johnson cook, bilinear and hollomon
20230206 - Ready to read nastran input files for rigid bodies (contact surfaces).
20230207 - Changed FSW_red model density (from input command)
         - Begining to add Contact_Compression_Rot example
         - Begining to add thermal properties (constant) and initial conditions to input file

20230213 - test
20230214 - Working on Input. 
		 - FIXED COMPRESSION EXAMPLE.
		 - FIRST TIME READING THERMAL-STRUCT coupled problem (Compression_thermal.json)
20230223 - ADDING RESTART read file for the first time. 
20230227 - Fixed cantilever algorithm 
         - Added output reading log
         - Changed box domain to write particles until (Length - r)
20230228 - Deprecated Standard Solve algorithm in cantilever example
----------------------------------
20230306 - Fixed Cantilever.json example bending direction was wrong.
20230307 - Added total memory allocated by particles.
20230313 - Added Cylindrical grid option in input
           Working on double sided contact compression example
20230322 - Working on Cylindrical coordinates
20230323 - Fixed Ghost Symmetry (Added Mirror_XYZ to mesh generator and use new function)
         - Now Symmetry WORKS BETTER (MIRRORING DIFFERENT VARIABlES)
20230327 - Trying to update Quarter Symm example. Error with AddXYSymCylinderLength. Issue 
20230328 - Added Thick wall Axi-Symm example. Not working yet. 
----------------------------------
20230403 - Extending contact to 2D
20230410 - Working on Metal Cut example
20230411 - Added Smoothing length update to Fraser Solver and Kickdrift
20230413 - Fixed friction partcile surface for 2D plain strain (TODO: AXI-SYMM)
         - Modified reader to work with CBEAM (2d file mesh)
         - automatically set dimension to 2 when Z value is zero.
20230427 - Deleted data weith error in SOA summation (not used).
--------------------------------------------------------------------
20230502 - Added rotational velocity to input
20230503 - Found Critic Error in CalcStressStrain. Eff Strain Rate was not updated (always zero).
=======

20220509 - Working on SOA version. Same solver response for thermal.
20220510 - Working on FSW example. Working on Thermal SOA version.
            Working on FSW example. Working on Thermal SOA version.
              Checking Johnson Cook Traction example. 
20220511 - FSW Example. Setting contact = true. Checking normals and min initial contact gap.
20220511  - 	FSW Example. Setting contact = true. Checking normals and min initial contact gap.
              Begining to add Mat3_t to flat conversions (to test soon SOA vs AOS).
20220512  -   Working on flat arrays, using Particle class. Next step is to compare with 
              Still not working. Fixed FSW example velocity.
              Working on contact Mesh update, now the update changes normals and centroids.
              Changed JC material to FSW example.
              Fixed thermal coupling. 
20220513  -   Working on FSW example. timestep 5e-8 diverging. So, now is 2.e-8, fixed.
              INITIAL GAP WAS WRONG. Fixed. 
20220519  -   Working on Compression TRIP problem. Manual TS with CFL values of 0.2 NOT CONVERGING.
              Found an error in Particles Move, ghost particles where moving BEFORE adjusting ghost velocity.
              and acceleration were not forced to zero. MoveGhost is now also fixing accel to zero.
20220520  -   Symm TRIP problem still does not work. Begining to add arrays for parallel sum (reduction)
              instead of using particle lock (slow).
20220523  -   Numerical integration. Qpplied dep/2 in Modiried verlet algorithm.
              Verlet is FAR FASTER than leapfrog. 
              XSPH. Found an ERROR (XSPH was not applied on leapfrog). 
              But not seeing results.
              RANDLES-LIBERSY 1996: Main loop updating variables order. 
              Begining to change this, alsp like fraser. Apparently allows to CFL up to 1.5
20220524  -   Working on New order update Solver. Not working.
              ERROR found in verlet, added a new kick-drift verlet-leapfrog integrator
              Error found at XSPH in leapfrog.
              Working on #271. For THE FIRST TIME IS CONVERGING WITH A CFL LARGER THAN Modified >Verlet
              A kick-drift based solver updating on different times.
              Still wrong at displacements and velocities, but not in accelerations.
              THIS SHOULD BE DONE ALSO WITH MOD VERLET IN ORDER TO ACHIEVE EVEN BETTER TIME STEP
              FIRST SOLVER FASTER THAN MODIFIED VERLET. 
              Succesful "Differential order kick-drift solver. Can solve TRIP benchmark with CFL 0.4 
              whereas mod verlet runs at 0.2 and greater is diverging.
20220525  -   Added mod euler Differential update like Kirk Fraser method.
              It also converges at cfl 0.4 but results are strange 
20220526  -   Added different untegral algortithms, all with Added MoveGhost to KickDrift.
              Added plastic deformation Neghbour update, NOW WORKING PLASTIC.
              Contact WORKING on kick-drift algorithm. Fraser compression test works ok up until 5ms.
              Then diverges. 
20220530  -   Working on Internal and Kinetic Energy. 
------------------------------------------------------
20220601  -   Found ERROR in ghost symmetry at high strains. Velocities are extremely high. (#280)
              Begining to work on allowance of more than 1 contact surface.
20220602  -  Working on 2 surface contact. DONE. WORKING OK.
             Should be corrected:
               -  Contact forces still uneven
               -  Autoadjust initial gap. 
             Added bonded contact type.
20220607  -  Added SEO contact algorithm (which looks for penetration only and not velocity direction).
             Added displacement constraint to double side contact TRIP example. 
             Found error in ID assignment of KickDrift Solver.
             Changed TRIP example to be Symmetric in Length Axis 
             Implemented higher Artif. Visc. constants on TRIP example. 
             Added XSPH on new KickDrift Solver.
20220610  -  Added some calculation time logs to KickDrift solver. 
             Begining to add a algebraic (non discrete) surface contact algorithm for calc time reduction.
20220614  -  Begining to add Full Implicit SPH.
             Add fixes in top and bottom for 2 side compression TRIP test 
20220616  -  Fixed Internal Energy calculation.
             KickDrift Solver now calculates all material models. (Strange results in Johnson Cook).
20220621  -  Solved Finally uneven contact forces, second contact algorithm seems to be even.
             FIRST CASE WITH STATIC FRICTION WORKS. Issue #275 closed.
20220622  -  Added auto time stepping to KickDrift solver.
20220623  -  Added plastic plateau to Hollomon material.
20220624  -  Added SAE 1010 Compression example. 
             Fixed hardening for Hollomon and Johnson Cook for KickDrift Integrator
             Begining to Work with generic executable input file reader.
             This should be priority, adding and compiling each example is nonsense.
20220626  -  Working with new parallel reduction without particle locking
20220627  -  Working with new parallel reduction without particle locking, flattening arrays.
             ATTENTION: ARRAYS COULD BE DIMENSIONED BY NProc
20220628  -  Fixed error in new reduction algorithm. 
             Working on Input. Added symmetry case.
20220629  -  Working with Symmetry. Cleaning old quarter mesh and adding 
             double symm (now XY symm) to input reading
----------------------------------------------------------------------------------------------------
20220704  -  Working on Input file, contact cases
20220705  -  Begining to add wang and Zhan static friction coeff criteria
             IMPORTANT. Velocity criteria is not working well.
             Try to do wag ceiteria as seo but with dist in future time: i.e. 
             Instead of xi for dist, use xi+v*dt
20220706  -  First satisfactory results in contact problem with generic friction.
             A mixed algorithm based on Wang for contact force and Zhan for
             tangential force comparison (velocity rates), comparing with 
             current velocity, leads to an acceptable algorithm.
20220707  -  Working on Contact. Found that displacement tg force criteria 
             (Wang2013) reduces displacements for same friction coeff
20220708  -  Working on reduction.FINALLY SOLVED NISHIKURA REDUCTION IN ACCEL.
             TIME IS ABOUT HALF THE TIME WITH OPENMP LOCK REDUCING IN PAIR PHASE.
             Written reduction in tensors. Resultant tensors are the same but whole results 
             Are still bad. 
20220712  -  SIGNIFICANT IMPROVEMENTS. 1. FINALLY IMPLEMENTATION OF LEAPFROG SOLVER WORKS ON 
             LARGE TIME STEPS. 2. SOLVED PARALLEL REDUCTION BY NISHIMURA ARRAYS. Is slightly
             faster than lock but the algorithm is applicable to parallel GPU.
20220713  -  FIXED GHOST PARTICLE METHOD. Equallying ghost stress, strain and density from 
             respective particles, is working. Now remains to make Wang's hybrid 
             contact-ghost symmetry method.
20220714  -  Working with CONTACT. New Leapfrog Algorithm gives Smooth Contact Forces
             with SEO Algorithm (CalcForces2), but static friction does not work.
             On the other side, original KickDFrift Solver (without second acc update cycle)
             gives smooth forces with Wang algorithm.
             MUST FIX Original KickDrift and check also with Verlet and Fraser. 
20220715  -  FIRST FRASER ALGORITHM WORKING. REINFORCED BCs before position update works.
             ALSO WORKS WITH CFL 0.7
20220721  -  Added Thermal Per Particle test (for comparing with conventional and non block)
20220725  -  Working on Slice Mesher. All ghost particles. 
---------------------------------------------------------------------------------------------
20220801  -  Slice Mesher. Corrected ghost particles at y plane. 
             Begining with MoveGhost, tangential and normal.
20220802  -  Fixed error in slice mesh generator. 
             Testing solver in slice. Errors found.
             fixed Some meshing error with z coordinate. 
             Fixed Ghost boundary conditions
             Added homogeneous cyl mesher. 
             Fixed Fraser for NONLOCK reduction.
20220805  -  Added Frictional Work to Wang contact.
             Added thermal calculation to fraser integrator.
20220809  -  Fixed frictional work.
             Added Min - Max temperatures in Fraser integration output LOG.
             Changed material of rotation compression to Johnson Cook.
20220810  -  Changed max displacement (Now only are calculated from solid particles, excluding contact ones
             Corrected position on workpiece in FSW example. 
20220816  -  Beginging to write Solid Mesh reader. 
             Added Contact Friction Work Sum  calc.
             Added Plastic Work Sum calc.
20220822  -  Working on solid SPH mesher.
             Fixed plastic work. Now it is NOT limited to thermal problems only.
             Also, value iscorrected 
             Recovering compression thermal problem.
20220823 -   Fixed thermal compression example with new Fraser Solver.
20220826 -   Corrected Nastran reader (Hexa nodes).
             Added Pyram vol elements.
             Removed (by the moment) solid (rigid) particle to increment temperature.
20220830 -   NASTRAN reader: 
              - Added element masses. 
              - Added element h
20220831 -   Fixed h calculation in nastran import. 
--------------------------------------------------------------------------------------------
20220906 -   Added solid_part_count to GenerateSPHMesh
             Fixed FSW_nastran example (surface tool was meshed with volumetric reader).
             Added move mesh feature.
             Working on calculate initial gap.
20220907 -   Added Compression Example with nastran imported mesh.
             Found 2 things with fraser integrator:
             KGC is not working (Compression example)
20220912 -   Found an CRUCIAL ERROR in Contact. 
             Now velocity results in rotation-compression are correct.
20220913 -   Adjusting FSW_reduced_test convection coeffs. 
20220914 -   Added contact heat conductance.
20220921 -   Added accumulated contact heat flux.
             Error found in heating of rigid surfaces. There was a deltat missing. 
20220923 -   Critical ERROR Corrected error in HEAT GENERATION. 
             Incorrect use of force.
20221005 -   Changed example.
             Added tangential force to output and external forces work evaluation.
20221017 -   Added things in Nastran reader.
20221206 -   Fixed frictional work. 
20221207 -   Fixed friction_hfl
------------------------------
20230125 -   Added shear stress in Wang contact Algorithm
20230126 -  Begining to add option in Contact Compression example to not use contact (only for testing)
20230131 -  Added plastic strain dissipation per unit volume output
         -  FIXED ERRORS DUE TO PARALLEL (NOT ATOMIZED)
         --  FIXED PLASTIC DISSIPATION SUM
         -   FIXED CONTACT FRICTION SUM 
         
         - FIXED COMPRESSION 1010 input file
20230201 - Working on input file, now reading contact (with errors).
20230202 - CONTACT FIRST TIME WORKING. 
         - Fixed Contact Compression example.
20230203 - Nishimura reductions is changed to if instead of preprocessor.
         - Addded reduction type to input file readinig
         - Added a correction to locking sum in case of gradient correction (not yet ready)
         - Changed input to read johnson cook, bilinear and hollomon
20230206 - Ready to read nastran input files for rigid bodies (contact surfaces).
20230207 - Changed FSW_red model density (from input command)
         - Begining to add Contact_Compression_Rot example
         - Begining to add thermal properties (constant) and initial conditions to input file

20230213 - test
20230214 - Working on Input. 
		 - FIXED COMPRESSION EXAMPLE.
		 - FIRST TIME READING THERMAL-STRUCT coupled problem (Compression_thermal.json)
20230223 - ADDING RESTART read file for the first time. 
20230227 - Fixed cantilever algorithm 
         - Added output reading log
         - Changed box domain to write particles until (Length - r)
20230228 - Deprecated Standard Solve algorithm in cantilever example
----------------------------------
20230306 - Fixed Cantilever.json example bending direction was wrong.
20230307 - Added total memory allocated by particles.
20230313 - Added Cylindrical grid option in input
           Working on double sided contact compression example
20230322 - Working on Cylindrical coordinates
20230323 - Fixed Ghost Symmetry (Added Mirror_XYZ to mesh generator and use new function)
         - Now Symmetry WORKS BETTER (MIRRORING DIFFERENT VARIABlES)
20230327 - Trying to update Quarter Symm example. Error with AddXYSymCylinderLength. Issue 
20230328 - Added Thick wall Axi-Symm example. Not working yet. 
----------------------------------
20230403 - Extending contact to 2D
20230410 - Working on Metal Cut example
20230411 - Added Smoothing length update to Fraser Solver and Kickdrift
20230413 - Fixed friction partcile surface for 2D plain strain (TODO: AXI-SYMM)
         - Modified reader to work with CBEAM (2d file mesh)
         - automatically set dimension to 2 when Z value is zero.
20230427 - Deleted data weith error in SOA summation (not used).
--------------------------------------------------------------------
20230502 - Added rotational velocity to input
20230503 - Found Critic Error in CalcStressStrain. Eff Strain Rate was not updated (always zero).
20230511 - Found 2 critical errors in gradient correction. 
           Contact force was wrong (about double)
           matrix m() is not updated. (See call Domain::CalcGradCorrMatrix in Fraser solver)
20230522 - Fixed merge errors
         - Fixed error which affects drilling contact (qj vector assingment, now is dynamic)
         - Added estimated solved size
------------------------------------------------------------------------
20230608 - Changed autots to velocity and accel check.      
         - Has been found that metal cut example with no accel check is not converging (even vel check with real particle distance or updated h). 
         - Added additional output after 60 seconds from last one (without writing results)
         - Fixed input in solver (Added "Mech-KickDrift")
20230609 - Changin h update to all steps have SIGNIFICANT IMPROVEMENT. 
20230613 - Added multilinear amplitudes to input reading
         - HUGE FIX IN KICKDRIFT SOLVER. Now variable time steps are a fact. 
         - Still not working on non coupled mechanical problems (diverging)
         - DEFAULT SOLVER HAS CHANGED TO KICKDRFIT RANDLES 
-------------------------------------------------------------
20230705 - Changed delta t in randles & libersky solver, first velocity update is with prev deltat
20230725 - FIRST SUCCESFUL 
         - Changed h update to frequency 1
         - Added option to change frequency in Neighbour search
         - Fixed Error in h update condition
20230727 - IMPROVED LEAPFROG SOLVER; NOW IT SUPPORTS LARGER CFL
-------------------------------------------------------------
20230822 - Fixed thermal coupled solver default to Leapfrog (was kickdrift with gives wrong results)
         - Fixed input to account for "Mech-Thermal-Fraser"
-------------------------------------------------------------
20230918 - Organize CMAKELISTS
         - Adding Campos Impact JSON 
         - Added initial velocity to input
-------------------------------------------------------------
20231004 - Added ROTATION VELOCITY TO INPUT
20231106 - Added Johnson Cook Damage Model.
         - Corrected fracture strain and add incremental plastic strain to particle damage
				 - Added dmage param input reading
				 - Corrected a problem with velocity initial conditions
				 - Fixed crash in Johnson Cook damage calc
				 - Prevented sigma asterisk for damage be NAN at sigma_eq = 0
				 - Added damage count
				 - Added damage output
				 - Corrected Johnson Cook damage expression
				 - Calculate fracture strain and stresses per particle and not per pair
				 - Corrected Acceleration expression
20231115 - Solved Johnson Cook strain hardening factor
20231126 - Fixed Johnson Cook fracture strain expression
20231128 - Fixed some examples. Added traction example. 
         - FIXED NB SEARCH WHEN DAMAGE MODEL
				 - Fixed Homologous temp fracture strain calculation
-------------------------------------------------------------
20231219 - FIXED NON DAMAGE Accel Calculation. (Damage param dam_f was set outside loop)
         - Added Compression with damage (seeing that Mass Scaling gives wrong results)
         - Added damage to metal cut (and remove mass scaling)
         - Recalculate free surface on contact problems
         - Added out file with output and date build
-------------------------------------------------------------
20240103 - Added Flag of damaged links, and decreased Nb count in order to proper surface calculation.
         - ADDED DIFERENT GRADTYPE STRESSES 
         - FIXED PARALLELIZATION OF Kernel Gradient Correction
20240104 - Fixed Initial Temperature 
         - IMPORTANT REGARDING TO CONTACT: FRICTION IS NOT WORKING WITH LEAPFROG
20240105 - Added LS-DYNA contact algorithm, Leapfrog tg problem is not duw to current algorithm
           but also due to leapfrog order
         - Acceleration is not updated now inside ContForce Functions
-------------------------------------------------------------
20240319 - Fixed bug in damage: calcsurface were wrong. 
           Solved BC zones (ID_orig is wrong)
           Fixed parallel calc surface (for damage)
-------------------------------------------------------------
20240411 - Added 3D Slice Cylinder with AxiSymm - BCs
20240425 - Restored Slice with Ghost (not workin yet)
         - Fixed Velocity BCs ON SLICE AT PI/2!!
20240426 - Added Axisymmetric (2D) input reading
         - FOUND ERROR ON AXISYMMETRIC acceleration (InteractionAlt, ACCELERATION[2] CHANGED to 1 !)
         ---> Z IS CHANGED TO Y AND HOOP IS Z AS IN PLANE STRAIN
-------------------------------------------------------------
20240502 - Added Line To Input reader
20240513 - Added reading than one contact surfaces
         - Changing normal calcs of planes
20240514 - Added GMT material to inpt
         - Begining to add hot compression example with GMT mat
         - Corrected yield stress calc with correct Initial Temp
20240515 - FIXED Two surfaces contact example input
20240517 - FIXED FLIP NORMALS ON NASTRAN FILE (WAS INVERTING X AND Y COORDINATES INSTEAD OF CONNECTIVITY)
         - Added error if CellNo[0] = 0 So there is not seg fault.
         - FOUND error on Scientific notation NASTRAN reader. 
20240527 - Added state of contact conduction at the begin of the solution.  
         - Fixed contact conduction reading 
20240528 - Added feature of assign initial diff conditions for different Zone IDs
         - Fixed contact BC with amplitude function (there was readng zero value)
         - Added amplitude factor to be 1.0 by default (it was zero)
         - Fixed contact conduction and friction heat for Axisymmetric
         - Added optional plastic work heat
20240529 - Fixed dS calculation on Wang contact (logical was wrong and also the expression)
         - sy calculation was made only once for GMT.
         - Fixed dTdt equation fo axisymm
         - Fixed CSV output (missing comma between CFZ and pressure)
-----------------------------------------------------------------
20240603 - Added BC Convection reading from json input file.
         - Fixed input in thermal case
20240604 - Added axisymmetric conduction (accordfing to castillo and García-Senz)
20240605 - FIXED reading BC conection (was appliyng to entire domain)
         - FIXED convection fo plane strain (dS were wrong).
20240606 - Added 3D cylinder convection example 
20240618 - Added Fraser Contact Algorithm to input (not working with LeapFrog)
-----------------------------------------------------------------
20240705 - Fixed Tangent modulus calc on GMT material
         - Fixed Vertical line on input (still remains inclined line)
20240725 - Fixed Log Format (was repeated each time step)
         - FOUND AN ERROR ON PARALLEL EXTRUSION. Differences between runs.
20240726 - Fixed Surface ID calc (reset each step from spourious calc).
------------------------------------------------------------------
20240801 - Fixed max outs video (extended from 1e3 to 1e6)
20240807 - Added Contact Force to History
         - Added thermal expansion to input
---------------------------------------------------------------------
20241127 - Adding lsdyna Domain reader
         - FIXED CRASH dueto buggy damage reading
         - ADDED COMMIT TO OUTPUT
20241202 - Added scalefactor to imported domain.
         - Added movement to rigid bodies and particle Domain! 
20241203 - Added option to overWrite particle radius friom distance
         - Added advice of NO SURFACE CALC 
         - FIXED DOMAIN DIMENSION SET ASSIGNENT ACCORDING TO READING LS-DYNA
20241206 - Added a converter from ls-dyna to nastran
