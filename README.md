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
- Checked for duplicates

### 2. Item
- Inserted a new column **`Cleaned_Item`** to fix invalid entries in the Item column.
- Formula:
  =IF(OR($B2="Unknown",$B2="Error",$B2=""),IFERROR(VLOOKUP($E2, UnitPrice_Lookup!$F$3:$G$10,2,FALSE),"N/A"),$B2)
- Logic:
  To replace invalid items with a lookup value based on Price Per Unit or "N/A" if not found; keeps valid items unchanged.

### 3. Quantity
- Inserted a new column Price_Cleaned to handle invalid entries.
- Used the formula:
  =IF(OR(E3="ERROR", E3="UNKNOWN", E3=""), VLOOKUP(C3, UnitPrice_Lookup!$E$3:$F$10, 2, 0), E3)
- **Logic**:
  If the original price is "ERROR", "UNKNOWN", or blank, the formula automatically looks up the correct unit price from a reference table based on the item. Otherwise, it keeps the original value.
