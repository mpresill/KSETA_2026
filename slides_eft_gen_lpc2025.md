---
marp: true
---

# EFT Event Generation at the LHC
## LPC EFT Workshop 2025 — Fermilab

---

## Overview

- EFT framework recap: SMEFT operators and Wilson coefficients
- Monte Carlo generation workflow with EFT insertions
- SMEFTsim UFO model and Madgraph5_aMC@NLO
- EFT reweighting techniques
- Practical examples: process generation and parameterisation

---

## SMEFT in a Nutshell

The SMEFT Lagrangian is written as:

$$\mathcal{L}_{\text{SMEFT}} = \mathcal{L}_{\text{SM}} + \sum_i \frac{C_i}{\Lambda^2} \mathcal{O}_i^{(6)} + \ldots$$

- $\mathcal{O}_i^{(6)}$: dimension-6 gauge-invariant operators
- $C_i$: Wilson coefficients (free parameters of the theory)
- $\Lambda$: new-physics scale

---

## Cross-section Parameterisation

At leading order in $1/\Lambda^2$, the cross section scales as:

$$\sigma = \sigma_{\text{SM}} + \sum_i \frac{C_i}{\Lambda^2}\, \sigma_i^{\text{int}} + \sum_{i,j} \frac{C_i C_j}{\Lambda^4}\, \sigma_{ij}^{\text{BSM}}$$

- Linear term: SM–EFT interference
- Quadratic term: pure EFT contribution

---

## Monte Carlo Generation Strategy

```
Import UFO model (SMEFTsim)
     │
     ▼
Define process card with NP<=1 or NP<=2
     │
     ▼
Generate matrix elements (Madgraph)
     │
     ▼
Event-level reweighting at multiple WC points
     │
     ▼
Extract EFT scaling functions per bin
```

---

## SMEFTsim UFO Model

- Self-consistent implementation of SMEFT at NLO-QCD
- Available flavour symmetry assumptions: `topU3l`, `U35`, `MFV`, `general`
- Renormalisation schemes: `MwScheme` (recommended), `alphaScheme`
- Restrict files control which operators are switched on

```
import model SMEFTsim_topU3l_MwScheme_UFO-massless_HVV
generate p p > h j j $$ w+ w- z a QCD=0 NP<=1, h > e mu vl vl~ NP=0
```

---

## Reweighting Approach

Instead of re-running generation for each WC point:

1. Generate events at a single reference point (SM or near-SM)
2. Compute per-event weight ratios: $w_i = |\mathcal{M}(C_i)|^2 / |\mathcal{M}_\text{SM}|^2$
3. Fill histograms with reweighted events

This is implemented natively in Madgraph via `reweight_card.dat`.

---

## EFT2Obs Workflow

```
auto_detect_operators.py  →  config.json
make_param_card.py        →  param_card.dat
                          →  reweight_card.dat
make_gridpack.sh          →  gridpack.tar.gz
run_gridpack.py           →  Rivet.yoda
get_scaling.py            →  scaling JSON
```

Extracts polynomial EFT scaling per observable bin:

$$\hat{\sigma}(\{C_i\}) = \sum_{\alpha} A_\alpha \prod_i C_i^{n_{i,\alpha}}$$

---

## Example: Higgs VBF $p_T$ Spectrum

Bosonic operators affecting $H$ production via VBF:

| Operator | Notation |
|----------|----------|
| $\mathcal{O}_{H\square}$ | `cHbox` |
| $\mathcal{O}_{HD}$ | `cHDD` |
| $\mathcal{O}_{HW}$ | `cHW` |
| $\mathcal{O}_{HB}$ | `cHB` |
| $\mathcal{O}_{HWB}$ | `cHWB` |

---

## Differential Distributions and Constraints

- Shape differences between operators are key for disentangling WCs
- High-$p_T$ bins are most sensitive to EFT effects
- PCA on the Fisher information matrix reveals best-constrained directions
- Marginalized (profiled) constraints vs. individual limits

---

## Summary

- SMEFTsim + Madgraph provide a flexible EFT MC generation framework
- Reweighting allows efficient exploration of the WC parameter space
- EFT2Obs automates the extraction of per-bin scaling functions
- Differential distributions enable simultaneous multi-operator fits

---

## References and Links

- [Original slides (Indico)](https://indico.fnal.gov/event/68174/contributions/316669/attachments/189121/261176/LPC_EFT_GEN_2025.pdf)
- [SMEFTsim](https://smeftsim.github.io)
- [EFT2Obs](https://github.com/ajgilbert/EFT2Obs)
- [Madgraph5_aMC@NLO](https://launchpad.net/mg5amcnlo)
