## What are Python’s built-in data serialization formats?


### Python’s Built-in Data Serialization Formats

Data serialization is the process of converting an object or data structure into a format that can be easily stored, transmitted, and later reconstructed. Python provides several built-in modules for data serialization and deserialization. The most commonly used formats are JSON, pickle, and CSV.

### 1. **JSON (JavaScript Object Notation)**

- **Purpose:** JSON is a lightweight, text-based format for serializing and deserializing structured data. It is commonly used for data interchange between systems, especially in web applications.
- **Supported Data Types:** JSON supports basic data types like strings, numbers, lists, dictionaries, booleans, and `None`.
- **Module:** `json`

- **Serialization (Converting Python objects to JSON):**
  - **Function:** `json.dumps()` converts a Python object into a JSON string.
  - **Example:**
    ```python
    import json

    data = {"name": "John", "age": 30, "city": "New York"}
    json_string = json.dumps(data)
    print(json_string)  # Output: {"name": "John", "age": 30, "city": "New York"}
    ```

- **Deserialization (Converting JSON to Python objects):**
  - **Function:** `json.loads()` converts a JSON string back into a Python object.
  - **Example:**
    ```python
    python_obj = json.loads(json_string)
    print(python_obj)  # Output: {'name': 'John', 'age': 30, 'city': 'New York'}
    ```

- **File Operations:**
  - **Writing to a File:** `json.dump()`
  - **Reading from a File:** `json.load()`

  ```python
  # Writing to a file
  with open("data.json", "w") as file:
      json.dump(data, file)

  # Reading from a file
  with open("data.json", "r") as file:
      data = json.load(file)
  ```

### 2. **Pickle**

- **Purpose:** Pickle is a Python-specific binary serialization format that can serialize and deserialize almost any Python object, including custom classes, functions, and complex data structures. However, it is Python-specific and not human-readable or cross-platform.
- **Module:** `pickle`

- **Serialization (Pickling):**
  - **Function:** `pickle.dumps()` converts a Python object into a byte stream.
  - **Example:**
    ```python
    import pickle

    data = {"name": "John", "age": 30, "city": "New York"}
    pickled_data = pickle.dumps(data)
    print(pickled_data)
    ```

- **Deserialization (Unpickling):**
  - **Function:** `pickle.loads()` converts a byte stream back into a Python object.
  - **Example:**
    ```python
    original_data = pickle.loads(pickled_data)
    print(original_data)  # Output: {'name': 'John', 'age': 30, 'city': 'New York'}
    ```

- **File Operations:**
  - **Writing to a File:** `pickle.dump()`
  - **Reading from a File:** `pickle.load()`

  ```python
  # Writing to a file
  with open("data.pkl", "wb") as file:
      pickle.dump(data, file)

  # Reading from a file
  with open("data.pkl", "rb") as file:
      data = pickle.load(file)
  ```

- **Caution:** Pickle should not be used with untrusted data as it is not secure against malicious code execution.

### 3. **CSV (Comma-Separated Values)**

- **Purpose:** CSV is a simple, text-based format used for tabular data. It is commonly used for exporting and importing data from spreadsheets and databases.
- **Module:** `csv`

- **Serialization (Writing to CSV):**
  - **Function:** `csv.writer()` writes data to a CSV file.
  - **Example:**
    ```python
    import csv

    data = [
        ["Name", "Age", "City"],
        ["John", 30, "New York"],
        ["Anna", 25, "Los Angeles"],
        ["Mike", 35, "Chicago"]
    ]

    with open("data.csv", "w", newline="") as file:
        writer = csv.writer(file)
        writer.writerows(data)
    ```

- **Deserialization (Reading from CSV):**
  - **Function:** `csv.reader()` reads data from a CSV file.
  - **Example:**
    ```python
    with open("data.csv", "r") as file:
        reader = csv.reader(file)
        for row in reader:
            print(row)
    ```

- **Handling CSV with Dictionaries:**
  - **Writing:** `csv.DictWriter()`
  - **Reading:** `csv.DictReader()`

  ```python
  with open("data.csv", "w", newline="") as file:
      fieldnames = ["Name", "Age", "City"]
      writer = csv.DictWriter(file, fieldnames=fieldnames)
      writer.writeheader()
      writer.writerow({"Name": "John", "Age": 30, "City": "New York"})
  ```

### Summary

- **JSON:** Best for interoperable and human-readable data serialization across different platforms and languages.
- **Pickle:** Best for Python-specific serialization of complex objects but should be used with caution due to security risks.
- **CSV:** Ideal for simple tabular data and is widely supported by various tools, including spreadsheet software.

These built-in formats cover a wide range of use cases, making it easy to serialize and deserialize data in Python.