# Dynamic Treatment Plan Optimization using Restless Multi-Armed Bandits (RMAB)

Anonymous implementation for reproducibility accompanying a research submission.

---

## 🔎 Overview

This repository contains the implementation of a **Restless Multi-Armed Bandit (RMAB)** framework designed for **dynamic treatment optimization in chronic disease management**.

The goal of this project is to learn an optimal treatment allocation policy from historical patient trajectories and evaluate it safely using **Off-Policy Evaluation (OPE)** methods before real-world deployment.

The pipeline includes:

1️⃣ Patient trajectory construction
2️⃣ Reward modelling from clinical outcomes
3️⃣ Learning policy value functions (Q-models)
4️⃣ Constructing a treatment policy bundle
5️⃣ Evaluating candidate policies using **Weighted Importance Sampling (WIS)** and bootstrap confidence intervals

---

## 🧠 Key Components

### RMAB Treatment Allocation

Patients are modeled as independent arms whose health states evolve over time.
At each time step, the system decides which patients should receive intervention.

### Policy Learning

A policy bundle is constructed containing:

* learned Q-models for treatment actions
* state feature definitions
* reward transformation logic

### Off-Policy Evaluation (OPE)

To ensure safety before deployment, learned policies are evaluated using:

* Weighted Importance Sampling (WIS)
* Effective Sample Size (ESS) diagnostics
* Bootstrap confidence intervals

This enables **reliable estimation of treatment policy performance using observational healthcare data**.

---

## 📁 Repository Structure

```
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
Implements RMAB policy utilities including policy evaluation, trajectory analysis, and importance-weight calculations.

**crmab_modelling.py**
Handles data preprocessing, feature construction, behavior policy modelling, and Q-model training.

**crmab.py**
Contains helper functions for trajectory generation and RMAB state transition processing.

**ope_testing.py**
Runs off-policy evaluation experiments and generates diagnostics such as WIS estimates and confidence intervals.

**policy_bundle.pkl**
Serialized artifact containing the learned policy bundle including trained models and state feature definitions.

---

## ⚙️ Installation

Create a Python environment and install dependencies.

```
pip install -r requirements.txt
```

---

## ▶ Running Off-Policy Evaluation

To evaluate the learned policy using the provided policy bundle:

```
python ope_testing.py
```

This will compute policy value estimates and diagnostic statistics used to assess treatment policy performance.

---

## 📊 Outputs

Running the evaluation scripts will produce:

* policy value estimates
* effective sample size (ESS)
* trajectory level diagnostics
* bootstrap confidence intervals

These metrics are used to analyze **policy reliability and stability**.

---

## 🔁 Reproducibility

This repository provides:

✔ code for trajectory modelling
✔ policy learning implementation
✔ off-policy evaluation scripts
✔ a precomputed policy bundle artifact

Together these components enable reproducibility of the policy evaluation pipeline.

---

## ⚠ Dataset

The experiments rely on a clinical dataset derived from critical care patient records.

Due to data usage restrictions, the raw dataset is not included in this repository.
Users should obtain access to the appropriate dataset and preprocess it using the provided scripts.

---

## 📄 License

This repository is released for research and reproducibility purposes.
