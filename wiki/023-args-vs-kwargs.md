## 23. What is the difference between *args and **kwargs?


### Difference Between `*args` and `**kwargs` in Python

1. **Purpose**
   - **`*args`:** 
     - Used to pass a variable number of non-keyword (positional) arguments to a function.
     - It allows the function to accept any number of positional arguments, which are then accessible as a tuple.
   - **`**kwargs`:**
     - Used to pass a variable number of keyword arguments to a function.
     - It allows the function to accept any number of keyword arguments, which are then accessible as a dictionary.

2. **Syntax**
   - **`*args`:**
     - Placed before a parameter name to capture all additional positional arguments.
     - Example:
       ```python
       def func(*args):
           print(args)
       
       func(1, 2, 3)
       ```
     - **Output:**
       ```
       (1, 2, 3)
       ```
   - **`**kwargs`:**
     - Placed before a parameter name to capture all additional keyword arguments.
     - Example:
       ```python
       def func(**kwargs):
           print(kwargs)
       
       func(a=1, b=2, c=3)
       ```
     - **Output:**
       ```
       {'a': 1, 'b': 2, 'c': 3}
       ```

3. **Usage**
   - **`*args`:**
     - Used when you want to pass a variable number of positional arguments to a function. The arguments are received as a tuple.
     - Example:
       ```python
       def add(*numbers):
           return sum(numbers)
       
       print(add(1, 2, 3))  # Output: 6
       ```
   - **`**kwargs`:**
     - Used when you want to pass a variable number of keyword arguments to a function. The arguments are received as a dictionary.
     - Example:
       ```python
       def display_info(**info):
           for key, value in info.items():
               print(f"{key}: {value}")
       
       display_info(name="Alice", age=25, city="New York")
       ```
     - **Output:**
       ```
       name: Alice
       age: 25
       city: New York
       ```

4. **Combining `*args` and `**kwargs`**
   - You can use `*args` and `**kwargs` together in a function definition to accept both positional and keyword arguments. However, `*args` must come before `**kwargs`.
   - **Example:**
     ```python
     def func(*args, **kwargs):
         print("args:", args)
         print("kwargs:", kwargs)
     
     func(1, 2, 3, a=4, b=5)
     ```
   - **Output:**
     ```
     args: (1, 2, 3)
     kwargs: {'a': 4, 'b': 5}
     ```

5. **Use Cases**
   - **`*args`:**
     - Useful when you don’t know how many positional arguments will be passed to the function.
     - Example: Summing an arbitrary number of numbers.
   - **`**kwargs`:**
     - Useful when you want to handle optional keyword arguments or configuration parameters that can vary.
     - Example: Building a function that accepts various configuration options.

### Summary
- **`*args`** allows you to pass a variable number of positional arguments to a function and accesses them as a tuple.
- **`**kwargs`** allows you to pass a variable number of keyword arguments to a function and accesses them as a dictionary.
- They can be used together in a function to handle a wide range of input arguments, making your functions more flexible and adaptable.