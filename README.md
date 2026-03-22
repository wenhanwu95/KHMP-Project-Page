<div align="center">

# KHMP: Frequency-Domain Kalman Refinement for High-Fidelity Human Motion Prediction

<p align="center">
  <a href="https://arxiv.org/abs/xxxx.xxxxx">Paper</a>
  &nbsp;|&nbsp;
  <a href="https://github.com/your-repo">Code</a>
  &nbsp;|&nbsp;
  <a href="./">Project Page</a>
  &nbsp;|&nbsp;
  <a href="#citation">BibTeX</a>
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

**KHMP** is a high-fidelity stochastic human motion prediction framework that combines physics-informed training with adaptive Kalman refinement in the DCT frequency domain. It is designed to suppress high-frequency jitter while preserving natural motion details, producing smoother, more realistic, and physically plausible future motion sequences.

---

## Abstract

Stochastic human motion prediction aims to generate diverse and plausible future motions from observed sequences. Despite recent progress in generative modeling, existing methods often suffer from high-frequency jitter, temporal discontinuities, and physically implausible poses. We propose **KHMP**, a novel framework for high-fidelity human motion prediction that applies an adaptive Kalman filter in the DCT domain to refine predicted motion sequences. By treating high-frequency DCT coefficients as a structured noisy signal, KHMP recursively suppresses jitter while preserving motion details. In addition, the framework incorporates training-time physical constraints, including temporal smoothness and joint angle limits, to enforce biomechanical plausibility. Experiments on Human3.6M and HumanEva-I demonstrate that KHMP achieves strong quantitative performance while producing smoother and more realistic motions.

---

## Motivation

### Why is KHMP needed?

Existing stochastic human motion prediction models face two major challenges:

1. **Lack of adaptive frequency-aware refinement**  
   High-frequency noise introduced by stochastic sampling often leads to visible jitter and temporal discontinuity.

2. **Lack of explicit biomechanical constraints**  
   Frame-wise reconstruction objectives alone do not sufficiently enforce physically plausible motion.

KHMP addresses both issues with a unified framework that combines physical constraints during training and adaptive frequency-domain Kalman refinement during inference.

---

## Comparison illustrating motion prediction

<p align="center">
  <img src="figs/fig1.png" width="85%">
</p>

<p align="center">
  <em>Comparison illustrating motion prediction.</em>
</p>

Previous stochastic prediction frameworks often generate predictions exhibiting physical implausibility and abrupt temporal transitions. KHMP produces more plausible and temporally smoother motion sequences.

---

## Overview of the proposed KHMP framework

<p align="center">
  <img src="figs/fig2.png" width="92%">
</p>

<p align="center">
  <em>Overview of the proposed KHMP framework.</em>
</p>

The KHMP pipeline consists of three main stages:

### 1. Motion generation backbone
A stochastic human motion prediction backbone first generates future 3D motion sequences.

### 2. Physics-informed training
During training, KHMP introduces:
- temporal smoothness constraints
- joint angle limit constraints

These constraints improve motion realism and reduce physically implausible predictions.

### 3. Frequency-domain adaptive Kalman refinement
During inference, KHMP:
- transforms predicted motion into the DCT domain
- separates low-frequency motion structure from high-frequency noisy components
- applies an adaptive Kalman filter to the high-frequency spectrum
- reconstructs refined motion through inverse DCT

This design effectively suppresses jitter while preserving detailed motion patterns.

---

## Visual comparison of joint trajectories

<p align="center">
  <img src="figs/fig3.png" width="95%">
</p>

<p align="center">
  <em>Visual comparison of joint trajectories.</em>
</p>

KHMP significantly improves trajectory smoothness across different body parts. Compared with the baseline, the refined trajectories better follow the ground truth and exhibit substantially less high-frequency oscillation.

---

## Visual comparison highlighting KHMP’s enhanced prediction quality

<p align="center">
  <img src="figs/fig4.png" width="95%">
</p>

<p align="center">
  <em>Visual comparison highlighting KHMP’s enhanced prediction quality.</em>
</p>

KHMP consistently produces smoother temporal evolution, more stable body articulation, fewer jitter artifacts, and more physically plausible pose transitions.

---

## Quantitative Comparison

The following table reproduces the main quantitative comparison in the paper.

<div align="center">

<table>
  <thead>
    <tr>
      <th rowspan="2">Method</th>
      <th rowspan="2">Venue</th>
      <th colspan="5">HumanEva-I</th>
      <th colspan="5">Human3.6M</th>
    </tr>
    <tr>
      <th>APD↑</th>
      <th>ADE↓</th>
      <th>FDE↓</th>
      <th>MMADE↓</th>
      <th>MMFDE↓</th>
      <th>APD↑</th>
      <th>ADE↓</th>
      <th>FDE↓</th>
      <th>MMADE↓</th>
      <th>MMFDE↓</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ERD [8]</td>
      <td>ICCV 2015</td>
      <td>0</td>
      <td>0.382</td>
      <td>0.461</td>
      <td>0.521</td>
      <td>0.595</td>
      <td>0</td>
      <td>0.722</td>
      <td>0.969</td>
      <td>0.776</td>
      <td>0.995</td>
    </tr>
    <tr>
      <td>DeLiGAN [9]</td>
      <td>CVPR 2017</td>
      <td>2.177</td>
      <td>0.306</td>
      <td>0.322</td>
      <td>0.385</td>
      <td>0.371</td>
      <td>6.509</td>
      <td>0.483</td>
      <td>0.534</td>
      <td>0.520</td>
      <td>0.545</td>
    </tr>
    <tr>
      <td>BoM [3]</td>
      <td>CVPR 2018</td>
      <td>2.846</td>
      <td>0.271</td>
      <td>0.279</td>
      <td>0.373</td>
      <td>0.351</td>
      <td>6.265</td>
      <td>0.448</td>
      <td>0.533</td>
      <td>0.514</td>
      <td>0.544</td>
    </tr>
    <tr>
      <td>DLow [34]</td>
      <td>ECCV 2020</td>
      <td>4.855</td>
      <td>0.251</td>
      <td>0.268</td>
      <td>0.362</td>
      <td>0.339</td>
      <td>11.741</td>
      <td>0.425</td>
      <td>0.518</td>
      <td>0.495</td>
      <td>0.531</td>
    </tr>
    <tr>
      <td>DSF [33]</td>
      <td>ICLR 2020</td>
      <td>4.538</td>
      <td>0.273</td>
      <td>0.290</td>
      <td>0.364</td>
      <td>0.340</td>
      <td>9.330</td>
      <td>0.493</td>
      <td>0.592</td>
      <td>0.550</td>
      <td>0.599</td>
    </tr>
    <tr>
      <td>GSPS [21]</td>
      <td>ICCV 2021</td>
      <td>5.825</td>
      <td>0.233</td>
      <td>0.244</td>
      <td>0.343</td>
      <td>0.331</td>
      <td>14.757</td>
      <td>0.389</td>
      <td>0.496</td>
      <td>0.476</td>
      <td>0.525</td>
    </tr>
    <tr>
      <td>MOJO [35]</td>
      <td>CVPR 2021</td>
      <td>4.181</td>
      <td>0.234</td>
      <td>0.260</td>
      <td>0.344</td>
      <td>0.339</td>
      <td>12.579</td>
      <td>0.412</td>
      <td>0.514</td>
      <td>0.497</td>
      <td>0.538</td>
    </tr>
    <tr>
      <td>DivSamp [6]</td>
      <td>ACM MM 2022</td>
      <td>6.109</td>
      <td>0.220</td>
      <td>0.234</td>
      <td>0.342</td>
      <td>0.316</td>
      <td>15.310</td>
      <td>0.370</td>
      <td>0.485</td>
      <td>0.475</td>
      <td>0.516</td>
    </tr>
    <tr>
      <td>STARS [31]</td>
      <td>ECCV 2022</td>
      <td>6.031</td>
      <td>0.217</td>
      <td>0.241</td>
      <td>0.328</td>
      <td>0.321</td>
      <td>15.884</td>
      <td>0.358</td>
      <td>0.445</td>
      <td>0.442</td>
      <td>0.471</td>
    </tr>
    <tr>
      <td>MotionDiff [28]</td>
      <td>AAAI 2023</td>
      <td>5.931</td>
      <td>0.232</td>
      <td>0.236</td>
      <td>0.352</td>
      <td>0.320</td>
      <td>15.353</td>
      <td>0.411</td>
      <td>0.509</td>
      <td>0.508</td>
      <td>0.536</td>
    </tr>
    <tr>
      <td>Belfusion [2]</td>
      <td>ICCV 2023</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>7.602</td>
      <td>0.372</td>
      <td>0.474</td>
      <td>0.473</td>
      <td>0.507</td>
    </tr>
    <tr>
      <td>HumanMAC [4]</td>
      <td>ICCV 2023</td>
      <td>6.554</td>
      <td>0.209</td>
      <td>0.223</td>
      <td>0.342</td>
      <td>0.320</td>
      <td>6.301</td>
      <td>0.369</td>
      <td>0.480</td>
      <td>0.509</td>
      <td>0.545</td>
    </tr>
    <tr>
      <td>TransFusion [26]</td>
      <td>RA-L 2024</td>
      <td>1.031</td>
      <td>0.204</td>
      <td>0.234</td>
      <td>0.408</td>
      <td>0.427</td>
      <td>5.975</td>
      <td>0.358</td>
      <td>0.468</td>
      <td>0.506</td>
      <td>0.539</td>
    </tr>
    <tr>
      <td>CoMotion [24]</td>
      <td>ECCV 2024</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>7.632</td>
      <td>0.350</td>
      <td>0.458</td>
      <td>0.494</td>
      <td>0.506</td>
    </tr>
    <tr>
      <td>SkeletonDiff [5]</td>
      <td>CVPR 2025</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>7.249</td>
      <td>0.344</td>
      <td>0.450</td>
      <td>0.487</td>
      <td>0.512</td>
    </tr>
    <tr>
      <td>MotionMap [10]</td>
      <td>CVPR 2025</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>7.840</td>
      <td>0.474</td>
      <td>0.598</td>
      <td>0.466</td>
      <td>0.532</td>
    </tr>
    <tr>
      <td>SOGM [27]</td>
      <td>DSP 2025</td>
      <td>6.761</td>
      <td>0.217</td>
      <td>0.217</td>
      <td>0.337</td>
      <td>0.322</td>
      <td>15.877</td>
      <td>0.367</td>
      <td>0.484</td>
      <td>0.495</td>
      <td>0.529</td>
    </tr>
    <tr>
      <td>Baseline*</td>
      <td>–</td>
      <td>6.516</td>
      <td>0.196</td>
      <td>0.211</td>
      <td>0.314</td>
      <td>0.303</td>
      <td>8.217</td>
      <td>0.357</td>
      <td>0.445</td>
      <td>0.438</td>
      <td>0.470</td>
    </tr>
    <tr>
      <td><b>KHMP (Ours)</b></td>
      <td><b>–</b></td>
      <td><b>7.481</b></td>
      <td><b>0.188</b></td>
      <td><b>0.204</b></td>
      <td><b>0.301</b></td>
      <td><b>0.291</b></td>
      <td><b>9.235</b></td>
      <td><b>0.349</b></td>
      <td><b>0.441</b></td>
      <td><b>0.436</b></td>
      <td><b>0.468</b></td>
    </tr>
  </tbody>
</table>

</div>

---

## Key Features

- Adaptive frequency-domain refinement
- Physics-informed human motion prediction
- Reduced temporal jitter
- Improved physical plausibility
- Strong performance on HumanEva-I and Human3.6M

---

## TODO

- [ ] Upload final figure assets to `figs/`
- [ ] Add paper link
- [ ] Add code link
- [ ] Add project page link
- [ ] Add supplementary materials
- [ ] Add demo videos or GIFs if needed

---

## Citation

```bibtex
@inproceedings{wu2026khmp,
  title     = {KHMP: Frequency-Domain Kalman Refinement for High-Fidelity Human Motion Prediction},
  author    = {Wenhan Wu and Zhishuai Guo and Chen Chen and Srijan Das and Hongfei Xue and Pu Wang and Aidong Lu},
  booktitle = {European Conference on Computer Vision (ECCV)},
  year      = {2026}
}
