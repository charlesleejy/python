## What are Python’s built-in debugging tools?


Python provides several built-in tools and modules that can help with debugging code. These tools range from simple print statements to more advanced interactive debuggers. Here’s a look at Python’s built-in debugging tools:

### 1. **`print()` Statements**

While not sophisticated, using `print()` statements is often the first line of defense in debugging. You can print the values of variables or program states to track what’s happening in your code.

**Example:**
```python
x = 10
y = 20
print(f"x: {x}, y: {y}")
```

### 2. **`pdb` (Python Debugger)**

The `pdb` module is Python’s built-in interactive debugger. It allows you to pause execution, inspect variables, step through code, and evaluate expressions.

**Key Features:**
- Set breakpoints with `pdb.set_trace()`.
- Step through code line by line.
- Inspect variables and the call stack.

**Example:**
```python
import pdb

def divide(a, b):
    pdb.set_trace()  # Pauses execution here and opens the debugger
    return a / b

result = divide(10, 2)
```

- **Common `pdb` Commands:**
  - `n`: Go to the next line.
  - `s`: Step into a function.
  - `c`: Continue execution until the next breakpoint.
  - `q`: Quit the debugger.
  - `p <variable>`: Print the value of a variable.

### 3. **`breakpoint()` (Python 3.7+)**

Starting from Python 3.7, the `breakpoint()` function provides a simple way to enter the debugger. It’s equivalent to calling `pdb.set_trace()` but more flexible, allowing you to customize the debugger used via the `PYTHONBREAKPOINT` environment variable.

**Example:**
```python
def multiply(a, b):
    breakpoint()  # Enters the debugger
    return a * b

result = multiply(3, 4)
```

### 4. **`assert` Statement**

The `assert` statement is used to verify assumptions in your code. If the condition is `False`, it raises an `AssertionError` with an optional message. Assertions are typically used during development to catch bugs early.

**Example:**
```python
def square_root(x):
    assert x >= 0, "x must be non-negative"
    return x ** 0.5
```

### 5. **`logging` Module**

The `logging` module allows you to track events that happen when software runs. Compared to `print()`, logging is more flexible and can be configured to output messages of different severity levels (DEBUG, INFO, WARNING, ERROR, CRITICAL).

**Example:**
```python
import logging

logging.basicConfig(level=logging.DEBUG)

def add(a, b):
    logging.debug(f"Adding {a} + {b}")
    return a + b

result = add(2, 3)
```

### 6. **`trace` Module**

The `trace` module allows you to trace the execution of Python statements, produce coverage reports, and investigate which parts of your code are being executed.

**Example:**
```bash
python -m trace --trace my_script.py
```

- **Explanation:** This command runs `my_script.py` with tracing enabled, showing every line executed.

### 7. **`sys.settrace()`**

The `sys.settrace()` function allows you to set a trace function that is invoked on various events like function calls, line execution, etc. This is more advanced and is typically used for implementing custom debuggers or profilers.

**Example:**
```python
import sys

def trace_calls(frame, event, arg):
    if event == 'call':
        print(f"Calling function: {frame.f_code.co_name}")
    return trace_calls

sys.settrace(trace_calls)

def hello():
    print("Hello, world!")

hello()
```

### 8. **`faulthandler` Module**

The `faulthandler` module helps you dump Python tracebacks explicitly, on a timeout, or when a fatal error (like a segmentation fault) occurs.

**Example:**
```python
import faulthandler

faulthandler.enable()
```

- **Explanation:** This can be useful for diagnosing crashes in Python programs that don’t provide much information.

### 9. **`cProfile` and `profile` Modules**

While these are more profiling tools than debuggers, they help identify performance bottlenecks in your code by showing where most of the time is being spent.

**Example:**
```bash
python -m cProfile my_script.py
```

### Summary

Python provides a variety of built-in tools for debugging, ranging from basic `print()` statements to sophisticated interactive debuggers like `pdb` and `breakpoint()`. You can also use the `logging` module for more controlled debugging output, or the `trace` and `faulthandler` modules for advanced tracing and fault diagnosis. These tools help you understand your code's behavior, catch bugs early, and ensure your program runs as expected.
