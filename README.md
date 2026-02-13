# Breast Cancer Diagnosis (WDBC) — End-to-End ML Pipeline

[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Accuracy](https://img.shields.io/badge/Accuracy-96.5%25-brightgreen.svg)](https://github.com/Taimisson/breast-cancer-wdbc-ml)
[![Status](https://img.shields.io/badge/Status-Complete-success.svg)](https://github.com/Taimisson/breast-cancer-wdbc-ml)

End-to-end machine learning classification pipeline to predict **malignant vs. benign** tumors using the **Wisconsin Diagnostic Breast Cancer (WDBC)** dataset.

---

## ✨ Highlights
- **Dataset:** 569 samples, 30 numeric features (cell nuclei characteristics from FNA images)
- **Data quality:** verified **no missing values** and **no duplicates**
- **Feature engineering:** renamed raw columns into descriptive names (mean / se / worst)
- **Feature selection:** removed highly correlated predictors (**threshold > 0.95**), reducing **30 → 23** features
- **Models:** Logistic Regression and Random Forest (with standardized preprocessing)
- **Best result (LogReg):** **96.5% accuracy**, **97.5% precision**, **92.9% recall** (malignant class)

---

## 🔗 Links
- **Repository:** https://github.com/Taimisson/breast-cancer-wdbc-ml  
- **Interactive (DataCamp DataLab):** https://www.datacamp.com/datalab/w/54ce12ff-34cb-46b5-b1b9-dc2715b9a821/edit
- **Slides (PDF):**  

---

## 🧠 Problem Context
Breast cancer is one of the most common causes of mortality among women worldwide. Early detection significantly improves treatment outcomes.  
This project uses supervised machine learning to learn patterns that separate **malignant** from **benign** tumors using nucleus-level morphological features extracted from digitized FNA images.

---

## 🧪 Approach (Pipeline)
1. **Load dataset (WDBC)** from UCI using `ucimlrepo`
2. **EDA & data validation**
   - descriptive statistics and class distribution
   - missing values & duplicates checks
3. **Preprocessing**
   - consistent and descriptive feature naming (mean / se / worst)
4. **Feature selection**
   - removed highly correlated predictors (**> 0.95**) to reduce multicollinearity (**30 → 23**)
5. **Training & evaluation**
   - stratified 80/20 split
   - standardized pipeline (`StandardScaler` + model)
   - metrics: accuracy, precision, recall, F1
   - confusion matrix
6. **Interpretability**
   - Random Forest feature importance
   - Logistic Regression coefficients

---

## 📊 Results (Test Set)

| Model | Accuracy | Precision (Malignant) | Recall (Malignant) | F1 (Malignant) |
|------|----------|------------------------|--------------------|----------------|
| Logistic Regression | **0.965** | **0.975** | **0.929** | **0.951** |
| Random Forest | 0.947 | 0.974 | 0.881 | 0.925 |

**Why recall matters here:** in medical screening, higher malignant recall helps reduce false negatives (malignant predicted as benign).

---

## 🔍 Interpretability (What drives the prediction?)
Top drivers identified via feature importance / coefficients include:
- concave points (mean/worst)
- radius-related features
- concavity-related features

These features align with morphological differences between malignant and benign cell nuclei.

---

## 📈 Key Visualizations

<p align="center">
  <img src="docs/assets/img/viz_01.png" width="100%" alt="Class Distribution">
  <br><em>Figure 1: Distribution of benign vs. malignant cases in the dataset</em>
</p>

<p align="center">
  <img src="docs/assets/img/viz_07.png" width="80%" alt="Confusion Matrix">
  <br><em>Figure 2: Confusion matrices showing model performance</em>
</p>

<p align="center">
  <img src="docs/assets/img/viz_09.png" width="80%" alt="Feature Importance">
  <br><em>Figure 3: Top 10 most important features (Random Forest)</em>
</p>

> 📊 **[View full analysis with all visualizations →](https://taimisson.github.io/breast-cancer-wdbc-ml/)**

---

## 🚀 How to Run

### Prerequisites
- Python 3.8 or higher
- Jupyter Notebook or JupyterLab

### Installation

```bash
# Clone the repository
git clone https://github.com/Taimisson/breast-cancer-wdbc-ml.git
cd breast-cancer-wdbc-ml

# Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

### Running the Analysis

1. Open `notebooks/projeto_cancer_mama.ipynb`
2. Run all cells sequentially (Cell → Run All)
3. View results and visualizations

### Quick Start (Google Colab)

Don't want to install anything? Run it in the cloud:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Taimisson/breast-cancer-wdbc-ml/blob/main/notebooks/projeto_cancer_mama.ipynb)

---

## 📁 Repository Structure
```txt
.
├── README.md
├── notebook.ipynb
├── requirements.txt
├── LICENSE
├── CITATION.cff
├── .gitignore
└── docs/
    ├── index.md
    ├── report.html
    ├── slides.pdf
    └── assets/
        ├── cover.png
        ├── figures/
        └── ...
