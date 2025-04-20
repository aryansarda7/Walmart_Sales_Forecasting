# Walmart_Sales_Forecasting
# Walmart Sales Forecasting Project

## 📌 Project Overview
This project focuses on forecasting weekly sales for Walmart stores using historical sales data. The goal is to build predictive models that can accurately forecast sales, taking into account various factors such as holidays, store types, and economic indicators. The project involves data cleaning, exploratory data analysis (EDA), feature engineering, and the implementation of both machine learning and time series forecasting models.

---

## 📂 Dataset
The dataset consists of the following files:
- **stores.csv**: Contains information about 45 Walmart stores, including store type and size.
- **features.csv**: Includes additional features like temperature, fuel price, markdowns, CPI, and unemployment rate.
- **train.csv**: Historical sales data for each store and department from 2010-02-05 to 2012-10-26.

### Key Features:
- **Store**: Store number (1-45).
- **Dept**: Department number (1-99).
- **Date**: Week of sales.
- **Weekly_Sales**: Sales for the given store and department.
- **IsHoliday**: Whether the week contains a holiday.
- **Temperature, Fuel_Price, CPI, Unemployment**: External factors.
- **MarkDown1-5**: Anonymized markdown data.
- **Type**: Store type (A, B, C).
- **Size**: Store size in square feet.

---

## 🛠️ Data Preprocessing
1. **Merging Datasets**: Combined `stores.csv`, `features.csv`, and `train.csv` into a single DataFrame.
2. **Handling Missing Values**: Filled missing markdown values with 0.
3. **Removing Invalid Data**: Dropped rows with zero or negative sales (0.3% of the data).
4. **Feature Engineering**:
   - Extracted `week`, `month`, and `year` from the `Date` column.
   - Created binary features for specific holidays (Super Bowl, Labor Day, Thanksgiving, Christmas).
5. **Encoding Categorical Variables**: Converted store types (A, B, C) to numerical values (1, 2, 3).

---

## 📊 Exploratory Data Analysis (EDA)
### Key Insights:
1. **Holidays Impact**:
   - Thanksgiving has the highest sales due to Black Friday.
   - Christmas sales peak in the weeks leading up to the holiday.
   - Sales during holidays are generally higher than non-holidays.
2. **Store Types**:
   - Type A stores (largest) contribute to 51.2% of total stores and have the highest sales.
   - Type B and C stores follow in size and sales.
3. **Temporal Trends**:
   - Sales peak in November and December (holiday season).
   - The lowest sales occur in January.
4. **Department Analysis**:
   - Department 92 has the highest average sales.
   - Department 72 shows seasonal spikes during Thanksgiving.
5. **External Factors**:
   - CPI, temperature, unemployment rate, and fuel price show no clear correlation with sales.

---

## 🧠 Modeling Approaches
### 1. Random Forest Regressor
- **Features Used**: Store, Dept, IsHoliday, Fuel_Price, MarkDowns, Type, Size, week, month, year.
- **Preprocessing**: Scaled features using `RobustScaler`.
- **Results**:
  - Best WMAE (Weighted Mean Absolute Error): **2000.84** (with feature selection).
  - Feature Importance: Dept, Size, and Type were the most influential features.

### 2. Time Series Forecasting
#### Auto-ARIMA
- **Data Preparation**: Differenced the data to make it stationary.
- **Results**: The model captured trends but lacked accuracy in predictions.

#### Exponential Smoothing (Holt-Winters)
- **Parameters**: Additive trend and seasonality with a damping factor.
- **Results**:
  - Achieved the best WMAE: **840.68** (~5% error relative to average sales).
  - Effectively captured seasonal patterns and trends.

---

## 📈 Results Comparison
| Model                     | Description                          | WMAE     |
|---------------------------|--------------------------------------|----------|
| RandomForestRegressor     | Whole data with feature selection    | 2000.84  |
| ExponentialSmoothing      | Holt-Winters with damping            | 840.68   |

The **Exponential Smoothing** model outperformed the Random Forest for this time-series forecasting task, providing more accurate predictions with a lower error rate.

---

## 🚀 Key Takeaways
1. **Holidays Drive Sales**: Thanksgiving and Christmas weeks are critical for revenue.
2. **Store Type Matters**: Larger stores (Type A) consistently outperform smaller ones.
3. **Time Series Superiority**: Traditional forecasting methods (Exponential Smoothing) outperformed machine learning for this temporal dataset.
4. **Feature Importance**: Dept, Store Type, and Size are the most predictive features.

---

## 🛠️ Tools & Technologies
- **Languages**: Python
- **Libraries**: Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Statsmodels, pmdarima
- **Models**: RandomForestRegressor, ARIMA, ExponentialSmoothing
- **Data Visualization**: Matplotlib, Seaborn
