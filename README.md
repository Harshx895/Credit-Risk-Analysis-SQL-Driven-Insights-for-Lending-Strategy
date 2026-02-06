# Credit Risk Analysis: SQL-Driven Insights for Lending Strategy

## 📊 Project Overview

This project analyzes **51,336 credit applicants** to uncover behavioral patterns that distinguish high-risk from low-risk borrowers. Using SQL-driven feature engineering and cohort analysis, we debunk common myths about credit scoring and provide actionable recommendations for improving lending decisions.

---

## 🎯 Objectives

- Identify the most predictive features for credit risk assessment
- Test common assumptions about borrower characteristics (education, income, marital status)
- Build a simple, interpretable risk scoring system using SQL
- Provide data-driven recommendations for lending strategy optimization

---

## 📁 Dataset Structure

The analysis uses **three main tables** from a MySQL database:

1. **`internal_bank_dataset`** - Bank-collected applicant information (demographics, income, employment)
2. **`external_cibil_dataset`** - Credit bureau data (payment history, loan types, delinquency records)
3. **`final_credit_data`** - Cleaned, feature-engineered view (47 key features from 88 original columns)

### Key Feature Categories:
- **Identity & Target**: Prospect ID, Credit Score, Approval Flag (P1-P4)
- **Demographics**: Age, Gender, Marital Status, Education, Income
- **Portfolio Mix**: Loan counts by type (Auto, CC, Consumer, Gold, Home, PL)
- **Credit History**: Age of oldest/newest trade lines
- **Recent Behavior**: 6-month velocity (openings, enquiries)
- **Payment History**: 12-month delinquency and account status
- **Risk Signals**: Missed payments, delinquency severity
- **Utilization Metrics**: CC/PL utilization, unsecured exposure

---

## 🔍 Methodology

### 1. **Data Preparation & Feature Engineering**
- Reduced dataset from 88 to 47 features using parsimony and banking logic
- Applied temporal optimization (6-month vs. 12-month windows)
- Removed redundant ratios, multicollinear features, and noisy indicators
- Handled missing values (coded as -99999) using `NULLIF`

### 2. **Cohort Analysis & Pattern Discovery**
- Segmented applicants by risk category (P1=Elite → P4=High Risk)
- Tested conventional wisdom about education, income, and marital status
- Analyzed behavioral patterns (credit hunger, utilization, payment history)

### 3. **Risk Scoring System Development**
- Created a simple 3-point risk score based on:
  1. High recent credit enquiries (top 30%)
  2. Credit card utilization >70%
  3. Any delinquency in last 12 months
- Validated scoring system against actual risk categories

---

## 📈 Key Findings

### 🎓 **Education ≠ Financial Responsibility**
- Highest percentage of educated borrowers (53%) found in **P4 (highest risk)** category
- Education level shows minimal distinction between elite (P1) and high-risk (P4) borrowers
- **Insight**: High earnings don't guarantee financial discipline

### 💍 **Marital Status as Stability Signal**
- Clear correlation: Married applicants dominate P1 (90%) vs. P4 (64%)
- **Insight**: Marital status is a stronger stability indicator than education

### 💰 **High-Income Risk Paradox**
- Riskiest borrowers (3-point risk score) have **27% higher average income** than safest group
- **Insight**: Capacity to pay ≠ willingness to pay

### ⚠️ **Behavioral Red Flags Are Powerful**
Simple 3-point system predicts risk with high accuracy:
- **0 risk points**: 88% chance of being in safe categories (P1/P2)
- **1+ risk points**: 10x increase in P4 probability (2.6% → 21.8%)

### 🕰️ **Time Builds Trust (With Thresholds)**
- **Credit history**: 5+ years marks significant risk reduction
- **Job tenure**: 5+ years at current employer → 79% approval rate vs. 58% for <1 year
- **Insight**: Both show threshold effects around the 5-year mark

### 🔄 **Gateway Loan Strategy Questioned**
- Applicants who skipped consumer loans had **highest P1 probability (23%)**
- Consumer-loan-only applicants had **lowest P1 probability (7%)**
- **Insight**: Highest-quality borrowers don't need "training wheels"

---

## 💡 Business Recommendations

### 1. **Revise Scoring Model Weights**
- Increase weight for **marital status** (strong stability signal)
- De-emphasize **education level** (poor predictor)
- Consider **job tenure thresholds** (5+ years = lower risk)

### 2. **Implement 3-Flag Quick Triage System**
For rapid risk assessment, check:
1. Recent credit enquiries (top 30%)
2. Credit card utilization (>70%)
3. Recent delinquency (12-month window)
- **0 flags**: Safe to proceed
- **1+ flags**: Require additional scrutiny

### 3. **Segment High-Income Applicants**
- Don't assume high income = low risk
- Apply behavioral checks regardless of income level
- Consider higher monitoring for high-income, high-utilization borrowers

### 4. **Optimize Youth Lending Strategy**
- For young borrowers (<28) with thin credit files:
  - Look beyond job stability alone
  - Consider smaller initial limits with behavior monitoring
  - Use graduated approval approach based on performance

### 5. **Rethink Product Strategy**
- Re-evaluate mandatory "gateway" consumer loans
- Allow qualified applicants to access appropriate products directly
- Create targeted products for 5+ year employment segment

---

## 🛠️ Technical Implementation

### Prerequisites
```bash
Python 3.8+
MySQL Server
Jupyter Notebook
```

### Dependencies
```python
!pip install jupysql pymysql sqlalchemy
```

### Database Connection
```python
%sql mysql+pymysql://root:password@127.0.0.1:3306/db_p1
```

### Key SQL Operations Demonstrated:
1. **Data Cleaning & Feature Engineering**
   - NULL handling for missing values
   - Feature selection based on banking logic
   - Temporal feature creation

2. **Cohort Analysis**
   - Risk category segmentation
   - Demographic pattern identification
   - Behavioral trend analysis

3. **Statistical Analysis**
   - Correlation testing
   - Threshold effect identification
   - Risk score validation

---

## 📊 Risk Distribution
- **P1 (Elite)**: 11.30% - Excellent credit, minimal risk
- **P2 (Good)**: 62.72% - Solid credit, manageable risk
- **P3 (Moderate)**: 14.52% - Some concerns, higher monitoring needed
- **P4 (High)**: 11.46% - Significant risk, requires strict controls


---

## 📝 Conclusion

This project demonstrates that **behavioral patterns matter more than demographic stereotypes** in credit risk assessment. By focusing on recent financial behavior rather than static characteristics, lenders can:

1. **Improve accuracy** of risk predictions
2. **Reduce losses** from unexpected defaults
3. **Identify opportunities** in underserved segments
4. **Optimize pricing** based on true risk factors

The analysis proves that simple, interpretable models built on behavioral data can outperform complex algorithms relying on traditional demographic markers.

---

## 👨‍💻 Author
**Harsh Abhishek Gupta**    
[LinkedIn Profile](https://www.linkedin.com/in/harsh-gupta-717494335?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app) | [GitHub Profile](https://github.com/Harshx895)

## 📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments
- [Dataset](https://www.kaggle.com/datasets/saurabhbadole/leading-indian-bank-and-cibil-real-world-dataset) 

---

**⚠️ Disclaimer**: This analysis is for educational purposes only. Actual credit decisions should consider regulatory requirements, business context, and comprehensive risk assessment frameworks.
