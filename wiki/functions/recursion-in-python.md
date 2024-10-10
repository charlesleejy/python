## Explain the concept of recursion with an example.


### Concept of Recursion

1. **Definition**
   - **Recursion** is a programming technique where a function calls itself directly or indirectly to solve a problem. The problem is typically divided into smaller subproblems of the same type, and recursion is used to solve these subproblems.

2. **Key Components of Recursion**
   - **Base Case:** The condition under which the recursion stops. Without a base case, the recursion would continue indefinitely, leading to a stack overflow.
   - **Recursive Case:** The part of the function where the function calls itself with a modified argument, moving closer to the base case.

3. **Example: Factorial Calculation**
   - The factorial of a non-negative integer `n` is the product of all positive integers less than or equal to `n`. It is denoted as `n!`.
   - **Mathematical Definition:**
     - `n! = n * (n - 1) * (n - 2) * ... * 1`
     - `n! = n * (n - 1)!`
     - `0! = 1` (Base case)

4. **Recursive Implementation of Factorial**
   - **Code:**
     ```python
     def factorial(n):
         if n == 0:
             return 1  # Base case
         else:
             return n * factorial(n - 1)  # Recursive case

     print(factorial(5))  # Output: 120
     ```
   - **Explanation:**
     - When `factorial(5)` is called, it follows these steps:
       1. `factorial(5)` calls `factorial(4)`
       2. `factorial(4)` calls `factorial(3)`
       3. `factorial(3)` calls `factorial(2)`
       4. `factorial(2)` calls `factorial(1)`
       5. `factorial(1)` calls `factorial(0)` (Base case, returns 1)
       6. The results are then multiplied as the stack unwinds: `1 * 1 * 2 * 3 * 4 * 5 = 120`

5. **Output:**
   ```
   120
   ```

6. **Advantages of Recursion**
   - **Simplifies Code:** Some problems, especially those involving hierarchical or repetitive structures (e.g., tree traversal, factorial, Fibonacci sequence), are easier to solve using recursion.
   - **Clean and Elegant:** Recursive solutions are often more elegant and easier to understand compared to their iterative counterparts.

7. **Disadvantages of Recursion**
   - **Performance:** Recursive solutions can be less efficient due to the overhead of multiple function calls and can lead to excessive memory use (stack overflow) if not handled properly.
   - **Complexity:** Recursive functions can be harder to debug and understand, especially for complex problems or deep recursion.

8. **Example: Fibonacci Sequence**
   - The Fibonacci sequence is another classic example where recursion is often used.
   - **Recursive Code:**
     ```python
     def fibonacci(n):
         if n <= 1:
             return n  # Base cases: fibonacci(0) = 0, fibonacci(1) = 1
         else:
             return fibonacci(n - 1) + fibonacci(n - 2)  # Recursive case

     print(fibonacci(6))  # Output: 8
     ```
   - **Explanation:** The `fibonacci` function calls itself twice to calculate the sum of the two preceding numbers.

### Summary
- **Recursion** is a technique where a function calls itself to solve smaller instances of a problem.
- It involves a base case to terminate the recursion and a recursive case that reduces the problem size.
- Although recursion can simplify code for certain problems, it can be less efficient and more complex than iterative approaches.