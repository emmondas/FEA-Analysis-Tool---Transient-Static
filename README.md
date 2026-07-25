# FEA-Analysis-Tool---Transient-Static
A MATLAB App Designer GUI for running finite element analysis (FEA) on 3D CAD models imported from STL files. The tool wraps MATLAB's Partial Differential Equation Toolbox in an interactive interface, so you can set up and solve structural and thermal simulations without writing code for each study.

Features
STL geometry import with face-label preview so you can identify boundary faces before applying loads or constraints
Four study types selectable from a single interface:
Structural Static — von Mises stress under a constant load
Structural Transient — time-dependent stress response, with optional sinusoidal loading at a user-defined frequency
Thermal Steady State — temperature distribution under fixed heat flux and convection
Thermal Transient — time-evolving temperature field starting from a user-defined initial condition
Preset materials (Stainless Steel, Brass, Aluminium) with Young's modulus, Poisson's ratio, thermal conductivity, mass density, and specific heat auto-populated
Configurable loading: point loads on vertices or distributed surface tractions on faces
Thermal boundary conditions: heat flux on a source face plus convection (coefficient + ambient temperature) on surrounding faces
Time-step slider for scrubbing through cached transient results without re-solving
Adaptive UI that shows or hides controls based on the selected study type (e.g., initial temperature only appears for transient thermal studies)
3D result visualization with the turbo colormap and a colorbar for quantitative reading
Tech Stack
MATLAB (R2020b or later recommended)
Partial Differential Equation Toolbox — createpde, structuralBC, thermalBC, solve, pdeplot3D
App Designer — UI layout and callbacks
How to Run
Open the .mlapp file in MATLAB, or run FEA_Analysis_Das_Transient from the command window if you've exported it as a class
Click Upload STL File and select a 3D model
Inspect the face labels shown on the imported geometry to confirm which faces will receive constraints and loads (defaults assume face 3 is fixed and faces 1, 5, 6, 7 are convection surfaces)
Choose the study type, material, and load or thermal parameters
For transient studies, set the end time, number of time steps, and (for thermal) initial temperature
Click Solve and use the time-step slider to explore the result over time
Notes

The face-number assumptions for boundary conditions (fixed face 3, load on face 5, convection on faces 1/5/6/7) are hard-coded and depend on how the STL is meshed. If you use a geometry with different face numbering, you'll need to adjust those indices in the SolveButtonPushed callback. STL units are assumed to be meters — there's a commented-out scale call in the upload callback for models exported in millimeters.
