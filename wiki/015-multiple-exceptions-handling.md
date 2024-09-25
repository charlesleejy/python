## 15. How can you handle multiple exceptions in a single block?


### Handling Multiple Exceptions in a Single Block

1. **Using a Tuple to Handle Multiple Exceptions**
   - You can catch multiple exceptions in a single `except` block by specifying the exception types as a tuple.
   - **Syntax:**
     ```python
     try:
         # Code that might raise multiple exceptions
     except (ExceptionType1, ExceptionType2, ExceptionType3) as e:
         # Code to handle the exceptions
         print(f"An error occurred: {e}")
     ```
   - **Example:**
     ```python
     try:
         num = int("abc")
     except (ValueError, TypeError) as e:
         print(f"An error occurred: {e}")
     ```
   - **Explanation:** In this example, both `ValueError` and `TypeError` are caught by the single `except` block.

   - **Output:**
     ```
     An error occurred: invalid literal for int() with base 10: 'abc'
     ```

2. **Catching All Exceptions (Using `Exception`)**
   - You can catch all exceptions using the `Exception` class, which is the base class for most built-in exceptions.
   - **Syntax:**
     ```python
     try:
         # Code that might raise multiple exceptions
     except Exception as e:
         # Code to handle any exception
         print(f"An unexpected error occurred: {e}")
     ```
   - **Example:**
     ```python
     try:
         result = 10 / 0
     except Exception as e:
         print(f"An error occurred: {e}")
     ```
   - **Output:**
     ```
     An error occurred: division by zero
     ```

3. **Chaining Multiple `except` Blocks**
   - Although not a single block, you can use multiple `except` blocks to handle different exceptions separately, with specific actions for each.
   - **Syntax:**
     ```python
     try:
         # Code that might raise multiple exceptions
     except ValueError:
         # Handle ValueError
     except TypeError:
         # Handle TypeError
     except ZeroDivisionError:
         # Handle ZeroDivisionError
     ```

4. **Why Use a Tuple for Multiple Exceptions?**
   - Using a tuple to handle multiple exceptions in a single block simplifies the code when you want to handle different types of exceptions in the same way.
   - This reduces redundancy and makes the code cleaner.

### Summary
- You can handle multiple exceptions in a single `except` block by listing the exception types as a tuple.
- This approach is useful when you want to apply the same handling logic to different exceptions, reducing the need for multiple `except` blocks.