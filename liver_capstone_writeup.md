# Liver Disease Analysis — Indian Liver Patient Dataset

**Author:** Abdul Wahab, MBBS
**Dataset:** Indian Liver Patient Dataset (Kaggle / UCI ML Repository), 583 patients, 11 clinical & demographic features

---

## Introduction

Liver disease remains a major cause of morbidity worldwide, and routine liver function tests (LFTs) — bilirubin, alkaline phosphatase, transaminases (ALT/AST), total protein, and albumin — form the backbone of hepatobiliary screening. This project applies exploratory data analysis (EDA) techniques from Python's NumPy, Pandas, and Seaborn libraries to the Indian Liver Patient Dataset, with the aim of:

1. Understanding the distribution and quality of the data (missingness, outliers, ranges).
2. Identifying patient subgroups (by age, gender, disease status) that show distinct enzyme profiles.
3. Quantifying which liver markers are most strongly associated with disease status.
4. Communicating these findings visually, in a form suitable for clinical review.

This analysis is exploratory and descriptive in nature — it is intended to surface patterns and generate hypotheses, not to establish diagnostic thresholds or causal claims.

---

## 1. Data Overview & NumPy Fundamentals

The dataset contains **583 patients** across 11 columns, including demographics (Age, Gender) and eight liver function markers (Total/Direct Bilirubin, Alkaline Phosphatase, ALT, AST, Total Proteins, Albumin, and the Albumin/Globulin Ratio). The target variable (`Diseased`) was recoded from its original numeric form (1/2) into readable labels (**Yes/No**) for clarity throughout the analysis.

A quick NumPy-level check on `Total_Bilirubin` confirmed a clean 1-dimensional numeric array (583 values, `float64`), consistent with what pandas reports — a useful sanity check before deeper analysis. Examining `Alanine_Aminotransferase` (ALT) directly via NumPy revealed a **mean of ~80.7 U/L** and a **maximum of 2000 U/L** — both well above the normal clinical reference range (roughly 7–56 U/L), indicating this dataset is weighted toward patients with more significant liver dysfunction rather than a general population sample.

---

## 2. Data Cleaning & Boolean Filtering

Checking for missing data revealed **4 patients** with a missing `Albumin_and_Globulin_Ratio` value — a small, manageable gap that doesn't meaningfully affect the analysis but is worth disclosing for transparency.

Filtering patients over age 50 **with** a positive diagnosis identified **158 patients** — a substantial subgroup, useful for age-stratified follow-up analysis if extended further.

As a data-quality exercise, `Total_Bilirubin` values were capped at 20 mg/dL purely for visualization purposes (a small number of extreme outliers, up to 75 mg/dL, would otherwise distort chart scaling). This is explicitly a **display-only adjustment** — real extreme bilirubin values are clinically meaningful and would never be altered before actual diagnostic or modeling work.

---

## 3. Grouped Statistics & Notable Cases

Average `Total_Bilirubin` differed by gender: **Females averaged 2.32 mg/dL**, while **Males averaged 3.61 mg/dL** — a noteworthy gap worth flagging, though this dataset does not allow us to say why (it may reflect referral patterns rather than true biological sex differences, given the sample is not gender-balanced).

The patient with the single highest ALT value in the dataset (**patient index 117**, a 32-year-old male) showed a strikingly severe enzyme profile: ALT of 2000 U/L and AST of 2946 U/L, alongside elevated bilirubin (12.7 mg/dL total, 6.2 mg/dL direct). This is consistent with an acute, severe hepatocellular injury pattern and stands out as a case worth discussing separately from the general trend, as a single outlier of this magnitude can disproportionately affect summary statistics.

Ranking patients by Albumin/Globulin ratio (ascending) identified the 3rd-lowest case (**patient index 533**, a 46-year-old female) with a ratio of just 0.3, alongside elevated ALT (509) and AST (623) — a profile suggestive of chronic liver dysfunction with impaired albumin synthesis.

---

## 4. Visualizations

**Chart 1 — Average Total Bilirubin by Gender and Disease Status (Bar Chart)**
This chart splits average bilirubin by both gender and disease status simultaneously. Both male and female diseased patients show clearly higher average bilirubin than their non-diseased counterparts, and the gap between disease groups is far larger than the gap between genders — suggesting disease status, not sex, is the primary driver of elevated bilirubin in this dataset. As with all group averages, this can be skewed by outliers (such as patient 117) and should be read alongside the underlying spread, not in isolation.

**Chart 2 — Age Distribution by Disease Status (Histogram)**
Overlaying age distributions for diseased vs. non-diseased patients shows that diagnosed patients are concentrated in the 40–60 age range, while non-diseased patients are fewer and more thinly spread across ages. This is consistent with liver disease prevalence generally increasing with age, though the disease group's much larger sample size (416 vs. 167) makes a direct height comparison somewhat misleading — proportional comparison would be a natural next step.

**Chart 3 — Correlation of Liver Markers with Disease Status (Ranked Bar Chart)**
Ranking each numeric marker by its correlation with disease status revealed **Direct Bilirubin (r ≈ 0.25)** and **Total Bilirubin (r ≈ 0.22)** as the strongest positive associations, followed by Alkaline Phosphatase, ALT, and AST — all pointing the expected direction (higher enzyme/bilirubin levels associated with disease). **Albumin (r ≈ -0.16)** and the **Albumin/Globulin Ratio (r ≈ -0.16)** showed the strongest negative associations, consistent with the liver's role in albumin synthesis being impaired in disease. Notably, **all correlations are weak-to-moderate in magnitude** (none exceed 0.3) — no single marker strongly predicts disease status alone, which mirrors real clinical practice, where diagnosis relies on a combination of findings rather than any one lab value in isolation.

---

## 5. Key Findings — Summary

- The dataset comprises 583 patients, with a notable class imbalance: **416 diagnosed with liver disease (71.4%) vs. 167 without (28.6%)** — important context for any future modeling work, as this imbalance would need to be addressed to avoid biased predictions.
- Liver enzyme and bilirubin levels in this dataset skew markedly high overall (mean ALT ~81 U/L vs. a normal upper limit of ~56 U/L), reflecting a patient population already enriched for significant liver pathology rather than a general screening population.
- **Direct and Total Bilirubin showed the strongest positive correlation with disease status**, while **Albumin and Albumin/Globulin Ratio showed the strongest negative correlation** — both directionally consistent with known liver physiology (impaired bile processing raises bilirubin; impaired protein synthesis lowers albumin).
- No single marker showed a strong (>0.3) correlation with disease status in isolation, reinforcing that liver disease diagnosis is inherently multi-factorial and unlikely to be captured by any single lab value.
- Individual outlier cases (e.g., patient 117, ALT 2000 / AST 2946) highlight the importance of examining extreme values individually rather than relying solely on group averages, which can be distorted by a small number of severe cases.
- **Limitations:** This analysis is descriptive and correlational only — no causal claims are made, and the class imbalance and lack of longitudinal data limit generalizability. Future work could include proportional (rather than raw count) comparisons across age groups, and formal statistical testing (e.g., t-tests) to confirm whether observed group differences are statistically significant.

---

*Analysis conducted using Python (NumPy, Pandas, Seaborn/Matplotlib) as part of an ongoing Clinical AI / Data Science learning program.*
