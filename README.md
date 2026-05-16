# 🇸🇦 Saudi Job Market Analysis — Bayt.com Dataset

> End-to-end SQL data analysis project exploring hiring trends across Saudi Arabia using 3,519 real job postings scraped from Bayt.com.

---

## 📸 Project Preview

<!-- Add your screenshots below — replace the placeholder paths with your actual image filenames -->

| Overview | City Analysis |
|----------|---------------|
![Image](https://github.com/saeedullah-tech/Saudi-Job-Market-Analysis-Bayt.com-Dataset/blob/f322ff99a88fc4a3da0e3d1cfc24513bebc60a4f/SQL%20Job1.png)
![Image](https://github.com/saeedullah-tech/Saudi-Job-Market-Analysis-Bayt.com-Dataset/blob/f322ff99a88fc4a3da0e3d1cfc24513bebc60a4f/SQL%20Jobs2.png)
![Image](https://github.com/saeedullah-tech/Saudi-Job-Market-Analysis-Bayt.com-Dataset/blob/f322ff99a88fc4a3da0e3d1cfc24513bebc60a4f/SQL%20Jobs3.png) 
![Image](https://github.com/saeedullah-tech/Saudi-Job-Market-Analysis-Bayt.com-Dataset/blob/f322ff99a88fc4a3da0e3d1cfc24513bebc60a4f/SQL%20Jobs.png)

---

## 📌 Project Overview

This project analyzes the Saudi job market using a real dataset sourced from **Bayt.com** — one of the largest job platforms in the Middle East. The goal was to extract, clean, and analyze job posting data entirely in SQL to uncover actionable hiring insights across cities, industries, career levels, and companies.

**All analysis was done using PostgreSQL via pgAdmin 4 — no BI tool, no Excel, pure SQL.**

---

## 🎯 Key Findings

| Insight | Finding |
|--------|---------|
| 🏙️ Top City | Riyadh accounts for **41% of all job postings** (1,443 jobs) |
| 🏥 Largest Sector | Business Support + Healthcare = **over 1,689 combined postings** |
| 🛢️ Oil & Gas | Aramco alone holds **211 vacancies** — 58% of the entire sector |
| 👔 Career Level | Mid Career is the most demanded — **fresh graduates face strong competition** |
| 🏨 Surprise | Marriott / Ritz Carlton posted **179 vacancies** — Vision 2030 hospitality boom |
| 🏥 Healthcare Giants | King Faisal Specialist Hospital appears across **3 cities** with 282 total postings |

---

## 🗂️ Dataset Structure

The dataset was loaded into a PostgreSQL table with **25 fields** including:

```sql
CREATE TABLE bayt_jobs (
    job_id              TEXT,
    title               TEXT,
    company_name        TEXT,
    job_city            TEXT,
    job_country         TEXT,
    company_industry    TEXT,
    career_level        TEXT,
    job_role            TEXT,
    employment_type     TEXT,
    monthly_salary_min  TEXT,
    monthly_salary_max  TEXT,
    min_years_experience TEXT,
    max_years_experience TEXT,
    degree              TEXT,
    gender              TEXT,
    number_of_vacancies TEXT
    -- ... and more
);
```

---

## 🧹 Data Cleaning

### Convert empty strings to NULL
```sql
UPDATE bayt_jobs
SET company_name = NULLIF(company_name, ''),
    job_city     = NULLIF(job_city, ''),
    job_country  = NULLIF(job_country, '');
```

### Remove duplicate records
```sql
DELETE FROM bayt_jobs a
USING bayt_jobs b
WHERE a.ctid < b.ctid
  AND a.job_id = b.job_id;
```

---

## 📊 Analysis Queries

### Total job count
```sql
SELECT COUNT(*) AS total_jobs FROM bayt_jobs;
-- Result: 3,519
```

### Jobs by city (Saudi Arabia only)
```sql
SELECT job_city, COUNT(*) AS total_jobs
FROM bayt_jobs
WHERE job_country ILIKE '%saudi%'
GROUP BY job_city
ORDER BY total_jobs DESC;
```

### Jobs by industry
```sql
SELECT company_industry, COUNT(*) AS total_jobs
FROM bayt_jobs
GROUP BY company_industry
ORDER BY total_jobs DESC;
```

### Career level distribution
```sql
SELECT career_level, COUNT(*) AS total_jobs
FROM bayt_jobs
GROUP BY career_level
ORDER BY total_jobs DESC;
```

### Job role demand
```sql
SELECT job_role, COUNT(*) AS total_jobs
FROM bayt_jobs
GROUP BY job_role
ORDER BY total_jobs DESC;
```

### Top 10 companies by vacancies
```sql
SELECT company_name, COUNT(*) AS total_jobs
FROM bayt_jobs
GROUP BY company_name
ORDER BY total_jobs DESC
LIMIT 10;
```

### Skill demand by city
```sql
SELECT job_role, job_city, COUNT(*) AS total_jobs
FROM bayt_jobs
GROUP BY job_role, job_city
ORDER BY total_jobs DESC;
```

---

## 📈 Results Summary

### 🏙️ Top 5 Cities
| City | Jobs | Share |
|------|------|-------|
| Riyadh | 1,443 | 41.0% |
| Jeddah | 428 | 12.2% |
| Khobar | 144 | 4.1% |
| Medina | 102 | 2.9% |
| Mecca | 86 | 2.4% |

### 🏭 Top Industries
| Industry | Jobs |
|----------|------|
| Business Support Services | 1,064 |
| Medical / Hospital | 625 |
| Oil & Gas | 363 |
| IT Services | 197 |
| Construction & Building | 88 |

### 👔 Career Levels
| Level | Jobs |
|-------|------|
| Mid Career | 581 |
| Management | 208 |
| Entry Level | 154 |
| Director / Head | 40 |
| Fresh Graduate | 11 |

### 🏢 Top Companies
| Company | Vacancies |
|---------|-----------|
| Aramco Services Company | 211 |
| Marriott International / Ritz Carlton | 179 |
| King Faisal Specialist Hospital (x3 branches) | 282 |
| King Abdulaziz Medical City – Riyadh | 113 |

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **PostgreSQL** | Database engine |
| **pgAdmin 4** | SQL query interface |
| **SQL** | Data cleaning, transformation & analysis |

---

## 📁 Repository Structure

```
📦 saudi-job-market-analysis
 ┣ 📂 screenshots/
 ┃ ┣ 01_overview.png
 ┃ ┣ 02_cities.png
 ┃ ┣ 03_industry.png
 ┃ ┣ 04_career_levels.png
 ┃ ┣ 05_companies.png
 ┃ ┗ 06_sql_methodology.png
 ┣ 📄 bayt_analysis.sql       ← All queries used in this project
 ┣ 📄 README.md
 ┗ 📄 Bayt_Saudi_JobMarket_Report.pdf
```

---

## 🚀 How to Reproduce

1. Clone this repo
2. Open **pgAdmin 4** and create a new database
3. Run the `CREATE TABLE` statement from the SQL section above
4. Import your dataset via pgAdmin's import tool (CSV format)
5. Run the queries in `bayt_analysis.sql` in order


---

*This project is part of my data analytics portfolio showcasing real-world SQL analysis on Saudi labor market data.*
