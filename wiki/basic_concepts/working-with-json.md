## How do you work with JSON data in Python?


In Python, you can work with JSON data using the built-in `json` module. JSON (JavaScript Object Notation) is a lightweight data interchange format that is easy to read and write for both humans and machines. The `json` module allows you to convert between JSON data and Python dictionaries (or other data structures) seamlessly.

### Key Operations with JSON in Python

1. **Loading JSON from a String**
2. **Loading JSON from a File**
3. **Dumping (Writing) JSON to a String**
4. **Dumping (Writing) JSON to a File**

### 1. **Loading JSON Data**

#### **Loading JSON from a String**

You can use `json.loads()` to parse a JSON string and convert it into a Python dictionary.

**Example:**
```python
import json

json_string = '{"name": "John", "age": 30, "city": "New York"}'
data = json.loads(json_string)
print(data)
# Output: {'name': 'John', 'age': 30, 'city': 'New York'}
```

- **Explanation:** `json.loads(json_string)` parses the JSON string and converts it into a Python dictionary.

#### **Loading JSON from a File**

You can use `json.load()` to read JSON data from a file and convert it into a Python dictionary.

**Example:**
```python
import json

with open('data.json', 'r') as file:
    data = json.load(file)
    print(data)
```

- **Explanation:** `json.load(file)` reads the JSON data from the file and converts it into a Python dictionary.

### 2. **Dumping JSON Data**

#### **Dumping JSON to a String**

You can use `json.dumps()` to convert a Python dictionary (or other data structures) into a JSON string.

**Example:**
```python
import json

data = {"name": "John", "age": 30, "city": "New York"}
json_string = json.dumps(data)
print(json_string)
# Output: {"name": "John", "age": 30, "city": "New York"}
```

- **Explanation:** `json.dumps(data)` converts the Python dictionary into a JSON-formatted string.

**Formatting Options:**
- **Pretty Printing:** You can make the JSON string more readable by using the `indent` parameter.
  ```python
  json_string = json.dumps(data, indent=4)
  print(json_string)
  ```
- **Sorting Keys:** You can sort the keys alphabetically using `sort_keys=True`.
  ```python
  json_string = json.dumps(data, sort_keys=True)
  print(json_string)
  ```

#### **Dumping JSON to a File**

You can use `json.dump()` to write JSON data to a file from a Python dictionary.

**Example:**
```python
import json

data = {"name": "John", "age": 30, "city": "New York"}

with open('data.json', 'w') as file:
    json.dump(data, file, indent=4)
```

- **Explanation:** `json.dump(data, file, indent=4)` writes the dictionary to a file in JSON format, with indentation for readability.

### 3. **Working with JSON Arrays**

JSON arrays correspond to Python lists. You can load and manipulate them in the same way.

**Example:**
```python
import json

json_string = '[{"name": "John"}, {"name": "Anna"}, {"name": "Peter"}]'
data = json.loads(json_string)
print(data)
# Output: [{'name': 'John'}, {'name': 'Anna'}, {'name': 'Peter'}]
```

### 4. **Handling Complex Data Types**

When working with custom Python objects, you may need to provide a custom serialization method, as `json` does not handle non-standard types like Python classes out of the box.

**Example:**
```python
import json
from datetime import datetime

class Employee:
    def __init__(self, name, hire_date):
        self.name = name
        self.hire_date = hire_date

def custom_serializer(obj):
    if isinstance(obj, datetime):
        return obj.isoformat()
    if isinstance(obj, Employee):
        return {"name": obj.name, "hire_date": obj.hire_date.isoformat()}
    raise TypeError(f"Type {type(obj)} not serializable")

employee = Employee("John Doe", datetime.now())
json_string = json.dumps(employee, default=custom_serializer, indent=4)
print(json_string)
```

- **Explanation:** The `custom_serializer` function handles the serialization of `datetime` and `Employee` objects.

### Summary

- **Loading JSON Data:**
  - **`json.loads()`**: Parse JSON from a string.
  - **`json.load()`**: Parse JSON from a file.

- **Dumping JSON Data:**
  - **`json.dumps()`**: Convert Python data structures to a JSON string.
  - **`json.dump()`**: Write Python data structures to a file in JSON format.

- **Formatting Options:**
  - Use `indent` for pretty printing and `sort_keys` for sorting the keys.

- **Handling Complex Data Types:**
  - Use the `default` parameter in `json.dumps()` to handle non-standard types with a custom serialization function.

The `json` module in Python provides a simple and efficient way to work with JSON data, making it easy to integrate Python with web services, APIs, and other systems that use JSON for data interchange.