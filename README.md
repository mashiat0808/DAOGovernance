# 🧩 DAO Governance Census 2025  
*A Unified Multi-Platform Dataset for Decentralized Autonomous Organization (DAO) Governance Analysis*  

![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)  
![Status](https://img.shields.io/badge/Status-Active-lightgreen.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)  
---

## 📘 Overview  
This repository contains the **code, notebooks, and methodology** used to construct an updated version of the **DAO Governance Census** dataset, which is hosted on [zenodo new census](10.5281/zenodo.17529116).
It consolidates DAO governance data from six major platforms — **Aragon**, **DAOstack**, **DAOhaus**, **Snapshot**, **Tally**, and **Realms (Solana)** — into a **unified schema** suitable for large-scale analysis of DAO activity, participation, and decision-making.  

This project extends the 2023 dataset released on [Zenodo](https://zenodo.org/records/10794916) with new data, improved retrieval logic, and reproducible Jupyter notebooks.

---

## 🗂 Repository Structure  

| File / Notebook | Description |
|------------------|-------------|
| `creating_census_dataset_(aragon,_daohaus,_daoStack)_from_zenodo.ipynb` | Processes DAO data from the [Zenodo dataset](https://zenodo.org/records/11663853) (Aragon, DAOstack, DAOhaus) and maps raw data to the unified schema. |
| `Snapshotdata-fullData.ipynb` | Retrieves and processes DAO data from the **Snapshot GraphQL API**, including proposals and votes with error handling and API rate-limit management. |
| `TallyData.ipynb` | Collects and processes data from the **Tally GraphQL API**; includes advanced multi-threaded vote retrieval (700K+ votes). |
| `RealmsData.ipynb` | Processes **Realms (Solana)** governance data. Raw data is retrieved locally via [mashiat0808/realmsData](https://github.com/mashiat0808/realmsData). |
| `dataset_merging_and_estimated_voting_power_and_total_voting_power_calculated.ipynb` | Estimates and normalizes voting power for platforms missing explicit data (e.g., Snapshot, Tally). |
| `aggregating_data_and_visualizations.ipynb` | Aggregates all platforms into the unified schema, generating the final `deployment.csv`, `proposals.csv`, and `votes.csv`, along with basic analytics and visualizations. |

---

## ⚙️ Data Sources  

| Platform | Source / Method | Description |
|-----------|------------------|--------------|
| **Aragon, DAOstack, DAOhaus** | [Zenodo DAO-analyzer Dataset (2025)](https://zenodo.org/records/11663853) | Updates daily |
| **Snapshot** | Snapshot GraphQL API | Queried directly for DAOs, proposals, and votes. |
| **Tally** | Tally GraphQL API | Expanded coverage with direct organization-level queries. |
| **Realms (Solana)** | [RealmsData GitHub Repo](https://github.com/mashiat0808/realmsData) via DRPC endpoint | On-chain Solana governance data fetched and parsed locally. |

---

## 🧠 Methodology  

Key improvements and features:
- **Unified schema** aligning six DAO platforms into common CSV formats (`deployment.csv`, `proposals.csv`, `votes.csv`).  
- **Enhanced error handling** and retry logic for rate-limited or unstable APIs.  
- **Voting power estimation** for incomplete datasets (e.g., uniform power for missing weight fields).  
- **Parallel data retrieval** using `ThreadPoolExecutor` for Tally and Snapshot.  
- **Automated aggregation and visualization** across platforms for cross-DAO comparison.  

---

## 📊 Output Datasets  

The final integrated dataset includes three CSV files:


├── deployment.csv:  # DAO-level metadata and activity summary


├── proposals.csv # Governance proposal information


└── votes.csv # Individual vote-level records


Each file follows a **standardized schema** for interoperability and ease of use in downstream analysis.

---

### DESCRIPTION

The dataset comprises three CSV files: **`deployments.csv`**, **`proposals.csv`**, and **`votes.csv`**, each containing essential information about DAO (Decentralized Autonomous Organization) deployments, their proposals, and the corresponding votes. It includes data from multiple DAO platforms, namely **Aragon**, **DAOHaus**, **DAOstack**, **Realms**, **Snapshot**, and **Tally**.

The file **`deployments.csv`** provides insights into the general aspects of DAO deployments, including the platform on which each DAO is deployed, the total number of proposals, the number of unique voters, total votes cast, and the estimated voting power used within the deployment.

The file **`proposals.csv`** contains detailed information about all proposals associated with each DAO deployment. It includes the date of creation, the number of votes received, the total voting power employed by voters on each proposal, and the platform from which the proposal originates.

The file **`votes.csv`** records data about individual votes cast on DAO proposals. It includes the blockchain address of each voter, the voting power (weight) used in casting the vote, the timestamp of the vote, and the corresponding platform where the vote was registered.

---


### DATA-SPECIFIC INFORMATION FOR: [deployments.csv]

**Number of variables:** 7
**Variable List:**

| Field               | Description                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **deployment_id**   | Unique DAO deployment identifier. Each record corresponds to a distinct DAO instance within a platform.             |
| **platform**        | Name of the DAO platform where the deployment is hosted (e.g., Aragon, DAOhaus, DAOstack, Realms, Snapshot, Tally). |
| **name**            | The official or recorded name of the DAO deployment.                                                                |
| **proposals_count** | Total number of proposals created within the DAO deployment.                                                        |
| **unique_voters**   | Total number of distinct voter addresses that have participated in at least one proposal within the DAO.            |
| **votes_count**     | Total number of votes cast across all proposals within the DAO deployment.                                          |
| **estimated_vp**    | Estimated total voting power accumulated or used across all proposals within the DAO deployment.                    |

**Missing data codes:** `NaN`

---

### DATA-SPECIFIC INFORMATION FOR: [proposals.csv]

**Number of variables:** 6
**Variable List:**

| Field             | Description                                                                  |
| ----------------- | ---------------------------------------------------------------------------- |
| **proposal_id**   | Unique proposal identifier within the dataset.                               |
| **deployment_id** | Identifier linking the proposal to its corresponding DAO deployment.         |
| **date**          | Date when the proposal was created or published on the DAO platform.         |
| **votes_count**   | Number of votes cast on this proposal.                                       |
| **total_vp**      | Total voting power (sum of weights) used by voters in this proposal.         |
| **platform**      | DAO platform where the proposal is hosted (e.g., Snapshot, Tally, DAOstack). |

**Missing data codes:** NaN

---

### DATA-SPECIFIC INFORMATION FOR: [votes.csv]

**Number of variables:** 7
**Variable List:**

| Field             | Description                                                                              |
| ----------------- | ---------------------------------------------------------------------------------------- |
| **vote_id**       | Unique identifier for each vote record.                                                  |
| **proposal_id**   | Identifier of the proposal to which the vote corresponds.                                |
| **deployment_id** | Identifier of the DAO deployment where the proposal belongs.                             |
| **voter**         | Blockchain address of the user who cast the vote.                                        |
| **date**          | Timestamp or date when the vote was cast.                                                |
| **weight**        | Amount of voting power (e.g., token weight or delegated power) used in casting the vote. |
| **platform**      | DAO platform where the vote was registered (e.g., Snapshot, Tally, DAOhaus).             |

**Missing data codes:** `NaN`

---






## 🧩 Code Inspirations  
Some code structures and schema mappings were inspired by the [Grasia DAO Ecosystem Census](https://github.com/Grasia/dao-ecosystem-census/tree/main/deployments) repository.  
This project expands on that foundation with updated APIs, and improved automation.

---

## 👥 Authors & Contributors

| Name                    | Affiliation                                            | 
| ----------------------- | ------------------------------------------------------ | 
| **Mashiat Amin Farin**  | University of Texas at Dallas                          | 
| **Prof. Samer Hassan**  | Universidad Complutense de Madrid / Harvard University | 
| **Prof. Javier Arroyo** | Universidad de Alcalá / Universidad Complutense de Madrid                      | 
---

## 🔗 Links  
- **Original Dataset from 2023:** [Census of the Ecosystem of Decentralized Autonomous Organizations](https://zenodo.org/records/10794916))  
- **Realms Data Retrieval Repo:** [mashiat0808/realmsData](https://github.com/mashiat0808/realmsData)  
- **Paper (in progress):** *DAO Governance Census 2025: A Unified Multi-Platform Dataset*
- **Dataset (in progress):** To be uploaded to zenodo and link attached here.

---





