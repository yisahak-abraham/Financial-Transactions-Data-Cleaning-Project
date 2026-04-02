# Financial-Transactions-Data-Cleaning-Project
This project focuses on cleaning a messy financial transactions dataset downloaded from Kaggle. The goal is to prepare a reliable and consistent dataset suitable for analysis or further processing. This project does not include dashboarding or visualization — it is strictly data cleaning.
1. Project Overview

The dataset contains financial transaction records with the following columns:

Transaction_ID – Unique ID for each transaction
Transaction_Date – Date of transaction (some invalid dates like Feb 30)
Customer_ID – Unique ID per customer
Product_Name – Name of product sold
Quantity – Number of items sold (some negative or unrealistic)
Price – Price per unit (some negative, missing, or unrealistic)
Payment_Method – Payment type (e.g., Credit Card, PayPal)
Transaction_Status – Status of transaction (Pending, Completed, Failed)
2. Data Quality Challenges

During exploration, the dataset had several issues:

Missing values
Price (~33% missing)
Quantity, Transaction_ID, Transaction_Date (~5% missing)
Invalid Dates
Nonexistent dates like 2025-02-30
Negative or unrealistic values
Negative quantity or price
Extremely large quantities (e.g., 669 headphones)
Extremely low prices for large quantities
Inconsistent categorical values
Payment methods: PayPal, pay pal, PayPal
Transaction status: completed, Completed, complete
Index gaps
Cleaning removed rows → indices were non-continuous
3. Cleaning Steps Performed

Column Standardization

Lowercased and replaced spaces with underscores
df.columns = df.columns.str.lower().str.strip().str.replace(" ", "_")
Handling Missing Values
Dropped rows with missing Transaction_ID, Customer_ID, Price, or Quantity
Filled missing Transaction_Status with "unknown"
Date Cleaning
Converted Transaction_Date to datetime
Invalid dates (Feb 30) converted to NaT and removed
Quantity and Price Cleaning
Converted to numeric
Negative values converted to positive
Removed outliers using thresholds:
Quantity: 1–100 (global), Price: 1–1000
Optionally, thresholds can be product-specific
Categorical Normalization
Standardized payment_method and transaction_status
Example: "pay pal" → "PayPal", "complete" → "Completed"
Outlier Handling
Flagged unrealistic rows (is_outlier)
Removed or retained based on thresholds
Index Reset
After cleaning, index reset to continuous 0…N

Total Amount Calculation (optional)

df_clean['total_amount'] = df_clean['quantity'] * df_clean['price']
4. Results
Original rows: 53,790
Cleaned rows: 15,872
Missing values reduced to almost zero
Outliers removed for realistic business context
Dataset ready for analysis or dashboarding
