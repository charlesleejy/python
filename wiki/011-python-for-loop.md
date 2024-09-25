## 11. How do you write a `for` loop in Python?


### Writing a For Loop in Python

1. **Basic Structure**
   - A `for` loop in Python is used to iterate over a sequence (like a list, tuple, dictionary, set, or string) and execute a block of code for each item in the sequence.
   - **Syntax:**
     ```python
     for item in sequence:
         # Code to execute for each item
     ```

2. **Example: Iterating Over a List**
   - **Code:**
     ```python
     fruits = ["apple", "banana", "cherry"]
     for fruit in fruits:
         print(fruit)
     ```
   - **Explanation:**
     - The loop iterates over each item in the `fruits` list, and the `print()` statement is executed for each item.
   - **Output:**
     ```
     apple
     banana
     cherry
     ```

3. **Example: Iterating Over a Range of Numbers**
   - **Code:**
     ```python
     for i in range(5):
         print(i)
     ```
   - **Explanation:**
     - The `range(5)` function generates numbers from 0 to 4, and the loop prints each number.
   - **Output:**
     ```
     0
     1
     2
     3
     4
     ```

4. **Example: Iterating Over a String**
   - **Code:**
     ```python
     for char in "Hello":
         print(char)
     ```
   - **Explanation:**
     - The loop iterates over each character in the string `"Hello"`.
   - **Output:**
     ```
     H
     e
     l
     l
     o
     ```

5. **Using `break` and `continue`**
   - **`break`:** Exits the loop prematurely when a certain condition is met.
   - **Example:**
     ```python
     for i in range(5):
         if i == 3:
             break
         print(i)
     ```
   - **Output:**
     ```
     0
     1
     2
     ```

   - **`continue`:** Skips the rest of the code inside the loop for the current iteration and moves to the next iteration.
   - **Example:**
     ```python
     for i in range(5):
         if i == 3:
             continue
         print(i)
     ```
   - **Output:**
     ```
     0
     1
     2
     4
     ```

6. **Iterating Over a Dictionary**
   - **Code:**
     ```python
     my_dict = {"name": "Alice", "age": 30, "city": "New York"}
     for key, value in my_dict.items():
         print(f"{key}: {value}")
     ```
   - **Explanation:**
     - The `items()` method returns key-value pairs, which are unpacked into `key` and `value` variables in each iteration.
   - **Output:**
     ```
     name: Alice
     age: 30
     city: New York
     ```

7. **Nested For Loops**
   - **Code:**
     ```python
     for i in range(3):
         for j in range(2):
             print(f"i={i}, j={j}")
     ```
   - **Explanation:**
     - The outer loop runs three times, and for each iteration of the outer loop, the inner loop runs twice.
   - **Output:**
     ```
     i=0, j=0
     i=0, j=1
     i=1, j=0
     i=1, j=1
     i=2, j=0
     i=2, j=1
     ```

### Summary
- A `for` loop in Python is a versatile construct for iterating over sequences such as lists, tuples, dictionaries, sets, and strings.
- The loop syntax is simple and allows the use of `break` and `continue` to control the flow of the loop based on conditions.