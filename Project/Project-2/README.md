# HR Employee Attrition Analysis
### Elevate Labs Data Analyst Internship — Main Project

> Predicting and preventing employee turnover using IBM's HR Analytics dataset.

---

## Project Overview

This project analyzes IBM's HR Employee Attrition dataset to uncover the key drivers of voluntary employee turnover and to build a machine learning model that identifies employees at high risk of leaving. The output is a ranked, actionable list of employees segmented into three retention tiers, along with concrete HR policy recommendations.

---

## Dataset

| Property | Details |
|----------|---------|
| Source | IBM HR Analytics Employee Attrition (Kaggle) |
| File | `HR Analytics - Predict Employee Attrition.csv` |
| Rows | 1,470 employees |
| Columns | 35 features |
| Missing Values | None |
| Target Variable | `Attrition` (Yes = 16.1% / No = 83.9%) |

---

## Key Findings

| Insight | Detail |
|--------|--------|
| **#1 Driver** | OverTime — 30.5% attrition vs 10.4% without (3× gap) |
| **Highest-Risk Dept** | Sales — 20.6% attrition rate |
| **Highest-Risk Role** | Sales Representative — 39.8% attrition |
| **Income Gap** | Employees who left earned $2,046/month less than those who stayed |
| **Single Employees** | Churn at 25.5% vs 12.5% for married |
| **No Stock Options** | 24.4% attrition vs 9.4% for those with stock options |
| **Low WLB Score (1)** | 31.2% attrition — highest among all WLB groups |

---

## Project Phases

### Phase 1 — Data Loading & Cleaning
- Loaded 1,470 rows × 35 columns
- Dropped 3 constant columns: `EmployeeCount`, `Over18`, `StandardHours`
- Dropped ID column: `EmployeeNumber`
- Confirmed zero nulls — no imputation required

### Phase 2 — Exploratory Data Analysis
- Attrition distribution (16.1% class imbalance confirmed)
- Attrition by OverTime, Department, Job Role, Age, Job Level
- Monthly income comparison between leavers and stayers
- Work-Life Balance, Marital Status, Stock Options analysis
- Correlation heatmap — `TotalWorkingYears` strongest numeric predictor (−0.171)
- Executive dashboard (6-panel chart)

### Phase 3 — Preprocessing & Feature Engineering
- Binary encoding: `Attrition`, `Gender`, `OverTime`
- One-hot encoding: `BusinessTravel`, `Department`, `EducationField`, `JobRole`, `MaritalStatus`
- 5 engineered features added:

  | Feature | Description |
  |---------|-------------|
  | `IncomePerYear` | Monthly income ÷ total working years |
  | `TenureRatio` | Years at company ÷ total working years |
  | `AvgSatisfaction` | Mean of 4 satisfaction survey scores |
  | `PromotionGap` | Years at company − years since last promotion |
  | `IsYoungAndNew` | Age < 30 AND tenure < 3 years (binary flag) |

- StandardScaler applied to 17 continuous columns
- 80/20 stratified train-test split → Train: 1,176 / Test: 294
- Class imbalance handled via `class_weight='balanced'` (5.2× penalty on minority class)

### Phase 4 — Model Building & Explainability

| Model | Accuracy | ROC-AUC | F1 Score |
|-------|----------|---------|---------|
| **Logistic Regression** ✅ | 76.9% | **0.808** | 0.469 |
| Gradient Boosting | 84.0% | 0.789 | 0.299 |
| Random Forest | 83.3% | 0.778 | 0.109 |
| Decision Tree | 73.5% | 0.577 | 0.304 |

**Logistic Regression** selected as the best model based on ROC-AUC (0.808) — the metric that matters most for ranking employees by churn risk.

Explainability via **Permutation Importance** (model-agnostic SHAP substitute):

| Rank | Feature | Importance |
|------|---------|-----------|
| 1 | OverTime | 0.1090 |
| 2 | BusinessTravel_Travel_Frequently | 0.0410 |
| 3 | NumCompaniesWorked | 0.0265 |
| 4 | MaritalStatus_Single | 0.0236 |
| 5 | MonthlyIncome | 0.0199 |

### Phase 5 — Employee Risk Segmentation

| Segment | Employees | Actual Attrition | Monthly Payroll | Avg Risk Score |
|---------|-----------|-----------------|-----------------|---------------|
| 🔴 Flight Risk | 441 (30.0%) | 40.6% | $2.10M | 72.1% |
| 🟡 At Watch | 349 (23.7%) | 10.9% | $2.13M | 37.0% |
| 🟢 Stable | 680 (46.3%) | 2.9% | $5.33M | 10.8% |

Each employee assigned a risk probability and segmented using thresholds: ≥ 50% → Flight Risk, 25–49% → At Watch, < 25% → Stable.

### Phase 6 — Business Recommendations & Report

Five actionable recommendations:

1. **Cap/compensate overtime for Sales roles** — the single highest-risk factor (3× attrition gap)
2. **Introduce promotion check-ins** — for employees with high PromotionGap (years in role without promotion)
3. **Review compensation** for Flight Risk employees earning below the $2,046/month retention gap
4. **Extend stock option eligibility** — employees with zero stock options churn at 24.4% vs 9.4%
5. **Run stay interviews** — prioritize the 441 Flight Risk employees this quarter before they disengage

---

## File Structure

```
hr_attrition_project/
│
├── hr_data.csv                        # Source dataset
│
├── pipeline.py                        # Full rebuild pipeline (EDA + model + segmentation)
│
├── hr_phase1_setup.py                 # Phase 1 — Data loading & cleaning
├── hr_phase2_eda.py                   # Phase 2 — Exploratory data analysis (9 charts)
├── hr_phase3_preprocessing.py         # Phase 3 — Preprocessing & feature engineering
├── hr_phase4_model_building.py        # Phase 4 — Model training & explainability (8 charts)
├── hr_phase5_segmentation.py          # Phase 5 — Risk segmentation (7 charts)
│
├── employee_risk_segments.csv         # All 1,470 employees scored with risk tier
│
├── hr_attrition_report.pdf            # Final 2-page project report (Elevate Labs format)
│
├── chart_dashboard.png                # Executive EDA dashboard
├── chart_corr.png                     # Feature correlation heatmap
├── chart_models.png                   # Model comparison + ROC + confusion matrix
├── chart_importance.png               # Permutation importance (top 12 features)
└── chart_segments.png                 # Risk segmentation donut + payroll chart
```

---

## How to Run

### Requirements
```bash
pip install pandas numpy scikit-learn matplotlib seaborn reportlab
```

### Reproduce everything in one command
```bash
python pipeline.py
```
This regenerates all 5 charts, trains all 4 models, scores all 1,470 employees, and saves `employee_risk_segments.csv`.

### Regenerate the PDF report
```bash
python build_report.py
```

### Run individual phases
```bash
python hr_phase1_setup.py        # Data loading & EDA summary
python hr_phase2_eda.py          # 9 EDA charts
python hr_phase3_preprocessing.py # Preprocessing & feature engineering
python hr_phase4_model_building.py # Model training (4 models, 8 charts)
python hr_phase5_segmentation.py   # Segmentation (7 charts + CSV)
```

---

## Tools & Libraries

| Tool | Purpose |
|------|---------|
| Python 3.x | Core language |
| Pandas | Data loading, cleaning, manipulation |
| NumPy | Numerical operations |
| Scikit-learn | Preprocessing, model training, evaluation |
| Matplotlib / Seaborn | All visualizations |
| ReportLab | PDF report generation |

---

## Deliverables

- `hr_attrition_report.pdf` — 2-page project report covering Introduction, Abstract, EDA, Preprocessing, Models, Segmentation, Recommendations, Conclusion
- `employee_risk_segments.csv` — Scored dataset with `RiskScore`, `RiskPct`, `RiskSegment`, `RiskLevel` columns for all 1,470 employees

---

## Author

**Elevate Labs Data Analyst Internship — 2026**
