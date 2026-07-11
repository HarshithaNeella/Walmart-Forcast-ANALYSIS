# Walmart Store Sales Forecasting

## Project Overview

This project focuses on forecasting weekly sales for Walmart stores using Machine Learning techniques. The objective was to develop an end-to-end demand forecasting pipeline capable of predicting future sales based on historical sales records, promotional activities, economic indicators, store characteristics, and seasonal trends.

Accurate sales forecasting enables retailers to optimize inventory management, promotional planning, staffing decisions, and overall business operations.

---

## Business Problem

Retail sales are influenced by multiple factors, including:

- Store characteristics
- Department-level demand
- Promotional markdown campaigns
- Economic conditions
- Fuel prices
- Seasonal trends
- Holiday periods

The goal of this project is to build a predictive model that can accurately forecast weekly sales by leveraging historical sales data and external business factors.

---

## Dataset Information

The project utilizes three datasets:

### 1. train.csv
Contains historical weekly sales records.

**Columns:**
- Store
- Dept
- Date
- Weekly_Sales
- IsHoliday

### 2. features.csv
Contains external economic and promotional variables.

**Columns:**
- Temperature
- Fuel_Price
- CPI
- Unemployment
- MarkDown1
- MarkDown2
- MarkDown3
- MarkDown4
- MarkDown5
- IsHoliday

### 3. stores.csv
Contains store-level information.

**Columns:**
- Store
- Type
- Size

---

## Project Workflow

### Step 1: Data Integration

Merged the three datasets using:

- Store
- Date
- IsHoliday

to create a unified dataset containing both sales information and external business factors.

---

### Step 2: Data Understanding

Performed exploratory analysis using:

- Dataset shape
- Data types
- Summary statistics
- Missing value analysis

#### Key Findings

- Dataset contains **421,570 records**
- No missing values after preprocessing
- Weekly sales exhibit a highly skewed distribution
- Promotional variables contain significant outliers
- Store sizes vary substantially across locations

---

### Step 3: Data Preprocessing

#### Missing Value Treatment

- Missing values in MarkDown variables were replaced with 0
- Numerical variables were cleaned and validated

#### Categorical Encoding

Store Type was transformed using One-Hot Encoding:

- Type_B
- Type_C

#### Date Processing

Date column was converted into datetime format for feature extraction.

---

### Step 4: Feature Engineering

The following temporal features were created:

- Year
- Month
- Week
- Quarter
- Month_End

### Why Feature Engineering?

Raw dates are difficult for machine learning models to interpret directly.

The engineered features help capture:

- Seasonal trends
- Monthly patterns
- Weekly demand cycles
- Quarter-end behavior
- Month-end purchasing activity

---

### Step 5: Exploratory Data Analysis

Several visualizations were created to understand the data.

#### Weekly Sales Distribution

Key Observation:

- Sales are highly right-skewed
- Extreme sales spikes exist during specific periods

#### Outlier Analysis

Boxplots revealed significant outliers in:

- Weekly_Sales
- MarkDown1
- MarkDown2
- MarkDown3
- MarkDown4
- MarkDown5

These outliers were retained because they represent real business events such as promotions and holiday sales.

#### Correlation Analysis

A correlation heatmap was used to analyze relationships between numerical variables.

---

## Machine Learning Models

### Model 1: Linear Regression

Linear Regression was used as a baseline model to establish a performance benchmark.

#### Results

| Metric | Score |
|----------|----------|
| MAE | 11,908 |
| RMSE | 18,527 |
| R² | 0.052 |

#### Observation

Linear Regression performed poorly, indicating that the sales forecasting problem contains complex non-linear relationships.

---

### Model 2: Random Forest Regressor

Random Forest was implemented to capture non-linear interactions among variables.

Hyperparameter tuning was performed using RandomizedSearchCV.

---

### Model 3: XGBoost Regressor

XGBoost was selected as the primary forecasting model because of its ability to capture complex patterns and interactions among features.

#### Hyperparameter Tuning

RandomizedSearchCV was used to optimize:

- n_estimators
- max_depth
- learning_rate
- min_child_weight
- colsample_bytree

#### Best Parameters

```python
{
    'n_estimators': 700,
    'max_depth': 4,
    'learning_rate': 0.05,
    'min_child_weight': 5,
    'colsample_bytree': 0.9
}
```

---

## Final Model Performance

### XGBoost Results

| Metric | Score |
|----------|----------|
| MAE | 5,587 |
| RMSE | 10,009 |
| R² | 0.723 |

### Performance Improvement

Compared to Linear Regression:

- MAE reduced significantly
- RMSE reduced significantly
- R² improved from 0.052 to 0.723

This demonstrates the effectiveness of gradient boosting for retail demand forecasting.

---

## Feature Importance Analysis

The most influential features identified by XGBoost were:

1. Dept
2. Type_B
3. Size
4. Store
5. CPI
6. Week
7. MarkDown3
8. Unemployment
9. Month
10. Type_C

### Business Interpretation

- Department strongly influences sales patterns
- Larger stores generate higher sales volumes
- Economic indicators impact customer spending
- Promotional campaigns significantly affect demand
- Seasonal effects contribute to sales variation

---

## Technologies Used

### Programming Language

- Python

### Libraries

- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn
- XGBoost

---

## Key Learnings

Through this project, I gained practical experience in:

- Data Integration
- Data Preprocessing
- Exploratory Data Analysis
- Feature Engineering
- Demand Forecasting
- Machine Learning Pipelines
- Hyperparameter Optimization
- Model Evaluation
- Feature Importance Analysis
- Business Interpretation of Machine Learning Models

---

## Conclusion

An end-to-end demand forecasting solution was developed using Walmart historical sales data and external business factors.

After evaluating multiple machine learning approaches, XGBoost achieved the best predictive performance with an R² score of 0.723 and was selected as the final forecasting model.

The project demonstrates how machine learning can effectively forecast retail demand by combining historical sales data with promotional, economic, and seasonal information.
