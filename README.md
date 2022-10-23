# Churn Prediction Portfolio
## About This File
The data set belongs to a leading online E-Commerce company. An online retail (E commerce) company wants to know the customers who are going to churn, so accordingly they can approach customer to offer some promos.
<br/> source: https://www.kaggle.com/datasets/ankitverma2010/ecommerce-customer-churn-analysis-and-prediction
<br/> **Disclaimer: This project is still an on going project**
## Exploratory Data Analysis
#### Content
- Descriptive Analysis
- Univariate Analysis
- Multivariate Analysis
- Business Insight

### 1. Descriptive Statistics

- Kolom dengan tipe data pada dataset E Commerce Dataset sudah sesuai
- Beberapa kolom yang memiliki nilai kosong antara lain =
 `Tenure, WarehouseToHome, HourSpendOnApp,
 OrderAmountHikeFromlastYear, CouponUsed, OrderCount,
 DaySinceLastOrder`
- Tidak ada kolom yang memiliki nilai summary (min/mean/median/max/unique/top/freq) aneh

### 2. Univariate Analysis

- Terdapat Outliers = `Tenure, WarehouseToHome, HoursSpend OnApp, NumberOfDeviceRegistered, NumberOfAddress, CouponUsed, OrderCount, DaySinceLastOrder, CashbackAmount`
- Skewed = Hampir semua skewed positif
- Untuk Target `Churn` terdapat class imbalance

### 3. Multivariate Analysis

Beberapa hal dapat diperhatikan dari Heatmap:

- `OrderCount` - `CouponUsed` = 0.75 (Korelasi tinggi perlu diperhatikan)
- `Churn` - `Complain` = 0.25 (Semakin tinggi complain semakin besar kemungkinan chum:
- `Churn` - `Tenure` = -0.35 (Semekin rendah Tenure semakin besar kemungkinan untuk Churn)

### 4. Business Insight

Setelah melakukan analisis diatas dapat ditarik beberapa insight

- Customer dengan **Tenure** rendah memiki kecendeningan untuk **Churn** lebih tinggi
- Customer yang pernah melakukan **Complain** lebih banyak memiliki kecenderungan untuk **Churn** lebih tinggi
- Customer dengan **status single** memiliki tingkat **churn** paling tinggi dibandingkan status lainnya

## Data Preprocessing
#### Content
- Data Cleansing
- Feature Engineering

### 1. Data Cleansing
- #### Handle missing values
Total ada 1.856 missing values, dan juga ada 1.856 rows dengan missing values, artinya setiap
missing values berada pada row yang berbeda, dan tidak ada rows yang memiliki lebih dari satu
missing values.
<br/> Jadi jika kita drop semua rows dengan missing values, kita akan membuang 1856 rows atau 32,97
persen dari dataset dan akan menyebabkan data loss, sehingga treatment yang paling tepat adalah
dengan imputation menggunakan nilai median. Hal ini dilakukan karena sebagian besar data
memiliki distribusi skewed kanan (positif)
- #### Handle Duplicate
Untuk value yang redundan seperti di bawah ini dilakukan merge value:
   - CC dengan Credit Card
   - COD dengan Cash on Delivery
   - Phone dengan Mobile Phone
<br/>
<br/>
- #### Handle outliers
    - Handlig outliers dilakukan dengan metode IQR dan Z-Score pada fitur yang berjenis numerical
    - Dataset dimaintain pada dua kondisi: dengan outlier dan tanpa outlier
- #### Feature transformation
Transformassi data dilakukan dengann metoder Normalisasi, Standarisasi, dan Logaritmik
- #### Feature encoding
    - abel Encoding=Fitur `PereferedLoginDevice` dan `Gender`
    - One hot Encoding=` PreferredPaymentMode`, `PreferedOrderCat`, `MaritalStatus`
- #### Handle class imbalance
Proses resampling dengan metode Oversampling dan SMOTE
### 2. Feature Engineering
- #### Feature Selection
    - Fitur `CouponUsed` tidak dimasukkan ke dalam fitur yang dipakai untuk memodelkan prediksi churn karena berkorelasi tinggi dengan fitur `OrderCount` (redundant)
    - `CustomerID` di drop karena hanya merupakan identifier
- #### Feature Extraction
    - `CashbackAmountPerOrder` = (CashbackAmount/OrderCount)
    - `CouponUsedPerOrder` = (CouponUsed/OrderCount)
- #### Fitur Tambahan
    1. Jumlah items di keranjang/cart
    2. Payment Fee (credit card/bank transfer/etc)
    3. Shipping Cost
    4. Shipment_method
    
## Modeling
#### Content

