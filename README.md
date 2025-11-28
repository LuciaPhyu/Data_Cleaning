# Messy Excel Dataset Cleaning

## Data_Source:
https://www.kaggle.com/datasets/ahmedmohamed2003/cafe-sales-dirty-data-for-cleaning-training/data

## Description: 
This project is focus on cleaning excel messey dataset Cafe Sales. The goal was to make the data ready for analysis and reporting.

## Dataset Overview
- Columns: Transaction ID, Item, Quantity, Price Per Unit, Total Spent, Payment Method, Location, Transaction Date
- Shape: 10,001 rows × 8 columns
- Data Types:
    - Text / categorical columns: 4 (Transaction ID, Item, Payment Method, Location)
    - Numerical columns: 3 (Quantity, Price Per Unit, Total Spent)
    - Date column: 1 (Transaction Date)

## Data Cleaning Steps
### 1. Transaction ID
- Checked for duplicates and found no duplicates. No more action required.

### 2. Item
- Inserted a new column **`Cleaned_Item`** to fix invalid entries in the Item column.
- Formula:
  =IF(OR($B2="Unknown",$B2="Error",$B2=""),IFERROR(VLOOKUP($E2, UnitPrice_Lookup!$F$3:$G$10,2,FALSE),"N/A"),$B2)
- Logic:
  Replace invalid items with a lookup value based on Price Per Unit or "N/A" if not found; keeps valid items unchanged.

### 3. Price Per Unit
- Inserted a new column **`Cleaned Price Per Unit`** to handle invalid entries.
- Used the formula:
  =IF(Or($E2="ERROR",$E2="UNKNOWN",$E2=""),IFERROR(VLOOKUP($C2,UnitPrice_Lookup!$E$3:$F$10,2,0),IF(Or($D2="Error",$D2="UNKNOWN",$D2=""),0,G2/D2)),$E2)
- **Logic**:
  - Valid prices are left unchanged. Replaces invalid prices with the correct value from the lookup table based on Cleaned_Item.
  - If no lookup value is found, calculates price as Total Spent ÷ Quantity. 
  - Returns 0 when calculation is not possible.
  - **Manual corrections:** 2 rows that still had errors after applying the formula were manually filled zero to make sure all prices are valid for analysis.
