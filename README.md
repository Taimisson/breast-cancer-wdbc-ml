# Breast Cancer Diagnosis (WDBC) — End-to-End ML Pipeline

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

## 🧩 Repository Structure (recommended)
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
