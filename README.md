# iFood Campaign Response Prediction

Predicting which customers will accept a marketing campaign using statistical hypothesis testing and machine learning — achieving **80.9% precision** with a Random Forest model.

---

## Results at a Glance

| Model | Precision | Recall | F1 | AUC-ROC |
|---|---|---|---|---|
| Random Forest + Grid Search (**winner**) | **0.809** | 0.458 | 0.585 | **0.895** |
| LightGBM (threshold 0.75) | 0.774 | 0.410 | 0.536 | 0.879 |
| XGBoost (threshold 0.85) | 0.760 | 0.422 | 0.542 | 0.871 |
| CatBoost (threshold 0.80) | 0.739 | 0.434 | 0.547 | 0.868 |

> **Why Precision?** Contacting a customer who won't respond has a direct cost. Maximizing precision minimizes wasted outreach while still capturing enough leads (Recall ≥ 0.40).

---

## Project Structure

```
ifood-data-analysis/
├── notebooks/
│   └── ifood_campaign_analysis.ipynb   # Main analysis notebook
├── data/
│   └── README.md                        # Dataset description & download instructions
├── requirements.txt
├── LICENSE
└── README.md
```

---

## Dataset

The dataset contains **2,240 records** of iFood customers across 29 features, including:

- **Demographics:** Age, marital status, number of dependents
- **Spending:** Wine, fruits, meat, fish, sweets, gold products
- **Purchase channels:** Web, catalog, store visits
- **Engagement:** Days as customer, recency, previous campaign responses

**Target variable:** `Response` — whether the customer accepted the last marketing campaign (14.9% positive rate — imbalanced).

> The raw `data.csv` file is not tracked in this repo. See [`data/README.md`](data/README.md) for sourcing instructions.

---

## Analysis Overview

### Part 1 — Statistical Hypothesis Testing (Z-test)

Compared the means of all numeric features between the two groups (accepted vs. rejected). **22 out of 27 features** showed statistically significant differences (α = 0.05).

Top differentiators:

- Responders have **higher income and total spending**
- Responders have **fewer teenagers at home**
- Responders show **more recent engagement** (lower Recency)
- Responders **accepted more previous campaigns**

### Part 2 — Machine Learning Modeling

Tested **10 models** across three stages:

1. **Baselines:** Logistic Regression, Decision Tree (+ SMOTE), Random Forest
2. **Boosting family:** LightGBM, XGBoost, CatBoost
3. **Hyperparameter tuning:** Grid Search, Randomized Search, Bayesian Optimization (× 2)

All models used stratified train/test splits (75/25) and 5-fold cross-validation. Class imbalance was addressed via `class_weight='balanced'`, SMOTE, and `scale_pos_weight`.

### Part 3 — Convergence Analysis (Z-test vs. Feature Importance)

All top 5 ML features (`Days_Customer`, `Recency`, `TotalAccepted`, `TotalMnt`, `MntMeatProducts`) were also statistically significant in the Z-test — providing **dual validation** from both univariate statistics and multivariate machine learning.

---

## Tech Stack

- **Data:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Statistics:** `statsmodels`
- **ML:** `scikit-learn`, `lightgbm`, `xgboost`, `catboost`
- **Optimization:** `scikit-optimize` (Bayesian Search)
- **Imbalance:** `imbalanced-learn` (SMOTE)

---

## How to Run

**1. Clone the repository**
```bash
git clone https://github.com/PedroIavaroneCustodio/ifood-data-analysis.git
cd ifood-data-analysis
```

**2. Create and activate a virtual environment**
```bash
python -m venv venv
source venv/bin/activate        # Linux/macOS
venv\Scripts\activate           # Windows
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Add the dataset**

See [`data/README.md`](data/README.md) for instructions on obtaining `data.csv`. Place it in the `data/` folder.

**5. Open the notebook**
```bash
jupyter notebook notebooks/ifood_campaign_analysis.ipynb
```

---

## Key Findings

- **Precision of 80.9%** with recall of 45.8% on unseen data — the model correctly identifies 4 in 5 predicted responders.
- **AUC-ROC of 0.895** confirms strong discriminative power between the two groups.
- The convergence between statistical significance (Z-test) and ML feature importance validates the robustness of the findings.
- The five most predictive features span customer tenure, recency, historical campaign engagement, and spending — all actionable dimensions for marketing segmentation.

---

## Author

**Pedro Iavarone Custódio**
- GitHub: [@PedroIavaroneCustodio](https://github.com/PedroIavaroneCustodio)
- Email: piavaronecustodio@gmail.com
