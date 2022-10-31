# Churn Prediction Portfolio
## About This File
The data set belongs to a leading online E-Commerce company. An online retail (E-commerce) company wants to know the customers who are going to churn, so accordingly they can approach customers to offer some promos.
<br/> source: https://www.kaggle.com/datasets/ankitverma2010/ecommerce-customer-churn-analysis-and-prediction
#### **Disclaimer: This project is still ongoing**
## Exploratory Data Analysis
#### Content
- Descriptive Analysis
- Univariate Analysis
- Multivariate Analysis
- Business Insight

### 1. Descriptive Statistics

- Columns with data types in the E-Commerce Dataset dataset are appropriate
- Some columns that have empty values include =
 `Tenure, WarehouseToHome, HourSpendOnApp,
 OrderAmountHikeFromlastYear, CouponUsed, OrderCount,
 DaySinceLastOrder`
- None of the columns have odd summary values (min/mean/median/max/unique/top/freq)

### 2. Univariate Analysis

- There are Outliers = `Tenure, WarehouseToHome, HoursSpend OnApp, NumberOfDeviceRegistered, NumberOfAddress, CouponUsed, OrderCount, DaySinceLastOrder, CashbackAmount`
- Skewed = Almost all skewed are positive
- For Target 'Churn' there is a class imbalance

### 3. Multivariate Analysis

A few things to note from the Heatmap:

- `OrderCount` - `CouponUsed` = 0.75 (High correlation is noteworthy)
- `Churn` - `Complain` = 0.25 (The higher the complaint the more likely it is to chum:
- `Churn` - `Tenure` = -0.35 (The lower the Tenure the more likely it is to Churn)

### 4. Business Insight

After doing the analysis above, some insights can be drawn

- Customers with low **Tenure** tend to have higher chance of **Churn**
- Customers who have done **Complain** are more likely to have a higher chance of **Churn**
- Customers with **single status** have the highest **churn** rate compared to other statuses

## Data Preprocessing
#### Content
- Data Cleansing
- Feature Engineering

### 1. Data Cleansing
- #### Handle missing values
In total there are 1,856 missing values, and there are also 1,856 rows with missing values, meaning every
missing values are in different rows, and no rows have more than one
missing value.
<br/> So if we drop all rows with missing values, we will discard 1856 rows or 32.97
percent of the dataset and will cause data loss, so the most appropriate treatment is
with imputation using the median value. This is done because most of the data
has a right-skewed distribution (positive)
- #### Handle Duplicate
For redundant values as below, merge values:
   - CC with Credit Card
   - COD with Cash on Delivery
   - Phone with Mobile Phone
<br/>
<br/>
- #### Handle outliers
    - Handling outliers is performed using the IQR and Z-Score methods on numerical features
    - The dataset is maintained under two conditions: with outliers and without outliers
- #### Feature transformation
Data transformation is carried out using Normalization, Standardization, and Logarithmic methods
- #### Feature encoding
    - able Encoding= `PereferedLoginDevice` and `Gender` . features
    - One hot Encoding=` PreferredPaymentMode`, `PreferedOrderCat`, `MaritalStatus`
- #### Handle class imbalance
Resampling process with Oversampling and SMOTE methods
### 2. Feature Engineering
- #### Feature Selection
    - The `CouponUsed` feature is not included in the feature used to model churn predictions because it is highly correlated with the `OrderCount` feature (redundant)
    - `CustomerID` is dropped because it is only an identifier
- #### Feature Extraction
    - `CashbackAmountPerOrder` = (CashbackAmount/OrderCount)
    - `CouponUsedPerOrder` = (CouponUsed/OrderCount)
- #### Additional Features
    1. Number of items in the cart/cart
    2. Payment Fee (credit card/bank transfer/etc)
    3. Shipping Cost
    4. Shipment_method
    
## Modeling
#### Content