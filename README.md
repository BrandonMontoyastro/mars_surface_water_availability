# Subsurface Liquid Water Habitability on Mars: Geophysical & Thermodynamic Modeling

> **Project Status:** Completed  
> **Development Period:** January 2025 – October 2025 *(Academic Research)*  

### Project Overview
This repository contains the computational pipeline and geophysical modeling framework developed to evaluate subsurface thermodynamic conditions for liquid water stability across Mars. 

By integrating **seismic interior models from NASA’s InSight mission** with surface climatology data from the **Mars Climate Database (MCD)**, this project solves planetary interior structure equations to reconstruct global temperature and pressure profiles with depth. The resulting global "water habitability map" (*mapa de aguabilidad*) identifies candidate subsurface zones capable of sustaining liquid water and potential extremophilic life.



### Methodology & Computational Workflow
1. **Seismic Interior Structure Modeling:**
   - Ingested 1,000 internal structural models derived from InSight seismic data (`LSL_Models`).
   - Calculated density gradients ($\frac{d\rho}{dr}$) to determine the crust-mantle (Moho) transition depth (~39 ± 8 km).
   - Solved hydrostatic equilibrium ($\frac{dP}{dr} = -\rho g$) and geothermal temperature profiles ($T(z) = T_0 + \Gamma_T z$) throughout the Martian crust.

2. **Surface Climatology Ingestion:**
   - Extracted global surface temperature ($T_0$) and pressure ($P_0$) grids across Mars from the **Mars Climate Database (MCD v6.1)**.
   - Averaged seasonal data across key orbital points (Spring/Autumn Equinoxes, Summer/Winter Solstices) to obtain an annual baseline.

3. **Thermodynamic Phase Stability Analysis:**
   - Implemented the **IAPWS** (`iapws` Python library) formulation to construct pure water phase boundaries (sublimation, vaporization, and melting curves for Ice Ih, III, V, VI, VII).
   - Applied Raoult's Law and colligative property shifts to model the impact of brine salinity on freezing point depression and triple-point shifts.

4. **Global Depth & Habitability Mapping:**
   - Solved for the exact depth where subsurface $P(z)$ and $T(z)$ profiles intersect the liquid water stability region.
   - Interpolated 2D/3D global depth grids using `scipy.interpolate` and `griddata` to map minimum melting depths across Martian latitudes and longitudes.


### Key Findings
- **Depth Range for Stable Liquid Water:** Thermodynamic conditions favorable for pure subsurface liquid water occur between **0 km and 27 km** depth across the planet.
- **Salinity Effect:** Incorporating brine salinity depresses the freezing point and shifts the triple point, reducing the required depth for liquid water stability closer to the near-surface.
- **Astrobiological Implications:** Subsurface liquid zones coincide with potential habitats for chemolithotrophic extremophiles (e.g., *Hydrogenophilus thermoluteolus*, hydrogenotrophic methanogens) sustained by radiolytic $H_2$ production from natural $U$, $Th$, and $K$ decay in the crust.

---

### Tech Stack & Dependencies
- **Language:** Python 3
- **Data Analysis & Integration:** `numpy`, `pandas`, `scipy` (`odeint`, `interp1d`, `minimize_scalar`, `griddata`, `cdist`)
- **Astrophysics & Units:** `astropy` (`astropy.units`, `astropy.constants`)
- **Thermodynamics:** `iapws` (International Association for the Properties of Water and Steam)
- **Visualization & Geospatial Mapping:** `matplotlib`

---

### Authors & Acknowledgments
- **Research Team (UdeA Astronomy Group):** Brandon Montoya, Sebastián Numpaque, Simón Rodríguez, David Pérez.
- **Institution:** Universidad de Antioquia (UdeA), Faculty of Exact and Natural Sciences, Institute of Physics / Astronomy Program, Medellín, Colombia.
- **Conference Presentation:** Presented individually by **Brandon Montoya** at the *II Congreso de Estudiantes de Física del Valle de Aburrá (CEFVA)*, Escuela de Ingenieros EIA, October 14, 2025.
