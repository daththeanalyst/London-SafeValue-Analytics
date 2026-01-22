# London Safe-Value Analytics (2024)

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![XGBoost](https://img.shields.io/badge/ML-XGBoost-green)
![Optuna](https://img.shields.io/badge/Tuning-Optuna-blueviolet)
![Status](https://img.shields.io/badge/Status-Completed-success)

### Project Overview
**London-SafeValue-Analytics** is a data science initiative that merges geospatial crime data with housing transaction records to analyze market efficiency. The primary objective is to identify "Arbitrage Zones"—geographic areas where high safety standards coexist with lower property valuations.

By implementing a custom spatio-temporal join, the project processed over **800,000 crime records** and **25,000 housing transactions** (January–September 2024) to engineer a composite "Livability Opportunity Index."

---

## Key Technical Features

* **Spatio-Temporal Data Integration:** Utilized `sklearn.BallTree` to map crime density within a 500-meter radius of each property. The algorithm enforces strict temporal matching to ensure crime data corresponds directly to the month of the property sale.
* **Weighted Crime Severity Index:** Developed a sophisticated scoring system rather than utilizing raw incident counts. Incidents were weighted based on severity (e.g., Violence = 10, Shoplifting = 2, Anti-social behaviour = 1) to provide a more accurate representation of local safety.
* **Hyperparameter Optimization:** Implemented **Optuna** to automate the tuning of XGBoost hyperparameters (learning rate, max depth, subsample), resulting in maximized model accuracy.
* **Machine Learning Pipeline:** Conducted a comparative analysis of Linear Regression, Polynomial Regression, K-Nearest Neighbors (KNN), and Gradient Boosting algorithms.
    * **Result:** The XGBoost Regressor achieved the highest predictive performance ($R^2 = 0.92$, MAE = £64,000).
* **Composite Metric Development:** Created an index combining Normalized Price and Crime Severity using Log-MinMax transformations to systematically highlight undervalued, high-safety neighborhoods.

---

## Data Sources

The project utilizes two primary datasets, hosted in this repository via compression:

1.  **Housing Data:** [Kaggle Source](https://www.kaggle.com/datasets/jakewright/house-price-data/data) - Transactional data filtered to the 2024 reporting period.
2.  **Crime Data:** [Kaggle Source](https://www.kaggle.com/datasets/rahulladhani/london-street-level-crime-data-2024) - Street-level reporting data filtered to the 2024 reporting period.

> **Note:** Due to GitHub storage limitations, data files are compressed (`.zip`). The provided notebook includes logic to extract these files automatically.

---

## Methodology

### 1. Data Preprocessing
The pipeline implements median-based imputation for missing room counts and removes non-residential outliers (properties priced under £50k) to ensure data integrity.

### 2. Feature Engineering
* **Spatio-Temporal Join:** Linked crime statistics to properties based on spatial proximity (500m) and temporal alignment (transaction month).
* **Scoring:** Calculated a "Weighted Severity Score" to quantify safety levels based on official sentencing guidelines.

### 3. Hypothesis Testing & Analysis
Analysis indicated distinct correlations between socioeconomic status and crime types; specifically, wealthy areas suffer disproportionately from theft, while affordable areas correlate more strongly with violence and anti-social behavior.

### 4. Predictive Modeling
An XGBoost model was trained and tuned to predict house prices. Feature importance analysis confirmed that location, floor area, and local crime severity are the primary determinants of property value.

---

## Model Evaluation

A comparative analysis was conducted to select the optimal predictive model. The XGBoost model, optimized via Optuna, demonstrated superior performance in explaining price variance.

| Model Strategy | $R^2$ Score | Mean Absolute Error (£) | Assessment |
| :--- | :--- | :--- | :--- |
| Linear Regression | 0.43 | £186,552 | High bias; underfitting |
| Polynomial Regression | 0.62 | £170,755 | Moderate improvement; non-linear capture |
| KNN (Spatial) | 0.81 | £93,708 | Strong local spatial performance |
| **XGBoost (Optuna Tuned)** | **0.92** | **£64,300** | **Optimal performance** |

---

## Installation and Usage

To reproduce the analysis locally:

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/YOUR_USERNAME/London-SafeValue-Analytics.git](https://github.com/YOUR_USERNAME/London-SafeValue-Analytics.git)
    ```

2.  **Install Dependencies:**
    Ensure the required Python libraries are installed:
    ```bash
    pip install pandas numpy scikit-learn xgboost matplotlib seaborn folium plotly optuna
    ```

3.  **Execute the Analysis:**
    Open `Final_File_Code.ipynb` in Jupyter Lab or Jupyter Notebook.
    * *Note:* The notebook automatically downloads and unzips the data from this repo if local files are not found.

---

## Author

* **Dimitrios Athinaios**
