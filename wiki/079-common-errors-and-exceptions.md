## 79. What are the common errors and exceptions in Python?


Python has a rich set of built-in exceptions that are raised when errors occur during the execution of a program. Understanding these common errors and exceptions is essential for debugging and writing robust Python code. Here is an overview of some of the most common errors and exceptions in Python:

### 1. **SyntaxError**

**Occurs When:** There is a syntax mistake in the Python code, such as missing a colon, unmatched parentheses, or incorrect indentation.

**Example:**
```python
if True
    print("Hello")
```
- **Error Message:** `SyntaxError: invalid syntax`

### 2. **IndentationError**

**Occurs When:** The code is not indented correctly. Python requires consistent indentation to define code blocks.

**Example:**
```python
def my_function():
print("Hello")
```
- **Error Message:** `IndentationError: expected an indented block`

### 3. **TypeError**

**Occurs When:** An operation or function is applied to an object of inappropriate type. For example, trying to add a string to an integer.

**Example:**
```python
result = "Hello" + 5
```
- **Error Message:** `TypeError: can only concatenate str (not "int") to str`

### 4. **ValueError**

**Occurs When:** A function receives an argument of the right type but an inappropriate value. For example, converting a non-numeric string to an integer.

**Example:**
```python
number = int("abc")
```
- **Error Message:** `ValueError: invalid literal for int() with base 10: 'abc'`

### 5. **IndexError**

**Occurs When:** Trying to access an index that is out of range for a list, tuple, or string.

**Example:**
```python
my_list = [1, 2, 3]
print(my_list[5])
```
- **Error Message:** `IndexError: list index out of range`

### 6. **KeyError**

**Occurs When:** Attempting to access a dictionary key that does not exist.

**Example:**
```python
my_dict = {"name": "Alice", "age": 30}
print(my_dict["address"])
```
- **Error Message:** `KeyError: 'address'`

### 7. **AttributeError**

**Occurs When:** Trying to access an attribute that an object does not have.

**Example:**
```python
class MyClass:
    pass

obj = MyClass()
print(obj.some_attribute)
```
- **Error Message:** `AttributeError: 'MyClass' object has no attribute 'some_attribute'`

### 8. **NameError**

**Occurs When:** Referring to a variable or function that has not been defined.

**Example:**
```python
print(x)
```
- **Error Message:** `NameError: name 'x' is not defined`

### 9. **ZeroDivisionError**

**Occurs When:** Attempting to divide a number by zero.

**Example:**
```python
result = 10 / 0
```
- **Error Message:** `ZeroDivisionError: division by zero`

### 10. **ImportError / ModuleNotFoundError**

**Occurs When:** An import statement fails to find the module definition or when trying to import a module that doesn’t exist.

**Example:**
```python
import non_existent_module
```
- **Error Message:** `ModuleNotFoundError: No module named 'non_existent_module'`

### 11. **FileNotFoundError**

**Occurs When:** Attempting to open a file that does not exist.

**Example:**
```python
with open("non_existent_file.txt", "r") as file:
    content = file.read()
```
- **Error Message:** `FileNotFoundError: [Errno 2] No such file or directory: 'non_existent_file.txt'`

### 12. **OSError**

**Occurs When:** A system-related error occurs, such as failing to open a file or issues related to file permissions.

**Example:**
```python
import os
os.remove("non_existent_file.txt")
```
- **Error Message:** `FileNotFoundError: [Errno 2] No such file or directory: 'non_existent_file.txt'` (inherits from `OSError`)

### 13. **RuntimeError**

**Occurs When:** A general-purpose error raised when an error is detected that doesn’t fall into any of the other categories.

**Example:**
```python
def recursive_function():
    return recursive_function()

recursive_function()
```
- **Error Message:** `RecursionError: maximum recursion depth exceeded in comparison` (inherits from `RuntimeError`)

### 14. **StopIteration**

**Occurs When:** The `next()` function is called on an iterator that has no more items.

**Example:**
```python
my_iter = iter([1, 2, 3])
next(my_iter)
next(my_iter)
next(my_iter)
next(my_iter)
```
- **Error Message:** `StopIteration` (silently handled in `for` loops)

### 15. **MemoryError**

**Occurs When:** The program runs out of memory.

**Example:**
```python
a = 'a' * (10**10)
```
- **Error Message:** `MemoryError`

### Summary

Understanding these common Python exceptions helps you write more robust code and handle errors more gracefully. By using `try-except` blocks, you can catch these exceptions and take appropriate action, such as logging errors, retrying operations, or providing user-friendly error messages.