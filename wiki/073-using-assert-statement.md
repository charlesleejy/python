## 73. How do you use the `assert` statement in Python?


The `assert` statement in Python is used as a debugging aid that tests a condition. If the condition evaluates to `True`, the program continues to execute as normal. If the condition evaluates to `False`, the `assert` statement raises an `AssertionError` with an optional error message. This is helpful for catching bugs early in the development process by ensuring that certain conditions hold true.

### Basic Usage of the `assert` Statement

The `assert` statement has the following syntax:

```python
assert condition, optional_message
```

- **`condition`:** The expression that is expected to be `True`. If `False`, an `AssertionError` is raised.
- **`optional_message`:** (Optional) A message that will be displayed if the assertion fails. This can help explain why the assertion failed.

### Example 1: Simple Assertion

```python
x = 10
y = 5

assert x > y, "x should be greater than y"
```

- **Explanation:** This `assert` statement checks if `x > y`. Since `10 > 5` is `True`, the program continues without error.

### Example 2: Assertion with Failure

```python
x = 10
y = 15

assert x > y, "x is not greater than y"
```

- **Explanation:** Here, `x > y` evaluates to `False`, so the `assert` statement raises an `AssertionError` with the message "x is not greater than y".

**Output:**
```python
Traceback (most recent call last):
  File "example.py", line 4, in <module>
    assert x > y, "x is not greater than y"
AssertionError: x is not greater than y
```

### Example 3: Using `assert` in a Function

```python
def divide(a, b):
    assert b != 0, "Division by zero is not allowed"
    return a / b

print(divide(10, 2))  # Output: 5.0
print(divide(10, 0))  # Raises AssertionError: Division by zero is not allowed
```

- **Explanation:** The `assert` statement ensures that `b` is not zero before performing the division. If `b` is zero, an `AssertionError` is raised with the message "Division by zero is not allowed".

### Use Cases for `assert`

1. **Debugging:** Use `assert` to catch bugs by ensuring that certain conditions hold true during development.
2. **Invariants:** Verify that certain invariants or conditions are maintained throughout the code, such as ensuring input values are within an expected range.
3. **Contract Programming:** Use `assert` to enforce preconditions, postconditions, and invariants in functions.

### Important Considerations

- **Assertions Can Be Disabled:** Python’s `assert` statements can be globally disabled using the `-O` (optimize) command-line switch. When running Python with `python -O`, all `assert` statements are stripped out, meaning they won’t be executed. This makes them useful primarily for debugging and development, rather than as a mechanism for error handling in production code.
- **Not for Input Validation:** Avoid using `assert` for validating user input or controlling program flow in production code. For these cases, use proper error handling (e.g., `if` statements and exceptions).

### Summary

- The `assert` statement is used to test if a condition is `True`. If not, it raises an `AssertionError` with an optional error message.
- Useful for debugging, ensuring invariants, and contract programming during development.
- `assert` statements can be disabled in optimized mode, so they should not be relied upon for critical checks in production code.

The `assert` statement is a simple but powerful tool for catching bugs and ensuring that your code behaves as expected during development.