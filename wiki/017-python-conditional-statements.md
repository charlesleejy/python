## 17. How do you create a conditional statement in Python?


### Creating a Conditional Statement in Python

A conditional statement in Python allows you to execute different blocks of code based on certain conditions. The most common conditional statements are created using `if`, `elif`, and `else` keywords.

1. **Basic `if` Statement**
   - **Purpose:** Executes a block of code if the condition is `True`.
   - **Syntax:**
     ```python
     if condition:
         # Code to execute if condition is True
     ```
   - **Example:**
     ```python
     age = 18
     if age >= 18:
         print("You are an adult.")
     ```
   - **Output:**
     ```
     You are an adult.
     ```

2. **`if-else` Statement**
   - **Purpose:** Provides an alternative block of code that executes if the condition is `False`.
   - **Syntax:**
     ```python
     if condition:
         # Code to execute if condition is True
     else:
         # Code to execute if condition is False
     ```
   - **Example:**
     ```python
     age = 16
     if age >= 18:
         print("You are an adult.")
     else:
         print("You are a minor.")
     ```
   - **Output:**
     ```
     You are a minor.
     ```

3. **`if-elif-else` Statement**
   - **Purpose:** Handles multiple conditions by checking additional conditions if the previous one is `False`.
   - **Syntax:**
     ```python
     if condition1:
         # Code to execute if condition1 is True
     elif condition2:
         # Code to execute if condition2 is True
     else:
         # Code to execute if all conditions are False
     ```
   - **Example:**
     ```python
     score = 85
     if score >= 90:
         print("Grade: A")
     elif score >= 80:
         print("Grade: B")
     elif score >= 70:
         print("Grade: C")
     else:
         print("Grade: F")
     ```
   - **Output:**
     ```
     Grade: B
     ```

4. **Nested `if` Statements**
   - **Purpose:** You can nest `if` statements within each other to check multiple conditions sequentially.
   - **Syntax:**
     ```python
     if condition1:
         if condition2:
             # Code to execute if both condition1 and condition2 are True
     ```
   - **Example:**
     ```python
     age = 20
     citizenship = "US"
     if age >= 18:
         if citizenship == "US":
             print("You are eligible to vote.")
         else:
             print("You are not eligible to vote.")
     else:
         print("You are not old enough to vote.")
     ```
   - **Output:**
     ```
     You are eligible to vote.
     ```

5. **Conditional Expression (Ternary Operator)**
   - **Purpose:** A shorthand way to write simple `if-else` statements.
   - **Syntax:**
     ```python
     value_if_true if condition else value_if_false
     ```
   - **Example:**
     ```python
     age = 20
     status = "adult" if age >= 18 else "minor"
     print(status)
     ```
   - **Output:**
     ```
     adult
     ```

### Summary
- Conditional statements in Python use `if`, `elif`, and `else` to control the flow of code based on conditions.
- You can check single conditions with `if`, handle alternative cases with `else`, and add multiple conditions with `elif`.
- Nested `if` statements and the ternary operator allow for more complex and concise conditionals.