# inferential-tension-penalized-regression
R implementation of the inferential tension framework for joint  hyperparameter estimation in penalized regression models (LASSO and Ridge).  Includes Monte Carlo simulation, bio-inspired optimization (DE, PSO),  and inferential evaluation protocols.
# Inferential Tension for Penalized Regression

This repository contains the complete R implementation of the inferential
tension framework proposed in:

> Plaza Maldonado, R. & Olivares, R. (under review). Optimization of
> regularization under inferential tension: a bio-inspired approach for
> stable estimation in penalized regression models.
> *Knowledge-Based Systems*.

## Overview

The inferential tension function T_m(theta) jointly integrates predictive
error, model complexity, and structural stability into a single normalized
cost functional. The full hyperparameter vector theta = (lambda, eta,
kappa_0) is estimated via bio-inspired global optimization over a
continuous search space, without fixing penalization weights a priori.

## Repository structure

| Script | Description |
|--------|-------------|
| `00_setup.R` | Package installation and project configuration |
| `01_dgp.R` | Data generating process — Monte Carlo replications |
| `02_estimators.R` | LASSO and Ridge estimation over lambda grid |
| `03_metrics.R` | Evaluation metrics: E_m, C_m, S_m |
| `04_pilot.R` | Pilot calibration of weights and algorithm parameters |
| `05_tension.R` | Inferential tension function T_m(theta) |
| `06_optimization.R` | Global optimization: Grid, DE, PSO |
| `07_hypotheses.R` | Hypothesis evaluation H1--H4 |
| `08_collapse.R` | Inferential collapse diagnostics |
| `09_sensitivity.R` | Global sensitivity analysis |
| `10_tables.R` | Results compilation |
| `11_figures.R` | Publication-ready figures |
| `12_inventory.R` | Table inventory for manuscript |

## Requirements

- R >= 4.5.0
- Packages: `glmnet`, `DEoptim`, `pso`, `MASS`, `tidyverse`,
  `ggplot2`, `patchwork`, `scales`, `knitr`, `kableExtra`

## Execution order

Scripts must be executed sequentially from `00` to `12`.
All intermediate objects are serialized as `.rds` files in `rds/`.
No global random seed is imposed — Monte Carlo replications are
genuinely independent by design. A local seed is applied exclusively
in scripts `04` and `06` for algorithm initialization reproducibility.

## Scenarios

Six simulation scenarios of increasing structural complexity:

| Scenario | n | p | rho | SNR | Error |
|----------|---|---|-----|-----|-------|
| S1 — Baseline | 200 | 50 | 0.1 | 4.0 | Normal |
| S2 — High correlation | 200 | 50 | 0.8 | 4.0 | Normal |
| S3 — Weak signal | 200 | 50 | 0.5 | 0.5 | Normal |
| S4 — High dimensionality | 100 | 200 | 0.5 | 2.0 | Normal |
| S5 — Heavy tails | 200 | 50 | 0.5 | 2.0 | t(3) |
| S6 — Adversarial | 80 | 300 | 0.9 | 0.5 | t(3) |

## License

MIT License
