# Dynamic Treatment Plan Optimization using Restless Multi-Armed Bandits (RMAB) 🧠⚕️

> **Anonymous implementation for double-blind review**

This repository provides the implementation and artifacts used for evaluating **dynamic treatment allocation policies** using a **Restless Multi-Armed Bandit (RMAB)** framework.

The goal is to learn treatment strategies from historical patient trajectories and evaluate them safely using **Off-Policy Evaluation (OPE)** before real-world deployment.

---

# 🔍 Overview

Healthcare systems often need to decide **which patients should receive treatment when resources are limited**.

In this project:

* Each patient is modeled as an **arm in a Restless Multi-Armed Bandit**
* Patient health states evolve over time
* Treatment decisions are learned from historical trajectories
* Policies are evaluated offline using statistical OPE methods

Pipeline:

1. Patient trajectory construction
2. Feature engineering and reward modelling
3. Policy learning using RMAB formulation
4. Policy bundle construction
5. Off-policy evaluation using historical data

---

# 🧠 Methodology

The framework consists of three major components.

### 1. Trajectory Construction

Patient trajectories are built from longitudinal ICU records where each timestep represents a clinical state.

### 2. Policy Learning

Action-value models are trained to estimate the expected long-term benefit of treatment decisions.

These models are combined to form a **policy bundle** representing the treatment allocation strategy.

### 3. Off-Policy Evaluation

Policies are evaluated using historical data through:

* **Weighted Importance Sampling (WIS)**
* **Effective Sample Size (ESS)**
* **Bootstrap confidence intervals**

This allows reliable estimation of policy performance **without deploying the policy in a real clinical environment**.

---

# 📁 Repository Structure

```text
.
├── improved_rmab_policy.py
├── crmab_modelling.py
├── crmab.py
├── ope_testing.py
├── policy_bundle.pkl
├── requirements.txt
└── README.md
```

### File Descriptions

**improved_rmab_policy.py**

Implements RMAB policy utilities, trajectory analysis, and importance weight calculations.

**crmab_modelling.py**

Handles preprocessing, feature construction, behaviour policy modelling, and Q-model training.

**crmab.py**

Contains utilities for trajectory generation and RMAB state transitions.

**ope_testing.py**

Runs off-policy evaluation experiments and generates evaluation diagnostics.

**policy_bundle.pkl**

Serialized artifact containing trained models, feature definitions, and policy metadata.

---

# ⚙️ Installation

Create a Python environment and install dependencies.

```bash
pip install -r requirements.txt
```

---

# 🚀 Running Policy Evaluation

To evaluate the learned policy using the provided policy bundle:

```bash
python ope_testing.py
```

The script computes policy value estimates and produces evaluation diagnostics.

---

# 📊 Output Metrics

Running the evaluation pipeline produces:

* Estimated policy value
* Effective Sample Size (ESS)
* Trajectory-level diagnostics
* Bootstrap confidence intervals

These metrics help analyze **policy reliability and robustness**.

---

# 📊 Dataset

This project uses the **MIMIC-III Clinical Database (v1.4)**.

MIMIC-III (Medical Information Mart for Intensive Care) is a publicly available dataset containing **de-identified electronic health records from intensive care unit patients** collected at Beth Israel Deaconess Medical Center between **2001 and 2012**.

The dataset contains information for **over 40,000 patients and around 60,000 ICU admissions**.

Data modalities include:

* Patient demographics
* Vital sign measurements
* Laboratory test results
* Medications and treatment events
* Clinical procedures
* Diagnostic codes (ICD-9)
* Fluid balance records
* Clinical notes
* Hospital outcomes

Dataset access:

https://physionet.org/content/mimiciii/1.4/

---

# 🔐 Dataset Access Requirements

Access to the dataset requires:

1. Completion of the **CITI “Data or Specimens Only Research” training**
2. Signing the **PhysioNet Data Use Agreement**
3. Credential approval through PhysioNet

---

# 🔁 Reproducibility

This repository provides:

* RMAB treatment allocation implementation
* Policy learning pipeline
* Off-policy evaluation scripts
* Precomputed policy bundle artifact

These components enable **reproducible policy evaluation experiments**.

---

# 📄 License

This repository is released for **research and reproducibility purposes**.
