<div align="center">

# OIBSIP — Data Science Internship Portfolio
### Oasis Infobyte Internship Program · Data Science Track

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![pandas](https://img.shields.io/badge/pandas-Data%20Analysis-150458?style=flat-square&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Status](https://img.shields.io/badge/Status-Completed-2ea44f?style=flat-square)]()
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)]()

**Three end-to-end data science projects — from raw, messy data to cleaned datasets, exploratory insight, and deployed ML models.**

[Unemployment Analysis](#-task-02--india-unemployment-analysis-the-covid-19-shock) ·
[Car Price Prediction](#-task-03--car-price-prediction) ·
[Email Spam Detection](#-task-04--email-spam-detection-with-machine-learning)

</div>

---

## 👋 About This Repository

This repository contains my project submissions for the **AICTE Oasis Infobyte Internship Program (OIBSIP)**, completed under the **Data Science** track. Each project was carried through the **full data science lifecycle** — problem framing, data cleaning, exploratory analysis, feature engineering, model building, evaluation, and clear communication of results — and is documented as a standalone, reproducible mini-project.

| | |
|---|---|
| **Intern** | Chaymae Hanini |
| **Offer Reference** | OIB/T2/IP150 |
| **Track** | Data Science |
| **Duration** | 1 Month |
| **Commencement Date** | 5 August 2026 |
| **Final Submission Deadline** | 15 September 2026 |
| **Organization** | [Oasis Infobyte](https://oasisinfobyte.com/) |

Out of five available tasks, a minimum of three completed projects is required for evaluation and certification — **three are completed here**, spanning exploratory data analysis, regression, and natural language processing.

---

## 🧭 Why This Portfolio

Each project below was deliberately built to reflect real-world data work rather than a tutorial walkthrough:

- **Raw → clean → analysis-ready** data pipelines, with every transformation justified and documented.
- **Insight-driven EDA** — every chart is paired with a plain-language takeaway, not just a plot.
- **Model comparison, not model guessing** — multiple algorithms are trained and benchmarked on the same held-out test set using appropriate metrics (not accuracy alone, where it would mislead).
- **Reproducibility** — fixed random seeds, `requirements.txt` per project, and notebooks that regenerate every chart and model artifact from scratch.
- **Persisted, inference-ready models** (`.pkl`) with runnable code samples — not just training logs.

---

## 📁 Repository Structure

```
OIBSIP/
├── Task_02_Unemployment_Analysis/     # EDA & time-series storytelling
│   ├── data/
│   ├── notebooks/
│   ├── report/                        # Exported charts
│   ├── requirements.txt
│   └── README.md
│
├── Task_03_Car_Price_Prediction/      # Regression & feature engineering
│   ├── data/
│   ├── notebooks/
│   ├── models/                        # Trained, pickled models
│   ├── report/
│   ├── requirements.txt
│   └── README.md
│
├── Task_04_Email_Spam_Detection/      # NLP & text classification
│   ├── data/
│   ├── notebooks/
│   ├── images/
│   ├── models/
│   ├── requirements.txt
│   └── README.md
│
└── README.md                          # You are here
```

Each task folder is fully self-contained with its own dataset, notebook(s), exported visualizations, trained model artifacts (where applicable), dependency list, and a dedicated deep-dive README.

---

## 📊 Project Portfolio

### 📉 Task 02 — India Unemployment Analysis: The COVID-19 Shock
**Focus: Exploratory Data Analysis · Time-Series Storytelling**

An analysis of India's labour market before and during COVID-19 (May 2019 – June 2020), tracing how national unemployment nearly **doubled from 9.5% to 17.5%** during the lockdown, and how that shock landed unevenly across states — with **Tamil Nadu spiking from ~4% to ~47%** — exposing structural inequality that existed long before the pandemic.

| | |
|---|---|
| **Dataset** | 740 monthly records · 28 states/UTs · Rural vs. Urban split |
| **Key techniques** | Data cleaning, datetime feature engineering, correlation analysis, time-series and distribution visualization |
| **Headline finding** | The April 2020 lockdown is a clear before/after boundary — national unemployment spiked to ~24% in a single month |
| **Stack** | pandas, numpy, matplotlib, seaborn |

📄 [Full write-up →](./Task_02_Unemployment_Analysis/README.md)

---

### 🚗 Task 03 — Car Price Prediction
**Focus: Regression · Feature Engineering · Model Benchmarking**

Predicts the resale price of used cars from specifications (brand, age, mileage, engine, fuel type, transmission) using the CarDekho listings dataset. Three regression models were trained and benchmarked on an identical held-out test set.

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Linear Regression | 167,381.03 | 297,516.25 | 0.5964 |
| Random Forest | 73,005.76 | 129,224.40 | 0.9239 |
| **Gradient Boosting ✅** | 81,382.75 | **125,421.10** | **0.9283** |

| | |
|---|---|
| **Dataset** | 8,129 raw listings → 6,927 cleaned records |
| **Key techniques** | `ColumnTransformer` preprocessing pipeline, median/most-frequent imputation, one-hot encoding, model comparison, feature importance analysis |
| **Result** | Gradient Boosting selected as final model — explains **~93% of price variance** on unseen data; ships as an inference-ready `.pkl` |
| **Stack** | pandas, numpy, scikit-learn, matplotlib, seaborn, joblib |

📄 [Full write-up →](./Task_03_Car_Price_Prediction/README.md)

---

### 📧 Task 04 — Email Spam Detection with Machine Learning
**Focus: Natural Language Processing · Text Classification**

Classifies SMS/email messages as spam or legitimate ("ham") using TF-IDF vectorization with Multinomial Naive Bayes and Logistic Regression, on the SMS Spam Collection dataset (5,169 unique messages after de-duplication, ~13% spam).

| Model | Accuracy | Precision (Spam) | Recall (Spam) | F1 (Spam) |
|---|---:|---:|---:|---:|
| **Multinomial Naive Bayes ✅** | 0.967 | 0.990 | 0.748 | **0.852** |
| Logistic Regression | 0.955 | 0.988 | 0.649 | 0.783 |

| | |
|---|---|
| **Key techniques** | Text normalization, NLTK stopword removal, TF-IDF (unigrams + bigrams) fit only on the training split to prevent leakage, stratified train/test split |
| **Result** | Naive Bayes selected on F1-score, with explicit attention to **recall** since a missed spam message is the costlier failure mode; vectorizer + model persisted together for inference |
| **Stack** | pandas, numpy, scikit-learn, NLTK, WordCloud, matplotlib, seaborn |

📄 [Full write-up →](./Task_04_Email_Spam_Detection/README.md)

---

## 🛠️ Tech Stack Across the Portfolio

`Python 3` · `pandas` · `NumPy` · `scikit-learn` · `NLTK` · `WordCloud` · `matplotlib` · `seaborn` · `Jupyter Notebook` · `joblib`

---

## ▶️ Running Any Project Locally

```bash
# 1. Clone the repository
git clone <repo-url>
cd OIBSIP/<Task_Folder_Name>

# 2. Install dependencies for that task
pip install -r requirements.txt

# 3. Launch the notebook(s)
jupyter notebook notebooks/
```

Each notebook is self-contained and will regenerate its cleaned dataset, charts, and (where applicable) trained model artifacts from the raw data on re-run.

---

## ✅ Guidelines Followed

- All work is original and submitted in compliance with the internship's plagiarism policy.
- Progress shared on LinkedIn as milestones were completed.
- Each project includes a dedicated README documenting objective, approach, findings, and conclusions.
- Submissions follow the required file naming convention: `Chaymae_Hanini_TaskNumber`.

## 🎓 Certification

Issued by **Oasis Infobyte** upon successful review of the submitted tasks.

---

<div align="center">

## 📬 Let's Connect

If this portfolio caught your interest, I'd love to talk data.

**Chaymae Hanini**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin&logoColor=white)]()
[![GitHub](https://img.shields.io/badge/GitHub-Profile-181717?style=flat-square&logo=github&logoColor=white)]()
[![Email](https://img.shields.io/badge/Email-Contact-D14836?style=flat-square&logo=gmail&logoColor=white)]()

⭐ *If you found this portfolio useful or interesting, consider giving the repository a star.*

</div>