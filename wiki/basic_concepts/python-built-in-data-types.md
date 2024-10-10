## What are Python’s built-in data types?


### Python’s Built-in Data Types

1. **Numeric Types**
   - **int**: 
     - Represents whole numbers, both positive and negative, without a decimal point.
     - Example: `x = 10`
   - **float**:
     - Represents real numbers, which include a decimal point.
     - Example: `y = 3.14`
   - **complex**:
     - Represents complex numbers with both a real and imaginary part.
     - Example: `z = 1 + 2j`

2. **Sequence Types**
   - **str (String)**:
     - Immutable sequence of Unicode characters used for storing text.
     - Example: `s = "Hello, World!"`
   - **list**:
     - Ordered, mutable collection of elements, which can be of different data types.
     - Example: `lst = [1, "apple", 3.14]`
   - **tuple**:
     - Ordered, immutable collection of elements, similar to a list, but cannot be changed after creation.
     - Example: `t = (1, "banana", 2.5)`

3. **Mapping Type**
   - **dict (Dictionary)**:
     - Unordered collection of key-value pairs where keys must be unique and immutable.
     - Example: `d = {"name": "Alice", "age": 30}`

4. **Set Types**
   - **set**:
     - Unordered collection of unique elements, useful for removing duplicates.
     - Example: `s = {1, 2, 3, 4}`
   - **frozenset**:
     - Immutable version of a set, meaning it cannot be modified after creation.
     - Example: `fs = frozenset([1, 2, 3, 4])`

5. **Boolean Type**
   - **bool**:
     - Represents one of two values: `True` or `False`.
     - Commonly used in conditional statements.
     - Example: `is_valid = True`

6. **Binary Types**
   - **bytes**:
     - Immutable sequence of bytes, typically used for binary data.
     - Example: `b = b"Hello"`
   - **bytearray**:
     - Mutable sequence of bytes, allowing for modification of its elements.
     - Example: `ba = bytearray([65, 66, 67])`
   - **memoryview**:
     - Provides a view object that exposes the buffer interface, enabling the manipulation of large data sets without copying.
     - Example: `mv = memoryview(b"Hello")`

7. **None Type**
   - **None**:
     - Represents the absence of a value or a null value.
     - Often used to signify that a variable has no value assigned.
     - Example: `x = None`

### Summary
- Python’s built-in data types are fundamental for handling various kinds of data, ranging from numbers and sequences to mappings and sets.
- Understanding these data types is crucial for effective programming in Python, as they form the building blocks of all data manipulation tasks.