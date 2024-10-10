## How do you work with data frames using `pandas`?


`pandas` is a powerful and flexible data analysis and manipulation library for Python. The core data structure in `pandas` is the `DataFrame`, which is essentially a table of data with labeled rows and columns. It is designed to handle and manipulate large datasets with ease. Here’s how you can work with `DataFrames` using `pandas`.

### 1. **Creating a DataFrame**

You can create a `DataFrame` from various data structures like lists, dictionaries, or even from files such as CSVs and Excel spreadsheets.

#### **From a Dictionary:**
```python
import pandas as pd

data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Los Angeles', 'Chicago']
}

df = pd.DataFrame(data)
print(df)
```

- **Output:**
  ```
      Name  Age         City
  0  Alice   25     New York
  1    Bob   30  Los Angeles
  2 Charlie   35     Chicago
  ```

#### **From a List of Dictionaries:**
```python
data = [
    {'Name': 'Alice', 'Age': 25, 'City': 'New York'},
    {'Name': 'Bob', 'Age': 30, 'City': 'Los Angeles'},
    {'Name': 'Charlie', 'Age': 35, 'City': 'Chicago'}
]

df = pd.DataFrame(data)
print(df)
```

### 2. **Reading Data from a File**

`pandas` provides functions to read data from various file formats, including CSV, Excel, JSON, and SQL databases.

#### **From a CSV File:**
```python
df = pd.read_csv('data.csv')
print(df.head())  # Display the first 5 rows
```

#### **From an Excel File:**
```python
df = pd.read_excel('data.xlsx')
print(df.head())
```

### 3. **Exploring and Summarizing Data**

Once you have a `DataFrame`, you can explore and summarize your data.

#### **Viewing Data:**
- **First few rows:**
  ```python
  print(df.head())  # First 5 rows
  print(df.head(10))  # First 10 rows
  ```
- **Last few rows:**
  ```python
  print(df.tail())  # Last 5 rows
  ```
- **Get the shape of the DataFrame (rows, columns):**
  ```python
  print(df.shape)
  ```

#### **Summary Statistics:**
- **Summary of numerical columns:**
  ```python
  print(df.describe())
  ```
- **Summary of all columns (including non-numerical):**
  ```python
  print(df.info())
  ```

### 4. **Selecting Data**

You can select specific columns, rows, or a combination of both.

#### **Selecting Columns:**
```python
# Single column as a Series
print(df['Name'])

# Multiple columns as a DataFrame
print(df[['Name', 'City']])
```

#### **Selecting Rows by Index:**
```python
# Single row by index
print(df.iloc[0])

# Multiple rows by index
print(df.iloc[0:2])
```

#### **Selecting Rows by Condition:**
```python
# Rows where Age is greater than 30
print(df[df['Age'] > 30])
```

### 5. **Adding and Modifying Data**

You can add new columns or modify existing ones.

#### **Adding a New Column:**
```python
df['Salary'] = [50000, 60000, 70000]
print(df)
```

#### **Modifying an Existing Column:**
```python
df['Age'] = df['Age'] + 1  # Increment age by 1
print(df)
```

### 6. **Handling Missing Data**

Missing data is common in real-world datasets. `pandas` provides tools to handle them.

#### **Checking for Missing Data:**
```python
print(df.isnull().sum())  # Count of missing values in each column
```

#### **Filling Missing Data:**
```python
df['Age'].fillna(df['Age'].mean(), inplace=True)  # Fill missing Age with the mean
```

#### **Dropping Missing Data:**
```python
df.dropna(inplace=True)  # Drop rows with any missing values
```

### 7. **Grouping and Aggregating Data**

You can group data by one or more columns and apply aggregation functions like sum, mean, count, etc.

#### **Group by a Column:**
```python
grouped = df.groupby('City').mean()
print(grouped)
```

#### **Multiple Aggregations:**
```python
grouped = df.groupby('City').agg({'Age': 'mean', 'Salary': 'sum'})
print(grouped)
```

### 8. **Sorting Data**

You can sort the data by one or more columns.

#### **Sort by a Single Column:**
```python
sorted_df = df.sort_values('Age')
print(sorted_df)
```

#### **Sort by Multiple Columns:**
```python
sorted_df = df.sort_values(['City', 'Age'], ascending=[True, False])
print(sorted_df)
```

### 9. **Merging and Joining DataFrames**

You can merge or join DataFrames similarly to SQL joins.

#### **Merging on a Key Column:**
```python
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Name': ['Alice', 'Bob', 'Charlie']})
df2 = pd.DataFrame({'ID': [1, 2, 4], 'Age': [25, 30, 40]})

merged_df = pd.merge(df1, df2, on='ID')
print(merged_df)
```

### 10. **Saving Data to a File**

You can save the modified `DataFrame` back to a file.

#### **Save to CSV:**
```python
df.to_csv('output.csv', index=False)
```

#### **Save to Excel:**
```python
df.to_excel('output.xlsx', index=False)
```

### Summary

- **Creating a DataFrame:** You can create `DataFrames` from dictionaries, lists, or files.
- **Exploring Data:** Use `head()`, `info()`, and `describe()` to get an overview of the data.
- **Selecting Data:** Use column names, `iloc[]`, and conditions to select specific data.
- **Modifying Data:** Add new columns, modify existing data, and handle missing data.
- **Grouping and Aggregating:** Use `groupby()` and `agg()` to summarize data.
- **Sorting Data:** Sort the `DataFrame` by one or more columns.
- **Merging DataFrames:** Combine multiple `DataFrames` using `merge()`.

`pandas` is an incredibly versatile tool that makes data manipulation and analysis easy and efficient, enabling you to handle complex datasets with minimal code.