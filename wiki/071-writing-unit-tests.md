## 71. How do you write unit tests in Python?


Writing unit tests in Python is essential for ensuring the correctness of your code. Python provides the `unittest` module, which is part of the standard library, to create and run unit tests. Here’s a step-by-step guide on how to write unit tests in Python using `unittest`.

### 1. **Import the `unittest` Module**

The `unittest` module provides classes and methods to create and run tests. You need to import it before writing your tests.

```python
import unittest
```

### 2. **Create a Test Class**

Create a test class that inherits from `unittest.TestCase`. This class will contain your test methods.

```python
class TestMyFunction(unittest.TestCase):
    # Test methods go here
```

### 3. **Write Test Methods**

Each test method in your test class should start with the word `test`. This naming convention ensures that `unittest` recognizes them as tests.

```python
class TestMyFunction(unittest.TestCase):
    
    def test_addition(self):
        self.assertEqual(1 + 1, 2)
    
    def test_subtraction(self):
        self.assertEqual(5 - 3, 2)
```

- **Explanation:**
  - `self.assertEqual(a, b)`: Asserts that `a` is equal to `b`. If they are not equal, the test fails.
  - `self.assertTrue(x)`: Asserts that `x` is `True`.
  - `self.assertFalse(x)`: Asserts that `x` is `False`.
  - `self.assertRaises(exception, callable, *args, **kwargs)`: Asserts that the given exception is raised when the callable is called with the specified arguments.

### 4. **Running the Tests**

You can run the tests using the command line or by adding the following block at the end of your test script:

```python
if __name__ == '__main__':
    unittest.main()
```

- **Explanation:** The `unittest.main()` function runs all test methods in the script. The `if __name__ == '__main__':` block ensures that the tests run only when the script is executed directly, not when imported as a module.

### 5. **Example of a Complete Test Case**

Here’s an example of a simple unit test for a function that adds two numbers:

```python
import unittest

# Function to be tested
def add(a, b):
    return a + b

class TestAddFunction(unittest.TestCase):
    
    def test_add_positive_numbers(self):
        self.assertEqual(add(1, 2), 3)
    
    def test_add_negative_numbers(self):
        self.assertEqual(add(-1, -2), -3)
    
    def test_add_zero(self):
        self.assertEqual(add(0, 0), 0)
    
    def test_add_positive_and_negative(self):
        self.assertEqual(add(1, -1), 0)

if __name__ == '__main__':
    unittest.main()
```

- **Explanation:**
  - The `add` function is the target of the unit tests.
  - The `TestAddFunction` class contains test methods to validate different scenarios (positive numbers, negative numbers, zero, and a mix of positive and negative numbers).
  - `unittest.main()` runs all the test methods.

### 6. **Using `setUp` and `tearDown` Methods**

If you need to perform some setup before each test method or clean up afterward, you can use `setUp()` and `tearDown()` methods.

```python
class TestMyFunction(unittest.TestCase):
    
    def setUp(self):
        # Code to set up test environment
        self.data = [1, 2, 3]

    def tearDown(self):
        # Code to clean up after tests
        self.data = None
    
    def test_data_sum(self):
        self.assertEqual(sum(self.data), 6)
```

- **Explanation:**
  - `setUp()`: Runs before each test method, useful for setting up any preconditions.
  - `tearDown()`: Runs after each test method, useful for cleaning up after tests.

### 7. **Assertions in `unittest`**

Some common assertions in `unittest` are:
- **`assertEqual(a, b)`**: Checks if `a` equals `b`.
- **`assertNotEqual(a, b)`**: Checks if `a` does not equal `b`.
- **`assertTrue(x)`**: Checks if `x` is `True`.
- **`assertFalse(x)`**: Checks if `x` is `False`.
- **`assertIsNone(x)`**: Checks if `x` is `None`.
- **`assertIsNotNone(x)`**: Checks if `x` is not `None`.
- **`assertIn(a, b)`**: Checks if `a` is in `b`.
- **`assertNotIn(a, b)`**: Checks if `a` is not in `b`.
- **`assertRaises(exception, callable, *args, **kwargs)`**: Checks if calling `callable` raises the specified `exception`.

### 8. **Running Tests with Command Line**

If you save your test in a file (e.g., `test_example.py`), you can run the tests using the command line:

```bash
python -m unittest test_example.py
```

This will automatically discover and run all tests in the file.

### Summary

- **Create Test Class:** Inherit from `unittest.TestCase`.
- **Write Test Methods:** Methods should start with `test` and contain assertions.
- **Run Tests:** Use `unittest.main()` or run tests using the command line.
- **Use `setUp` and `tearDown`:** For setting up and cleaning up before and after tests.
- **Assertions:** Use the various `assert` methods to validate conditions.

The `unittest` framework is versatile and can be easily extended, making it suitable for both simple and complex testing scenarios.