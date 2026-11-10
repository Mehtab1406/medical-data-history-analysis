# 🏥 Medical Data History Analysis — SQL Project

**Medical Data History Analysis** is a SQL-based data analytics project that queries a **hospital patient history database** using **34 structured SQL queries**. The project works across 4 related tables — patients, admissions, doctors, and province names — to extract meaningful patterns from medical records and support healthcare reporting and decision-making.

The project demonstrates real-world SQL skills including **multi-table joins, subqueries, aggregate functions, conditional logic, and data classification** — all applied to a live MySQL database accessed through phpMyAdmin.

---

## 🎯 Project Objective

The primary objective of this project is to build a structured SQL query layer over raw medical data that enables the healthcare client to:

- Filter and retrieve specific patient records by demographics, diagnosis, and location
- Identify patients with repeated admissions for the same condition
- Link patients to their attending doctors and medical specialties
- Classify patients by BMI to flag obesity risk
- Analyse admission patterns by day, province, and diagnosis type
- Replace missing allergy data with standardised 'NKA' values
- Deliver a reusable query library for ongoing healthcare reporting

---

## 📌 Key Performance Indicators

The project covers the following key metrics:

- 🗄️ **Tables in Database:** 4 (patients, admissions, doctors, province_names)
- 📋 **Total SQL Queries Written:** 34
- 🔗 **Join Types Used:** 2-table JOIN, 3-table JOIN, UNION ALL
- 📐 **SQL Concepts Covered:** 15+ techniques
- 🏥 **Data Type:** Hospital patient records — diagnoses, admissions, doctors
- 🛠️ **Tool:** MySQL via phpMyAdmin

---

## 🔍 Key Insights

### Patient Demographics
The database contains patients across multiple Canadian provinces with varying demographics. Gender distribution, weight ranges, and birth year trends were extracted to give the client a clear picture of their patient base.

### Diagnosis Patterns
Patients diagnosed with conditions like Dementia and Epilepsy were isolated using JOIN queries. Repeat admission analysis revealed which patients returned with the same diagnosis — a key indicator for healthcare planning and resource allocation.

### Doctor–Patient Relationships
3-table joins across patients, admissions, and doctors allowed the client to see exactly which doctor treated which patient for which condition. This is essential for specialty reporting and workload analysis.

### Obesity Classification
BMI was calculated per patient using the standard formula: `weight(kg) / height(m)²`. Patients were classified as obese (BMI ≥ 30) or not using CASE WHEN logic, giving the client a ready-made obesity flag across their entire patient base.

### Admission Trends
Admission volume was broken down by day of month to identify the busiest admission days. Same-day discharge cases were also identified separately — useful for capacity and bed management planning.

### Allergy Data Quality
NULL allergy values were replaced with 'NKA' (No Known Allergies) using an UPDATE statement, standardising the data for clean reporting going forward.

---

## 💡 Sample Queries

**Patients admitted multiple times with the same diagnosis:**
```sql
SELECT patient_id, diagnosis
FROM admissions
GROUP BY patient_id, diagnosis
HAVING COUNT(*) > 1;
```

**Classify patients as Obese or Not (BMI ≥ 30):**
```sql
SELECT patient_id, weight, height,
  CASE
    WHEN weight / POWER(height / 100.0, 2) >= 30 THEN 1
    ELSE 0
  END AS isObese
FROM patients;
```

**3-table JOIN — Epilepsy patients treated by Dr. Lisa:**
```sql
SELECT p.patient_id, p.first_name, p.last_name, d.specialty
FROM patients p
JOIN admissions a ON p.patient_id = a.patient_id
JOIN doctors d ON a.attending_doctor_id = d.doctor_id
WHERE a.diagnosis = 'Epilepsy'
  AND d.first_name = 'Lisa';
```

**Most common allergies (NULLs excluded):**
```sql
SELECT allergies, COUNT(*) AS total_count
FROM patients
WHERE allergies IS NOT NULL
GROUP BY allergies
ORDER BY total_count DESC;
```

---

## 📂 Project Files

| File | Description |
|------|-------------|
| [`medical_analysis.sql`](medical_analysis.sql) | All 34 SQL queries with comments and explanations |
| `README.md` | Project documentation |

---

## 🛠️ Tools & Technologies

- MySQL
- phpMyAdmin
- SQL (DDL, DML, DQL)
- Google Colab (for documentation)
- Microsoft Word (project report)

---

## 📋 SQL Concepts Covered

### Filtering & Selection
Covers techniques for:
- WHERE, AND, OR, IN, BETWEEN
- LIKE pattern matching (starts with, ends with, contains)
- IS NULL / IS NOT NULL
- DISTINCT

### Aggregation & Grouping
Focuses on:
- COUNT, SUM, MAX, MIN, AVG
- GROUP BY with HAVING
- Filtering on aggregated results

### Joins & Set Operations
Provides skills in:
- INNER JOIN across 2 tables
- INNER JOIN across 3 tables
- UNION ALL to combine result sets

### Functions & Logic
Covers:
- String: CONCAT, UPPER, LOWER, LENGTH
- Date: YEAR, DAY
- Math: FLOOR, POWER
- Conditional: CASE WHEN ... THEN ... ELSE ... END

### Data Modification
- UPDATE with WHERE to standardise NULL values

---

## 💡 Business Value

This project helps the healthcare client:

- Access structured, filtered patient data without manual searching
- Identify high-risk patients (repeat admissions, obesity classification)
- Match patients to doctors and specialties for resource planning
- Understand admission load patterns by day and province
- Maintain clean, standardised allergy records across the database
- Run any of the 34 queries on updated data without rewriting them

By delivering a reusable SQL query library, the client's team can generate reports on demand without depending on a data analyst for every request.

---

## 👩‍💻 Author

**Mehtab Bibi**

Data Analyst | Dubai, UAE | SQL | Python | Power BI | Machine Learning

*DataMites Certified Data Analyst — NASSCOM Accredited | 2026*
