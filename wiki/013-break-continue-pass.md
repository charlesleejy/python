## 13. What is the difference between `break`, `continue`, and `pass` statements?


### Difference Between `break`, `continue`, and `pass` Statements in Python

1. **`break` Statement**
   - **Purpose:** Immediately terminates the loop (for or while) in which it is used, and control is transferred to the first statement following the loop.
   - **Usage:** Used when you want to exit the loop early, typically when a certain condition is met.
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
   - **Explanation:** The loop stops when `i` equals 3, so the numbers after 2 are not printed.

2. **`continue` Statement**
   - **Purpose:** Skips the rest of the code inside the loop for the current iteration and moves to the next iteration of the loop.
   - **Usage:** Used when you want to skip the current iteration but continue with the loop.
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
   - **Explanation:** When `i` equals 3, the `continue` statement skips printing 3 and moves to the next iteration.

3. **`pass` Statement**
   - **Purpose:** Does nothing; it’s a null statement that is used as a placeholder.
   - **Usage:** Used in situations where a statement is syntactically required but you don’t want to execute any code. Commonly used for creating minimal class or function definitions, or when stubbing out code during development.
   - **Example:**
     ```python
     for i in range(5):
         if i == 3:
             pass  # Placeholder, no action taken
         print(i)
     ```
   - **Output:**
     ```
     0
     1
     2
     3
     4
     ```
   - **Explanation:** The `pass` statement does nothing; the loop continues as if the `pass` statement wasn’t there.

### Summary
- **`break`:** Exits the loop entirely, stopping further iterations.
- **`continue`:** Skips the remaining code in the current iteration and proceeds to the next iteration.
- **`pass`:** Does nothing; it’s used as a placeholder where a statement is syntactically required but no action is needed.