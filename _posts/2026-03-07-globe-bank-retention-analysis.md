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
  overlay_image: https://images.unsplash.com/photo-1563013544-824ae1b704d3?w=1200&auto=format&fit=crop
  teaser: https://images.unsplash.com/photo-1563013544-824ae1b704d3?w=400&auto=format&fit=crop&q=80
  caption: "Photo credit: Unsplash: Avery Evans"(https://unsplash.com/@blakewisz)"
description: An end-to-end Python data analysis project uncovering the key drivers of customer churn across 10,127 bank customers — covering EDA, feature engineering, statistical analysis, Random Forest modelling, and data storytelling.
---
Globe Bank International — Customer Retention Analysis
Python Portfolio Project | End-to-End Customer Churn Analysis

🎯 The Challenge
Banks face a costly and persistent problem: customers leave without warning, and by the time it is noticed, it is too late to act.
Imagine being a retention manager responsible for thousands of credit card customers — but your only visibility into churn risk is a monthly report that arrives two weeks after the fact. You are left asking:

Which customers are most likely to churn next month?
Are certain demographic groups leaving at higher rates?
What behaviours distinguish churned customers from retained ones?
Where should we focus our retention budget for maximum impact?

This was the business problem I set out to solve.

💡 My Solution
I built a complete four-stage Python analysis pipeline that transforms raw customer data into actionable retention insights. The solution moves from raw data exploration through to polished executive dashboards and prioritised business recommendations — demonstrating the full analytical workflow a data analyst would follow in a real organisation.

📊 Project Architecture
The solution is structured as a four-stage analytical framework, with each stage building on the last.

Stage 1 — Setup and Exploration
Notebook: 01_setup_exploration.ipynb
The first stage establishes the analytical foundation — loading the data, understanding its structure, checking quality, and visualising key distributions.
Key activities:

Loaded 10,127 customer records across 23 raw columns
Dropped 2 Naive Bayes classifier columns and the CLIENTNUM identifier
Confirmed zero missing values and zero duplicate rows
Encoded the target variable: Attrition_Flag (0 = Retained, 1 = Churned)
Visualised churn distribution, numeric feature histograms, and categorical breakdowns

Key finding: 16.1% churn rate — 1,627 customers left the bank out of 10,127 total. Significant class imbalance (~84% retained vs ~16% churned) was flagged for modelling consideration.

Stage 2 — Cleaning and Transformation
Notebook: 02_cleaning_transformation.ipynb
The second stage prepares a clean, analysis-ready dataset through encoding and feature engineering.
Encoding applied:
ColumnMethodDetailAttrition_FlagBinaryExisting Customer = 0, Attrited Customer = 1Education_LevelOrdinalUneducated (0) through Doctorate (6)Income_CategoryOrdinalLess than $40K (0) through $120K+ (5)Card_CategoryOrdinalBlue (0) through Platinum (3)GenderBinaryM = 1, F = 0Marital_StatusOne-hotDummy variables, drop first
Features engineered:
FeatureBusiness MeaningTrans_Freq_RatioHow actively the customer transacts relative to tenureInactivity_RateProportion of the year spent inactiveContact_IntensityContact frequency relative to tenureUtilisation_BandUtilisation ratio binned into Very Low / Low / Medium / High
Output: data/processed/bank_churners_clean.csv — 10,127 rows x 30 columns

Stage 3 — Analysis and Insights
Notebook: 03_analysis_insights.ipynb
The analytical core of the project — four complementary techniques to identify churn drivers from different angles.
Correlation analysis
Pearson correlation coefficients were calculated between each numeric feature and Attrition_Flag.
Strongest features associated with retention: Total_Trans_Ct, Total_Trans_Amt, and Trans_Freq_Ratio — customers who transact more stay longer.
Strongest features associated with churn: Months_Inactive_12_mon and Contacts_Count_12_mon — inactivity and frequent contact both signal churn risk.
Churn by demographic groups
Churn rates were calculated across all five categorical features. Notable findings:

Platinum card holders churn at notably higher rates than Blue card holders
Lower income brackets show higher churn rates
Single customers churn at a slightly higher rate than married customers
Minimal difference in churn rate between male and female customers

Statistical comparisons — Churned vs Retained
Welch's independent samples t-tests were run for all 17 numeric features, with Cohen's d calculated to measure practical effect size.
FeatureDirectionInterpretationTotal_Trans_CtHigher in retainedRetained customers transact far more frequentlyTotal_Trans_AmtHigher in retainedRetained customers spend significantly moreMonths_Inactive_12_monHigher in churnedChurned customers were inactive for longerTotal_Revolving_BalHigher in retainedRetained customers carry higher revolving balancesContacts_Count_12_monHigher in churnedChurned customers contacted the bank more often
Key churn driver identification — Random Forest
A Random Forest classifier (100 estimators, random_state=42) was fitted to rank features by predictive importance.
RankFeatureImportance1Total_Trans_CtHighest2Total_Trans_AmtHigh3Total_Ct_Chng_Q4_Q1High4Total_Amt_Chng_Q4_Q1Medium-High5Months_Inactive_12_monMedium-High
Transaction behaviour dominates churn prediction — both the volume and trend of transactions are far more predictive than demographic characteristics.

Stage 4 — Visualisation and Storytelling
Notebook: 04_visualisation_storytelling.ipynb
The final stage translates analysis into polished, portfolio-ready visualisations and actionable business recommendations.
OutputDescriptionExecutive DashboardKPI cards, churn split, transaction comparison, distribution chartTop Churn Drivers ChartRanked horizontal bar chart with colour-coded importance tiersDemographic BreakdownInteractive Plotly dashboard and static PNG across all 5 segmentsRecommendations CardDark-theme visual card with prioritised business actions

🗂️ Project Structure
globe-bank-retention-analysis/
|
|-- data/
|   |-- raw/                               <- Original dataset (never modified)
|   |-- processed/                         <- Cleaned, analysis-ready data
|
|-- notebooks/
|   |-- 01_setup_exploration.ipynb         <- Stage 1: EDA and data inspection
|   |-- 02_cleaning_transformation.ipynb   <- Stage 2: Cleaning and feature engineering
|   |-- 03_analysis_insights.ipynb         <- Stage 3: Statistical analysis and churn drivers
|   |-- 04_visualisation_storytelling.ipynb <- Stage 4: Dashboards and recommendations
|
|-- outputs/
|   |-- figures/                           <- Saved .png charts
|   |-- reports/                           <- Saved .html interactive charts
|
|-- .gitignore
|-- README.md
|-- requirements.txt

🛠️ Tools and Libraries
CategoryToolsLanguagePython 3.13Data manipulationpandas, numpyVisualisationmatplotlib, seaborn, PlotlyStatistical analysisscipy (Welch's t-test, Cohen's d)Machine learningscikit-learn (Random Forest)EnvironmentJupyter Notebook, VS Code

💡 Business Recommendations
PriorityFindingRecommended ActionHIGHLow transaction activity is the #1 churn signalTrigger automated re-engagement campaigns when transaction count drops below the 3-month rolling averageHIGHInactive customers churn at significantly higher ratesImplement 60-day inactivity alerts with personal outreach from a relationship managerMEDIUMFewer bank products = lower retentionCross-sell complementary products to single-product customersMEDIUMHigh contact frequency signals dissatisfactionFlag customers with 3+ contacts in 12 months for a proactive satisfaction reviewLOWLower income segments churn at higher ratesReview product-market fit and consider a tailored entry-level card with lower fees

🎓 Reflections and Key Takeaways
Technical lessons:

Transaction behaviour dominates demographic features — Transaction count and amount were far more predictive than age or income. The data tells the real story.
Effect size matters as much as p-values — With 10,000+ rows, almost everything is statistically significant. Cohen's d was essential for understanding which differences are practically meaningful.
Feature engineering adds genuine signal — The engineered Trans_Freq_Ratio and Inactivity_Rate features captured behavioural patterns that raw columns missed.

Design lessons:

Storytelling is a skill separate from analysis — Stage 4 required thinking about what a non-technical stakeholder needs to see, not just what the data shows.
Consistent visual design builds trust — Using the same colour palette (blue for retained, red for churned) across all charts makes the story immediately readable.

Process lessons:

Working notebook by notebook keeps complexity manageable — Splitting the project into four focused notebooks made debugging easier and the final portfolio much cleaner.
A beginner can build production-quality work — This was my first Python project. Focusing on fundamentals, clean structure, and clear communication produced a result I am genuinely proud of.


📂 Project Resources
GitHub Repository: View Full Code and Notebooks
Project files include all four Jupyter notebooks, the cleaned dataset, saved chart PNG files, and interactive HTML reports.

📧 Let's Connect
I am actively seeking Data Analyst opportunities where I can apply Python, statistical analysis, and data storytelling skills to drive data-informed business decisions.
Portfolio: https://moshraf.github.io/
LinkedIn: https://www.linkedin.com/in/moshrafhossain/
GitHub: https://github.com/moshraf

Built with: Python 3.13 | pandas | matplotlib | seaborn | Plotly | scikit-learn | Jupyter | VS Code
Project Duration: March 2026 | Status: Complete and Portfolio-Ready