# Dynamic Treatment Plan Optimization using Restless Multi-Armed Bandits (RMAB)

This repository contains the implementation used for studying **dynamic treatment allocation using a Restless Multi-Armed Bandit (RMAB) framework**.
The objective is to learn treatment strategies from historical patient trajectories and evaluate them safely using **off-policy evaluation techniques**.

---

## Overview

In many healthcare settings, clinicians must decide **which patients should receive intervention when resources are limited**.
This work models patients as arms in a **Restless Multi-Armed Bandit**, where each patient’s health state evolves over time.

Using historical ICU data, the framework:

* constructs longitudinal patient trajectories
* learns value functions for treatment actions
* builds a treatment policy
* evaluates the policy using off-policy evaluation methods before any real-world deployment

This allows treatment strategies to be studied **without directly testing them on patients**.

---

## Methodology

The implementation follows three main stages.

### 1. Patient Trajectory Construction

Clinical records are converted into **time-ordered patient trajectories** where each timestep represents a patient state and the corresponding clinical intervention.

### 2. Policy Learning

Action-value models are trained to estimate the expected long-term impact of treatment decisions.
These models are combined into a policy that determines **which patients should receive treatment at each timestep**.

### 3. Off-Policy Evaluation

The learned policy is evaluated using historical data through:

* Weighted Importance Sampling (WIS)
* Effective Sample Size (ESS)
* Bootstrap confidence intervals

These methods estimate policy performance **without deploying the policy in practice**.

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

**improved_rmab_policy.py**
Implements policy evaluation utilities and importance-weight calculations.

**crmab_modelling.py**
Handles preprocessing, feature construction, behavior policy modelling, and Q-model training.

**crmab.py**
Provides utilities for constructing patient trajectories and RMAB state transitions.

**ope_testing.py**
Runs the off-policy evaluation experiments and produces evaluation metrics.

**policy_bundle.pkl**
Serialized artifact containing trained models and policy metadata used during evaluation.

---

## Installation

Install the required Python packages:

```
pip install -r requirements.txt
```

---

## Running Policy Evaluation

To evaluate the learned treatment policy using the provided artifacts:

```
python ope_testing.py
```

The script computes policy value estimates and produces diagnostic metrics used in the analysis.

---

## Output Metrics

The evaluation pipeline produces:

* estimated policy value
* effective sample size (ESS)
* trajectory-level diagnostics
* bootstrap confidence intervals

These metrics help assess the **stability and reliability of the learned policy**.

---

## Dataset

This project uses the **MIMIC-III Clinical Database (v1.4)**.

MIMIC-III (Medical Information Mart for Intensive Care) is a publicly available dataset containing **de-identified electronic health records of ICU patients** collected at Beth Israel Deaconess Medical Center between **2001 and 2012**.

The dataset includes records for more than **40,000 patients and roughly 60,000 ICU stays**.

Available data types include:

* demographics
* vital signs
* laboratory measurements
* medications and procedures
* diagnostic codes
* clinical notes
* hospital outcomes

Dataset access:

https://physionet.org/content/mimiciii/1.4/

### Access Requirements

Access to the dataset requires:

1. completing the **CITI data research training**
2. signing the **PhysioNet data use agreement**
3. obtaining credentialed access through PhysioNet

---

## Reproducibility

The repository provides the code used for:

* trajectory construction
* policy learning
* off-policy evaluation

A precomputed `policy_bundle.pkl` artifact is included so that the evaluation pipeline can be reproduced.

---

## License

This repository is released for **research and reproducibility purposes**.
