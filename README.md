```markdown
# Probabilistic Evidence Synthesis for Fenofibrate Prescribing Decisions

A proof-of-concept Monte Carlo simulation framework evaluating prescribing decision concordance between the **LENS (2024)** and **ACCORD-Eye (2010)** trials. 

By harmonizing trial estimands onto a unified 4-year Risk Ratio (RR) scale and mapping patient-level baseline risk, eGFR decline penalties, and pill burden utilities, this framework quantifies where clinical evidence converges and where prescribing decisions become sensitive to trial choice.

---

## Key Features

* **Effect-Scale Harmonization:** Converts LENS Hazard Ratios ($HR = 0.73$) and ACCORD Odds Ratios ($OR = 0.60$) into approximate 4-year Risk Ratios ($RR$) under constant-hazard and baseline-risk assumptions.
* **Log-Normal Uncertainty Propagation:** Draws 100,000 sampling distributions to capture parameter uncertainty across both trials.
* **Distributional Overlap Metrics:** Quantifies divergence between evidence bases using Jensen-Shannon distance, Bhattacharyya distance, Wasserstein distance, and 95% equal-tail interval overlap.
* **Expected Utility Decision Engine:** Evaluates individual expected utility $E[\Delta U \mid \text{data}, \text{patient}] > 0$ incorporating analytical eGFR decline penalties and incremental pill burden disutility.
* **Calibrated Logit-Normal Heterogeneity:** Generates synthetic patient populations with calibrated logit-normal risk distributions to preserve population target means.
* **Multi-Way Sensitivity Analysis:** Evaluates robustness across varying between-patient heterogeneity levels ($\sigma \in [0.1, 0.7]$) and continuous utility weight distributions (1,000 configurations).

---

## Workflow Overview


```

```
                      ┌───────────────────────────┐
                      │  LENS (2024) HR: 0.73     │
                      │  ACCORD (2010) OR: 0.60   │
                      └─────────────┬─────────────┘
                                    │
                     [ Estimand Harmonization ]
                                    │
                                    ▼
                      ┌───────────────────────────┐
                      │  Log-Normal Sampling      │
                      │  4-Year Risk Ratios (RR)  │
                      └─────────────┬─────────────┘
                                    │
                    ┌───────────────┴───────────────┐
                    ▼                               ▼
     ┌──────────────────────────────┐ ┌──────────────────────────────┐
     │ Synthetic Patient Profiles   │ │ Analytical Expected Utility  │
     │ (Risk, eGFR, Pill Count)     │ │ E[ΔU] = Benefit - Penalties  │
     └──────────────┬───────────────┘ └──────────────┬───────────────┘
                    └───────────────┬────────────────┘
                                    │
                                    ▼
                      ┌───────────────────────────┐
                      │ Decision Concordance      │
                      │ & Threshold Boundaries    │
                      └───────────────────────────┘

```

```

---

## Key Findings & Performance Metrics

* **High Decision Concordance:** Achieving **94.7% overall concordance** in the pooled population between LENS and ACCORD parameterizations.
* **Utility Weight Robustness:** Across 1,000 sampled utility weight configurations, mean concordance remained high at **95.2%** (95% range: 89.5%–99.2%), with 95.9% of configurations exceeding 90% concordance.
* **Unidirectional Discordance:** Decision discordance is concentrated near the 11%–18% baseline risk boundary and within eGFR levels of 60–67 mL/min/1.73m², where ACCORD adopts a lower threshold for prescribing relative to LENS.

---

## Installation & Setup

### Prerequisites
* Python 3.9 or higher

### Dependencies
Install required packages via `pip`:

```bash
pip install numpy pandas matplotlib scipy

```

---

## Usage

Run the primary framework simulation directly from your terminal:

```bash
python fenofibrate_synthesis.py

```

### Outputs

The execution script sequentially performs:

1. **Section 1–3:** Data initialization and log-normal sampling.
2. **Section 4:** Calculation of distributional distance metrics (Jensen-Shannon, Wasserstein, Bhattacharyya).
3. **Section 5–7:** Synthetic population generation and reciprocal parameterization analysis.
4. **Section 8–10:** Robustness and sensitivity analyses (Heterogeneity & Utility Weights).
5. **Section 11:** Deterministic risk threshold mapping across varying eGFR and pill burden levels.
6. **Section 12:** Visualization generation.

---

## Mathematical Formulation

Prescribing decisions are driven by net expected utility **E[ΔU]**:

> **E[ΔU] = Baseline Risk × RRR × (ω_progression + ω_treatment) − Penalty_eGFR − Penalty_pill**

Where:
* **RRR** = 1 − RR
* **Penalty_eGFR** is calculated analytically for normal eGFR decline distributions *D ~ N(μ, σ²)* using truncated normal expectations.
* **Penalty_pill** = ω_pill × max(0, Pills − Pills_baseline)
---

## Limitations & Disclaimer

This software is a **proof-of-concept analytical framework** intended strictly for medical informatics and health economics research. It is not prospectively validated for clinical decision support or direct patient care. Utility weights and synthetic patient profiles are illustrative and should be validated against individual patient data (IPD) and empirical patient elicitation studies.

---

## License

Distributed under the MIT License. See `LICENSE` for more information.

```

```
