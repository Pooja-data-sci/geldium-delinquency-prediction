# Geldium Delinquency Prediction & AI-Powered Collections Strategy

An end-to-end analysis of customer delinquency risk for Geldium, a consumer lending company — completed as part of the **Tata GenAI-Powered Data Analytics job simulation** (via Forage). This project covers EDA, missing-data handling, predictive modeling, business recommendations, and a proposed AI-driven collections system, using generative AI (Claude) as a thinking partner throughout.

## Business Problem

Geldium wanted to understand which customers were most likely to become delinquent on payments, so its collections team could intervene earlier and more effectively — reducing missed payments while treating customers fairly. The task: analyze 500 customer records, build a predictive model concept, and translate the findings into a responsible, business-ready collections strategy.

## Approach

### 1. Exploratory Data Analysis (`notebooks/geldium_eda_modeling.ipynb`)
- Reviewed structure and quality of a 500-record dataset spanning demographic, credit, and loan attributes plus a 6-month payment history
- Identified and standardized inconsistent category labels (e.g. `EMP` / `Employed` / `employed` collapsed into one group)
- Found and corrected invalid `Credit_Utilization` values above the theoretical 100% cap
- Flagged that the target variable (`Delinquent_Account`) is imbalanced — only 16% of accounts are delinquent

### 2. Missing Data Treatment
Three numeric fields had missing values, each handled with a method suited to its distribution rather than a one-size-fits-all fill:
- **Income** (7.8% missing) — imputed via random draws from a fitted normal distribution, with a "was imputed" flag kept for transparency
- **Loan_Balance** (5.8% missing) — imputed using a regression on Income and Debt-to-Income Ratio, to preserve real inter-variable relationships
- **Credit_Score** (0.4% missing) — simple median imputation

### 3. Feature Engineering & Modeling
- Engineered a `Missed_Months_Count` feature from the raw 6-month payment history
- Trained two models — **logistic regression** (chosen for interpretability, the industry standard in credit risk) and a **decision tree** (comparison baseline) — with class weighting to account for the imbalanced target

### 4. The Honest Finding
Every numeric field's correlation with delinquency fell under 0.05 — far below the 0.15–0.35 range typical of real, even weak, credit-risk predictors. Both trained models scored **at or below random chance** (AUC ≈ 0.43–0.44) on held-out data. Rather than force a result, the analysis concludes this pattern — flat delinquency rates across credit-score bands, and inconsistency between related fields — is most consistent with a **synthetic dataset where the target wasn't generated as a function of the other fields**, and recommends confirming this with the data source before further modeling investment.

Customer *segments* (business cardholders, unemployed customers, Los Angeles-based customers) showed modest delinquency-rate gaps of 7–9.5 percentage points — the closest thing to a usable early signal, though flagged as leads to confirm, not settled findings.

### 5. Business Recommendation
Rather than a full rollout based on unconfirmed assumptions, the report proposes a **6-month pilot**: targeted outreach to customers with utilization above 70%, measured against a matched control group — testing the industry-standard utilization-delinquency link against Geldium's own data before committing further.

### 6. AI-Powered Collections Strategy (`AI-Powered_Collections_Strategy.pptx`)
A high-level system design for applying these insights at scale: system workflow (data → decision logic → action → learning loop), a clear split between autonomous and human-in-the-loop decisions, responsible AI guardrails (fairness, explainability, compliance), and expected business/customer impact.

## Key Files
- `notebooks/geldium_eda_modeling.ipynb` — full code: EDA, cleaning, imputation, feature engineering, modeling
- `data/Delinquency_prediction_dataset.xlsx` — raw dataset
- `EDA_Summary_Report.docx` — written EDA findings
- `Task_2_ModelPlan.docx` — model logic, justification, and evaluation strategy
- `Business_Summary_Report.docx` — business-facing insights and recommendation
- `AI-Powered_Collections_Strategy.pptx` — proposed AI collections system design

## Tools
Python (Pandas, scikit-learn), Excel, PowerPoint, GenAI (Claude) for analysis support and drafting

## Key Takeaway
The most valuable finding in this project wasn't a high-performing model — it was recognizing that the data didn't support one, and saying so clearly rather than overstating a weak result. The recommendation reflects that: pilot and verify, don't deploy on an unconfirmed assumption.

---
*Completed as part of the Tata GenAI-Powered Data Analytics job simulation on Forage.*
