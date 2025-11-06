# 🧩 Environment Setup and Usage Guide

## Environment Setup

To reproduce the analyses and validation of the DAO dataset, first set up a Python environment using the provided `requirements.txt` file:

```bash
pip install -r requirements.txt
```

---

## Loading the Dataset

The dataset consists of three CSV files:

* **`deployments.csv`** – General DAO deployment information, including platform, number of proposals, unique voters, total votes, and estimated voting power.
* **`proposals.csv`** – Detailed proposal-level information for each DAO, including date, votes count, and total voting power.
* **`votes.csv`** – Vote-level data for all proposals, including voter address, vote weight, and vote date.

You can load the datasets in Python using `pandas`:

```python
import pandas as pd

deployments = pd.read_csv("deployments.csv")
proposals = pd.read_csv("proposals.csv")
votes = pd.read_csv("votes.csv")
```

---

## Reproducing the Analyses

A fully annotated Jupyter Notebook — **`DAO_data_usage_and_validation.ipynb`** — is provided.
It includes the following reproducible steps:

### 1. Basic Dataset Inspection

* Displays the number of rows, columns, and data types for each file.

### 2. Automated Validation Checks

* Ensures uniqueness of primary keys (`deployment_id`, `proposal_id`, `vote_id`)
* Detects missing values
* Verifies proposal counts per deployment
* Validates vote counts per proposal
* Checks total voting power per deployment

### 3. Flagging Missing or Incomplete Data

* Identifies DAOs with missing names
* Flags votes with missing timestamps

### 4. Exploratory Analyses and Visualizations

* Lists top DAOs by total voting power
* Plots the distribution of vote weights

---

## Reproducibility Notes

* The notebook is **self-contained** and can be executed from start to finish to reproduce all validation and analysis results.
* Any missing values or inconsistencies are **explicitly flagged** for transparency.
* Example visualizations are included to demonstrate potential use cases; reviewers and researchers can extend the analyses within the same environment.

---

