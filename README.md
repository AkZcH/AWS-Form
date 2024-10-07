Here’s a detailed section for your README file with Python commands for data cleaning. This will provide step-by-step instructions for users to follow and implement various cleaning techniques.

---

# Data Cleaning Commands in Python

In this repository, we use Python and **Pandas** to perform common data cleaning operations. Below are detailed explanations and Python code snippets for each cleaning technique, which you can apply to your dataset.

## 1. **Importing Necessary Libraries**
Before performing any data cleaning, we first need to import necessary libraries, mainly `pandas` and `numpy`.

```python
import pandas as pd
import numpy as np
```

---

## 2. **Loading the Dataset**
To begin with, load the dataset using `pandas`. Ensure that your dataset is properly formatted (e.g., CSV, Excel, etc.).

```python
df = pd.read_csv('path_to_your_dataset.csv')
```

---

## 3. **Handling Missing Values**

### a. **Identifying Missing Values**
Check for missing values in your dataset using the `isnull()` function combined with `sum()`.

```python
# Check for missing values
print(df.isnull().sum())
```

### b. **Dropping Rows with Missing Values**
To drop rows where any column contains missing data:

```python
# Drop rows with any NaN values
df = df.dropna()
```

To drop rows only if all columns contain NaN values:

```python
# Drop rows where all columns are NaN
df = df.dropna(how='all')
```

### c. **Imputing Missing Values**
Instead of dropping rows, you can fill missing values using the `fillna()` method.

```python
# Fill NaN values with a specific value (e.g., 0)
df = df.fillna(0)

# Fill NaN values with the mean of the column
df['column_name'] = df['column_name'].fillna(df['column_name'].mean())

# Fill NaN values with the median of the column
df['column_name'] = df['column_name'].fillna(df['column_name'].median())
```

---

## 4. **Handling Duplicates**

### a. **Identifying Duplicates**
To identify duplicate rows in your dataset:

```python
# Check for duplicate rows
duplicates = df.duplicated()
print(duplicates.sum())
```

### b. **Removing Duplicates**
To remove duplicate rows:

```python
# Drop duplicate rows
df = df.drop_duplicates()
```

---

## 5. **Data Type Conversion**

Sometimes the data type of certain columns might not be appropriate (e.g., numeric data stored as text). You can convert these columns to the correct type using the `astype()` function.

### a. **Converting to Numeric**
```python
df['column_name'] = pd.to_numeric(df['column_name'], errors='coerce')
```

### b. **Converting to DateTime**
```python
df['date_column'] = pd.to_datetime(df['date_column'], errors='coerce')
```

---

## 6. **Handling Outliers**

### a. **Identifying Outliers Using IQR**
Outliers can be identified using the **Interquartile Range (IQR)** method.

```python
Q1 = df['column_name'].quantile(0.25)
Q3 = df['column_name'].quantile(0.75)
IQR = Q3 - Q1

# Filter out rows with outliers
df = df[~((df['column_name'] < (Q1 - 1.5 * IQR)) | (df['column_name'] > (Q3 + 1.5 * IQR)))]
```

---

## 7. **Renaming Columns**
You can rename columns to more meaningful names using the `rename()` function.

```python
# Rename columns
df = df.rename(columns={'OldName': 'NewName'})
```

---

## 8. **Dropping Columns**

To drop unnecessary columns:

```python
# Drop specific columns
df = df.drop(['column1', 'column2'], axis=1)
```

---

## 9. **Removing Rows**

To remove specific rows by index or condition:

### a. **By Index**
```python
# Drop rows by index
df = df.drop([0, 1, 2])
```

### b. **By Condition**
```python
# Remove rows where a column value meets a condition
df = df[df['column_name'] != 'UnwantedValue']
```

---

## 10. **Data Transformation**

### a. **Creating New Columns**
You can generate new columns based on existing data:

```python
# Create a new column based on a condition
df['new_column'] = df['existing_column'].apply(lambda x: 'Yes' if x > 10 else 'No')
```

### b. **Applying Functions to Columns**
Apply custom functions to modify column data.

```python
# Applying a function to a column
df['column_name'] = df['column_name'].apply(lambda x: x ** 2)
```

---

## 11. **Standardizing Data**

### a. **Converting to Lower/Upper Case**
To standardize text columns, convert all text to lowercase or uppercase:

```python
# Convert text to lowercase
df['text_column'] = df['text_column'].str.lower()

# Convert text to uppercase
df['text_column'] = df['text_column'].str.upper()
```

### b. **Stripping Whitespace**
Remove leading or trailing spaces from text columns:

```python
# Strip spaces
df['text_column'] = df['text_column'].str.strip()
```

---

## 12. **Saving the Cleaned Dataset**
After all the cleaning operations, you can save the cleaned dataset to a new file.

```python
# Save to CSV
df.to_csv('cleaned_dataset.csv', index=False)

# Save to Excel
df.to_excel('cleaned_dataset.xlsx', index=False)
```

---

These are the basic and essential commands for data cleaning that you can apply to any dataset. The examples provided will help you handle common issues such as missing data, duplicates, and incorrect data types. You can also extend these commands based on your specific data requirements.

For more detailed examples, refer to the Jupyter notebooks and scripts included in this repository.

