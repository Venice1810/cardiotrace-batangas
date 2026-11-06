# CardioTrace Batangas: A Hybrid ECG Signal Processing ans Machine Learning Framework for Accurate Heart Rate Monitoring 

Comparative evaluation of conventional RR intervals and Random Forest regression on MIT-BIH Arrhythmia Database
# CardioTrace Batangas: ECG Signal Processing & Heart Rate Estimation Framework

[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Dataset: PhysioNet MIT-BIH](https://img.shields.io/badge/Dataset-MIT--BIH%20Arrhythmia-red.svg)](https://physionet.org/content/mitdb/)

An open-source computational electrophysiology framework for digital signal processing (DSP), fiducial R-peak detection, and continuous heart rate (HR) estimation. This repository compares deterministic time-domain inter-beat interval calculations ($\text{HR} = 60 / \overline{\text{RR}}$) against machine learning ensemble regression (Random Forest) across 10 selected recordings from the PhysioNet MIT-BIH Arrhythmia Database.

---

## 📌 Project Overview

Accurate heart rate estimation relies on robust fiducial point identification within the electrocardiogram (ECG) waveform. The **CardioTrace Batangas** framework evaluates:
1. **Digital Preprocessing:** Attenuation of baseline wander ($0.1\text{--}0.5\text{ Hz}$) and high-frequency electromyographic ($>50\text{ Hz}$) noise using a digital Butterworth bandpass filter.
2. **R-Peak Detection:** QRS complex feature tracking evaluating a matching tolerance window of $\pm 50\text{ ms}$.
3. **Comparative HR Estimation:** Benchmarking classic deterministic inter-beat interval averages against feature-based Random Forest regression models under strict record-grouped patient splitting to prevent data leakage.

---

## 📊 Key Findings & Empirical Performance

* **R-Peak Detection Precision:** Achieved an **F1-Score of 95.60%** and a **Positive Predictive Value (PPV) of 99.35%** across 9,067 true positive beat identifications.
* **Arrhythmia Sensitivity Bottlenecks:** Sensitivity dropped to $92.13\%$ primarily due to Record 106 ($71.78\%$ beat yield), where premature ventricular contractions (PVCs) distorted QRS morphology and bypassed fixed derivative thresholds.
* **Deterministic vs. Machine Learning:** The classical time-domain RR-averaging method significantly outperformed Random Forest regression:
  * **Conventional HR MAE:** $2.6548\text{ bpm}$ (59.78% lower error)
  * **Random Forest MAE:** $6.6016\text{ bpm}$ (exhibited output clustering at $\approx 55$ and $\approx 93\text{ bpm}$ due to feature space compression)

---

## 📂 Repository Structure

```text
CardioTrace-Batangas/
│
├── data/                      # Dataset access guidelines
│   └── README.md              # Instructions for downloading MIT-BIH via WFDB / PhysioNet
│
├── docs/                      # Research documentation & manuscripts
│   ├── manuscript_discussion.md  # Detailed discussion & literature integration
│   └── figures/               # Generated high-resolution plots (ECG signals, scatter plots)
│
├── src/                       # Core Python source code
│   ├── __init__.py
│   ├── preprocessing.py       # Butterworth bandpass filtering functions
│   ├── detection.py           # R-peak detection pipeline
│   ├── features.py            # RR interval extraction & statistical vector construction
│   └── modeling.py            # Random Forest regressor & evaluation metrics
│
├── .gitignore                 # Files excluded from version control
├── LICENSE                    # MIT Open-Source License
├── README.md                  # Main repository documentation
├── requirements.txt           # Python library dependencies
└── run_pipeline.py            # Main entry-point execution script
