<div align="center">

# KHMP: Frequency-Domain Kalman Refinement for High-Fidelity Human Motion Prediction

<p align="center">
  <a href="https://arxiv.org/abs/xxxx.xxxxx">[Paper]</a>
  &nbsp;&nbsp;&nbsp;
  <a href="https://github.com/your-repo">[Code]</a>
  &nbsp;&nbsp;&nbsp;
  <a href="./">[Project Page]</a>
  &nbsp;&nbsp;&nbsp;
  <a href="#citation">[BibTeX]</a>
</p>

<p align="center">
  <b>Wenhan Wu</b>, Zhishuai Guo, Chen Chen, Srijan Das, Hongfei Xue, Pu Wang, Aidong Lu
</p>

<p align="center">
  Yunnan University &nbsp;|&nbsp; UNC Charlotte &nbsp;|&nbsp; Northern Illinois University &nbsp;|&nbsp; University of Central Florida
</p>

</div>

---

## Overview

**KHMP** is a high-fidelity stochastic human motion prediction framework that combines:

- **physics-informed training**
- **adaptive Kalman refinement in the DCT frequency domain**
- **improved temporal smoothness and physical plausibility**

It is designed to suppress **high-frequency jitter** while preserving natural motion details, producing smoother and more realistic future motion sequences.

---

## Teaser

<p align="center">
  <img src="figs/fig1.png" width="85%">
</p>

<p align="center">
  <em>Fig. 1. Comparison illustrating motion prediction for the jogging action.</em>
</p>

Previous stochastic prediction frameworks often generate physically implausible motion and temporal discontinuity.  
KHMP addresses this issue by integrating **physical constraints during training** and **adaptive frequency-domain Kalman refinement during inference**, leading to more plausible and temporally smoother motion sequences.

---

## Abstract

Stochastic human motion prediction aims to generate diverse and plausible future motions from observed sequences. Despite recent progress in generative modeling, existing methods often suffer from **high-frequency jitter**, **temporal discontinuities**, and **physically implausible poses**. We propose **KHMP**, a novel framework for high-fidelity human motion prediction that applies an **adaptive Kalman filter in the DCT domain** to refine predicted motion sequences. By treating high-frequency DCT coefficients as a structured noisy signal, KHMP recursively suppresses jitter while preserving motion details. In addition, the framework incorporates **training-time physical constraints**, including **temporal smoothness** and **joint angle limits**, to enforce biomechanical plausibility. Experiments on **Human3.6M** and **HumanEva-I** demonstrate that KHMP achieves strong quantitative performance while producing smoother and more realistic motions.

---

## Motivation

### Why is KHMP needed?

Existing stochastic human motion prediction models face two major challenges:

1. **Lack of adaptive frequency-aware refinement**  
   High-frequency noise introduced by stochastic sampling often leads to visible jitter.

2. **Lack of explicit biomechanical constraints**  
   Frame-wise reconstruction objectives alone do not sufficiently enforce physically plausible motion.

KHMP is designed to address both issues with a simple but effective pipeline.

---

## Method

<p align="center">
  <img src="figs/fig2.png" width="92%">
</p>

<p align="center">
  <em>Fig. 2. Overall framework of KHMP.</em>
</p>

The KHMP pipeline consists of three main stages:

### 1. Motion generation backbone
A stochastic human motion prediction backbone first generates future 3D motion sequences.

### 2. Physics-informed training
During training, KHMP introduces:
- **temporal smoothness constraints**
- **joint angle limit constraints**

These constraints improve motion realism and reduce physically implausible predictions.

### 3. Frequency-domain adaptive Kalman refinement
During inference, KHMP:
- transforms predicted motion into the **DCT domain**
- separates low-frequency motion structure from high-frequency noisy components
- applies an **adaptive Kalman filter** to the high-frequency spectrum
- reconstructs refined motion through inverse DCT

This design effectively suppresses jitter while preserving detailed motion patterns.

---

## Trajectory-Level Refinement

<p align="center">
  <img src="figs/fig4.png" width="95%">
</p>

<p align="center">
  <em>Fig. 4. Visual comparison of joint trajectories showing KHMP refinement over the baseline across multiple actions and body parts.</em>
</p>

KHMP significantly improves trajectory smoothness across body parts such as:
- ankle
- shin
- thigh
- wrist
- upper arm

Compared with the baseline, the refined trajectories better follow ground truth and exhibit substantially less high-frequency oscillation.

---

## Qualitative Results

<p align="center">
  <img src="figs/fig5.png" width="95%">
</p>

<p align="center">
  <em>Fig. 5. Qualitative comparison of generated motion sequences across different actions.</em>
</p>

KHMP consistently produces:
- smoother temporal evolution
- more stable body articulation
- fewer jitter artifacts
- more physically plausible pose transitions

This improvement is especially visible in dynamic actions and limb motion.

---

## Quantitative Analysis

### Fixed suppression vs. adaptive refinement

<p align="center">
  <img src="figs/table2d.png" width="70%">
</p>

<p align="center">
  <em>Table 2(d). Fixed frequency suppression versus KHMP.</em>
</p>

A simple non-adaptive suppression strategy cannot handle varying noise levels across stochastic predictions.  
KHMP outperforms fixed suppression by adaptively adjusting Kalman parameters based on estimated signal quality.

### Jitter reduction

<p align="center">
  <img src="figs/table2e.png" width="70%">
</p>

<p align="center">
  <em>Table 2(e). Quantitative jitter reduction across body parts.</em>
</p>

KHMP reduces jitter across nearly all body parts, with particularly strong improvements on:
- **upper arm**
- **shin**
- **ankle**
- **wrist**

The average jitter reduction reaches **28.0%**.

---

## Key Features

- **Adaptive frequency-domain refinement**
- **Physics-informed human motion prediction**
- **Reduced temporal jitter**
- **Improved physical plausibility**
- **Strong performance on HumanEva-I and Human3.6M**

---

## Repository Structure

```text
.
├── README.md
├── figs
│   ├── fig1.png
│   ├── fig2.png
│   ├── fig4.png
│   ├── fig5.png
│   ├── table2d.png
│   └── table2e.png
└── ...
