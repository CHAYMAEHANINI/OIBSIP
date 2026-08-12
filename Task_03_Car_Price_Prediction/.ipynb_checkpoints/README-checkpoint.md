# 🚗 Car Price Prediction

Predicting the resale (selling) price of used cars from their technical specifications and market attributes, using the [CarDekho](https://www.cardekho.com/) used-car listings dataset. The project covers the full workflow — data cleaning, exploratory data analysis, feature engineering, model training, and evaluation — and ships three trained regression models ready for inference.

**Best model: Gradient Boosting Regressor — R² = 0.928, RMSE ≈ 125,421**

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Workflow](#-workflow)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Modeling & Results](#-modeling--results)
- [Feature Importance](#-feature-importance)
- [Installation](#-installation)
- [Usage](#-usage)
- [Tech Stack](#-tech-stack)
- [Author](#-author)

---

## 🔍 Overview

Used-car pricing depends on a mix of factors — brand, age, mileage, engine specs, fuel type, and transmission — that don't always relate to price in a simple, linear way. This project builds and compares regression models that learn these relationships directly from historical listing data, so a fair selling price can be estimated for a car given its specifications.

**Pipeline:**

```
Raw data (cardekho.csv)
        │
        ▼
Data Cleaning  →  cardekho_Cleaned.csv
        │
        ▼
Exploratory Data Analysis (EDA)
        │
        ▼
Feature Engineering + Preprocessing (impute, encode)
        │
        ▼
Model Training (Linear Regression / Random Forest / Gradient Boosting)
        │
        ▼
Evaluation + Model Selection  →  models/*.pkl
```

## 📊 Dataset

The dataset contains used-car listings scraped from CarDekho, with **8,129 raw records** reduced to **6,927 clean records** after deduplication and missing-value handling.

| Column | Description |
|---|---|
| `name` | Full listing name of the car |
| `brand` | Car manufacturer, extracted from `name` |
| `year` | Year of manufacture |
| `car_age` | Engineered feature — car age relative to dataset year (2020) |
| `selling_price` | **Target variable** — resale price |
| `km_driven` | Total kilometers driven |
| `fuel` | Fuel type (Petrol, Diesel, CNG, LPG) |
| `seller_type` | Individual, Dealer, or Trustmark Dealer |
| `transmission` | Manual or Automatic |
| `owner` | Ownership history (First Owner, Second Owner, ...) |
| `mileage(km/ltr/kg)` | Fuel efficiency |
| `engine` | Engine displacement (CC) |
| `max_power` | Maximum power output (bhp) |
| `seats` | Number of seats |

## 📁 Project Structure

```
Task_03_Car_Price_Prediction/
├── data/
│   ├── cardekho.csv                # Raw dataset
│   └── cardekho_Cleaned.csv        # Cleaned dataset used for modeling
├── notebooks/
│   ├── Chaymae_Hanini_Task3_Data_Cleaning.ipynb
│   ├── Chaymae_Hanini_Task3_EDA.ipynb
│   └── Chaymae_Hanini_Task3_Modeling.ipynb
├── models/
│   ├── linear_regression.pkl
│   ├── random_forest.pkl
│   └── gradient_boosting.pkl
├── report/                         # Exported charts (see below)
├── requirements.txt
└── README.md
```

## ⚙️ Workflow

**1. Data Cleaning** (`Chaymae_Hanini_Task3_Data_Cleaning.ipynb`)
- Removed duplicate records
- Converted `max_power` from text to numeric
- Imputed missing values in `mileage`, `max_power`, and other numeric columns using the median
- Engineered `car_age` from the listing year
- Extracted `brand` from the car `name`

**2. Exploratory Data Analysis** (`Chaymae_Hanini_Task3_EDA.ipynb`)
- Analyzed the distribution and spread of the target variable
- Studied price relationships with fuel type, transmission, brand, and age
- Investigated correlations between numerical features

**3. Modeling** (`Chaymae_Hanini_Task3_Modeling.ipynb`)
- Built a `ColumnTransformer` preprocessing pipeline (median imputation for numeric features, most-frequent imputation + one-hot encoding for categorical features)
- Split data into 80% train / 20% test (`random_state=42`)
- Trained and evaluated three regressors: Linear Regression, Random Forest, Gradient Boosting
- Compared performance using MAE, RMSE, and R²
- Persisted all trained models with `joblib`

## 📈 Exploratory Data Analysis

<table>
<tr>
<td width="50%">

**Selling price distribution**
<img src="report/01_Selling_price_distribution_Histogram.png" width="100%">

</td>
<td width="50%">

**Selling price — outliers**
<img src="report/02_Selling_price_distribution_Boxplot.png" width="100%">

</td>
</tr>
<tr>
<td width="50%">

**Price vs. fuel type**
<img src="report/04_Selling_Price_VS_Fuel_Type_Boxplot.png" width="100%">

</td>
<td width="50%">

**Price vs. car age**
<img src="report/05_Selling_Price_vs_Car_Age.png" width="100%">

</td>
</tr>
<tr>
<td width="50%">

**Top 10 brands by listing count**
<img src="report/06_Top_10_Car_Brands_by_Number_of_Listings.png" width="100%">

</td>
<td width="50%">

**Top 10 brands by average price**
<img src="report/07_Top_10_Brands_by_Average_Selling_Price.png" width="100%">

</td>
</tr>
</table>

**Correlation between numerical features**

<img src="report/08_Correlation_Heatmap_of_Numerical_Features.png" width="70%">

Key takeaways:
- Selling price is **right-skewed**, with most cars priced in the lower range and a long tail of premium listings.
- **Diesel** cars and **automatic transmissions** tend to command higher prices.
- Price **decreases with car age** — newer cars retain significantly more value.
- **Maruti and Hyundai** dominate the market by volume, while luxury brands lead in average price.
- `max_power` and `engine` show the strongest correlation with `selling_price` among numerical features.

## 🤖 Modeling & Results

Three regression models were trained on the same preprocessed features and evaluated on a held-out 20% test set:

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Linear Regression | 167,381.03 | 297,516.25 | 0.5964 |
| Random Forest | **73,005.76** | 129,224.40 | 0.9239 |
| **Gradient Boosting** ✅ | 81,382.75 | **125,421.10** | **0.9283** |

**Gradient Boosting** was selected as the final model. It achieves the lowest RMSE and the highest R², explaining roughly **93% of the variance** in selling price on unseen data. Random Forest achieved a slightly lower MAE, but Gradient Boosting generalizes better overall in terms of error magnitude and explained variance. Linear Regression underperforms both tree-based models, confirming that the relationship between car specifications and price is not well captured by a linear model.

<img src="report/09_Actual_vs_Predicted_Gradient_Boosting.png" width="70%">

*Predicted vs. actual selling price for the Gradient Boosting model — points cluster tightly around the diagonal, with slightly higher variance on high-value cars.*

## 🏆 Feature Importance

<img src="report/010_Top_15_Most_Important_Features_Gradient_Boosting.png" width="70%">

The Gradient Boosting model relies most heavily on **maximum power**, **engine size**, **car age**, and **brand**, aligning with the correlation patterns observed during EDA.

## 🛠 Installation

```bash
# Clone the repository
git clone <repo-url>
cd Task_03_Car_Price_Prediction

# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

## ▶️ Usage

**Reproduce the pipeline** by running the notebooks in order:

```bash
jupyter notebook notebooks/Chaymae_Hanini_Task3_Data_Cleaning.ipynb
jupyter notebook notebooks/Chaymae_Hanini_Task3_EDA.ipynb
jupyter notebook notebooks/Chaymae_Hanini_Task3_Modeling.ipynb
```

**Load a trained model for inference:**

```python
import joblib
import pandas as pd

model = joblib.load("models/gradient_boosting.pkl")

sample = pd.DataFrame([{
    "car_age": 6,
    "km_driven": 145500,
    "mileage(km/ltr/kg)": 23.4,
    "engine": 1248.0,
    "max_power": 74.0,
    "seats": 5.0,
    "brand": "Maruti",
    "fuel": "Diesel",
    "seller_type": "Individual",
    "transmission": "Manual",
    "owner": "First Owner"
}])

predicted_price = model.predict(sample)
print(f"Estimated selling price: {predicted_price[0]:,.2f}")
```

## 🧰 Tech Stack

- **Python** — pandas, NumPy
- **Scikit-learn** — pipelines, preprocessing, regression models, metrics
- **Matplotlib / Seaborn** — data visualization
- **Joblib** — model persistence
- **Jupyter Notebook** — analysis and experimentation

## ✍️ Author

**Chaymae Hanini**

---

⭐ If you found this project useful, consider giving it a star!