[README_connecting_rod.md](https://github.com/user-attachments/files/29433041/README_connecting_rod.md)
# Static Structural FEA Analysis of a Connecting Rod

**Tools:** SolidWorks 2026 · ANSYS Workbench 2026 R1  
**Institution:** Delhi Skills and Entrepreneurship University (DSEU), New Delhi  
**Author:** Aayush · B.Tech Mechanical Engineering (3rd Year) · June 2026

---

## Overview

Static structural FEA of a connecting rod representative of a small 4-cylinder petrol engine. A peak combustion load of 16,000 N was applied at the small end bore. The project covers 3D modelling in SolidWorks, manual stress calculations (axial stress, second moment of area, radius of gyration, slenderness ratio, Kt-corrected stress), and FEA in ANSYS Workbench. The governing FEA factor of safety is 3.87, confirming the design is structurally adequate.

---

## Component Dimensions

| Dimension | Value |
|---|---|
| Small End Bore Diameter | Ø 33.80 mm |
| Small End Outer Diameter | Ø 45.00 mm |
| Big End Bore Diameter | Ø 72.00 mm |
| Centre-to-Centre Shank Length | 90.00 mm |
| Shank Slot Fillet Radius | R 8.00 mm |
| Overall Assembly Width | 76.00 mm |

---

## Material

**Low Alloy Steel 4140 (Normalized)** — assigned from ANSYS Engineering Data library.

| Property | Value |
|---|---|
| Young's Modulus (E) | 2.125 × 10¹¹ Pa |
| Poisson's Ratio (ν) | 0.29 |
| Tensile Yield Strength (Sy) | 652.2 MPa |
| Tensile Ultimate Strength (Su) | 1015 MPa |
| Density | 7850 kg/m³ |

---

## Manual Calculations

Critical section: annular cross-section at the small end boss.

| Parameter | Value |
|---|---|
| Cross-Section Area (A) | 693 mm² |
| Second Moment of Area (I) | 137,220 mm⁴ |
| Radius of Gyration (k) | 14.07 mm |
| Slenderness Ratio (λ) | 3.20 → Short column, no buckling |
| Axial Compressive Stress | 23.09 MPa |
| Kt (fillet, r/d = 0.24) | 1.5 |
| Kt-Corrected Peak Stress | 34.64 MPa |
| FoS (direct) | 28.25 |
| FoS (Kt-corrected) | 18.83 |

Slenderness ratio of 3.20 (well below threshold of 40) confirms direct stress governs — Euler buckling does not apply.

---

## Boundary Conditions

| Condition | Detail |
|---|---|
| Fixed Support | Full inner surface of big end bore (all 6 DOF) |
| Applied Force | 16,000 N at small end bore inner surface (Y-direction) |
| Simulates | Peak combustion gas load, shank in compression |

---

## FEA Results

| Result | Value |
|---|---|
| Max Von Mises Stress | **168.55 MPa** (at small end boss fillet) |
| Max Stress as % of Yield | 25.8% |
| Max Total Deformation | **0.0634 mm** (at small end bore) |
| Min Safety Factor | **3.87** (at small end boss fillet) |
| Average Safety Factor | 14.198 |
| Design Status | ✅ No yielding predicted |

---

## Manual vs FEA Comparison

| Parameter | Manual Calculation | ANSYS FEA |
|---|---|---|
| Max Stress | 34.64 MPa (Kt-corrected) | 168.55 MPa (Von Mises) |
| FoS | 18.83 | **3.87** ← governing |
| Max Deformation | — | 0.0634 mm |
| Failure Prediction | No yielding ✅ | No yielding ✅ |

**Why the difference?** Manual calculation treats the load as purely axial on an annular section with a single Kt factor. FEA captures the full 3D geometry, combined axial and bending stresses, and the actual notch shape at the fillet. The FEA value of 3.87 is the design-governing figure. Both methods confirm no yielding — FEA is simply more complete.

The FEA FoS of 3.87 is within the accepted design range of 2.5–4.0 for connecting rods.

---

## Limitations & Future Work

- This is a **static** analysis only. In service, the rod sees fully reversed loading (compression on power stroke, tension on intake/exhaust). A fatigue assessment using S-N data for 4140 normalized steel would be needed to determine endurance life.
- The fixed big end bore is a simplification. A partial contact model over ~180° would better represent the hydrodynamic bearing load path.
- A **mesh convergence study** at the small end fillet is recommended to confirm the sensitivity of the 168.55 MPa peak to element size.

---

## Files in This Repository

```
├── Report_Connecting_Rod_FEA.pdf    # Full report with FEA screenshots and hand calcs
├── SolidWorks/                      # .SLDPRT model file
└── README.md
```

---

## References

- Shigley, Mischke & Budynas — *Mechanical Engineering Design*, 11th ed., McGraw-Hill
- Norton, R.L. — *Machine Design: An Integrated Approach*, 5th ed., Pearson
- ANSYS Inc. — *ANSYS Mechanical User Guide*, Release 2026 R1
- Dassault Systèmes — *SolidWorks 2026 Help Documentation*
- Repgen, G. (1998) — *Optimised Connecting Rods to Enable Higher Engine Performance*, SAE 980882
