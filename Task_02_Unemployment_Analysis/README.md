# 📉 India Unemployment Analysis: The COVID-19 Shock

**An exploratory data analysis of India's labour market before and during the COVID-19 pandemic (May 2019 – June 2020), uncovering how a nationwide lockdown reshaped employment across states, sectors, and seasons.**

---

## 📖 The Story in One Paragraph

India entered 2020 with an unemployment rate hovering around **9–10%**, a figure already marked by wide regional inequality. Then, in a matter of weeks, that number nearly **doubled to 17.5%** as the country went into lockdown. This project traces that story through the data — from calm, pre-pandemic baselines, to an April 2020 shock that pushed states like **Tamil Nadu from ~4% to a staggering 47% unemployment**, to the beginning of a fragile recovery by year's end. Along the way, it asks a harder question: was this crisis felt equally everywhere, or did it expose fault lines that already existed between states, and between rural and urban India?

---

## 🎯 Objective

To clean, explore, and visualize India's unemployment data in order to answer three questions:

1. **Where** was unemployment structurally worse, independent of COVID-19?
2. **When** did the pandemic hit hardest, and how sharp was the shock?
3. **Who** was more exposed — rural or urban workers — and did labour participation actually protect people from unemployment?

---

## 🗂️ Dataset

| | |
|---|---|
| **Source file** | `data/Unemployment_in_India.csv` (raw) → `data/Unemployment_Cleaned.csv` (processed) |
| **Observations** | 740 monthly records |
| **Regions covered** | 28 Indian states/union territories |
| **Time span** | May 2019 – June 2020 |
| **Granularity** | Monthly, split by Rural and Urban areas |

**Key columns:**

| Column | Description |
|---|---|
| `Region` | Indian state or union territory |
| `Date` | Observation month (end-of-month) |
| `Estimated Unemployment Rate (%)` | Share of the labour force without work |
| `Estimated Employed` | Number of people employed |
| `Estimated Labour Participation Rate (%)` | Share of working-age population actively working or seeking work |
| `Area` | Rural or Urban |
| `Year`, `Month` | Engineered from `Date` for trend analysis |

---

## 🧹 Data Cleaning Pipeline

*Notebook: `notebooks/Chaymae_Hanini_Task2_Cleaning_Data.ipynb`*

The raw dataset arrived with the usual real-world mess: inconsistent spacing, stray blank rows, and dates stored as text. The cleaning process:

1. **Diagnosed the data** — inspected shape, dtypes, missing values, and duplicate rows.
2. **Dropped fully empty rows** that added no information.
3. **Stripped whitespace** from column names (e.g. `" Date"` → `"Date"`) to prevent silent key errors downstream.
4. **Parsed dates properly**, converting the `Date` column from string to `datetime` (day-first format).
5. **Engineered time features** — extracted `Year` and `Month` to enable seasonal and pre/post-pandemic comparisons.
6. **Exported a clean, analysis-ready file**: `data/Unemployment_Cleaned.csv`.

Result: a fully typed, duplicate-free, 740-row dataset with zero missing values.

---

## 📊 Exploratory Analysis & Key Findings

*Notebook: `notebooks/Chaymae_Hanini_Task2_EDA.ipynb`*

Each finding below is backed by a chart in the [`report/`](./report) folder.

### 1. Regional inequality was already severe — before COVID even hit
`report/01_region_average_unemployment.png` · `report/04_top10_states_unemployment.png`

Average unemployment across the full period ranged enormously by state. **Tripura (~26.5%) and Haryana (~25.5%)** sit at the top, followed by **Jharkhand and Bihar**, while **Karnataka, Gujarat, Uttarakhand, and Odisha** stayed as low as ~2.5%. This isn't a COVID story alone — it reflects structural differences in industrial base and agricultural employment between states.

### 2. April 2020 is the story's turning point
`report/02_monthly_unemployment_trend.png`

The monthly trend line is calm for most of the period (~9–10%) until it **spikes to ~24% in April 2020** — the month the nationwide lockdown took full effect. By October–December, the rate eases back toward 9–10%, tracing a **"V-shaped" recovery**.

### 3. The shock hit some states far harder than others
`report/03_unemployment_time_series.png`

Tracking Maharashtra, Delhi, and Tamil Nadu individually shows just how uneven the shock was:
- **Tamil Nadu**: ~4% → **~47%**
- **Delhi**: → **~20%**
- **Maharashtra**: → **~16%**

All three were relatively stable (1–6%) throughout 2019 — the pandemic is the only variable that explains this divergence.

### 4. Employment metrics don't move together the way you'd expect
`report/05_correlation_heatmap.png`

A correlation matrix between unemployment rate, number employed, and labour participation rate reveals **near-zero correlation** (coefficients close to 0.02) between these variables. In plain terms: a state having more active job-seekers doesn't mean more of them found work. Labour participation alone is not a predictor of employment outcomes.

### 5. The pandemic nearly doubled unemployment nationally
`report/06_pre_vs_post_covid.png`

Splitting the data at March 2020:
- **Pre-COVID average**: 9.5%
- **Post-COVID average**: 17.5%

That's an **~84% relative increase**, a direct, measurable fingerprint of the lockdown on the labour market.

### 6. Rural and urban workers were both hit — but differently
`report/07_urban_vs_rural.png`

A box plot comparison shows Rural and Urban areas share a similar median and spread, but **Rural areas show a wider range of outliers**, suggesting pockets of extreme, localized unemployment spikes in the countryside that the urban aggregate doesn't capture as dramatically.

---

## 🧾 Bottom Line

- Unemployment in India is not uniform — it's a patchwork shaped by state-level economic structure.
- COVID-19 didn't create inequality, but it dramatically **amplified** it, with the April 2020 lockdown standing out as a clear before/after boundary.
- Labour participation rate is **not** a reliable proxy for employment health — the two barely correlate.
- Both rural and urban India absorbed the shock, just through different distributions of pain.

---

## 📁 Project Structure

```
Task_02_Unemployment_Analysis/
├── data/
│   ├── Unemployment_in_India.csv       # Raw dataset
│   └── Unemployment_Cleaned.csv        # Cleaned, analysis-ready dataset
├── notebooks/
│   ├── Chaymae_Hanini_Task2_Cleaning_Data.ipynb   # Cleaning & feature engineering
│   └── Chaymae_Hanini_Task2_EDA.ipynb             # Exploratory analysis & visualizations
├── report/
│   ├── 01_region_average_unemployment.png
│   ├── 02_monthly_unemployment_trend.png
│   ├── 03_unemployment_time_series.png
│   ├── 04_top10_states_unemployment.png
│   ├── 05_correlation_heatmap.png
│   ├── 06_pre_vs_post_covid.png
│   └── 07_urban_vs_rural.png
├── requirements.txt
└── README.md
```

---

## 🛠️ Tech Stack

- **Python 3**
- **pandas** & **numpy** — data cleaning and manipulation
- **matplotlib** & **seaborn** — visualization
- **Jupyter Notebook** — analysis environment

---

## ▶️ How to Reproduce

```bash
# 1. Clone the repository
git clone <repo-url>
cd Task_02_Unemployment_Analysis

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the notebooks in order
jupyter notebook notebooks/Chaymae_Hanini_Task2_Cleaning_Data.ipynb
jupyter notebook notebooks/Chaymae_Hanini_Task2_EDA.ipynb
```

Running the cleaning notebook regenerates `data/Unemployment_Cleaned.csv`; running the EDA notebook regenerates all charts in `report/`.

---

## ✍️ Author

**Chaymae Hanini**
