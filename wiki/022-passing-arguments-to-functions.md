## 22. How do you pass arguments to a Python function?


### Passing Arguments to a Python Function

In Python, you can pass arguments to a function in several ways. These arguments allow you to provide input values that the function can use to perform its operations. Here's how you can pass arguments to a Python function:

1. **Positional Arguments**
   - Arguments are passed in the same order as the parameters are defined in the function.
   - **Example:**
     ```python
     def greet(name, message):
         print(f"{message}, {name}!")
     
     greet("Alice", "Hello")
     ```
   - **Output:**
     ```
     Hello, Alice!
     ```

2. **Keyword Arguments**
   - You can pass arguments using the parameter names. This allows you to pass arguments in any order.
   - **Example:**
     ```python
     def greet(name, message):
         print(f"{message}, {name}!")
     
     greet(message="Good morning", name="Bob")
     ```
   - **Output:**
     ```
     Good morning, Bob!
     ```

3. **Default Arguments**
   - You can define default values for function parameters. If an argument is not provided, the default value is used.
   - **Example:**
     ```python
     def greet(name, message="Hello"):
         print(f"{message}, {name}!")
     
     greet("Charlie")
     ```
   - **Output:**
     ```
     Hello, Charlie!
     ```

4. **Variable-Length Arguments**
   - **`*args` (Non-Keyword Arguments):**
     - Allows you to pass a variable number of positional arguments. The function receives these arguments as a tuple.
     - **Example:**
       ```python
       def add(*numbers):
           return sum(numbers)
       
       print(add(1, 2, 3))  # Output: 6
       print(add(10, 20))   # Output: 30
       ```

   - **`**kwargs` (Keyword Arguments):**
     - Allows you to pass a variable number of keyword arguments. The function receives these arguments as a dictionary.
     - **Example:**
       ```python
       def display_info(**kwargs):
           for key, value in kwargs.items():
               print(f"{key}: {value}")
       
       display_info(name="David", age=30, city="New York")
       ```
     - **Output:**
       ```
       name: David
       age: 30
       city: New York
       ```

5. **Combining Different Types of Arguments**
   - You can combine positional, keyword, default, and variable-length arguments in a single function. However, you must follow the correct order: positional arguments, followed by `*args`, then keyword arguments, followed by `**kwargs`.
   - **Example:**
     ```python
     def function_example(arg1, arg2, *args, kwarg1="default", **kwargs):
         print(f"arg1: {arg1}, arg2: {arg2}")
         print(f"args: {args}")
         print(f"kwarg1: {kwarg1}")
         print(f"kwargs: {kwargs}")
     
     function_example(1, 2, 3, 4, kwarg1="custom", kwarg2="extra")
     ```
   - **Output:**
     ```
     arg1: 1, arg2: 2
     args: (3, 4)
     kwarg1: custom
     kwargs: {'kwarg2': 'extra'}
     ```

### Summary
- Python functions can accept arguments in various forms, including positional, keyword, default, and variable-length arguments.
- Positional arguments must be in order, while keyword arguments can be passed in any order.
- Default arguments provide fallback values, and `*args` and `**kwargs` allow for flexible argument passing. Understanding how to use these types effectively enhances the versatility and readability of your functions.