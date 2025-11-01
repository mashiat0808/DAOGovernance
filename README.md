# 🧩 DAO Governance Census 2025  
*A Unified Multi-Platform Dataset for Decentralized Autonomous Organization (DAO) Governance Analysis*  

![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)  
![Status](https://img.shields.io/badge/Status-Active-lightgreen.svg)

---

## 📘 Overview  
This repository contains the **code, notebooks, and methodology** used to construct an updated version of the **DAO Governance Census** dataset.  
It consolidates DAO governance data from six major platforms — **Aragon**, **DAOstack**, **DAOhaus**, **Snapshot**, **Tally**, and **Realms (Solana)** — into a **unified schema** suitable for large-scale analysis of DAO activity, participation, and decision-making.  

This project extends the 2023 dataset released on [Zenodo](https://zenodo.org/records/11663853) with new data, improved retrieval logic, and reproducible Jupyter notebooks.

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
| **Aragon, DAOstack, DAOhaus** | [Zenodo DAO Census Dataset (2023)](https://zenodo.org/records/11663853) | Original census data reprocessed for schema consistency. |
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


├── deployment.csv # DAO-level metadata and activity summary


├── proposals.csv # Governance proposal information


└── votes.csv # Individual vote-level records


Each file follows a **standardized schema** for interoperability and ease of use in downstream analysis.

---

## 🧩 Code Inspirations  
Some code structures and schema mappings were inspired by the [Grasia DAO Ecosystem Census](https://github.com/Grasia/dao-ecosystem-census/tree/main/deployments) repository.  
This project expands on that foundation with additional platforms, updated APIs, and improved automation.

---

## 🔗 Links  
- **Original Dataset:** [Zenodo Record (2023)](https://zenodo.org/records/11663853)  
- **Realms Data Retrieval Repo:** [mashiat0808/realmsData](https://github.com/mashiat0808/realmsData)  
- **Paper (in progress):** *DAO Governance Census 2025: A Unified Multi-Platform Dataset*
- **Dataset (in progress):** To be uploaded to zenodo and link attached here.

---





