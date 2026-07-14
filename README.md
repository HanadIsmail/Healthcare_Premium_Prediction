# Health Insurance Premium Prediction

An end-to-end regression pipeline that predicts annual health insurance premiums from customer demographic, financial, and health data — covering data cleaning, EDA, feature engineering, model training, and error analysis.

## Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Project Workflow](#project-workflow)
- [Results](#results)
- [Key Insight](#key-insight)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Future Work](#future-work)

## Overview

Insurance providers need to price premiums accurately — overcharging risks losing customers, undercharging risks financial loss. This project builds a regression model to predict `annual_premium_amount` using customer attributes such as age, income, BMI category, smoking status, medical history, and insurance plan tier, then diagnoses *where* the model still gets it wrong.

## Dataset

The dataset includes demographic (age, gender, region, marital status), financial (income), and health (BMI category, smoking status, medical history) attributes for insurance customers, along with their annual premium amount.

> Note: add dataset source/license here if the data isn't proprietary, or a note that it's excluded from the repo.

## Project Workflow

### 1. Data Cleaning
- Handled missing values and duplicate records
- Corrected invalid negative values in `number_of_dependants`
- Removed outliers: invalid ages (>100 years), extreme income values using a domain-informed quantile threshold rather than strict IQR
- Standardized inconsistent categorical labels (e.g., multiple variants of "non-smoker" collapsed into one category)

### 2. Exploratory Data Analysis
- Univariate and bivariate analysis across numeric features (age, income, dependants) and categorical features (gender, region, smoking status, plan tier)
- Cross-tabulations and heatmaps to examine relationships (e.g., income level vs. insurance plan)

### 3. Feature Engineering
- Engineered a `total_risk_score` from parsed medical history (diabetes, heart disease, high blood pressure, thyroid), weighted by clinical severity
- Ordinal encoding for `insurance_plan` and `income_level`
- One-hot encoding for nominal categorical features
- Multicollinearity check via Variance Inflation Factor (VIF); dropped high-VIF feature (`income_level`)
- Min-max scaling applied to numeric features

### 4. Model Training
- Trained and compared Linear Regression, Ridge Regression, and XGBoost
- Hyperparameter tuning for XGBoost via `RandomizedSearchCV`
- Evaluated using R², MSE, and RMSE

### 5. Error Analysis
- Analyzed residual distribution (% error per prediction)
- Flagged "extreme errors" (>10% over/undercharge) — present in ~30% of test customers
- Isolated severe cases (>50% error) — approximately 549 customers
- Compared feature distributions between high-error and overall test populations

## Results

| Model | RMSE | Test R² |
|---|---|---|
| Linear Regression | 2272.80 | 0.928 |
| Ridge Regression | 2272.81 | 0.928 |
| XGBoost (default) | 1250.23 | 0.978 |
| XGBoost (tuned) | — | 0.981 (CV) |

Best tuned XGBoost hyperparameters: `n_estimators=50`, `max_depth=5`, `learning_rate=0.1`

## Key Insight

Extreme prediction errors are concentrated in customers **under 25 years old**. This suggests the model underperforms for younger customers — likely due to insufficient signal or higher variance in premiums within this segment — and would benefit from a dedicated sub-model or additional engineered features targeting this group.

## Tech Stack

`Python` · `pandas` · `NumPy` · `seaborn` · `matplotlib` · `scikit-learn` · `XGBoost` · `statsmodels`

## Project Structure
```
health-insurance-premium-prediction/
├── notebooks/
│   └── ml_premium_prediction.ipynb   # Full analysis and modeling notebook
└── README.md
```

> Raw dataset (`premiums.xlsx`) is excluded from version control — see [Dataset](#dataset) for source details.

## Installation

```bash
git clone https://github.com/HanadIsmail/health-insurance-premium-prediction.git
cd health-insurance-premium-prediction
pip install -r requirements.txt
jupyter notebook notebooks/ml_premium_prediction.ipynb
```

## Future Work
- Build a segmented model for customers under 25 (identified as the high-error group)
- Build a Streamlit app for interactive premium prediction
- Deploy the app and set up an MLOps pipeline (versioning, CI/CD, monitoring)

## License
This project is licensed under the MIT License.
