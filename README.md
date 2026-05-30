# solar-prediction
## 📌Overview of Solar Energy Prediction
To maintain an optimal grid balance, accurate predictions of solar power production at one hour intervals is essential. In this study, we aim to develop a comprehensive machine learning pipeline for energy prediction on hourly weather datasets using 7 models by performing effective feature engineering through atmospheric physics insights.

## 📊Dataset

| Property | Details |
| :--- | :--- |
| Size	| 7,536 hourly records |
| Features | Cloud coverage, Temperature, Dew point, Humidity, Wind speed, Station pressure, Altimeter, Visibility, Hour |
| Target | Solar energy — continuous (Wh/m²)|
| Task	| Regression |

## ⚙️Methodology
### 1. Data Cleaning
-> Removed 4 irrelevant columns: (Inverter), Date, Random, Unnamed: 13\
-> Imputed missing values with median (preferred method due to significant skewness in pressure variables)\
-> Fixed bug: Original notebook incorrectly applied conversion to Celsius of already Celsius data, leading to an average temperature of −8.65°C. Fixed with a simple renaming of the column.\
-> Cleansed negative wind speed values via abs() (sensor issue)

### 2. Exploratory Data Analysis (7 Layers)
-> Distribution of feature data and skewness\
-> IQR detection of outliers — Visibility: 1,692 outliers (22%); entirely real physical occurrences of fog/haze\
-> Analysis of correlation between atmospheric feature data and solar production\
-> Visualization of relationship between feature and target values via scatterplots\
-> Distribution of solar production by hour of day\
-> Multivariate and bivariate analysis\

### 3. Outlier Treatment Strategy
| Feature | Skewness | Treatment | Reason |
| :--- | :--- | :--- | :--- |
| Visibility | -2.8 | Log transform (`log1p`) | Real fog events; scale compression |
| Altimeter | -9.0 | Log transform (`log1p`) | Severe skew |
| Station pressure | -5.4 | Winsorization (1-99%) | Preserve all rows, cap extremes |

4. Feature Engineering
-> Generated 6 engineered features motivated by physics from atmospheric variables.

5. Modelling & Evaluation
-> Metrics used to evaluate model: MAE, RMSE, R²\
-> Result: Ensemble models proved superior to individual regressor models.

## 🛠️ Tech Stack
-> Language: Python 3.8+\
-> ML: scikit-learn (ensemble methods, base regressors)\
-> Data: pandas, NumPy\
-> Visualisation: matplotlib, seaborn\
-> Preprocessing: StandardScaler, MinMaxScaler, log transform, winsorization

## 🔑 Skills:
-> Physics-based feature extraction from data specific to machine learning\
-> Outlier management strategy with analysis of skewness (log transformation against winsorization)\
-> Multiple model evaluation workflow using ensemble techniques
-> Data cleaning process using real data (bug hunting and unit tests)
