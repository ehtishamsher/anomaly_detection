# 🌲 Anomaly Detection Using Isolation Forest

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=for-the-badge&logo=jupyter)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-green?style=for-the-badge&logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

A practical implementation of **Isolation Forest** for detecting fraudulent credit card transactions — an unsupervised anomaly detection approach that isolates outliers instead of profiling normal behavior.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [How Isolation Forest Works](#-how-isolation-forest-works)
- [Dataset](#-dataset)
- [What's Covered](#-whats-covered)
- [Results](#-results)
- [Tech Stack](#-tech-stack)
- [How to Run](#-how-to-run)
- [Key Parameters](#-key-parameters)

---

## 🌍 Overview

Most fraud detection models learn what "normal" looks like and flag anything different. Isolation Forest takes the opposite approach — it tries to **isolate anomalies directly** by randomly partitioning the data. Fraudulent transactions are rare and unusual, so they get isolated much faster than normal ones.

This notebook applies Isolation Forest to real-world credit card transaction data to detect fraudulent activity.

---

## 🧠 How Isolation Forest Works

1. Randomly select a feature and a split value
2. Recursively partition the data into a tree
3. **Anomalies** (rare, unusual points) get isolated in fewer splits → shorter path length
4. **Normal points** require many splits to isolate → longer path length
5. Average path length across many trees gives an anomaly score

> Think of it like a game of "20 questions" — a weird, unique answer gets identified in far fewer questions than a common one.

---

## 📊 Dataset

| Property       | Details                                                           |
| -------------- | ----------------------------------------------------------------- |
| Name           | Credit Card Fraud Detection                                       |
| Source         | [Kaggle](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) |
| Size           | 284,807 transactions                                              |
| Fraud cases    | 492 (only 0.17%)                                                  |
| Features       | Time, V1–V28 (PCA transformed), Amount, Class                     |
| Missing values | None                                                              |

> ⚠️ Dataset not included due to size (143MB). Download from Kaggle link above and place in `Isolation_Forest/dataset/`.

---

## ✅ What's Covered

- **Data Loading & Exploration** — shape, data types, class distribution
- **Feature Selection** — using `Time` and `Amount` as primary features
- **Feature Scaling** — StandardScaler applied to `Amount`
- **Model Training** — Isolation Forest with `contamination=0.001`
- **Anomaly Detection** — predictions mapped to normal (1) and anomaly (-1)
- **Visualization** — scatter plot of Time vs Amount with anomalies highlighted in red
- **Result Analysis** — total anomalies detected vs actual fraud count

---

## 📈 Results

| Metric             | Value        |
| ------------------ | ------------ |
| Total transactions | 284,807      |
| Anomalies detected | ~285 (0.1%)  |
| Contamination rate | 0.001        |
| Features used      | Time, Amount |

The scatter plot clearly shows normal transactions clustered at low amounts while anomalies (red dots) appear as high-value outliers spread across time.

---

## 🛠️ Tech Stack

```
Python 3.8+
pandas          — data loading and manipulation
numpy           — array operations
matplotlib      — scatter plot visualization
scikit-learn    — IsolationForest, StandardScaler
```

---

## 🚀 How to Run

### 1. Clone the repository

```bash
git clone https://github.com/ehtishamsher/anomaly_detection.git
cd anomaly_detection/Isolation_Forest
```

### 2. Download the dataset

Download from: https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud  
Place `creditcard.csv` inside the `dataset/` folder.

### 3. Install dependencies

```bash
pip install pandas numpy matplotlib scikit-learn jupyter
```

### 4. Run the notebook

```bash
jupyter notebook Anomaly_detection_using_Isolation_Forest.ipynb
```

---

## ⚙️ Key Parameters

| Parameter       | Value Used | Meaning                               |
| --------------- | ---------- | ------------------------------------- |
| `contamination` | 0.001      | Expected 0.1% of data to be anomalous |
| `n_estimators`  | 100        | Number of isolation trees             |
| `random_state`  | 42         | Reproducibility                       |

**Why `contamination=0.001`?**  
The real fraud rate in this dataset is 0.17%. Setting contamination too high (e.g. 0.2) causes the model to flag 20% of all transactions as fraud — far too many false alarms. `0.001` keeps it close to the true fraud rate.

---

## 🔗 Related Notebooks

- [DBSCAN Clustering Anomaly Detection](../DBSCAN/)
- [Local Outlier Factor Detection](../LOF/) _(coming soon)_

---

_Part of the Anomaly Detection series — comparing unsupervised methods for fraud detection._
