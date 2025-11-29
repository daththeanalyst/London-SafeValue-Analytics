# 🏡 London Safe-Value Analytics (2024)

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![XGBoost](https://img.shields.io/badge/ML-XGBoost-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

### 📊 Is Safety Efficiently Priced in the London Housing Market?

**London-SafeValue-Analytics** is a data science project that merges **Geospatial Crime Data** with **Housing Transaction Records** to identify "Arbitrage Zones"—neighborhoods where high safety and low prices coexist.

Using a custom **Spatio-Temporal Join**, we processed over **800,000 crime records** and **25,000 housing transactions** from Jan–Sept 2024 to engineer a "Livability Opportunity Index."

---

## 🚀 Key Features

* **Spatio-Temporal Engineering:** Used `sklearn.BallTree` to map crime density within a 500m radius of each property, strictly matching the month of sale.
* **Crime Severity Index:** Moved beyond simple crime counts by weighting incidents based on severity (e.g., Violence = 10, Shoplifting = 1).
* **Advanced ML Pipeline:** Compared Linear Regression, KNN, and a Stacked Ensemble.
    * **Winner:** XGBoost Regressor ($R^2 = 0.87$, MAE = £77k).
* **Investment Scout Interface:** An interactive tool that recommends properties based on user budget and safety tolerance.

---

## 📂 The Data

The project utilizes two primary datasets, hosted in this repository via compression:

1.  **Housing Data:** [Kaggle Source](https://www.kaggle.com/datasets/jakewright/house-price-data/data) - Transactional data filtered to 2024.
2.  **Crime Data:** [Kaggle Source](https://www.kaggle.com/datasets/rahulladhani/london-street-level-crime-data-2024) - Street-level reporting data filtered to 2024.

*> **Note:** Data files are compressed (`.zip`) to comply with GitHub storage limits. The notebook handles extraction automatically.*

---

## 🧠 Methodology Overview

1.  **Data Cleaning:** Implemented smart imputation for missing room counts (using Median) and removed non-residential outliers (<£50k).
2.  **Feature Engineering:**
    * **Distance to Center:** Calculated Haversine distance to Charing Cross.
    * **Clustering:** Used K-Means to categorize neighborhoods into 4 archetypes (e.g., "Hidden Gems" vs "Wealth Targets").
3.  **Hypothesis Testing:** Discovered the **"Wealth Crime Paradox"**—rich areas suffer disproportionately from theft, while poor areas suffer from violence.
4.  **Modelling:** Trained an XGBoost model to predict house prices, finding that **Local Crime Score** is the 4th most important driver of value in London.

---

## 📈 Results & Performance

We ran a "Model Tournament" to select the best predictor:

| Model Strategy | $R^2$ Score | Mean Absolute Error (£) | Verdict |
| :--- | :--- | :--- | :--- |
| Linear Regression | 0.44 | £191,617 | ❌ Too Simple |
| KNN (Spatial) | 0.80 | £93,885 | ⚠️ Good, but localized |
| **XGBoost (Tuned)** | **0.87** | **£77,564** | ✅ **Selected** |

---

## 🛠️ How to Run This Project

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/YOUR_USERNAME/London-SafeValue-Analytics.git](https://github.com/YOUR_USERNAME/London-SafeValue-Analytics.git)
    ```
2.  **Install Requirements:**
    Ensure you have the necessary libraries. Run this in your terminal:
    ```bash
    pip install pandas numpy scikit-learn xgboost matplotlib seaborn folium plotly optuna ipywidgets
    ```
3.  **Run the Notebook:**
    Open `Coursework_Notebook.ipynb` in Jupyter Lab or Jupyter Notebook.
    * *Note:* The notebook automatically downloads and unzips the data from this repo using the "Cloud Load" section.

---

## 👥 Contributors

* **Dimitrios Athinaios**
* **Maria Tsakiri**
* **Simon Kolarik**

*University College London (UCL) - MSIN0143: Programming for Business Analytics*
