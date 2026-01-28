# Effect of Physiological Parameters on PPG Signal-Based Glucose Estimation

This repository presents a **signal processing and exploratory analysis study** investigating
the relationship between **PPG-derived features** and **glucose levels**, supported by
invasively measured physiological parameters.

The work was conducted as part of a **Master’s-level Signal Analysis coursework** and is
based on data collected using a **custom-built physiological signal acquisition prototype**.

---

## Background & Physiological Motivation

Hemoglobin (Hb) directly absorbs green light and primarily affects the **DC component**
of the PPG signal, while **blood pressure (BP) and glucose** influence vascular tone,
thereby altering the **AC component** of the waveform.

This physiological relationship motivates the use of **PPG morphology and derivative-based
features** for indirect glucose analysis, as supported by optical and cardiovascular
literature.

---

## Dataset Overview

- Data collected personally from mostly clinically healthy volunteers,
  including students and professionals, with a limited number of pre-diabetic individuals.
- All measurements were acquired under controlled conditions using a custom prototype.
- **Invasive glucose measurements** were obtained during data collection and used as the
  **gold-standard reference**.
- Additional measurements included:
  - Systolic Blood Pressure (SBP)
  - Diastolic Blood Pressure (DBP)
  - Hemoglobin (Hb)- Invasive measurement & non inavsive from prototype

The final dataset consisted of **71 subjects** after preprocessing.

---

## Signal Processing Pipeline

The signal processing workflow includes:

- DC removal and Butterworth band-pass filtering for noise suppression
- Segmentation of clean PPG pulses based on signal quality criteria
- First and second derivative computation (APG analysis)
- Peak detection on PPG and APG signals

These steps follow established methodologies in PPG signal analysis literature.

---

## Feature Extraction

Features were extracted from selected high-quality PPG pulses rather than short sliding
windows, as glucose-related physiological changes occur gradually.

Extracted feature categories include:
- Statistical features
- Morphological PPG features
- Derivative-based (APG) features
- Physiological ratio-based features linked to vascular stiffness

Feature selection strategies were informed by prior studies
(e.g., Elgendi 2012; Oh et al. 2003).

---

## Exploratory Analysis

### Normalization
- Z-score normalization was applied to address large inter-feature scale variations.

### Correlation Analysis
- **Spearman correlation** was used to assess monotonic relationships between PPG-derived
  features and physiological parameters (Glucose, SBP, DBP, Hb).
- Correlation heatmaps were used to identify **multicollinearity** and feature redundancy.

### Dimensionality Reduction
Dimensionality reduction was applied **separately** using:

- **Principal Component Analysis (PCA)**  
  - Unsupervised
  - Glucose excluded from PCA input
- **Linear Discriminant Analysis (LDA)**  
  - Supervised
  - Glucose used as the class label

Multiple feature sets were evaluated independently.

---

## Classification Strategy (Exploratory)

- Glucose values were binarized using the **median glucose level (101 mg/dL)**:
  - Below median → Class 0
  - Above median → Class 1
- Random Forest classifiers were trained on:
  - Raw features
  - PCA-reduced features
  - LDA-transformed features
- Model selection used 5-fold cross-validation and grid search.

---

## Key Observations

- Individual PPG features showed weak correlations with glucose.
- Combined physiological features improved discrimination.
- PCA revealed that ~95.75% of variance could be captured using 13 components.
- Outlier removal improved variance concentration and class separation.
- Best performance was achieved using **LDA with all features**, yielding:
  - **AUC ≈ 0.84** on held-out test data.

---

## Conclusion

The results indicate that while individual PPG-derived features have limited predictive
power, **combined feature interactions**, particularly involving blood pressure and
hemoglobin, contribute meaningfully to glucose estimation.

This study highlights the **potential** of integrating physiological parameters into
PPG-based glucose analysis but does **not** claim clinical applicability.

Future work includes validation on larger cohorts, algorithm optimization, and real-time
integration into wearable systems.

---

## Notebook

- Main analysis notebook:
  
Effect_of_Physiological_Parameters_on_PPG_Signal_based_Glucose_Estimation.ipynb

## Notes on Data Availability

⚠️ The dataset is **not publicly available** due to privacy considerations. 

---
