# Fenofibrate_Diabetic-Retinopathy
Bidirectional Bayesian evidence synthesis framework modeling Fenofibrate efficacy for Diabetic Retinopathy by synthesizing LENS &amp; ACCORD-Eye trial data. Features Monte Carlo sampling, posterior overlap metrics (Bhattacharyya, Wasserstein), and utility-based decision concordance with sensitivity analysis.

---

# README.md

```markdown
# Bidirectional Bayesian Evidence Synthesis: LENS ⇄ ACCORD-Eye
### Fenofibrate for Diabetic Retinopathy — Primary Care Decision Framework

This repository implements a **Bidirectional Bayesian Evidence Synthesis** model to evaluate the real-world clinical utility and decision stability of Fenofibrate for Diabetic Retinopathy (DR) progression. 

By modeling and harmonizing parameter estimates from two landmark trials—**LENS (2024)** and **ACCORD-Eye (2010)**—this quantitative framework quantifies statistical effect overlaps and tests point-of-care prescribing decision concordance across multi-variable patient profiles.

---

## 📌 Key Features

- **Monte Carlo Posterior Sampling:** Propagates trial-level uncertainty using normal approximations on the log-Hazard Ratio scale alongside Beta-Binomial conjugate models for baseline event rates ($N = 100,000$).
- **Posterior Overlap Metrics:** Evaluates distributional similarity using **Bhattacharyya Distance**, **Jensen-Shannon Divergence**, **Wasserstein Distance**, and **95% High-Density Interval (HDI) Overlap**.
- **Utility Decision Concordance Index (UDCI):** Calculates net utility differences considering absolute risk reduction (ARR), eGFR penalties (renal safety), and cumulative daily pill burden across simulated patient cohorts ($N = 5,000$).
- **Comprehensive Sensitivity Analysis:** Tests 5 pre-defined clinical preference scenarios (*Base Case*, *Pro-Treatment*, *Pro-Conservative*, *eGFR-Sensitive*, and *Pill-Burden-Sensitive*) to assess boundary stability.
- **Automated Visualization:** Produces publication-ready four-panel figures detailing posterior densities, decision concordance heatmaps, sensitivity bar charts, and pre-specified scenario typologies.

---

## 🛠️ Installation & Dependencies

Ensure you have **Python 3.8+** installed along with the following numerical and visualization libraries:

```bash
pip install numpy pandas matplotlib seaborn scipy

```

---

## 🚀 Usage

Execute the pipeline directly from your terminal:

```bash
python bayesian_fenofibrate_synthesis.py

```

### Outputs

1. **Console Summary:** Full step-by-step breakdown of trial estimates, sampling parameters, distance metrics, classified decision scenario (A–D typology), and pre-specified discussion templates.
2. **Visual Artifact:** Saves `bidirectional_bayesian_framework_sensitivity.png` (300 DPI) to the current working directory.

---

## 📊 Pre-Specified Typology Framework

The model categorizes decision stability into a mutually exclusive framework based on statistical overlap and clinical decision concordance:

| Scenario | Posterior Overlap | Decision Concordance (UDCI) | Structural Interpretation |
| --- | --- | --- | --- |
| **A** | **High** (>80%) | **High** (>90%) | **Full Structural & Utility Stability** — Universal decision framework suitable for simple point-of-care integration. |
| **B** | **Low** (<=80%) | **Low** (<=90%) | **Contextual Non-Equivalence** — Trials cannot be treated as interchangeable; guidelines require strict risk stratification. |
| **C** | **Low** (<=80%) | **High** (>90%) | **Robust Utility Boundary** — Effect heterogeneity does not alter clinical choices; baseline risk drives prescribing boundaries. |
| **D** | **High** (>80%) | **Low** (<=90%) | **Utility Threshold Hypersensitivity** — Statistical compatibility, but baseline risk shifts require individualized calculators. |

---

## 🔬 Trial Data Inputs

| Parameter | LENS (2024) | ACCORD-Eye (2010) |
| --- | --- | --- |
| **Trial Design** | Pragmatic, dedicated DR trial | Explanatory, CV trial sub-study |
| **Sample Size (Treatment / Control)** | 576 / 575 | 1,428 / 1,428 |
| **Hazard Ratio (95% CI)** | **0.73** (0.58 – 0.91) | **0.60** (0.42 – 0.87) |
| **Relative Risk Reduction (RRR)** | 27% | 40% |
| **Control Event Rate** | 29.2% | 10.2% |
| **Number Needed to Treat (NNT)** | 15.4 | 27.0 |

---

## 📜 License

Distributed under the **MIT License**. Feel free to adapt and extend for secondary Bayesian clinical decision analyses.

```

```
