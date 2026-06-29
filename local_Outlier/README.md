# 🔍 Anomaly Detection Using Local Outlier Factor (LOF)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=for-the-badge&logo=jupyter)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-green?style=for-the-badge&logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

A practical implementation of **Local Outlier Factor (LOF)** for anomaly detection — a density-based approach that identifies outliers by comparing the local density of each point to its neighbors.

---

## 📌 Table of Contents

- [🔍 Anomaly Detection Using Local Outlier Factor (LOF)](#-anomaly-detection-using-local-outlier-factor-lof)
  - [📌 Table of Contents](#-table-of-contents)
  - [🌍 Overview](#-overview)
  - [🧠 How LOF Works](#-how-lof-works)
  - [📊 Dataset](#-dataset)
  - [✅ What's Covered](#-whats-covered)
  - [📈 Results](#-results)
  - [🛠️ Tech Stack](#️-tech-stack)
  - [🚀 How to Run](#-how-to-run)
    - [1. Clone the repository](#1-clone-the-repository)
    - [2. Install dependencies](#2-install-dependencies)
    - [3. Run the notebook](#3-run-the-notebook)
  - [⚙️ Key Parameters](#️-key-parameters)

---

## 🌍 Overview

Unlike DBSCAN which groups points into clusters and flags noise, **LOF scores each point individually** based on how isolated it is relative to its local neighborhood. Points with a significantly lower density than their neighbors are flagged as outliers — label `-1`.

This makes LOF powerful for detecting anomalies in datasets with **clusters of varying densities**, such as concentric circles, where global thresholds would fail.

---

## 🧠 How LOF Works

1. For each point, find its **k nearest neighbors**
2. Compute the **local reachability density (LRD)** — how densely packed the neighborhood is
3. Compare the point's LRD to its neighbors' LRDs → produces an **LOF Score**
4. Points with an LOF score **much greater than 1** are flagged as anomalies (label `-1`)

> Think of it like a neighborhood — if everyone around you lives in a busy city block but you're standing alone in a field, you're the anomaly.

**LOF Score interpretation:**

- **Score ≈ -1.0** — Inlier, similar density to neighbors → **normal point**
- **Score << -1.5** — Outlier, much lower density than neighbors → **anomaly**

---

## 📊 Dataset

| Property | Details |
| -------- | ------- |
| Name | Make Circles (Synthetic) |
| Source | `sklearn.datasets.make_circles` |
| Size | 1000 points |
| Shape | Two concentric circles |
| Noise | 0.1 (10% Gaussian noise) |
| Missing values | None |

```python
from sklearn.datasets import make_circles
X, y = make_circles(n_samples=1000, factor=0.5, noise=0.1)
```

---

## ✅ What's Covered

- **Data Generation** — synthetic concentric circles with noise using `make_circles`
- **Model Configuration** — LOF with tuned `n_neighbors`, `metric`, and `contamination`
- **Model Training** — `fit_predict()` to detect outliers within the training data
- **Anomaly Labeling** — points with label `-1` identified as anomalies
- **Visualization** — scatter plot with outliers in red, inliers in blue
- **Score Distribution** — histogram of LOF scores with threshold line to verify separation

---

## 📈 Results

| Metric | Value |
| ------ | ----- |
| Total points analyzed | 1000 |
| Inliers detected (label = 1) | 900 |
| Outliers detected (label = -1) | 100 |
| LOF score range (inliers) | close to `-1.0` |
| LOF score range (outliers) | beyond `-1.5` |
| Outlier color in plot | Red |
| Normal point color | Blue |

---

## 🛠️ Tech Stack

```
Python 3.8+
numpy           — array operations
matplotlib      — scatter plot and score distribution visualization
scikit-learn    — LocalOutlierFactor, make_circles
```

---

## 🚀 How to Run

### 1. Clone the repository

```bash
git clone https://github.com/ehtishamsher/anomaly_detection.git
cd anomaly_detection/local_Outlier
```

### 2. Install dependencies

```bash
pip install numpy matplotlib scikit-learn jupyter
```

### 3. Run the notebook

```bash
jupyter notebook local_outlier_detection.ipynb
```

---

## ⚙️ Key Parameters

| Parameter | Meaning | Effect |
| --------- | ------- | ------ |
| `n_neighbors` | Number of neighbors used to compute local density | Smaller = more sensitive, larger = smoother density estimate |
| `contamination` | Expected proportion of outliers in the dataset | Sets the decision threshold for flagging anomalies |
| `metric` | Distance metric used to find neighbors | Euclidean works best for circular/spatial data |
| `algorithm` | Method used for nearest neighbor search | Ball Tree aligns naturally with circular geometry |
| `novelty` | Switches between outlier and novelty detection mode | `False` = flag outliers within training data |

**Tuning tip:**

- If too many points are flagged as `-1` → decrease `contamination` or increase `n_neighbors`
- If too few anomalies detected → increase `contamination` or decrease `n_neighbors`


