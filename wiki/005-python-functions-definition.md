## 5. What are Python functions, and how do you define them?


### Python Functions and How to Define Them

1. **What are Python Functions?**
   - **Reusable Code Blocks:** Functions in Python are blocks of organized, reusable code that perform a specific task.
   - **Modularity:** Functions help break down large programs into smaller, manageable, and modular pieces.
   - **Encapsulation:** Functions encapsulate code logic, which makes code easier to understand, maintain, and debug.
   - **DRY Principle:** Functions help adhere to the "Don't Repeat Yourself" (DRY) principle by avoiding code duplication.

2. **Defining a Python Function**
   - **Syntax:**
     - Functions are defined using the `def` keyword, followed by the function name, parentheses `()`, and a colon `:`.
     - The function body, which contains the code to be executed, is indented.

   - **Basic Structure:**
     ```python
     def function_name(parameters):
         """Docstring (optional): Describes the function's purpose."""
         # Function body
         return value  # (optional) Return statement
     ```

3. **Parameters and Arguments**
   - **Parameters:** Variables listed inside the parentheses in the function definition. They act as placeholders for the values (arguments) passed to the function.
     - Example: In `def add(a, b):`, `a` and `b` are parameters.
   - **Arguments:** The actual values passed to the function when it is called.
     - Example: In `add(5, 3)`, `5` and `3` are arguments.

4. **Return Statement**
   - **Purpose:** The `return` statement is used to exit a function and pass a value back to the caller.
   - **Optional:** If a function does not have a `return` statement, it returns `None` by default.
   - Example:
     ```python
     def add(a, b):
         return a + b
     ```

5. **Docstrings**
   - **Purpose:** A docstring is an optional, triple-quoted string that describes what the function does.
   - **Best Practice:** It is a good practice to include a docstring to improve code readability and documentation.
   - Example:
     ```python
     def greet(name):
         """This function greets the person whose name is passed as a parameter."""
         print(f"Hello, {name}!")
     ```

6. **Calling a Function**
   - **Syntax:** To execute a function, you call it by its name followed by parentheses. If the function requires arguments, pass them inside the parentheses.
   - Example:
     ```python
     result = add(5, 3)  # Calls the add function with arguments 5 and 3
     ```

7. **Types of Functions**
   - **Built-in Functions:** Python provides several built-in functions like `print()`, `len()`, `sum()`, etc.
   - **User-defined Functions:** These are functions that developers create to perform specific tasks.
   - **Lambda Functions:** Anonymous, small functions defined using the `lambda` keyword.

8. **Default Parameters**
   - **Definition:** You can define default values for parameters, which are used if no argument is passed.
   - Example:
     ```python
     def greet(name="Guest"):
         print(f"Hello, {name}!")
     ```

9. **Variable-Length Arguments**
   - **`*args`:** Used to pass a variable number of non-keyword arguments to a function.
   - **`**kwargs`:** Used to pass a variable number of keyword arguments to a function.
   - Example:
     ```python
     def display(*args, **kwargs):
         print(args)
         print(kwargs)
     ```

### Summary
- Python functions are essential for writing modular, reusable, and maintainable code.
- They are defined using the `def` keyword, can take parameters, and may return a value using the `return` statement.
- Understanding how to define and use functions effectively is crucial for writing efficient Python programs.