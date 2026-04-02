# Financial-Transactions-Data-Cleaning-Project
This project focuses on cleaning a messy financial transactions dataset downloaded from Kaggle. The goal is to prepare a reliable and consistent dataset suitable for analysis or further processing. This project does not include dashboarding or visualization — it is strictly data cleaning.
# Financial Transactions Data Cleaning Project

## Project Overview
This project focuses on **cleaning a messy financial transactions dataset** downloaded from Kaggle. The goal is to prepare a **reliable and consistent dataset** suitable for analysis or further processing. This project does **not include dashboarding or visualization** — it is strictly data cleaning.

The dataset contains the following columns:

- `Transaction_ID` – Unique ID for each transaction  
- `Transaction_Date` – Date of transaction (some invalid dates like Feb 30)  
- `Customer_ID` – Unique ID per customer  
- `Product_Name` – Name of product sold  
- `Quantity` – Number of items sold (some negative or unrealistic)  
- `Price` – Price per unit (some negative, missing, or unrealistic)  
- `Payment_Method` – Payment type (e.g., Credit Card, PayPal)  
- `Transaction_Status` – Status of transaction (Pending, Completed, Failed)  

---

## Data Quality Challenges
During exploration, the dataset had several issues:

1. **Missing values**  
   - `Price` (~33% missing)  
   - `Quantity`, `Transaction_ID`, `Transaction_Date` (~5% missing)  

2. **Invalid Dates**  
   - Nonexistent dates like `2025-02-30`  

3. **Negative or unrealistic values**  
   - Negative quantity or price  
   - Extremely large quantities (e.g., 669 headphones)  
   - Extremely low prices for large quantities  

4. **Inconsistent categorical values**  
   - Payment methods: `PayPal`, `pay pal`, `PayPal `  
   - Transaction status: `completed`, `Completed`, `complete`  

5. **Index gaps**  
   - Cleaning removed rows → indices were non-continuous  

---

## Cleaning Steps Performed

1. **Column Standardization**  
   - Lowercased and replaced spaces with underscores:  
   ```python
   df.columns = df.columns.str.lower().str.strip().str.replace(" ", "_")
## Data Cleaning Steps

### 2. Handling Missing Values
- Dropped rows with missing `Transaction_ID`, `Customer_ID`, `Price`, or `Quantity`  
- Filled missing `Transaction_Status` with `"unknown"`  

```python
# Example
df.dropna(subset=['transaction_id','customer_id','price','quantity'], inplace=True)
df['transaction_status'].fillna('unknown', inplace=True)
## Data Cleaning Steps


