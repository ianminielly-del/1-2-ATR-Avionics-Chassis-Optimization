# 1/2 ATR Avionics Chassis Structural & Thermal Optimization (Rev A vs. Rev B)

## Project Overview
This repository contains the finite element analysis (FEA) structural and thermal trade study for a 1/2 ATR (Air Transport Radio) avionics enclosure fabricated from 6061-T6 aluminum. The objective was to aggressively lightweight a solid baseline structure (Rev A) while maintaining structural integrity under a 500 lbf static load and preserving thermal dissipation capacity.

---

## Performance Comparison (Rev A vs. Rev B)

| Parameter / Metric | Rev A (Baseline Solid) | Rev B (Optimized Waffle-Grid) | Delta / Optimization Impact |
| :--- | :--- | :--- | :--- |
| **Mass** | 3.89 lbs | 1.99 lbs | **-48.8% Mass Reduction** |
| **Min Factor of Safety (FOS)** | 6.5 (6.528e+00) | 6.1 (6.065e+00) | -0.4 (High structural margin preserved) |
| **Max von Mises Stress** | 42.13 MPa (4.213e+07 N/m²) | 45.34 MPa (4.534e+07 N/m²) | +7.6% Stress increase |
| **Max Displacement (URES)** | 4.258e-03 mm | 3.771e-03 mm | **-11.4% Displacement reduction (stiffer)** |
| **Max Temperature** | 346.4 K (73.25°C) | 347.9 K (74.75°C) | +1.5 K (+1.5°C) Minor thermal penalty |
| **Material Yield Strength** | 275 MPa (2.750e+08 N/m²) | 275 MPa (2.750e+08 N/m²) | 6061-T6 Aluminum Limit |

---

## Visual FEA Comparison Matrix

| Analysis Type | Rev A (Baseline Solid) | Rev B (Optimized Waffle-Grid) |
| :--- | :---: | :---: |
| **von Mises Stress** | ![Rev A Stress](Plots_and_Renders/Stress_RevA_vonMises.png) | ![Rev B Stress](Plots_and_Renders/Stress_RevB_vonMises.png) |
| **Displacement** | ![Rev A Displacement](Plots_and_Renders/Displacement_RevA.png) | ![Rev B Displacement](Plots_and_Renders/Displacement_RevB.png) |
| **Factor of Safety** | ![Rev A FOS](Plots_and_Renders/FOS_RevA.png) | ![Rev B FOS](Plots_and_Renders/FOS_RevB.png) |
| **Thermal Contour** | ![Rev A Thermal](Plots_and_Renders/Thermal_RevA.png) | ![Rev B Thermal](Plots_and_Renders/Thermal_RevB.png) |

---

## Design Features & Engineering Rationale

1. **Mass Reduction & Wall Topology:**
   - Reduced wall thickness from a uniform 0.375" solid baseline down to 0.250" pocketed side walls featuring 0.090" residual webs and 0.250" x 0.100" stiffening ribs.
   - Reduced component mass by 1.90 lbs (~48.8%) while maintaining a minimum Factor of Safety of 6.1 under 500 lbf static floor load.

2. **Stress Concentration Mitigation:**
   - Implemented 0.125" internal pocket radii, matching standard 1/4" end mills to reduce CNC tool chatter and prevent stress risers.
   - Applied 0.250" vertical and floor-to-wall fillets to transition bending moments smoothly from the base floor into the side walls.

3. **Thermal Management Trade-off & Boundary Conditions:**
   - **Internal Heat Source:** Applied a thermal heat power of **50 W** ($50\text{ J/s}$) uniformly across the internal base floor to simulate active avionics component heat dissipation.
   - **Convective Cooling:** Applied a surface convection boundary condition of **$25\text{ W/(m}^2\cdot\text{K)}$** to exposed external chassis faces at an ambient temperature of **298.15 K ($25^\circ\text{C}$)**.
   - **Thermal Performance Impact:** 
     - **Rev A (Baseline Solid):** Max equilibrium temperature reached **346.4 K ($73.25^\circ\text{C}$)**.
     - **Rev B (Optimized Waffle-Grid):** Max equilibrium temperature reached **347.9 K ($74.75^\circ\text{C}$)**.
     - **Trade-off Analysis:** Thinning the side walls slightly reduced internal conduction cross-sections, but pocketing increased convective surface area ($Q = h A \Delta T$). This resulted in a minor temperature increase of only **$+1.5^\circ\text{C}$**, leaving substantial margin below standard maximum operating limits for commercial/military avionics ($\le 85^\circ\text{C}$).

4. **Design for Manufacturing & Fasteners:**
   - Preserved full 0.250" flange thickness around bolt pads to handle 750 lbf preload forces without local yielding.
   - Scalloped non-load-bearing flange sections between bolt holes to eliminate stray mass.

---

## Repository Structure

```text
├── CAD/
│   ├── Chassis_Baseline_Rev_A.SLDPRT
│   └── Chassis_Optimized_Rev_B.SLDPRT
├── Plots_and_Renders/
│   ├── Displacement_RevA.png
│   ├── Displacement_RevB.png
│   ├── FOS_RevA.png
│   ├── FOS_RevB.png
│   ├── Stress_RevA_vonMises.png
│   ├── Stress_RevB_vonMises.png
│   ├── Thermal_RevA.png
│   └── Thermal_RevB.png
└── README.md
