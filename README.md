# 🧬 Cancer Classification via Dimensionality Reduction & Feature Engineering

A machine learning project that classifies multi-class cancer types from high-dimensional RNA-Seq gene expression data using a progressive dimensionality reduction pipeline — from linear PCA to supervised LDA to non-linear t-SNE — combined with biomarker discovery techniques.

---

## 📌 Project Overview

Gene expression datasets contain tens of thousands of features per sample, making them computationally expensive and prone to the **curse of dimensionality**. This project implements a hierarchical progression of dimensionality reduction strategies to demonstrate measurable accuracy gains at each stage, ultimately achieving state-of-the-art multi-class cancer classification.

**Submitted to:** Professor Daniyal Adeeb — Section D1  
**Author:** Abdul Moeez (F2023332094)

---

## 📂 Dataset

**UCI Gene Expression Cancer RNA-Seq Dataset**  
🔗 [https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq](https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq)

| Property | Value |
|---|---|
| Samples | 801 tumor samples |
| Features | 20,531 gene expression values |
| Classes | BRCA, KIRC, LUAD, PRAD, COAD |
| Format | Two CSVs — `data.csv` (features) & `labels.csv` (targets) |

---

## 🚀 Pipeline Architecture

```
Raw RNA-Seq Data (801 × 20,531)
        │
        ▼
┌─────────────────────────┐
│  1. Data Preprocessing  │
│  - Log2 Normalization   │
│  - StandardScaler       │
│  - Train/Test Split     │
│    (80/20, Stratified)  │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  2. Feature Engineering │
│  - Variance Threshold   │
│    (remove zero-var     │
│     genes)              │
│  - Chi-Squared Test     │
│    (Top 20 Biomarkers)  │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────────────────────────────┐
│         3. Dimensionality Reduction Ladder       │
│                                                 │
│  Phase 1 → PCA  (Unsupervised, Linear)          │
│            95% variance retained                │
│                                                 │
│  Phase 2 → LDA  (Supervised, Linear)            │
│            Maximizes class separation           │
│                                                 │
│  Phase 3 → t-SNE (Unsupervised, Non-Linear)     │
│            Captures manifold structure          │
└────────────┬────────────────────────────────────┘
             │
             ▼
┌─────────────────────────┐
│  4. Classification      │
│  - k-NN                 │
│  - SVM (linear kernel)  │
│  - Random Forest        │
│  - LDA Classifier       │
└─────────────────────────┘
```

---

## 🧪 Methods

### Preprocessing
- **Log2 Normalization** followed by `StandardScaler` to normalize expression levels across samples
- **Train/Test Split** (80/20) applied *before* any fitting to prevent data leakage
- **Variance Threshold** to remove constant genes with zero variance

### Feature Engineering
- **Biomarker Discovery** via Chi-Squared (`SelectKBest`) to identify the top 20 statistically significant genes
- **Pathway Activity Scores** — aggregating genes into biological pathways (ssGSEA)
- **Gene Pair Ratios** — robust, self-normalizing features invariant to normalization errors

### Dimensionality Reduction
| Phase | Method | Type | Expected Accuracy |
|---|---|---|---|
| Baseline | PCA | Unsupervised, Linear | ~95% |
| Intermediate | LDA | Supervised, Linear | ~98% |
| Advanced | t-SNE | Unsupervised, Non-Linear | ~99% |

### Classification Models
- **k-Nearest Neighbors (k-NN)** — `k=5`
- **Support Vector Machine (SVM)** — Linear kernel, `C=1.0`
- **Random Forest** — 100 estimators
- **Linear Discriminant Analysis (LDA)**

### Evaluation
- Accuracy, Precision, Recall, F1-Score
- Confusion Matrix (visualized with Seaborn heatmap)
- Model comparison bar chart

---

## 🗂️ Repository Structure

```
📦 cancer-classification-rna-seq/
├── 📓 final_project_machine_learning2.ipynb   # Main Jupyter Notebook
├── 📄 Project_Proposal.docx                   # Project proposal document
├── 📄 README.md                               # This file
└── 📁 data/                                   # Place dataset files here
    ├── data.csv                               # Gene expression matrix
    └── labels.csv                             # Cancer type labels
```

---

## ⚙️ Installation & Setup

### Prerequisites
- Python 3.8+
- Google Colab (recommended) or a local Jupyter environment

### Install Dependencies

```bash
pip install numpy pandas matplotlib seaborn scikit-learn
```

### Running the Notebook

**Option A — Google Colab (Recommended)**
1. Upload `data.csv` and `labels.csv` to your Google Drive
2. Open `final_project_machine_learning2.ipynb` in Colab
3. Update the file paths in the **Load Data** cell to match your Drive location
4. Run all cells sequentially

**Option B — Local Jupyter**
1. Clone this repository
2. Place `data.csv` and `labels.csv` inside the `data/` folder
3. Update file paths in the notebook accordingly
4. Launch Jupyter and run all cells

---

## 📊 Results

The notebook produces:
- **PCA vs t-SNE cluster visualization** — side-by-side scatter plots showing how well each method separates cancer types
- **Confusion matrices** for all four classifiers
- **Final accuracy comparison bar chart** across k-NN, SVM, Random Forest, and LDA

---

## 📚 References

1. Jolliffe, I. T. (2002). *Principal Component Analysis.*
2. UCI Machine Learning Repository — [Gene Expression Cancer RNA-Seq Dataset](https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq)
3. Poličar et al. (2024). openTSNE: a modular Python library for t-SNE dimensionality reduction.
4. Georgiou et al. (2025). Stage-specific gene pair ratios highlight genes and mechanisms related to Multiple Myeloma. *Computational and Structural Biotechnology Journal.*
5. Chuiqin et al. (2024). irGSEA: The integration of single-cell rank-based gene set enrichment analysis. *Brief. Bioinform.*

---

## 👤 Author

**Muhammad Hashaam**  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/muhammadhashaam633/)
