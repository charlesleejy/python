## 19. How do you use the `range()` function in loops?


### Using the `range()` Function in Loops

The `range()` function is commonly used in Python loops, especially `for` loops, to generate a sequence of numbers. It provides a simple way to iterate over a series of numbers, making it essential for controlling the number of loop iterations.

1. **Basic Usage of `range()`**
   - **Syntax:**
     ```python
     range(start, stop, step)
     ```
   - **Parameters:**
     - `start` (optional): The starting value of the sequence (inclusive). Defaults to `0` if not specified.
     - `stop` (required): The end value of the sequence (exclusive).
     - `step` (optional): The difference between each number in the sequence. Defaults to `1` if not specified.

2. **Example: Iterating with `range()` in a For Loop**
   - **Loop from 0 to 4:**
     ```python
     for i in range(5):
         print(i)
     ```
   - **Explanation:**
     - This loop starts at `0` and goes up to (but does not include) `5`, printing each number.
   - **Output:**
     ```
     0
     1
     2
     3
     4
     ```

3. **Using `range()` with a Start Value**
   - **Loop from 2 to 5:**
     ```python
     for i in range(2, 6):
         print(i)
     ```
   - **Explanation:**
     - This loop starts at `2` and stops before `6`, printing numbers from `2` to `5`.
   - **Output:**
     ```
     2
     3
     4
     5
     ```

4. **Using `range()` with a Step Value**
   - **Loop from 0 to 8, with a step of 2:**
     ```python
     for i in range(0, 10, 2):
         print(i)
     ```
   - **Explanation:**
     - This loop starts at `0` and increments by `2` each time, stopping before `10`.
   - **Output:**
     ```
     0
     2
     4
     6
     8
     ```

5. **Using `range()` with a Negative Step**
   - **Loop from 5 to 1 in reverse:**
     ```python
     for i in range(5, 0, -1):
         print(i)
     ```
   - **Explanation:**
     - This loop starts at `5` and decrements by `1` each time, stopping before `0`.
   - **Output:**
     ```
     5
     4
     3
     2
     1
     ```

6. **Using `range()` in Combination with Other Functions**
   - **Example with `len()` to Iterate Over a List:**
     ```python
     fruits = ["apple", "banana", "cherry"]
     for i in range(len(fruits)):
         print(f"Index {i}: {fruits[i]}")
     ```
   - **Output:**
     ```
     Index 0: apple
     Index 1: banana
     Index 2: cherry
     ```

### Summary
- The `range()` function is a powerful tool for generating sequences of numbers, making it ideal for controlling loop iterations.
- It can be used with different start, stop, and step values to create flexible loops, including forward, backward, and skipped iterations.
- `range()` is particularly useful in `for` loops, enabling efficient and readable code for iterating over sequences.