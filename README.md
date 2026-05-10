# Alibaba Microservice Trace Analysis & Node Prediction

## 📌 Project Overview
This research project focuses on identifying resource dependencies and predicting node traffic patterns within a large-scale microservice architecture. By leveraging the **Alibaba Cluster Trace dataset**, we analyze how logical service interactions (Upstream/Downstream calls) impact physical resource allocation. The core objective is to predict whether a microservice call will be assigned to a **High Request Node**, facilitating proactive system optimization.

## 🛠️ Tech Stack & Environment
*   **Language:** Python 3.x
*   **Libraries:** `pandas`, `scikit-learn`, `numpy`
*   **Environment:** Virtual Environment (`.venv`)
*   **Model:** Logistic Regression with Cost-Sensitive Learning

## 📊 Data Engineering
The project integrates multiple data streams to build a comprehensive system view:
*   **CallGraph Analysis:** Interpreting `rpc_id` (dot-notation) to reconstruct call hierarchies and determine execution depth.
*   **Metric Integration:** Merging logical traces with physical `node_metrics` and `ms_metrics` to correlate response times (`rt`) with hardware utilization.
*   **Feature Transformation:** Converting categorical microservice IDs and interface names into numerical formats suitable for machine learning.

## 🚀 Machine Learning Results
We implemented a Logistic Regression classifier to distinguish between **Normal Nodes (0)** and **High Request Nodes (1)**. 

### Final Performance Metrics
To address the natural class imbalance in cluster data, the model was trained using **balanced class weights**.

| Metric | Score |
| :--- | :--- |
| **Model Accuracy** | 58.18% |
| **Recall (High Request Nodes)** | **0.41** |
| **Precision (High Request Nodes)** | 0.26 |
| **F1-Score (Normal Nodes)** | 0.70 |

Later On Went ahead with different implemtation strategy as the values in the columns were descrete, so for this Decision Tree was selected and instead of all the columns we used the top 5 important columns ,whose importance was extracted from the feature importance result of Logistic Regression.

| Metric | Score |
| :--- | :--- |
| **Model Accuracy** | 58.18% |
| **Recall (High Request Nodes)** | **0.98** |
| **Precision (High Request Nodes)** | **0.98** |
| **F1-Score (Normal Nodes)** | **0.98** |

### Feature Importance (Weights)
The model coefficients reveal the primary drivers of node traffic:
*   **Upstream Microservice InstanceID(`uminstanceid`):** **0.587** (Strongest predictor; traffic is driven by the caller's identity).
*   **Upstream Microservice (`um`):** **0.61** (The Upstream service has a secondary influence).

## 📂 Repository Structure
```text
├── .venv/                   # Virtual environment
├── .gitignore               # Excludes large CSVs and environment files
├── Alibaba_Analysis.ipynb    # Main research notebook & model training
├── data_cleaning.py         # Scripts for data merging and preprocessing
└── README.md                # Project documentation
