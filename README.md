# Dynamic Treatment Plan Optimization using Restless Multi-Armed Bandits (RMAB)

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
├── CRMAB.ipynb
├── OPE_Testing.ipynb
├── crmab_modelling.py
├── improved_rmab_policy.py
├── final_traj_clean_training_heart_v2_sorted_imputed.csv
├── policy_bundle.pkl
├── requirements
└── README.md
```

### File Descriptions

**CRMAB.ipynb**

Notebook used for constructing patient trajectories and preparing the RMAB training pipeline.

**OPE_Testing.ipynb**

Notebook used to perform off-policy evaluation experiments and analyze the learned policy.

**crmab_modelling.py**

Contains the implementation for data preprocessing, trajectory generation, feature construction, and policy learning.

**improved_rmab_policy.py**

Implements utilities used for evaluating the RMAB policy and computing importance weights.

**policy_bundle.pkl**

Serialized artifact containing the trained policy and model components used for evaluation.

**final_traj_clean_training_heart_v2_sorted_imputed.csv**

Processed dataset used to construct patient trajectories for training and evaluation.

**requirements**

List of Python dependencies required to run the project.

---

# Installation

Install the required Python packages:

```bash
pip install -r requirements
```

---

# Running the Experiments

The experimental pipeline consists of four main stages: trajectory construction, model training, policy evaluation, and policy refinement.  
The steps below follow the same workflow used in our experiments.

### Step 1: Data Preparation and Trajectory Construction

First, construct the patient trajectories from the processed ICU dataset.

Open and run the notebook:

```
CRMAB.ipynb
```

This notebook:

- loads the processed patient dataset  
- filters the required heart patient cohort  
- constructs time-ordered patient trajectories  
- prepares the data required for RMAB model training  

The output of this step is a structured trajectory dataset used for training the RMAB model.

---

### Step 2: RMAB Model Training

After trajectories are prepared, train the RMAB model using:

```
python crmab_modelling.py
```

This script:

- performs feature processing  
- trains the action-value models  
- learns the RMAB treatment policy  

The trained policy and model artifacts are saved as:

```
policy_bundle.pkl
```

---

### Step 3: Off-Policy Evaluation

Next, evaluate the learned treatment policy using historical patient trajectories.

Open and run:

```
OPE_Testing.ipynb
```

This notebook performs off-policy evaluation using importance sampling based methods to estimate the expected value of the learned policy.

The evaluation includes:

- Weighted Importance Sampling (WIS)
- Effective Sample Size (ESS)
- bootstrap confidence intervals

---

### Step 4: Policy Refinement and Validation

Finally, additional policy improvements and validation experiments can be performed using:

```
improved_rmab_policy.py
```

This script evaluates alternative policy configurations and compares the learned policy against the clinician policy under the off-policy evaluation framework.

# Output Metrics

The evaluation produces several metrics including:

* estimated policy value
* effective sample size (ESS)
* trajectory-level diagnostics
* bootstrap confidence intervals

These metrics help assess the **stability and reliability of the learned treatment policy**.

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
