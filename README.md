# Mode-Constrained Two-Stage Current Injection Optimization for Voltage Unbalance Mitigation

## Overview

This repository contains the implementation and supplementary materials for the paper:

**Mode-Constrained Two-Stage Current Injection Optimization for Voltage Unbalance Mitigation in IBR-Rich Distribution Network**

Published in:

**IEEE Journal of Emerging and Selected Topics in Power Electronics (JESTPE), 2026**

---

## Abstract

Voltage unbalance (VU) is one of the most critical power quality issues in inverter-based resource (IBR) dominated distribution networks.

Most existing voltage unbalance mitigation (VUM) strategies focus on the optimization of steady-state current references, while transient oscillations caused by reference switching are often neglected.

This work proposes a **Mode-Constrained Two-Stage Current Injection Optimization Framework**, which:

* Identifies dominant oscillatory modes of grid-connected IBR systems through eigenvalue analysis.
* Formulates current reference trajectory optimization as a frequency-domain optimization problem.
* Introduces the concepts of:

  * Virtual Acceleration
  * Virtual Energy
  * Spectral Energy Constraints
* Generates the fastest possible current switching trajectory without exciting underdamped oscillatory modes.

The proposed method significantly improves transient performance while preserving steady-state voltage unbalance mitigation capability.

---

## Key Contributions

### Stage I: Dominant Mode Identification

A closed-loop transfer-function matrix is established for the dual-sequence current control system.

The dominant oscillatory modes are identified through:

* Transfer function modeling
* Eigenvalue analysis
* Pole-zero analysis
* Frequency response analysis

Three dominant oscillatory modes are extracted from the studied system:

| Mode   | Frequency |
| ------ | --------- |
| Mode 1 | 50 Hz     |
| Mode 2 | 725 Hz    |
| Mode 3 | 825 Hz    |

---

### Stage II: Optimal Current Reference Trajectory (OCRT)

Instead of directly optimizing current references, the trajectory is reformulated using virtual acceleration.

The optimization objective is:

* Maximum virtual energy
* Minimum modal excitation
* Fastest switching trajectory

subject to:

* Spectral energy constraints
* Boundary constraints
* Current transition constraints

The resulting optimization problem is formulated as a:

**Second-Order Cone Programming (SOCP)** problem.

---

## Framework

```text
Stage I
│
├── Transfer Function Modeling
├── Modal Analysis
└── Dominant Mode Extraction
        │
        ▼
Stage II
│
├── Virtual Acceleration Modeling
├── DFT Analysis
├── Spectral Energy Constraints
└── SOCP Optimization
        │
        ▼
Optimal Current Reference Trajectory (OCRT)
```

---

## Main Advantages

Compared with conventional methods:

| Method         | Oscillation Suppression | Transition Speed | Robustness |
| -------------- | ----------------------- | ---------------- | ---------- |
| Step Reference | ✗                       | Fast             | Low        |
| Input Shaper   | ✓                       | Slow             | Moderate   |
| S-Curve        | ✓                       | Moderate         | Low        |
| MPC            | Depends                 | Moderate         | High       |
| Proposed OCRT  | ✓✓                      | Fastest          | High       |

The proposed OCRT:

* Avoids excitation of dominant oscillatory modes.
* Requires no modification of existing controllers.
* Maintains compatibility with commercial IBR products.
* Improves settling time and reduces current overshoot.

---

## Experimental Results

### Case 1

Voltage Unbalance Factor (VUF)

```text
Before Compensation: 11.11%
After Compensation : 1.57%
```

Current peak reduction:

```text
12.1% reduction
16.5% reduction
```

Settling time:

```text
46 ms → 35 ms
70 ms → 52 ms
```

---

### Case 2

Voltage Unbalance Factor (VUF)

```text
Before Compensation: 30.00%
After Compensation : 18.10%
```

Compared with ZZVD input shaper:

* Lower current overshoot
* Faster transient response
* Improved dynamic stability

---

## Research Highlights

* Frequency-domain trajectory optimization
* Voltage unbalance mitigation (VUM)
* Grid-connected inverter control
* Negative-sequence current injection
* Oscillation mode suppression
* SOCP optimization
* Power quality enhancement
* Converter-dominated power systems

---

## Citation

```bibtex
@ARTICLE{11309707,
  author={Ji, Tiantian and Lin, Pengfeng and Zhu, Miao and Jiang, Wentao and Zhang, Xinan and Wen, Changyun and Wang, Peng},
  journal={IEEE Journal of Emerging and Selected Topics in Power Electronics},
  title={Mode-Constrained Two-Stage Current Injection Optimization for Voltage Unbalance Mitigation in IBR-Rich Distribution Network},
  year={2026},
  volume={14},
  number={2},
  pages={1754-1766},
  doi={10.1109/JESTPE.2025.3646918}
}
```

---

## Repository Structure

### `Main_Model.slx`

Main Simulink model of the grid-connected inverter system used for validation.

Functions:

* Dual-sequence current control
* Negative-sequence current injection
* Voltage unbalance mitigation
* Dynamic response evaluation

---

### `Mode_Identification.mlx`

Implementation of Stage I: Dominant Mode Identification.

Functions:

* Transfer-function matrix construction
* Eigenvalue analysis
* Pole extraction
* Dominant mode frequency calculation

Output:

* Modal frequencies
* Damping ratios
* Mode constraint bands

---

### `OCRT_Optimization.mlx`

Implementation of Stage II: Frequency-Domain Optimization.

Functions:

* Virtual acceleration generation
* DFT-based spectral analysis
* SOCP formulation
* OCRT generation

Output:

* Optimal acceleration sequence
* Optimal Current Reference Trajectory (OCRT)
