# 🔵 Anomaly Detection Using DBSCAN Clustering

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=for-the-badge&logo=jupyter)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-green?style=for-the-badge&logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

A practical implementation of **DBSCAN (Density-Based Spatial Clustering of Applications with Noise)** for anomaly detection — a clustering approach that naturally identifies outliers as points that don't belong to any cluster.

---

## 📌 Table of Contents

- [🔵 Anomaly Detection Using DBSCAN Clustering](#-anomaly-detection-using-dbscan-clustering)
  - [📌 Table of Contents](#-table-of-contents)
  - [🌍 Overview](#-overview)
  - [🧠 How DBSCAN Works](#-how-dbscan-works)
  - [📊 Dataset](#-dataset)
  - [✅ What's Covered](#-whats-covered)
  - [📈 Results](#-results)
  - [🛠️ Tech Stack](#️-tech-stack)
  - [🚀 How to Run](#-how-to-run)
    - [1. Clone the repository](#1-clone-the-repository)
    - [2. Download the dataset](#2-download-the-dataset)
    - [3. Install dependencies](#3-install-dependencies)
    - [4. Run the notebook](#4-run-the-notebook)
  - [⚙️ Key Parameters](#️-key-parameters)
  - [⚖️ DBSCAN vs Isolation Forest](#️-dbscan-vs-isolation-forest)

---

## 🌍 Overview

Unlike Isolation Forest which scores individual points, **DBSCAN groups dense regions into clusters** and labels anything that doesn't fit as noise — label `-1`. These noise points are our anomalies.

This makes DBSCAN powerful for detecting anomalies in datasets where normal behavior forms clear clusters and fraudulent behavior is sparse and scattered.

---

## 🧠 How DBSCAN Works

1. Pick any unvisited point
2. Find all points within radius **epsilon (ε)**
3. If enough neighbors exist (`min_samples`) → start a new cluster
4. Expand the cluster by visiting each neighbor recursively
5. Points with **no nearby neighbors** get labeled **-1 (noise/anomaly)**

> Think of it like a city map — dense neighborhoods are clusters, isolated houses in the middle of nowhere are anomalies.

**Two types of points:**

- **Core points** — have at least `min_samples` neighbors within `ε`
- **Noise points** (label = `-1`) — don't belong to any cluster → **these are our anomalies**

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

> ⚠️ Dataset not included due to size (143MB). Download from Kaggle link above and place in the `dataset/` folder.

---

## ✅ What's Covered

- **Data Loading & Exploration** — shape, class distribution, feature overview
- **Feature Selection** — selecting relevant features for clustering
- **Feature Scaling** — StandardScaler to normalize features before DBSCAN
- **Model Training** — DBSCAN with tuned `eps` and `min_samples`
- **Anomaly Labeling** — points with label `-1` identified as anomalies
- **Visualization** — scatter plot with outliers highlighted in red, clusters in blue
- **Result Analysis** — number of clusters found and anomalies detected

---

## 📈 Results

| Metric                          | Value                      |
| ------------------------------- | -------------------------- |
| Total transactions analyzed     | 284,807                    |
| Clusters found                  | depends on eps/min_samples |
| Anomalies detected (label = -1) | varies by parameters       |
| Outlier color in plot           | Red                        |
| Normal cluster color            | Blue                       |

---

## 🛠️ Tech Stack

```
Python 3.8+
pandas          — data loading and manipulation
numpy           — array operations
matplotlib      — scatter plot visualization
scikit-learn    — DBSCAN, StandardScaler
```

---

## 🚀 How to Run

### 1. Clone the repository

```bash
git clone https://github.com/ehtishamsher/anomaly_detection.git
cd anomaly_detection/DBSCAN
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
jupyter notebook DBSCAN_clustering_anomaly_detection.ipynb
```

---

## ⚙️ Key Parameters

| Parameter     | Meaning                                                        | Effect                                      |
| ------------- | -------------------------------------------------------------- | ------------------------------------------- |
| `eps`         | Maximum distance between two points to be considered neighbors | Smaller = stricter clusters, more anomalies |
| `min_samples` | Minimum points required to form a dense region                 | Higher = stricter clusters, more anomalies  |

**Tuning tip:**

- If too many points are labeled `-1` → increase `eps` or decrease `min_samples`
- If too few anomalies detected → decrease `eps` or increase `min_samples`

---

## ⚖️ DBSCAN vs Isolation Forest

| Feature              | DBSCAN                   | Isolation Forest      |
| -------------------- | ------------------------ | --------------------- |
| Approach             | Density-based clustering | Tree-based isolation  |
| Anomaly label        | -1 (noise)               | -1 (anomaly)          |
| Needs contamination? | No                       | Yes                   |
| Finds clusters?      | Yes                      | No                    |
| Best for             | Spatial/clustered data   | High-dimensional data |
| Speed on large data  | Slower                   | Faster                |

---



