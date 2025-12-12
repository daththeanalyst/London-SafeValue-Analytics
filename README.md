# 🏡 London Safe-Value Analytics (2024)

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![XGBoost](https://img.shields.io/badge/ML-XGBoost-green)
![Optuna](https://img.shields.io/badge/Tuning-Optuna-blueviolet)
![Status](https://img.shields.io/badge/Status-Completed-success)

### 📊 Is Safety Efficiently Priced in the London Housing Market?

**London-SafeValue-Analytics** is an individual data science project that merges **Geospatial Crime Data** with **Housing Transaction Records** to identify "Arbitrage Zones"—neighborhoods where high safety and low prices coexist.

Using a custom **Spatio-Temporal Join**, I processed over **800,000 crime records** and **25,000 housing transactions** from Jan–Sept 2024 to engineer a "Livability Opportunity Index."

---

## 🚀 Key Features

* **Spatio-Temporal Engineering:** Used `sklearn.BallTree` to map crime density within a 500m radius of each property, strictly matching the month of sale.
* **Crime Severity Index:** Moved beyond simple crime counts by weighting incidents based on severity (e.g., Violence = 10, Shoplifting = 2, Anti-social behaviour = 1).
* **Hyperparameter Optimization:** Utilized **Optuna** to automate the tuning of XGBoost hyperparameters (learning rate, max depth, subsample), maximizing model accuracy.
* **Advanced ML Pipeline:** Compared Linear Regression, Polynomial Regression, KNN, and Gradient Boosting.
    * **Winner:** XGBoost Regressor ($R^2 = 0.92$, MAE = £64k).
* **Opportunity Index:** A composite metric combining Normalised Price and Crime Severity using Log-MinMax transformation to identify "Hidden Gems".

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
    * **Spatio-Temporal Join:** Linked crimes to properties based on a 500m radius and specific month.
    * **Composite Scoring:** Created a "Weighted Severity Score" to quantify danger levels using official sentencing guidelines.
3.  **Hypothesis Testing:** Discovered that wealthy areas suffer disproportionately from theft, while affordable areas suffer more from violence and anti-social behaviour.
4.  **Modelling:** Trained an XGBoost model (tuned via **Optuna**) to predict house prices, finding that location, floor area, and local crime severity are the dominant drivers of value.

---

## 📈 Results & Performance

I ran a "Model Tournament" to select the best predictor. The XGBoost model, optimized with Optuna, significantly outperformed the baselines, explaining 92% of the variance in house prices.

| Model Strategy | $R^2$ Score | Mean Absolute Error (£) | Verdict |
| :--- | :--- | :--- | :--- |
| Linear Regression | 0.43 | £186,552 | ❌ Too Simple |
| Polynomial Regression | 0.62 | £170,755 | ⚠️ Captures some curves |
| KNN (Spatial) | 0.81 | £93,708 | ⚠️ Good local patterns |
| **XGBoost (Optuna Tuned)** | **0.92** | **£64,300** | ✅ **Selected** |

---

## 🛠️ How to Run This Project

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/YOUR_USERNAME/London-SafeValue-Analytics.git](https://github.com/YOUR_USERNAME/London-SafeValue-Analytics.git)
    ```
2.  **Install Requirements:**
    Ensure you have the necessary libraries. Run this in your terminal:
    ```bash
    pip install pandas numpy scikit-learn xgboost matplotlib seaborn folium plotly optuna
    ```
3.  **Run the Notebook:**
    Open `Final_File_Code.ipynb` in Jupyter Lab or Jupyter Notebook.
    * *Note:* The notebook automatically downloads and unzips the data from this repo if local files are not found.

---

## 👤 Author

* **Dimitrios Athinaios**
* *Individual Data Science Project*
