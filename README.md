# Dynamic Treatment Plan Optimization using Restless Multi-Armed Bandits (RMAB)

> **Anonymous implementation for double-blind review**

This repository contains the implementation of a **Restless Multi-Armed Bandit (RMAB)** framework for **dynamic treatment planning in chronic disease management**. The system learns treatment policies from historical patient trajectories and evaluates them safely using **Off-Policy Evaluation (OPE)** methods before deployment.

---

## Overview

Healthcare decision systems often need to decide **which patients should receive treatment at each time step when resources are limited**.
This work models patients as **arms in a Restless Multi-Armed Bandit**, where each patient's health state evolves over time.

The proposed framework:

1. Constructs longitudinal patient trajectories
2. Defines reward signals based on clinical outcomes
3. Learns value functions for treatment actions
4. Builds a policy bundle representing the learned treatment strategy
5. Evaluates the policy using robust off-policy evaluation techniques

This approach allows **safe evaluation of treatment strategies using observational healthcare data**.

---

## Key Components

### RMAB Treatment Allocation

Each patient is modeled as an independent arm whose state evolves over time.
At every timestep the system decides **which subset of patients should receive intervention**.

### Policy Learning

The framework learns action-value functions (Q-models) that estimate the long-term impact of treatment decisions.

### Off-Policy Evaluation

Before applying a policy in practice, its performance is estimated using historical data via:

* Weighted Importance Sampling (WIS)
* Effective Sample Size (ESS)
* Bootstrap confidence intervals

These methods allow **reliable evaluation without deploying the policy in real clinical environments**.

---

## Repository Structure

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
Implements policy evaluation utilities, trajectory analysis, and importance-weight calculations.

**crmab_modelling.py**
Handles preprocessing, feature construction, behavior policy modelling, and Q-model training.

**crmab.py**
Provides utilities for trajectory generation and RMAB state transition handling.

**ope_testing.py**
Runs off-policy evaluation experiments and produces diagnostics for policy performance.

**policy_bundle.pkl**
Serialized artifact containing trained models, feature definitions, and policy metadata.

---

## Installation

Create a Python environment and install dependencies.

```
pip install -r requirements.txt
```

---

## Running Off-Policy Evaluation

To evaluate the learned policy using the provided bundle:

```
python ope_testing.py
```

This script computes policy value estimates and evaluation diagnostics.

---

## Outputs

Running the evaluation scripts produces:

* Estimated policy value
* Effective Sample Size (ESS)
* Trajectory-level diagnostics
* Bootstrap confidence intervals

These metrics help assess **policy reliability and robustness**.

---

## Reproducibility

This repository provides:

* Implementation of the RMAB treatment allocation framework
* Policy learning pipeline
* Off-policy evaluation code
* Precomputed policy bundle artifact

Together these components enable **reproducible policy evaluation experiments**.

---

## Dataset

The experiments rely on a clinical dataset derived from critical care patient records.

Due to dataset access restrictions, the raw dataset is not included in this repository.
Users should obtain the dataset through the appropriate access process and preprocess it using the provided scripts.

---

## License

This repository is provided for **research and reproducibility purposes**.
