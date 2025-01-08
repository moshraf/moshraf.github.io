---
layout: posts
title:  "Healthcare Insights"
date:   2023-07-01 16:13:27 -0500
tags: [tutorial, sql]
author_profile: true
author: Moshraf Hossain
categories: work
highlight_home: true
tagline: "Uncovering Patterns in Healthcare Data"
header:
  overlay_image: https://plus.unsplash.com/premium_photo-1682130157004-057c137d96d5?w=400&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MXx8aG9zcGl0YWx8ZW58MHx8MHx8fDA%3D
  teaser: https://plus.unsplash.com/premium_photo-1682130157004-057c137d96d5?w=400&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MXx8aG9zcGl0YWx8ZW58MHx8MHx8fDA%3D
  
  caption: "Photo credit: [**Unsplash: Getty Images**](https://unsplash.com/@gettyimages)"
description:  This article showcases a comprehensive SQL portfolio project focused on hospital data analysis, highlighting key SQL queries and insights that demonstrate data manipulation and analysis skills.
---

# Introduction
The project is to demonstrate the use of SQL to extract meaningful insights from a hospital database. This includes analysing patient demographics, hospital stays, risk factors, and other relevant metrics to improve hospital operations and patient care.

## Datasets
- **appointment_analysis**: Contains information about patient appointments including date, time, and department.
- **hospital_records**: Includes details on patient hospital stays, such as duration and department.
- **outpatient_visits**: Records outpatient visits with diagnosis, medication prescribed, and smoker status.
- **patients_table**: Stores patient demographic information.
- **lab_results**: Contains lab test results.

## Key SQL Queries and Their Insights

### 1. Patients in the Pediatrics Department
```sql
SELECT
    patient_id,
    department_name
FROM appointment_analysis
WHERE department_name = 'pediatrics';
```
**Insight:** Identifies which patients have appointments in the Pediatrics department, aiding in resource management and patient distribution analysis.

### 2. Average Days in Cardiology Department
```sql
SELECT AVG(days_in_the_hospital) AS average_days_cardiology
FROM hospital_records
WHERE department_name = 'Cardiology';
```
**Insight:** Calculates the average length of stay for patients in the Cardiology department, helping to assess efficiency and recovery times.

### 3. Average Days per Department
```sql
SELECT
    department_name,
    AVG(days_in_the_hospital) AS avg_days_per_department
FROM hospital_records
GROUP BY department_name
ORDER BY avg_days_per_department DESC;
```
**Insight:** Lists the average patient stay across all departments, highlighting departments with longer or shorter stays.

### 4. Patient Stay Categorization
```sql
SELECT
    patient_id,
    days_in_the_hospital,
    CASE
        WHEN days_in_the_hospital <=3 THEN 'Short'
        WHEN days_in_the_hospital <= 5 THEN 'Medium'
        ELSE 'Long'
    END AS stay_category
FROM hospital_records;
```
**Insight:** Categorizes patients based on the length of their hospital stay, aiding in resource utilization analysis.

### 5. Count of Patients by Stay Category
```sql
SELECT
    CASE
        WHEN days_in_the_hospital <=3 THEN 'Short'
        WHEN days_in_the_hospital <= 5 THEN 'Medium'
        ELSE 'Long'
    END AS stay_category,
    COUNT(*) AS number_of_records
FROM hospital_records
GROUP BY
    CASE
        WHEN days_in_the_hospital <=3 THEN 'Short'
        WHEN days_in_the_hospital <= 5 THEN 'Medium'
        ELSE 'Long'
    END;
```
**Insight:** Provides a count of patients in each stay category, useful for capacity planning.

### 6. Day of the Week from Appointment Date
```sql
SELECT
  appointment_date,
  DAYOFWEEK(appointment_date) AS day_of_the_week
FROM appointment_analysis;
```
**Insight:** Extracts the day of the week from appointment dates, useful for identifying patterns in appointment scheduling and patient flow on different days.

### 7. Day of Hour from Appointment Time
```sql
SELECT
appointment_time,
HOUR(appointment_time) AS appointment_hour
FROM appointment_analysis;
```
**Insight:** Provides the hour of appointments, which can help in analyzing peak times and scheduling efficiency.


### 8. Safety Concerns Based on Smoking and Medication
```sql
SELECT
    patient_id,
    diagnosis,
    medication_prescribed,
    smoker_status,
    CASE
        WHEN smoker_status = 'Y' AND medication_prescribed IN ('Insulin', 'Metformin', 'Lisinopril') THEN 'Potential Safety Concern: Smoking and Medication Interactions'
        ELSE 'No Safety Concern Identified'
    END AS 'safety_concern'
FROM outpatient_visits;
```
**Insight:** Flags potential safety concerns related to smoking and specific medications, critical for patient safety management.

### 9. Risk Classification Based on BMI and Family History
```sql
SELECT
    patient_id,
    patient_name,
    bmi,
    family_history_of_hypertension,
    CASE
        WHEN bmi >= 30 AND family_history_of_hypertension = 'Yes' THEN 'High Risk'
        WHEN bmi >= 25 AND family_history_of_hypertension = 'Yes' THEN 'Medium Risk'
        ELSE 'Low Risk'
    END risk_category
FROM hospital_records;
```
**Insight:** Classifies patients into risk categories based on BMI and family history, supporting targeted health interventions.

### 10. Demographic Characteristics of Diabetic Patients
```sql
SELECT
    gender,
    CASE
        WHEN TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) BETWEEN 18 AND 30 THEN '18-30'
        WHEN TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) BETWEEN 31 AND 50 THEN '31-50'
        WHEN TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) BETWEEN 51 AND 70 THEN '51-70'
        ELSE '71+'
    END AS age_group,
    COUNT(*) AS patient_count
FROM patients_table AS p
INNER JOIN outpatient_visits AS ov
ON p.patient_id = ov.patient_id
WHERE diagnosis = 'Diabetes'
GROUP BY
    gender,
    CASE
        WHEN TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) BETWEEN 18 AND 30 THEN '18-30'
        WHEN TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) BETWEEN 31 AND 50 THEN '31-50'
        WHEN TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) BETWEEN 51 AND 70 THEN '51-70'
        ELSE '71+'
    END;
```
**Insight:** Provides demographic characteristics of diabetic patients, aiding in understanding population distribution and tailoring healthcare services.


## Conclusion
This documentation highlights essential SQL queries used in analyzing hospital data. These queries help in patient care management, risk assessment, and demographic analysis, contributing to better decision-making in hospital operations.
