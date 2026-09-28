# Healthcare Analytics for Doctor Visits

**Data Analytics DIY Project | VOIS For Tech, AICTE TIRTC (August Batch, 2026-27)**

| | |
|---|---|
| **Author** | Gajanan Harinarayan Raje |
| **Course** | TYBCA (Third Year Bachelor of Computer Applications) |
| **College** | MGM's College of Computer Science & IT, Nanded |
| **University** | Swami Ramanand Teerth Marathwada University (SRTMU) |
| **Tools** | Python, Pandas, NumPy, Matplotlib, Seaborn, Google Colab |

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Dataset Description](#3-dataset-description)
4. [Methodology](#4-methodology)
5. [Data Cleaning](#5-data-cleaning)
6. [Exploratory Data Analysis (10 Charts)](#6-exploratory-data-analysis-10-charts)
7. [Key Findings](#7-key-findings)
8. [Correlation Summary](#8-correlation-summary)
9. [Conclusion](#9-conclusion)
10. [Limitations](#10-limitations)
11. [Project Structure](#11-project-structure)
12. [How to Run](#12-how-to-run)

---

## 1. Project Overview

Hospitals and clinics collect a lot of patient data, but the raw records do not show *why* some people visit a doctor more often than others. This project analyses a healthcare dataset of **5,190 patients** to find which factors are linked to the number of doctor visits.

The work follows a complete data analytics workflow: load the data, check its quality, clean it, explore it with 10 visualizations, measure correlations, and write down the insights. All code runs in Google Colab.

## 2. Objectives

- Load, inspect and clean the healthcare dataset.
- Understand how doctor visits are distributed across patients.
- Compare visits across gender, age, income, illness score, chronic conditions and insurance type.
- Measure which variables are most strongly related to the number of visits.
- Summarise the findings in a report and a presentation.

## 3. Dataset Description

| Item | Value |
|------|-------|
| File | `Healthcare_Analytics_for_Doctor_Visits.csv` |
| Rows | 5,190 patients |
| Columns | 13 (1 row-index column + **12 variables**) |
| Missing values | 0 |
| Duplicate rows | 0 |
| Target variable | `visits` |

| Variable | Type | Range / Values | Meaning |
|----------|------|----------------|---------|
| `visits` | Numeric | 0 to 9 | Number of doctor visits (target) |
| `gender` | Categorical | male / female | Gender of the patient |
| `age` | Numeric | 0.19 to 0.72 | Age (scaled value) |
| `income` | Numeric | 0.0 to 1.5 | Income (scaled value) |
| `illness` | Numeric | 0 to 5 | Illness score |
| `reduced` | Numeric | 0 to 14 | Days of reduced activity |
| `health` | Numeric | 0 to 12 | Health score |
| `private` | Yes / No | 2,298 yes | Has private health insurance |
| `freepoor` | Yes / No | 222 yes | Free government insurance (low income) |
| `freerepat` | Yes / No | 1,091 yes | Free government insurance (other category) |
| `nchronic` | Yes / No | 2,092 yes | Chronic condition (not limiting activity) |
| `lchronic` | Yes / No | 605 yes | Chronic condition (limiting activity) |

> Variable meanings follow the standard description of this dataset. The first column (`Unnamed: 0`) is only a row index and is dropped during cleaning.

**Basic statistics of `visits`:** mean 0.30, median 0, maximum 9.

## 4. Methodology

```
Load CSV  ->  Explore  ->  Clean  ->  10 Charts  ->  Correlation  ->  Insights
```

1. **Load** the CSV into a Pandas DataFrame.
2. **Explore** with `head`, `tail`, `shape`, `info`, `describe`, null and duplicate checks.
3. **Clean** and encode the columns for analysis.
4. **Visualize** the data with 10 charts (saved as PNG).
5. **Correlate** every variable with `visits`.
6. **Summarise** the findings.

## 5. Data Cleaning

- Dropped the unnecessary row-index column (`Unnamed: 0`).
- Checked for missing values: **none found**.
- Checked for duplicate rows: **none found**.
- Converted the Yes/No columns (`private`, `freepoor`, `freerepat`, `nchronic`, `lchronic`) to 1 / 0.
- Created `gender_encoded` (male = 1, female = 0) for correlation analysis, keeping the original `gender` column for chart labels.
- Created age groups and reduced-activity groups to make category-wise charts clearer.
- Saved the cleaned data as `Healthcare_Analytics_Cleaned.csv`.

## 6. Exploratory Data Analysis (10 Charts)

### Chart 1: Doctor Visits Distribution
![Chart 1](charts/chart1.png)

79.8% of patients had **0 visits**; only 20.2% visited at least once (maximum 9).

### Chart 2: Visits by Gender
![Chart 2](charts/chart2.png)

Females average **0.36** visits and males **0.24**. The sample is 52% female (2,702 of 5,190).

### Chart 3: Illness Score vs Visits
![Chart 3](charts/chart3.png)

Average visits rise with the illness score, from 0.08 (score 0) to 0.81 (score 5).

### Chart 4: Income vs Visits
![Chart 4](charts/chart4.png)

Income has a weak negative link with visits (correlation -0.08).

### Chart 5: Age Groups vs Visits
![Chart 5](charts/chart5.png)

Visits rise with age, from 0.21 in the youngest group to 0.43 in the oldest group.

### Chart 6: Chronic Conditions
![Chart 6](charts/chart6.png)

Patients with a limiting chronic condition average **0.60** visits vs 0.26 without (about 2.3 times). For the non-limiting chronic condition the gap is smaller: 0.35 vs 0.27.

### Chart 7: Insurance Type
![Chart 7](charts/chart7.png)

Free-insurance (`freerepat`) patients average 0.47 visits vs 0.26. `freepoor` patients average only 0.16 vs 0.31. Private insurance makes little difference (0.30 vs 0.31).

### Chart 8: Health Score
![Chart 8](charts/chart8.png)

Health score and visits are positively related (correlation +0.19): a higher score goes with more visits. The median score is 0.

### Chart 9: Reduced Activity Days vs Visits
![Chart 9](charts/chart9.png)

| Reduced activity days | Patients | Average visits |
|-----------------------|----------|----------------|
| 0 days | 4,454 | 0.18 |
| 1-5 days | 444 | 0.66 |
| 6-10 days | 91 | 1.33 |
| 11+ days | 201 | 1.66 |

Patients with 11 or more reduced-activity days visit about **9 times** as often as those with none.

### Chart 10: Correlation Heatmap
![Chart 10](charts/chart10.png)

A single view of how all variables relate to each other and to `visits`.

## 7. Key Findings

1. **Most patients rarely visit a doctor.** 79.8% had no visits; the average is 0.30 per person.
2. **Reduced activity days is the strongest factor** linked with visits (correlation +0.42).
3. **Chronic conditions matter.** Patients with a limiting chronic condition average 0.60 visits vs 0.26.
4. **Illness score matters.** Average visits go from 0.08 to 0.81 as the score rises from 0 to 5.
5. **Females visit more than males** in this sample (0.36 vs 0.24).
6. **Age and income have a weak effect** compared with health-related variables.
7. **Insurance groups behave differently.** `freerepat` patients visit more, `freepoor` patients visit less, and private insurance shows almost no difference.

## 8. Correlation Summary

Correlation of each variable with `visits` (from the cleaned data):

| Variable | Correlation | Strength |
|----------|-------------|----------|
| `reduced` | +0.42 | Moderate |
| `illness` | +0.22 | Weak |
| `health` | +0.19 | Weak |
| `lchronic` | +0.14 | Weak |
| `age` | +0.13 | Weak |
| `freerepat` | +0.11 | Weak |
| `nchronic` | +0.05 | Very weak |
| `private` | -0.01 | Very weak |
| `freepoor` | -0.04 | Very weak |
| `income` | -0.08 | Very weak |
| `gender` (male = 1) | -0.08 | Very weak |

## 9. Conclusion

Health-related variables, especially **reduced activity days**, the **illness score**, the **health score** and **limiting chronic conditions**, are more closely linked to doctor visits than age, gender or income. A small group of patients with health problems accounts for most of the visits, since about 80% of patients did not visit a doctor at all.

These findings suggest that providers could use simple indicators such as reduced-activity days and chronic-condition status to identify patients who are likely to need more care.

## 10. Limitations

- The analysis shows **association, not cause and effect**.
- About 80% of the target values are 0, so averages are small and the data is highly skewed.
- Age and income are scaled values, so their charts show relative rather than exact levels.
- No prediction model was built; this project is exploratory analysis only.

## 11. Project Structure

```
healthcare-analytics-doctor-visits/
├── README.md
├── Healthcare_Analytics_for_Doctor_Visits.ipynb   # full Colab code
├── data/
│   ├── Healthcare_Analytics_for_Doctor_Visits.csv # original dataset
│   └── Healthcare_Analytics_Cleaned.csv           # cleaned dataset
├── charts/
│   └── chart1.png ... chart10.png                 # 10 visualizations
└── docs/
    ├── Healthcare_Analytics_Presentation.pptx     # project presentation
    └── Healthcare_Analytics_Report.pdf            # project report
```

## 12. How to Run

1. Open [Google Colab](https://colab.research.google.com) and upload `Healthcare_Analytics_for_Doctor_Visits.ipynb` (File > Upload notebook).
2. Upload `data/Healthcare_Analytics_for_Doctor_Visits.csv` using the folder icon on the left.
3. Make sure the file path in the first code cell matches your uploaded file name:
   ```python
   df = pd.read_csv('/content/Healthcare_Analytics_for_Doctor_Visits.csv')
   ```
4. Run all cells (Runtime > Run all). The 10 charts and the cleaned CSV are saved in the Colab file panel.

**Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn` (all pre-installed in Colab).

---

**Author:** Gajanan Harinarayan Raje | TYBCA, MGM's College of Computer Science & IT, Nanded
