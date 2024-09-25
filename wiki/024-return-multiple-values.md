## 24. How do you return multiple values from a function?


### Returning Multiple Values from a Function in Python

Python allows you to return multiple values from a function in a straightforward and flexible way. There are several methods to do this, and they all involve packing multiple values into a single structure that can be unpacked by the caller.

1. **Returning Multiple Values as a Tuple**
   - Python functions can return multiple values by separating them with commas. These values are automatically packed into a tuple.
   - **Example:**
     ```python
     def get_coordinates():
         x = 10
         y = 20
         return x, y  # Returns a tuple (x, y)
     
     coords = get_coordinates()
     print(coords)  # Output: (10, 20)
     ```
   - **Unpacking the Tuple:**
     ```python
     x, y = get_coordinates()
     print(f"x: {x}, y: {y}")  # Output: x: 10, y: 20
     ```

2. **Returning Multiple Values as a List**
   - You can also return multiple values as a list. This is useful if the number of returned values might change, or if you need a mutable sequence.
   - **Example:**
     ```python
     def get_numbers():
         return [1, 2, 3]
     
     numbers = get_numbers()
     print(numbers)  # Output: [1, 2, 3]
     ```

3. **Returning Multiple Values as a Dictionary**
   - Returning a dictionary allows you to label the returned values, making the code more readable and reducing the risk of mistakes when unpacking the results.
   - **Example:**
     ```python
     def get_person_info():
         return {"name": "Alice", "age": 30, "city": "New York"}
     
     info = get_person_info()
     print(info["name"])  # Output: Alice
     ```

4. **Returning Multiple Values as a Named Tuple**
   - Named tuples are like regular tuples but with named fields. They provide a convenient way to return multiple values with meaningful names.
   - **Example:**
     ```python
     from collections import namedtuple
     
     def get_point():
         Point = namedtuple('Point', ['x', 'y'])
         return Point(10, 20)
     
     point = get_point()
     print(point.x, point.y)  # Output: 10 20
     ```

5. **Returning Multiple Values as a Class Instance**
   - For more complex cases, you can return an instance of a class that holds the values as attributes.
   - **Example:**
     ```python
     class Result:
         def __init__(self, value1, value2):
             self.value1 = value1
             self.value2 = value2
     
     def compute():
         return Result(5, 10)
     
     result = compute()
     print(result.value1, result.value2)  # Output: 5 10
     ```

### Summary
- In Python, you can return multiple values from a function using tuples, lists, dictionaries, named tuples, or class instances.
- The most common and straightforward method is returning a tuple by separating values with commas. However, for more readability or structured data, you can use dictionaries, named tuples, or class instances.