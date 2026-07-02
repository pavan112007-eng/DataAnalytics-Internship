# 📡 Telecom Customer Churn Analysis
**Elevate Labs Internship Project — Data Analytics Domain | 2026**

> Predicting which telecom customers are about to leave — and telling the business exactly what to do about it.

---

## 📌 Project Overview

Customer churn is the single largest revenue threat in the telecom industry. Acquiring a new customer costs roughly 5× more than retaining an existing one. With a **26.5% churn rate** in this dataset, over one in four customers leaves every billing cycle.

This project delivers a complete, end-to-end churn intelligence pipeline:
- Root cause discovery through Exploratory Data Analysis
- Predictive modelling with four ML classifiers
- Model explainability using permutation importance
- Customer risk scoring and segmentation
- Actionable retention strategy for each segment

---

## 📂 Dataset

| Property | Value |
|---|---|
| Name | IBM Telco Customer Churn |
| Source | [Kaggle / IBM](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) |
| File | `telco_churn_cleaned.csv` |
| Rows | 7,043 |
| Original Features | 21 |
| Engineered Features | +7 (28 total) |
| Target Column | `Churn` (Yes / No) |

---

## 🗂️ Project Structure

```
telecom-churn-analysis/
│
├── data/
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv
│
├── outputs/
│   ├── charts/                  # All 9 EDA charts + model charts
│   ├── churn_segments.csv       # All 7,043 customers scored & segmented
│   └── churn_model.pkl          # Saved Logistic Regression model
│
├── phase1_setup.py              # Data loading & initial cleaning
├── phase2_eda.py                # Exploratory Data Analysis (9 charts)
├── phase3_preprocessing.py      # Feature engineering & SMOTE
├── phase4_model_building.py     # Model training & evaluation (4 models)
├── phase5_segmentation.py       # Customer risk scoring & segmentation
│
├── Telecom_Churn_Report_2026.pdf   # Final 2-page project report
└── README.md
```

---

## 🔧 Tools & Libraries

| Tool / Library | Purpose |
|---|---|
| Python 3.10 | Core language |
| Pandas | Data loading & wrangling |
| NumPy | Numeric operations |
| Matplotlib | Custom visualisations |
| Seaborn | Statistical charts |
| Scikit-learn | ML models, metrics, scaling |
| LabelEncoder | Binary categorical encoding |
| StandardScaler | Numeric feature scaling |
| SMOTE (imbalanced-learn) | Class balancing |
| Permutation Importance | Model explainability (SHAP-equivalent) |
| Joblib | Model persistence (.pkl) |
| ReportLab | PDF report generation |

---

## ⚙️ How to Run

**1. Clone the repository and install dependencies**
```bash
git clone https://github.com/your-username/telecom-churn-analysis.git
cd telecom-churn-analysis
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn reportlab joblib
```

**2. Place the dataset in the `data/` folder**
```
data/WA_Fn-UseC_-Telco-Customer-Churn.csv
```

**3. Run each phase in order**
```bash
python phase1_setup.py          # Clean data, fix TotalCharges
python phase2_eda.py            # Generate 9 EDA charts
python phase3_preprocessing.py  # Encode, engineer features, apply SMOTE
python phase4_model_building.py # Train & evaluate 4 models
python phase5_segmentation.py   # Score & segment all customers
```

All charts are saved automatically as `.png` files. The segmented customer list is exported as `churn_segments.csv`.

---

## 📊 Key EDA Findings

| # | Finding | Insight |
|---|---|---|
| 1 | **Contract type** | Month-to-month customers churn at **42.7%** vs only **2.8%** for two-year contracts — a 15× gap |
| 2 | **Early tenure** | Customers in their first 12 months churn at **47.7%**; churned avg tenure = 18 mo vs 38 mo retained |
| 3 | **Monthly charges** | Churned customers pay **$74.44/mo** on average vs $61.27 for retained |
| 4 | **Internet service** | Fiber optic users churn at **41.9%** vs 7.4% with no internet |
| 5 | **Payment method** | Electronic check payers churn at **45.3%** — highest of any method |
| 6 | **Correlation** | Tenure is the strongest numeric predictor of churn (r = −0.352) |

---

## 🤖 Model Results

Four models trained on a SMOTE-balanced training set, evaluated on the original unbalanced test set (1,409 customers). **ROC-AUC** was the primary metric — it measures the model's ability to rank customers by churn risk.

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC | CV-AUC |
|---|---|---|---|---|---|---|
| **Logistic Regression ★** | **80.7%** | **65.0%** | **55.7%** | **60.0%** | **0.848** | **0.842** |
| Random Forest | 80.6% | 64.4% | 53.4% | 58.3% | 0.845 | 0.839 |
| Gradient Boosting | 80.0% | 63.3% | 53.4% | 58.0% | 0.844 | 0.837 |
| Decision Tree | 79.6% | 60.2% | 50.4% | 54.7% | 0.830 | 0.812 |

**Selected model:** Logistic Regression — highest ROC-AUC, confirmed stable by 5-fold cross-validation (0.842 ± 0.008).

**Explainability:** Permutation importance confirms `tenure`, `Contract_Two year`, and `MonthlyCharges` as the top three predictors — consistent across both tree-based feature importance charts and the EDA findings.

---

## 👥 Customer Segmentation

Every customer was scored using `predict_proba()` to obtain a personalised churn probability (0–100%), then placed into one of three segments:

| Segment | Threshold | Count | % of Base | Actual Churn | Monthly Revenue | Priority |
|---|---|---|---|---|---|---|
| 🔴 **At Risk** | ≥ 60% | 976 | 13.9% | 72.5% | $79,650 | **URGENT** |
| 🟡 **Dormant** | 30–59% | 1,609 | 22.8% | 44.7% | $120,900 | **HIGH** |
| 🟢 **Loyal** | < 30% | 4,458 | 63.3% | 9.9% | $255,567 | **MAINTAIN** |

---

## 💡 Business Recommendations

### 🔴 At Risk — 976 customers | $79,650/mo
- **Personal outreach within 48 hrs** to every customer with churn probability > 60%
- **Contract upgrade offer** — 20% discount for first 3 months on a 1-year contract; converting just 30% saves ~$23,900/mo
- **Free add-on bundle** — 3 months of OnlineSecurity + TechSupport at no charge (reduces churn by ~27 percentage points for non-subscribers)

### 🟡 Dormant — 1,609 customers | $120,900/mo
- **Re-engagement email sequence** — value reminder, usage insights, time-limited loyalty offer
- **Loyalty credits** — $10–15 bill credit for a 6-month commitment
- **Quarterly satisfaction surveys** to catch dissatisfaction before month-12 churn

### 🟢 Loyal — 4,458 customers | $255,567/mo
- **VIP milestone rewards** at 12/24/36 months (bill credits, upgrades, exclusive pricing)
- **Referral programme** — $20–30 bill credit per successful referral (near-zero CAC growth)
- **Cross-sell premium bundles** to grow ARPU without adding churn risk

---

## 📈 Business Impact

Retaining just **30% of the 976 At-Risk customers** saves approximately **$23,900/month** — a return that comfortably exceeds any reasonable retention campaign budget.

---

## 🏁 Conclusion

Contract type is the dominant churn driver, with month-to-month customers churning at 15× the rate of two-year customers. The validated Logistic Regression model (ROC-AUC 0.848) identifies at-risk customers before they leave, enabling proactive, targeted retention rather than reactive win-back campaigns.

**Next step:** operationalise the model into a monthly scoring pipeline integrated with the CRM for automated, threshold-triggered outreach — closing the loop between data science and business execution.

---

## 👤 Author

**[Your Name]**
Data Analytics Intern — Elevate Labs | 2026

---

## 📄 License

This project is for educational and internship purposes under Elevate Labs. Dataset credit: IBM / Kaggle.
