# Stress_Optimizer_Surrogate
Physics-Informed Neural Network for beam deflection using PyTorch
# Physics-Informed Neural Network for Euler-Bernoulli Beam Deflection

## Overview
A PINN implemented in PyTorch to solve the 2nd order Euler-Bernoulli 
beam deflection ODE without any labeled training data, validated against 
the analytical double integration method solution.

## Problem
Simply supported beam under uniformly distributed load:

EI·u'' = M(x),   M(x) = 20x - 2x²

**Engineering Data:**
- Beam length: L = 10 m
- UDL: w = 4 kN/m  
- Flexural Rigidity: EI = 6.25×10⁵ kN·m²

**Boundary Conditions:**
- u(0) = 0, u(10) = 0       ← zero deflection at supports
- u'(0) = +wL³/24EI         ← slope at left support
- u'(10) = -wL³/24EI        ← slope at right support

## Network Architecture
| Layer | Neurons | Activation |
|-------|---------|------------|
| Input | 1 | SiLU |
| Hidden 1,2,3 | 150 each | Tanh |
| Output | 1 | Linear |

A hybrid SiLU-Tanh activation strategy is adopted —
SiLU handles domain-wide feature extraction while Tanh 
ensures smooth higher-order derivatives for accurate 
physics residual computation.

## Results

| Metric | Value |
|--------|-------|
| Max absolute error | 1.77 × 10⁻⁵ m |
| Mean absolute error | 7.67 × 10⁻⁶ m |
| PDE residual loss | 1.49 × 10⁻¹⁰ |
| BC loss | 5.62 × 10⁻¹⁵ |

## Tech Stack
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat&logo=pytorch&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)

## Repository Structure
├── Beam_Deflection_PINN.ipynb  ← full notebook
├── report.pdf                  ← detailed report
├── results/
│   └── solution.png
└── README.md

## References
- Raissi et al. (2019) — Physics-informed neural networks
- Hibbeler — Structural Analysis (Double Integration Method)

## Author
Soutrik | github.com/Soutrik-77
