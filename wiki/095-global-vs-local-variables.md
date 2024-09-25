## 95. What are Python’s global and local variables?


In Python, variables can be classified as either **global** or **local** based on where they are defined and how they are used within the code. Understanding the distinction between global and local variables is crucial for managing scope, avoiding unintended side effects, and writing clean, maintainable code.

### 1. **Local Variables**

Local variables are those that are defined inside a function or a block of code. They are only accessible within the function or block in which they are created.

#### **Key Points:**
- Local variables are declared within a function.
- They can only be used inside that function.
- They are created when the function is called and destroyed when the function exits.

#### **Example:**
```python
def my_function():
    x = 10  # x is a local variable
    print(x)

my_function()  # Output: 10
print(x)       # Error: NameError: name 'x' is not defined
```

- **Explanation:** The variable `x` is local to `my_function()` and is not accessible outside of it. Attempting to print `x` outside the function will raise a `NameError`.

### 2. **Global Variables**

Global variables are those that are defined outside of any function or block. They are accessible from any part of the program, including inside functions (unless shadowed by a local variable with the same name).

#### **Key Points:**
- Global variables are declared outside of all functions.
- They can be accessed and modified from any function, unless a local variable with the same name is declared within the function.
- Use the `global` keyword to modify a global variable inside a function.

#### **Example:**
```python
x = 20  # x is a global variable

def my_function():
    print(x)  # Accesses the global variable x

my_function()  # Output: 20
print(x)       # Output: 20
```

- **Explanation:** The variable `x` is global and can be accessed both inside and outside `my_function()`.

#### **Modifying Global Variables:**
If you want to modify a global variable inside a function, you must use the `global` keyword.

**Example:**
```python
x = 20  # Global variable

def my_function():
    global x
    x = 30  # Modify the global variable x
    print(x)

my_function()  # Output: 30
print(x)       # Output: 30
```

- **Explanation:** By using the `global` keyword, the function `my_function()` modifies the global variable `x`.

### 3. **Scope and Lifetime of Variables**

- **Scope:** The scope of a variable determines where it can be accessed. Local variables are scoped to the function they are defined in, while global variables are scoped to the entire script/module.
- **Lifetime:** The lifetime of a variable refers to how long the variable exists in memory. Local variables are created when the function is called and destroyed when the function exits. Global variables exist for the duration of the program.

### 4. **Global vs. Local Variables with the Same Name**

If a local variable shares the same name as a global variable, the local variable takes precedence within its scope (inside the function). This is known as "shadowing."

**Example:**
```python
x = 50  # Global variable

def my_function():
    x = 100  # Local variable
    print(x)

my_function()  # Output: 100 (local variable)
print(x)       # Output: 50 (global variable)
```

- **Explanation:** The local variable `x` inside `my_function()` shadows the global variable `x`. Outside the function, the global `x` remains unchanged.

### 5. **Global Variables in Nested Functions**

When working with nested functions, you can use the `nonlocal` keyword to modify variables in the nearest enclosing (non-global) scope.

**Example:**
```python
def outer_function():
    x = 10  # This is in the enclosing scope
    
    def inner_function():
        nonlocal x  # Refers to the x in outer_function
        x = 20
    
    inner_function()
    print(x)  # Output: 20

outer_function()
```

- **Explanation:** The `nonlocal` keyword allows `inner_function` to modify the variable `x` defined in `outer_function`.

### Summary

- **Local Variables:** Defined inside a function and accessible only within that function. They have a limited scope and short lifetime.
- **Global Variables:** Defined outside of functions and accessible throughout the entire script. Use the `global` keyword to modify them inside a function.
- **Scope and Lifetime:** The scope of a variable determines where it can be accessed, and the lifetime determines how long it exists in memory.
- **Shadowing:** If a local and global variable share the same name, the local variable shadows the global one within its scope.

Understanding the distinction between local and global variables helps you manage scope effectively, avoid bugs, and write clean, maintainable code in Python.