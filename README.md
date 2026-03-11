# Dynamic Treatment Plan Optimization using Restless Multi-Armed Bandits (RMAB) 🧠⚕️

This repository contains the implementation used to study **dynamic treatment allocation using a Restless Multi-Armed Bandit (RMAB) framework**.
The goal is to learn treatment strategies from historical patient trajectories and evaluate them safely using **off-policy evaluation (OPE)** techniques.

---

# Overview

In many healthcare environments, clinicians must decide **which patients should receive treatment when resources are limited**.

This project models patients as arms in a **Restless Multi-Armed Bandit**, where each patient’s health state evolves over time.

Using historical ICU records, the framework:

* constructs longitudinal patient trajectories
* learns value functions for treatment actions
* builds a treatment policy
* evaluates the policy using off-policy evaluation methods before any real-world deployment

This allows treatment strategies to be studied **without directly testing them on patients**.

---

# Methodology

The implementation follows three main stages.

### 1. Patient Trajectory Construction

Clinical records are converted into **time-ordered patient trajectories** where each timestep represents a patient state and the corresponding clinical intervention.

### 2. Policy Learning

Action-value models are trained to estimate the expected long-term impact of treatment decisions.
These models are combined into a policy that determines **which patients should receive treatment at each timestep**.

### 3. Off-Policy Evaluation

The learned policy is evaluated using historical data through:

* **Weighted Importance Sampling (WIS)**
* **Effective Sample Size (ESS)**
* **Bootstrap confidence intervals**

These methods estimate policy performance **without deploying the policy in practice**.

---

# Repository Structure

```text
.
├── code
│   ├── crmab_modelling.py
│   ├── crmab.py
│   ├── improved_rmab_policy.py
│   └── ope_testing.py
│
├── data
│   └── final_traj_clean_training_heart_v2_sorted_imputed.csv
│
├── models
│   ├── policy_bundle.pkl
│   ├── q_models_fqe_strong.pkl
│   ├── behavior_model_lgbm.pkl
│   └── behavior_model_lgbm_statecols.pkl
│
├── outputs
│   ├── ope_crossfit_results.csv
│   ├── ope_crossfit_summary.json
│   ├── policy_mix_grid_wis_TUNE.csv
│   └── policy_mix_selected_summary.json
│
├── notebooks
│   ├── CRMAB.ipynb
│   └── OPE_Testing.ipynb
│
├── scripts
│   ├── reproduce_ope.sh
│   └── build_sequences_from_csv.py
│
├── requirements.txt
└── README.md
```

---

# Installation

Install the required Python packages.

```bash
pip install -r requirements.txt
```

---

# Quick Reproduction

After installing dependencies, the full evaluation pipeline can be reproduced with:

```bash
bash scripts/reproduce_ope.sh
```

This script will:

* load the trained policy bundle
* run the off-policy evaluation pipeline
* generate evaluation results and diagnostic outputs

---

# Running Policy Evaluation Manually

You can also run the evaluation script directly:

```bash
python ope_testing.py
```

Results will be written to the **outputs** directory.

---

# Generated Outputs

Running `crmab_modelling.py` produces several artifacts used in policy evaluation.

Important outputs include:

* **policy_bundle.pkl** – trained RMAB policy bundle
* **q_models_fqe_strong.pkl** – fitted Q-evaluation models
* **behavior_model_lgbm.pkl** – learned behavior policy model
* **behavior_model_lgbm_statecols.pkl** – behavior model with feature ordering
* **ope_crossfit_results.csv** – cross-fitted off-policy evaluation results
* **ope_crossfit_summary.json** – summary statistics of policy performance
* **policy_mix_selected_summary.json** – selected policy configuration

These artifacts allow the evaluation pipeline to be reproduced without retraining models.

---

# Dataset

This project uses the **MIMIC-III Clinical Database (v1.4)**.

MIMIC-III (Medical Information Mart for Intensive Care) is a publicly available dataset containing **de-identified electronic health records from intensive care unit patients** collected at Beth Israel Deaconess Medical Center between **2001 and 2012**.

The dataset contains records for **over 40,000 patients and approximately 60,000 ICU admissions**.

Available data types include:

* patient demographics
* vital sign measurements
* laboratory test results
* medications and treatment events
* clinical procedures
* diagnostic codes (ICD-9)
* fluid balance records
* clinical notes
* hospital outcomes

Dataset access:

https://physionet.org/content/mimiciii/1.4/

### Access Requirements

Access to the dataset requires:

1. completion of the **CITI data research training**
2. signing the **PhysioNet data use agreement**
3. credentialed access approval through PhysioNet

---

# Reproducibility

The repository provides the code used for:

* trajectory construction
* policy learning
* off-policy evaluation

A precomputed **policy_bundle.pkl** artifact is included so the evaluation pipeline can be reproduced.

---

# Notes for Double-Blind Review

To maintain anonymity during the review process, the repository does not contain author names or institutional affiliations.

---

# License

This repository is released for **research and reproducibility purposes**.
