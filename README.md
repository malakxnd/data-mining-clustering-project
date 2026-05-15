# Mall Customer Segmentation — Clustering Analysis

> **Data Mining Assignment 2 | University Group Assignment

---

## Overview

This project applies unsupervised machine learning to segment mall customers into meaningful groups based on their demographic and behavioral attributes. Two clustering algorithms — **K-Means** and **DBSCAN** — are implemented, tuned, and rigorously compared using three internal validation metrics.

The goal is to identify distinct customer personas that can inform targeted marketing strategies.

---

## Dataset

**File:** `Mall_Customers.csv`  
**Source:** Classic mall customer dataset (200 records)

| Feature | Description |
|---|---|
| `CustomerID` | Unique identifier |
| `Gender` | Male / Female |
| `Age` | Customer age |
| `Annual Income (k$)` | Annual income in thousands of USD |
| `Spending Score (1-100)` | Mall-assigned score based on spending behavior |

**Features used for clustering:** `Age`, `Annual Income (k$)`, `Spending Score (1-100)`

---

## Project Structure

```
├── DM_Assign2_3.ipynb          # Main Jupyter notebook (full analysis)
├── Mall_Customers.csv          # Input dataset
├── Data Mining Assign 2 Report.docx  # Written report
├── cover_page_IDs.pdf          # Cover page
└── README.md                   # This file
```

---

## Methodology

### 1. Clusterability Assessment
- Computed the **Hopkins Statistic** (~0.73) to confirm meaningful cluster structure before applying any algorithm.

### 2. Optimal K Selection (for K-Means)
Three methods were used in combination:
- **Empirical Rule** (√(n/2))
- **Elbow Method** (WCSS vs. K)
- **Silhouette Score** across K = 2–10

**Result:** K = 6 was selected — silhouette score peaked at K=6, consistent with the elbow flattening after K=5.

### 3. Algorithms Applied

#### K-Means (K=6)
- Initialization: `k-means++`
- Standard-scaled features
- Visualized across 3 feature-pair projections

#### DBSCAN
- Optimal `eps` determined via k-distance graph (k=5, i.e., 2×features−1)
- Tested eps ∈ {0.6, 0.625, 0.65, 0.675, 0.7}
- Best eps selected by silhouette score on non-noise points

### 4. Evaluation Metrics

| Metric | Interpretation |
|---|---|
| **Silhouette Score** | [-1, 1] — higher = better separation |
| **Davies-Bouldin Score** | [0, ∞) — lower = more compact clusters |
| **Calinski-Harabasz Score** | [0, ∞) — higher = denser, more distinct clusters |

---

## Key Results

| Algorithm | Silhouette ↑ | Davies-Bouldin ↓ | Calinski-Harabasz ↑ |
|---|---|---|---|
| **K-Means (k=6)** | **Higher** | **Lower** | **Higher** |
| DBSCAN | Lower | Higher | Lower |

**K-Means outperformed DBSCAN across all three metrics** on this dataset.

**Why K-Means won:** The mall customer data forms convex, roughly spherical segments with relatively uniform density — ideal conditions for K-Means. DBSCAN collapsed most data into 2 clusters and labeled ~10.5% of points as noise, losing valuable segmentation granularity.

**When DBSCAN would be preferred:** Datasets with irregular cluster shapes, meaningful outlier detection needs, or highly varying densities.

---

## Dependencies

```
numpy
pandas
scikit-learn
matplotlib
```

Install all at once:

```bash
pip install numpy pandas scikit-learn matplotlib
```

---

## How to Run

1. Clone or download this repository.
2. Place `Mall_Customers.csv` in the same directory as the notebook.
3. Open `DM_Assign2_3.ipynb` in Jupyter Notebook or JupyterLab.
4. Run all cells top-to-bottom (`Kernel → Restart & Run All`).

---

## Team Contributions

| Member ID | Responsibility |
|---|---|
| 20236076 | Data preprocessing & Hopkins statistic |
| 20237003 | Optimal K selection (Elbow, Silhouette) |
| 20237015 | Clustering implementation & visualization | => my role
| 20237020 | Evaluation metrics & comparative analysis |

---

## Conclusion

K-Means with k=6 is the recommended algorithm for this dataset. The six customer segments provide interpretable, actionable groups (e.g., high-income high-spenders vs. young low-income high-spenders) that directly support marketing personalization at the mall.
