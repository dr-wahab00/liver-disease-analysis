Liver Disease Analysis — Indian Liver Patient Dataset 🩺

Exploratory data analysis of liver function markers and their association with liver disease, using Python (NumPy, Pandas, Seaborn/Matplotlib). Built as part of an ongoing self-directed Clinical AI / Data Science learning program, bridging clinical medicine with data science tooling.

📊 Dataset

Indian Liver Patient Dataset — 583 patients, 11 features including demographics (Age, Gender) and liver function tests (Total/Direct Bilirubin, Alkaline Phosphatase, ALT, AST, Total Proteins, Albumin, Albumin/Globulin Ratio).

🎯 Objectives
Explore data quality: missingness, distributions, outliers
Compare liver marker profiles across gender and disease status
Quantify which markers correlate most strongly with disease status
Present findings in a clinically interpretable, visual format

🛠️ Tools

Python — NumPy, Pandas
Visualization — Seaborn, Matplotlib
Environment — Jupyter Notebook

📁 Contents

liver_capstone_analysis.ipynb — full analysis notebook (data cleaning, filtering, grouped statistics, visualizations)
liver_capstone_writeup.md — written interpretation and key findings summary

🔑 Key Findings

Dataset shows a class imbalance: 416 diseased (71.4%) vs. 167 non-diseased (28.6%) patients
Direct Bilirubin and Total Bilirubin show the strongest positive correlation with disease status
Albumin and Albumin/Globulin Ratio show the strongest negative correlation, consistent with impaired hepatic protein synthesis in liver disease
No single marker strongly predicts disease status alone (all correlations < 0.3 in magnitude) — consistent with real clinical practice, where diagnosis relies on combined findings
Enzyme levels in this dataset skew notably high overall, suggesting a population enriched for significant liver pathology

Full interpretation and limitations discussed in liver_capstone_writeup.md.

🚀 How to Run

pip install pandas numpy seaborn matplotlib
jupyter notebook liver_capstone_analysis.ipynb

👤 Author

Abdul Wahab, MBBS — transitioning toward Clinical AI & healthcare data science.
LinkedIn - linkedin.com/in/dr-abdul-wahab-memon-1ab19a3b4
Github - https://github.com/dr-wahab00

⚠️ Disclaimer

This is an exploratory, educational analysis. Findings are descriptive and correlational, not diagnostic. Not intended for clinical decision-making.
