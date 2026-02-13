---
layout: default
title: "Breast Cancer WDBC — ML Classification"
description: "Supervised learning pipeline for binary classification of breast tumors using the Wisconsin Diagnostic Breast Cancer dataset"
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

<div class="hero-section">
  <h1>Breast Cancer Diagnosis via Supervised Learning</h1>
  <p class="subtitle">A reproducible machine learning pipeline for binary classification of breast tumors (malignant vs. benign) using morphological features from the Wisconsin Diagnostic Breast Cancer (WDBC) dataset.</p>

  <div class="badges">
    <img src="https://img.shields.io/badge/Python-3.8+-3776ab.svg?style=flat-square" alt="Python 3.8+">
    <img src="https://img.shields.io/badge/License-MIT-444.svg?style=flat-square" alt="MIT License">
    <img src="https://img.shields.io/badge/Accuracy-96.5%25-2e7d32.svg?style=flat-square" alt="96.5% Accuracy">
  </div>
</div>

---

## Abstract

This project implements an end-to-end supervised classification pipeline applied to the Wisconsin Diagnostic Breast Cancer (WDBC) dataset (Wolberg et al., 1995). The dataset comprises 569 observations with 30 numeric features derived from digitized images of fine needle aspirate (FNA) cytology samples. Each feature describes morphological properties of cell nuclei — including radius, texture, perimeter, area, smoothness, compactness, concavity, symmetry, and fractal dimension — computed as mean, standard error, and worst-case values.

The pipeline encompasses exploratory data analysis, multicollinearity-based feature selection, standardization, and comparative evaluation of Logistic Regression and Random Forest classifiers. The best-performing model (Logistic Regression) achieved **96.5% accuracy** and **97.5% precision** for the malignant class on the held-out test set.

<div class="summary-grid">
  <div class="summary-item">
    <span class="label">Observations</span>
    <span class="value">569</span>
    <span class="detail">357 benign, 212 malignant</span>
  </div>
  <div class="summary-item">
    <span class="label">Original Features</span>
    <span class="value">30</span>
    <span class="detail">Reduced to 23 after selection</span>
  </div>
  <div class="summary-item">
    <span class="label">Best Accuracy</span>
    <span class="value">96.5%</span>
    <span class="detail">Logistic Regression</span>
  </div>
  <div class="summary-item">
    <span class="label">Malignant Precision</span>
    <span class="value">97.5%</span>
    <span class="detail">Low false-positive rate</span>
  </div>
</div>

---

## Background

Breast cancer remains the most frequently diagnosed malignancy among women globally, with early detection substantially improving five-year survival rates (WHO, 2024). Computer-aided diagnosis (CAD) systems that leverage machine learning have demonstrated clinical value in supporting pathologists during screening workflows.

The WDBC dataset, originally compiled at the University of Wisconsin–Madison, provides quantitative descriptors of cell nuclei observed in FNA biopsy images. These features capture geometric and textural properties that correlate with malignancy, making the dataset a well-established benchmark in medical classification literature.

This project applies standard supervised learning techniques to this dataset, with emphasis on interpretable models suited to clinical decision support.

---

## Methodology

The analysis follows a structured six-stage pipeline:

<div class="pipeline-steps">
  <div class="step">
    <span class="step-number">1</span>
    <div class="step-content">
      <h4>Data Acquisition</h4>
      <p>Dataset loaded from the UCI Machine Learning Repository via the <code>ucimlrepo</code> library. Target variable encoded as binary (M = 1, B = 0).</p>
    </div>
  </div>

  <div class="step">
    <span class="step-number">2</span>
    <div class="step-content">
      <h4>Exploratory Data Analysis</h4>
      <p>Class distribution analysis, descriptive statistics, missing value verification, and distribution assessment for each feature group (mean, SE, worst).</p>
    </div>
  </div>

  <div class="step">
    <span class="step-number">3</span>
    <div class="step-content">
      <h4>Feature Preprocessing</h4>
      <p>Column names standardized to reflect measurement type (mean, standard error, worst-case). No missing values or categorical encoding required.</p>
    </div>
  </div>

  <div class="step">
    <span class="step-number">4</span>
    <div class="step-content">
      <h4>Feature Selection</h4>
      <p>Pairwise Pearson correlation computed; features with |r| > 0.95 were removed to mitigate multicollinearity, reducing the feature space from 30 to 23 variables.</p>
    </div>
  </div>

  <div class="step">
    <span class="step-number">5</span>
    <div class="step-content">
      <h4>Model Training</h4>
      <p>Logistic Regression and Random Forest classifiers trained on standardized features (StandardScaler) with a 75/25 train-test split and fixed random state for reproducibility.</p>
    </div>
  </div>

  <div class="step">
    <span class="step-number">6</span>
    <div class="step-content">
      <h4>Evaluation</h4>
      <p>Performance assessed via accuracy, precision, recall, F1-score, and confusion matrix analysis on the held-out test set.</p>
    </div>
  </div>
</div>

---

## Results

### Classification Performance (Test Set)

<div class="results-table">
  <table>
    <thead>
      <tr>
        <th>Model</th>
        <th>Accuracy</th>
        <th>Precision</th>
        <th>Recall</th>
        <th>F1-Score</th>
      </tr>
    </thead>
    <tbody>
      <tr class="best-model">
        <td><strong>Logistic Regression</strong></td>
        <td><strong>96.5%</strong></td>
        <td><strong>97.5%</strong></td>
        <td><strong>92.9%</strong></td>
        <td><strong>95.1%</strong></td>
      </tr>
      <tr>
        <td>Random Forest</td>
        <td>94.7%</td>
        <td>97.4%</td>
        <td>88.1%</td>
        <td>92.5%</td>
      </tr>
    </tbody>
  </table>
</div>

<div class="note-box">
  <h4>Clinical Relevance of Recall</h4>
  <p>In diagnostic screening, recall (sensitivity) for the malignant class is particularly important: a false negative — classifying a malignant tumor as benign — carries significantly higher clinical risk than a false positive. Logistic Regression achieved 92.9% recall, reducing the probability of missed malignant diagnoses.</p>
</div>

### Key Predictive Features

Feature importance analysis identified the following morphological descriptors as the strongest predictors of malignancy:

1. **Concave points** (mean and worst) — captures the number of concave portions of the cell nucleus contour, a known indicator of irregular cell morphology
2. **Radius measurements** (mean and worst) — reflects overall nucleus size, which tends to be larger in malignant cells
3. **Concavity metrics** — quantifies the severity of concave portions, correlating with irregular nuclear shape

These findings are consistent with established cytopathological criteria, where nuclear size and shape irregularity are primary indicators of malignancy (Wolberg et al., 1995).

---

## Visualizations

### Class Distribution

<div class="viz-container">
  <img src="assets/img/viz_01.png" alt="Class distribution: 357 benign (62.7%) and 212 malignant (37.3%) samples">
  <p class="viz-caption"><strong>Fig. 1.</strong> Target variable distribution in the WDBC dataset. The dataset exhibits moderate class imbalance with 62.7% benign (n=357) and 37.3% malignant (n=212) cases.</p>
</div>

### Feature Distributions by Diagnosis

<div class="viz-grid">
  <div class="viz-item">
    <img src="assets/img/viz_02.png" alt="Kernel density estimates of key features grouped by diagnosis">
    <p class="viz-caption"><strong>Fig. 2.</strong> Distribution of selected features by diagnosis class, illustrating separability between benign and malignant populations.</p>
  </div>

  <div class="viz-item">
    <img src="assets/img/viz_04.png" alt="Pearson correlation matrix across all 30 features">
    <p class="viz-caption"><strong>Fig. 3.</strong> Pearson correlation matrix for the full feature set. Highly correlated pairs (|r| > 0.95) were identified for removal during feature selection.</p>
  </div>
</div>

### Feature Selection and Correlation Analysis

<div class="viz-grid">
  <div class="viz-item">
    <img src="assets/img/viz_05.png" alt="Top 15 features ranked by absolute correlation with diagnosis">
    <p class="viz-caption"><strong>Fig. 4.</strong> Top 15 features ranked by absolute Pearson correlation with the target variable. Concave points (worst) exhibits the strongest linear association (r = 0.79).</p>
  </div>

  <div class="viz-item">
    <img src="assets/img/viz_06.png" alt="Correlation heatmap of the 10 most predictive features">
    <p class="viz-caption"><strong>Fig. 5.</strong> Pairwise correlation heatmap of the top 10 predictive features. Multicollinearity between radius, perimeter, and area is evident.</p>
  </div>
</div>

### Confusion Matrices

<div class="viz-grid">
  <div class="viz-item">
    <img src="assets/img/viz_07.png" alt="Confusion matrix for Logistic Regression classifier">
    <p class="viz-caption"><strong>Fig. 6.</strong> Confusion matrix — Logistic Regression. 3 false negatives and 2 false positives on the test set (n=143).</p>
  </div>

  <div class="viz-item">
    <img src="assets/img/viz_08.png" alt="Confusion matrix for Random Forest classifier">
    <p class="viz-caption"><strong>Fig. 7.</strong> Confusion matrix — Random Forest. 5 false negatives and 1 false positive on the test set (n=143).</p>
  </div>
</div>

### Feature Importance

<div class="viz-grid">
  <div class="viz-item">
    <img src="assets/img/viz_09.png" alt="Random Forest feature importance (Gini impurity)">
    <p class="viz-caption"><strong>Fig. 8.</strong> Feature importance scores from the Random Forest model, computed via mean decrease in Gini impurity.</p>
  </div>

  <div class="viz-item">
    <img src="assets/img/viz_10.png" alt="Logistic Regression coefficient magnitudes">
    <p class="viz-caption"><strong>Fig. 9.</strong> Standardized coefficient magnitudes from Logistic Regression, indicating each feature's contribution to the decision boundary.</p>
  </div>
</div>

---

## Implementation Details

<div class="tech-detail">
  <h4>Environment and Dependencies</h4>
  <ul>
    <li><strong>Language:</strong> Python 3.8+</li>
    <li><strong>Core libraries:</strong> pandas, NumPy, matplotlib, seaborn, scikit-learn</li>
    <li><strong>Data source:</strong> <code>ucimlrepo</code> (UCI ML Repository API)</li>
    <li><strong>Scaling:</strong> <code>StandardScaler</code> — zero mean, unit variance normalization</li>
    <li><strong>Train/test split:</strong> 75/25, stratified, <code>random_state=42</code></li>
  </ul>
</div>

<div class="tech-detail">
  <h4>Design Decisions</h4>
  <ul>
    <li><strong>Feature selection threshold (|r| > 0.95):</strong> chosen to remove near-redundant features while preserving information. Radius/perimeter/area groups exhibited the highest multicollinearity.</li>
    <li><strong>Logistic Regression as primary model:</strong> preferred for interpretability and strong performance on linearly separable data, which aligns with the structure of morphological features.</li>
    <li><strong>Random Forest as baseline comparison:</strong> included to evaluate whether non-linear decision boundaries improve classification. The marginal accuracy decrease (−1.8 pp) suggests linear separation is sufficient for this feature space.</li>
    <li><strong>No hyperparameter tuning:</strong> default scikit-learn parameters were used. Further gains may be achievable through cross-validated grid search.</li>
  </ul>
</div>

### Reproducing the Analysis

```bash
git clone https://github.com/Taimisson/breast-cancer-wdbc-ml.git
cd breast-cancer-wdbc-ml
pip install -r requirements.txt
jupyter notebook notebooks/projeto_cancer_mama.ipynb
```

---

## Project Structure

```
breast-cancer-wdbc-ml/
├── README.md
├── requirements.txt
├── LICENSE
├── CITATION.cff
├── notebooks/
│   └── projeto_cancer_mama.ipynb    # Full analysis notebook
└── docs/
    ├── index.md                      # This page
    ├── notebook.html                 # Exported notebook (HTML)
    └── assets/
        ├── css/custom.css
        └── img/                      # Generated figures
```

---

## Resources

<div class="links-section">
  <a href="https://github.com/Taimisson/breast-cancer-wdbc-ml" class="button primary">
    Repository
  </a>
  <a href="notebook.html" class="button secondary">
    Full Notebook
  </a>
  <a href="https://www.datacamp.com/datalab/w/54ce12ff-34cb-46b5-b1b9-dc2715b9a821/edit" class="button secondary">
    Interactive Version
  </a>
</div>

---

## References

- Wolberg, W. H., Street, W. N., & Mangasarian, O. L. (1995). *Image analysis and machine learning applied to breast cancer diagnosis and prognosis.* Analytical and Quantitative Cytology and Histology, 17(2), 77–87.
- UCI Machine Learning Repository — [Breast Cancer Wisconsin (Diagnostic)](https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic)
- World Health Organization (2024). *Breast Cancer Fact Sheet.* [who.int](https://www.who.int/news-room/fact-sheets/detail/breast-cancer)

---

## License & Citation

Licensed under the MIT License. See [LICENSE](https://github.com/Taimisson/breast-cancer-wdbc-ml/blob/main/LICENSE).

```bibtex
@software{breast_cancer_wdbc_ml,
  author = {Taimisson},
  title = {Breast Cancer Diagnosis ML Pipeline},
  year = {2026},
  url = {https://github.com/Taimisson/breast-cancer-wdbc-ml}
}
```

---

<div class="portfolio-banner">
  <div class="portfolio-content">
    <div class="portfolio-icon">
      <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
    </div>
    <div class="portfolio-text">
      <p class="portfolio-label">About the Author</p>
      <h3 class="portfolio-name">Taimisson</h3>
      <p class="portfolio-desc">Software Developer &amp; Data Science Enthusiast — explore more projects, skills, and contact info on my portfolio.</p>
    </div>
    <a href="https://taimisson.vercel.app/" target="_blank" rel="noopener noreferrer" class="portfolio-button">
      Visit Portfolio
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
    </a>
  </div>
</div>

<div class="footer-section">
  <p>Built with Python, scikit-learn, and Jupyter</p>
  <p>Dataset: Wisconsin Diagnostic Breast Cancer (WDBC) — UCI Machine Learning Repository</p>
</div>
