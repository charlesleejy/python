## How does Python handle exceptions?


### How Python Handles Exceptions

1. **What are Exceptions?**
   - **Definition:** Exceptions are errors that occur during the execution of a program. When an exception occurs, the normal flow of the program is interrupted, and Python raises an error.
   - **Common Exceptions:** Examples include `ZeroDivisionError`, `TypeError`, `ValueError`, `IndexError`, and `KeyError`.

2. **Handling Exceptions with `try-except` Blocks**
   - **Basic Structure:**
     - Use `try` to wrap the code that might raise an exception.
     - Use `except` to catch and handle the exception.
   - **Syntax:**
     ```python
     try:
         # Code that might raise an exception
     except ExceptionType:
         # Code to handle the exception
     ```
   - **Example:**
     ```python
     try:
         result = 10 / 0
     except ZeroDivisionError:
         print("You cannot divide by zero!")
     ```
   - **Output:**
     ```
     You cannot divide by zero!
     ```

3. **Catching Multiple Exceptions**
   - **Handling Multiple Exceptions:**
     - You can handle multiple exceptions by specifying multiple `except` blocks.
   - **Syntax:**
     ```python
     try:
         # Code that might raise multiple exceptions
     except (TypeError, ValueError) as e:
         print(f"An error occurred: {e}")
     ```
   - **Example:**
     ```python
     try:
         num = int("abc")
     except (ValueError, TypeError) as e:
         print(f"An error occurred: {e}")
     ```
   - **Output:**
     ```
     An error occurred: invalid literal for int() with base 10: 'abc'
     ```

4. **Using `else` with `try-except`**
   - **Purpose:** The `else` block is executed if no exceptions are raised in the `try` block.
   - **Syntax:**
     ```python
     try:
         # Code that might raise an exception
     except ExceptionType:
         # Code to handle the exception
     else:
         # Code to execute if no exception occurs
     ```
   - **Example:**
     ```python
     try:
         result = 10 / 2
     except ZeroDivisionError:
         print("You cannot divide by zero!")
     else:
         print("Division successful:", result)
     ```
   - **Output:**
     ```
     Division successful: 5.0
     ```

5. **Using `finally` Block**
   - **Purpose:** The `finally` block is executed no matter what, whether an exception occurs or not. It’s often used for cleanup actions (e.g., closing a file or releasing resources).
   - **Syntax:**
     ```python
     try:
         # Code that might raise an exception
     except ExceptionType:
         # Code to handle the exception
     finally:
         # Code that runs regardless of whether an exception occurs
     ```
   - **Example:**
     ```python
     try:
         file = open("test.txt", "r")
         # Code to read the file
     except FileNotFoundError:
         print("File not found.")
     finally:
         print("Closing file.")
         file.close()
     ```
   - **Output:**
     ```
     File not found.
     Closing file.
     ```

6. **Raising Exceptions Manually**
   - **Purpose:** You can manually raise an exception using the `raise` keyword.
   - **Syntax:**
     ```python
     raise ExceptionType("Error message")
     ```
   - **Example:**
     ```python
     def divide(a, b):
         if b == 0:
             raise ValueError("Denominator cannot be zero.")
         return a / b
     ```

7. **Custom Exceptions**
   - **Purpose:** You can define your own exception classes by inheriting from the built-in `Exception` class.
   - **Example:**
     ```python
     class CustomError(Exception):
         pass

     try:
         raise CustomError("This is a custom error")
     except CustomError as e:
         print(e)
     ```

### Summary
- Python handles exceptions using `try-except` blocks, allowing the program to catch and handle errors gracefully.
- The `else` block runs if no exceptions are raised, and the `finally` block runs regardless of whether an exception occurred.
- You can manually raise exceptions and create custom exception classes for more specific error handling.