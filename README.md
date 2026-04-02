# 🌀 OpenFOAM Case: pipeBase

## 📌 Overview

This case simulates incompressible turbulent flow over a 2D circular cylinder.

- **Objective:** Analyze vortex shedding and compute drag/lift coefficients  
- **Solver:** pimpleFoam  
- **Physics:** Incompressible, transient, turbulent flow  
- **Geometry:** 2D cylinder in a rectangular domain  

---
```
## 📁 Case Structure

pipeBase/
├── 0/                          # Initial and boundary conditions
├── 0.orig/                     # Backup of initial conditions
│   ├── p
│   ├── U
├── constant/
│   └── transportProperties
│   └── turbulenceProperties
│   └── variablesDict
├── system/                     # Simulation controls
│   ├── blockMeshDict           # Mesh files
│   ├── controlDict
│   ├── fvSchemes
│   ├── fvSolution
├── Allrun
├── Allclean

```

## 🧪 Case Details

### Geometry & Mesh
- Domain size: 20D × 10D  
- Cylinder diameter (D): 1 m  
- Number of cells: ~120,000  
- Mesh type: Structured (blockMesh) + refinement near cylinder  

### Boundary Conditions

| Field | Inlet        | Outlet       | Cylinder Wall | Top/Bottom |
|------|-------------|-------------|---------------|------------|
| U    | fixedValue  | zeroGradient| noSlip        | slip       |
| p    | zeroGradient| fixedValue  | zeroGradient  | zeroGradient |

---

### Flow Properties

- Reynolds number: 10,000  
- Fluid: Air  
- Kinematic viscosity: 1e-5 m²/s  

---

### Turbulence Model

- Model: k-ω SST  
- Wall treatment: automatic wall functions  

---

## 📈 Results Summary

- Vortex shedding observed downstream of cylinder  
- Periodic lift coefficient fluctuations  
- Mean drag coefficient ≈ 1.2  

### Key Observations

- Stable vortex street formed after initial transient  
- Good agreement with literature for Strouhal number (~0.2)  
---

## ⚙️ Requirements

- OpenFOAM version: v2506  
- OS: Linux / WSL  
- Additional tools:
  - ParaView (visualization)
  - Python (optional, post-processing)

---

## ▶️ How to Run

### 1. Mesh generation
blockMesh

### 2. Mesh refinement (if applicable)
snappyHexMesh -overwrite

### 3. Check mesh quality
checkMesh

### 4. Run simulation
pimpleFoam > log.pimpleFoam

### 5. Parallel execution (optional)
decomposePar
mpirun -np 4 pimpleFoam -parallel > log.pimpleFoam
reconstructPar

---

## 📊 Post-Processing

### Open in ParaView
paraFoam

### Available outputs
- Residuals: postProcessing/residuals/
- Forces: postProcessing/forces/
- Lift/Drag coefficients: postProcessing/forceCoeffs/

---

## ⚠️ Notes

- Simulation assumes 2D flow (no spanwise effects)  
- Mesh resolution impacts vortex accuracy  
- Time step adjusted to maintain CFL < 1  

---

## 🧑‍💻 Author

- Name: Nicolas Forestal
- Contact: nicolasforestal.pro@gmail.com  

---

## 📚 References

- OpenFOAM User Guide  
- CFD Online resources  
- Literature on flow over cylinder (Re = 10,000)
