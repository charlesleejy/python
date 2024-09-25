## 9. What are Python’s built-in data structures?


### Python’s Built-in Data Structures

1. **List**
   - **Definition:** An ordered, mutable collection of elements, which can be of different data types.
   - **Features:**
     - Supports indexing, slicing, and iteration.
     - Allows duplicate elements.
     - Dynamic size; elements can be added or removed.
   - **Example:**
     ```python
     my_list = [1, "apple", 3.14, True]
     ```

2. **Tuple**
   - **Definition:** An ordered, immutable collection of elements, which can be of different data types.
   - **Features:**
     - Similar to lists, but cannot be modified (no adding, removing, or changing elements).
     - Often used to represent fixed collections of items.
     - Supports indexing, slicing, and iteration.
   - **Example:**
     ```python
     my_tuple = (1, "banana", 2.5)
     ```

3. **Set**
   - **Definition:** An unordered collection of unique elements.
   - **Features:**
     - Does not allow duplicate elements.
     - Unordered, so elements cannot be accessed via index.
     - Supports set operations like union, intersection, and difference.
   - **Example:**
     ```python
     my_set = {1, 2, 3, 4}
     ```

4. **Dictionary (dict)**
   - **Definition:** An unordered collection of key-value pairs, where keys must be unique and immutable.
   - **Features:**
     - Fast lookups, additions, and deletions.
     - Keys are used to access values.
     - Mutable; allows dynamic insertion, deletion, and modification of key-value pairs.
   - **Example:**
     ```python
     my_dict = {"name": "Alice", "age": 30, "city": "New York"}
     ```

5. **String**
   - **Definition:** A sequence of Unicode characters, used for storing and manipulating text.
   - **Features:**
     - Immutable, meaning once created, it cannot be changed.
     - Supports indexing, slicing, and a wide range of string methods.
   - **Example:**
     ```python
     my_string = "Hello, World!"
     ```

### Summary
- Python’s built-in data structures include **lists**, **tuples**, **sets**, **dictionaries**, and **strings**.
- These structures are fundamental to writing efficient and effective Python code, allowing for a wide range of operations on collections of data.