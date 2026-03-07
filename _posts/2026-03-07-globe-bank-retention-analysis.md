---
layout: posts
title:  "Globe Bank International — Customer Retention Analysis"
date:   2026-03-07
tags: [python]
author_profile: true
author: Moshraf Hossain
categories: work
highlight_home: true
tagline: "Uncovering the drivers of customer churn through end-to-end Python data analysis"
header:
  overlay_image: https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=1200&auto=format&fit=crop
  teaser: https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=400&auto=format&fit=crop&q=80
  caption: "Photo credit: [**Unsplash: Sean Pollock**](https://unsplash.com/@seanpollock)"
description: An end-to-end Python data analysis project uncovering the key drivers of customer churn across 10,127 bank customers — covering EDA, feature engineering, statistical analysis, Random Forest modelling, and data storytelling.
---

# Globe Bank International — Customer Retention Analysis
**Python Portfolio Project | End-to-End Customer Churn Analysis**

## 🎯 The Challenge
Banks face a costly and persistent problem: customers leave without warning. As a retention manager, you might only see monthly reports that arrive too late. Key questions include:

- Which customers are most likely to churn next month?  
- Are certain demographic groups leaving at higher rates?  
- What behaviours distinguish churned customers from retained ones?  
- Where should the retention budget be prioritised for maximum impact?  

This was the business problem I set out to solve.

## 💡 My Solution
I built a **four-stage Python analysis pipeline** that transforms raw customer data into actionable retention insights. The solution moves from data exploration to polished dashboards and prioritised recommendations — demonstrating a full analytical workflow.

---

## 📊 Project Architecture

### Stage 1 — Setup and Exploration
**Notebook:** `01_setup_exploration.ipynb`  

- Loaded 10,127 customer records across 23 raw columns  
- Dropped 2 Naive Bayes classifier columns and the `CLIENTNUM` identifier  
- Confirmed zero missing values and duplicates  
- Encoded `Attrition_Flag` (0 = Retained, 1 = Churned)  
- Visualised churn distribution, numeric histograms, and categorical breakdowns  

**Key finding:** 16.1% churn rate — 1,627 customers left out of 10,127.

---

### Stage 2 — Cleaning and Transformation
**Notebook:** `02_cleaning_transformation.ipynb`  

**Encoding applied:**

| Column | Method | Detail |
|--------|--------|--------|
| Attrition_Flag | Binary | Existing Customer = 0, Attrited Customer = 1 |
| Education_Level | Ordinal | Uneducated (0) → Doctorate (6) |
| Income_Category | Ordinal | < $40K (0) → $120K+ (5) |
| Card_Category | Ordinal | Blue (0) → Platinum (3) |
| Gender | Binary | M = 1, F = 0 |
| Marital_Status | One-hot | Dummy variables, drop first |

**Features engineered:**

| Feature | Meaning |
|---------|--------|
| Trans_Freq_Ratio | Transaction activity relative to tenure |
| Inactivity_Rate | Proportion of year spent inactive |
| Contact_Intensity | Contact frequency relative to tenure |
| Utilisation_Band | Utilisation ratio binned: Very Low / Low / Medium / High |

**Output:** `data/processed/bank_churners_clean.csv` — 10,127 rows × 30 columns

---

### Stage 3 — Analysis and Insights
**Notebook:** `03_analysis_insights.ipynb`  

**Techniques used:**

1. **Correlation Analysis** — Total_Trans_Ct, Total_Trans_Amt, and Trans_Freq_Ratio predict retention; Months_Inactive_12_mon and Contacts_Count_12_mon predict churn  
2. **Churn by Demographics** — Platinum card holders and lower-income segments churn more; single customers slightly more than married  
3. **Statistical Comparisons** — Welch's t-tests with Cohen's d for numeric features  
4. **Random Forest Feature Importance**  

**Top 5 churn predictors:**

| Rank | Feature | Importance |
|------|--------|-----------|
| 1 | Total_Trans_Ct | Highest |
| 2 | Total_Trans_Amt | High |
| 3 | Total_Ct_Chng_Q4_Q1 | High |
| 4 | Total_Amt_Chng_Q4_Q1 | Medium-High |
| 5 | Months_Inactive_12_mon | Medium-High |

**Insight:** Transaction behaviour dominates churn prediction over demographics.

---

### Stage 4 — Visualisation and Storytelling
**Notebook:** `04_visualisation_storytelling.ipynb`  

**Outputs:**

| Output | Description |
|--------|------------|
| Executive Dashboard | KPI cards, churn split, transaction comparison, distribution charts |
| Top Churn Drivers Chart | Ranked horizontal bar chart with colour-coded importance |
| Demographic Breakdown | Interactive Plotly and static PNGs |
| Recommendations Card | Prioritised business actions in a visual card |

---

## 🗂️ Project Structure

## 🗂️ Project Structure

```
globe-bank-retention-analysis/
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
│   ├── 01_setup_exploration.ipynb
│   ├── 02_cleaning_transformation.ipynb
│   ├── 03_analysis_insights.ipynb
│   └── 04_visualisation_storytelling.ipynb
├── outputs/
│   ├── figures/
│   └── reports/
├── .gitignore
├── README.md
└── requirements.txt
```
---

## 🛠️ Tools and Libraries

| Category | Tools |
|---------|-------|
| Language | Python 3.13 |
| Data manipulation | pandas, numpy |
| Visualisation | matplotlib, seaborn, Plotly |
| Statistical analysis | scipy (Welch's t-test, Cohen's d) |
| Machine learning | scikit-learn (Random Forest) |
| Environment | Jupyter Notebook, VS Code |

---

## 💡 Business Recommendations

| Priority | Finding | Recommended Action |
|---------|---------|------------------|
| HIGH 🔴 | Low transaction activity | Trigger automated re-engagement campaigns when transaction count drops below the 3-month rolling average |
| HIGH 🔴 | Inactive customers churn | Implement 60-day inactivity alerts with personal outreach |
| MEDIUM 🟠 | Fewer bank products | Cross-sell complementary products to single-product customers |
| MEDIUM 🟠 | High contact frequency | Flag customers with 3+ contacts in 12 months for proactive satisfaction review |
| LOW 🟡 | Lower income segments | Review product-market fit and offer tailored entry-level cards |

---

## 🎓 Reflections and Key Takeaways

**Technical lessons:**

- Transaction behaviour dominates demographic features  
- Effect size matters as much as p-values  
- Feature engineering captures real behavioural patterns

**Design lessons:**

- Storytelling is separate from analysis  
- Consistent visual design builds trust

**Process lessons:**

- Working notebook by notebook keeps complexity manageable  
- A beginner can produce portfolio-ready, structured, and clean work

---

## 📂 Project Resources

- **GitHub Repository:** [View Full Code and Notebooks](https://github.com/moshraf/globe-bank-retention-analysis)  
- Includes Jupyter notebooks, cleaned dataset, charts, and interactive HTML reports

---

## 📧 Let's Connect

- Portfolio: [https://moshraf.github.io/](https://moshraf.github.io/)  
- GitHub: [https://github.com/moshraf](https://github.com/moshraf)  

Built with Python 3.13 | pandas | matplotlib | seaborn | Plotly | scikit-learn | Jupyter | VS Code  
Project Duration: March 2026 | Status: Complete and Portfolio-Ready