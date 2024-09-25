## 29. What is the difference between `import` and `from` import?


### Difference Between `import` and `from ... import` in Python

In Python, both `import` and `from ... import` are used to bring external modules, functions, classes, or variables into your current script. However, they differ in how they import these elements and how you access them afterward.

1. **`import` Statement**
   - **Purpose:** The `import` statement imports an entire module, making all of its content available under the module’s namespace.
   - **Syntax:**
     ```python
     import module_name
     ```
   - **Usage:**
     - You must use the module name as a prefix when accessing any of its functions, classes, or variables.
     - **Example:**
       ```python
       import math
       result = math.sqrt(16)
       print(result)  # Output: 4.0
       ```
   - **Explanation:** The entire `math` module is imported, and its `sqrt` function is accessed using the prefix `math.`.

2. **`from ... import` Statement**
   - **Purpose:** The `from ... import` statement allows you to import specific functions, classes, or variables directly from a module, bringing them into the current namespace.
   - **Syntax:**
     ```python
     from module_name import item_name
     ```
   - **Usage:**
     - You can access the imported item directly without needing to prefix it with the module name.
     - **Example:**
       ```python
       from math import sqrt
       result = sqrt(16)
       print(result)  # Output: 4.0
       ```
   - **Explanation:** Only the `sqrt` function is imported from the `math` module, so you can use it directly without the `math.` prefix.

3. **`from ... import *` Statement**
   - **Purpose:** The `from ... import *` statement imports everything from a module into the current namespace.
   - **Syntax:**
     ```python
     from module_name import *
     ```
   - **Usage:**
     - All functions, classes, and variables from the module are imported, allowing direct access to them.
     - **Example:**
       ```python
       from math import *
       result = sqrt(16)
       print(result)  # Output: 4.0
       ```
   - **Drawback:**
     - This approach is generally discouraged because it can lead to namespace pollution and make the code harder to understand, especially if there are name conflicts.

4. **Key Differences**
   - **Namespace:**
     - `import module_name`: Imports the entire module. All items must be accessed using the module’s name as a prefix.
     - `from module_name import item_name`: Imports specific items from the module directly into the current namespace, allowing you to use them without a prefix.
   - **Granularity:**
     - `import module_name`: Useful when you need multiple items from a module or want to keep the namespace organized.
     - `from module_name import item_name`: Useful when you need only a few specific items from a module and want to avoid using the module prefix.

5. **Example Comparison**
   - **Using `import`:**
     ```python
     import random
     number = random.randint(1, 10)
     ```
   - **Using `from ... import`:**
     ```python
     from random import randint
     number = randint(1, 10)
     ```

### Summary
- The `import` statement imports an entire module and requires you to use the module name as a prefix when accessing its items.
- The `from ... import` statement imports specific items from a module directly into the current namespace, allowing you to use them without a prefix.
- Choose the approach that best suits your needs based on how many items you need from the module and how you want to organize your code.