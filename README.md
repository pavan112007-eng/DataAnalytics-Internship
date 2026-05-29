# Task 1 - Data Cleaning and Preprocessing

## Internship
Data Analyst Internship

---

# Objective
The objective of this task was to clean and preprocess a raw dataset by handling missing values, removing duplicates, correcting inconsistent formats, and preparing the dataset for further analysis.

---

# Dataset Used
Amazon Product Dataset (`amazon.csv`)

The dataset contains:
- Product Name
- Category
- Discounted Price
- Actual Price
- Discount Percentage
- Ratings
- Rating Count
- Review Details

---

# Tools Used
- Python
- Pandas
- VS Code

---

# Steps Performed

## 1. Imported Required Libraries
Used Pandas library for data preprocessing.

## 2. Loaded Dataset
Loaded the CSV dataset using `pd.read_csv()`.

## 3. Explored Dataset
Checked:
- Dataset shape
- Column names
- Data types
- Null values

## 4. Handled Missing Values
Used:
- `fillna()`
- Mean/median replacement
- Default text replacement

## 5. Removed Duplicate Records
Removed duplicate rows using `drop_duplicates()`.

## 6. Renamed Column Names
Converted column headers into lowercase and underscore format.

## 7. Cleaned Currency Columns
Removed:
- ₹ symbol
- commas

Converted columns into numeric format.

## 8. Cleaned Percentage Column
Removed `%` symbol and converted values to numeric type.

## 9. Fixed Data Types
Converted:
- ratings
- prices
- rating count
- discount percentage

into proper numeric formats.

## 10. Standardized Text Data
- Removed extra spaces
- Converted text to lowercase

## 11. Removed Invalid Values
Filtered incorrect values such as ratings greater than 5.

## 12. Saved Cleaned Dataset
Exported final cleaned dataset as:

```text
amazon_cleaned.csv
