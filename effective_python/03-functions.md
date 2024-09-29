### Chapter 3. Functions

---

#### **Item 19: Never Unpack More Than Three Variables When a Function Returns Multiple Values**

Unpacking allows functions to seemingly return more than one value. For example:

```python
def get_stats(numbers):
    minimum = min(numbers)
    maximum = max(numbers)
    return minimum, maximum

lengths = [63, 73, 72, 60, 67, 66, 71, 61, 72, 70]
minimum, maximum = get_stats(lengths)

print(f"Min: {minimum}, Max: {maximum}")
```

This works well when returning a few values. However, unpacking becomes problematic when dealing with more than three values. Consider this extended example:

```python
def get_stats(numbers):
    maximum = max(numbers)
    minimum = min(numbers)
    count = len(numbers)
    average = sum(numbers) / count
    sorted_numbers = sorted(numbers)
    middle = count // 2
    if count % 2 == 0:
        lower = sorted_numbers[middle - 1]
        upper = sorted_numbers[middle]
        median = (lower + upper) / 2
    else:
        median = sorted_numbers[middle]
    return minimum, maximum, average, median, count

minimum, maximum, average, median, count = get_stats(lengths)
```

Unpacking so many values can lead to:
1. **Errors due to reordering**: Mistakenly reordering return values will introduce bugs that are hard to catch.
2. **Poor readability**: Long unpacking statements go against Python’s readability principles (PEP 8).

Instead, use a **`namedtuple`** or a small class to package related values:

```python
from collections import namedtuple

Stats = namedtuple('Stats', ['minimum', 'maximum', 'average', 'median', 'count'])

def get_stats(numbers):
    maximum = max(numbers)
    minimum = min(numbers)
    count = len(numbers)
    average = sum(numbers) / count
    sorted_numbers = sorted(numbers)
    middle = count // 2
    if count % 2 == 0:
        lower = sorted_numbers[middle - 1]
        upper = sorted_numbers[middle]
        median = (lower + upper) / 2
    else:
        median = sorted_numbers[middle]
    return Stats(minimum, maximum, average, median, count)

stats = get_stats(lengths)
print(f"Min: {stats.minimum}, Max: {stats.maximum}")
```

---

#### **Item 20: Prefer Raising Errors to Returning `None`**

Returning `None` might seem like a good idea for invalid cases, but it can cause subtle bugs. Consider this function:

```python
def careful_divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return None
```

In some cases, it works fine:
```python
x, y = 1, 0
result = careful_divide(x, y)
if result is None:
    print("Invalid inputs")
```

But `None` can lead to confusion when checked improperly:
```python
x, y = 0, 5
result = careful_divide(x, y)
if not result:
    print("Invalid inputs")  # This runs incorrectly because result is 0.
```

To avoid this ambiguity, raise an exception instead:
```python
def careful_divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        raise ValueError("Invalid inputs")
```

Now, the caller must handle exceptions properly:
```python
x, y = 1, 0
try:
    result = careful_divide(x, y)
except ValueError:
    print("Invalid inputs")
else:
    print(f"Result is {result}")
```

This approach is more explicit and forces proper error handling.

---

#### **Item 21: Know How Closures Interact with Variable Scope**

Closures in Python allow functions to capture variables from their enclosing scopes. Consider the following example where you prioritize sorting a list based on membership in a specific group:

```python
def sort_priority(values, group):
    def helper(x):
        if x in group:
            return (0, x)
        return (1, x)
    values.sort(key=helper)

numbers = [8, 3, 1, 2, 5, 4, 7, 6]
group = {2, 3, 5, 7}
sort_priority(numbers, group)
print(numbers)
```

This works because:
1. **Closures**: The `helper` function captures the `group` variable from the outer `sort_priority` scope.
2. **First-class functions**: Functions are treated as objects, which is why we can pass `helper` as a key to `sort()`.

Now, imagine you want to return whether a number from the group was found. You may attempt the following:

```python
def sort_priority2(values, group):
    found = False
    def helper(x):
        if x in group:
            found = True  # This doesn't work as expected.
            return (0, x)
        return (1, x)
    values.sort(key=helper)
    return found

found = sort_priority2(numbers, group)
print('Found:', found)
```

This fails because Python treats the `found` variable as local to the `helper` function. To fix this, use the `nonlocal` keyword:

```python
def sort_priority3(values, group):
    found = False
    def helper(x):
        nonlocal found
        if x in group:
            found = True
            return (0, x)
        return (1, x)
    values.sort(key=helper)
    return found

found = sort_priority3(numbers, group)
print('Found:', found)
print(numbers)
```

Alternatively, you can use a class to encapsulate this behavior:

```python
class Sorter:
    def __init__(self, group):
        self.group = group
        self.found = False
    def __call__(self, x):
        if x in self.group:
            self.found = True
            return (0, x)
        return (1, x)

sorter = Sorter(group)
numbers.sort(key=sorter)
print('Found:', sorter.found)
```

---

#### **Item 22: Reduce Visual Noise with Variable Positional Arguments (`*args`)**

Positional arguments can help reduce the need for verbose function signatures, especially when handling variable-length inputs.

For example:
```python
def log(message, *values):
    if not values:
        print(message)
    else:
        values_str = ", ".join(str(x) for x in values)
        print(f"{message}: {values_str}")

log("My numbers are", 1, 2, 3)
log("Hello!")
```

Using `*args` simplifies the function definition and allows flexible inputs. You can also pass sequences with the `*` operator:

```python
favorites = [7, 33, 99]
log("Favorite numbers", *favorites)
```

However, use `*args` sparingly to avoid confusion and only when you expect a small number of arguments.

---

#### **Item 23: Provide Optional Behavior with Keyword Arguments**

Keyword arguments make function calls clearer, especially when dealing with default or optional behavior. For example:

```python
def remainder(number, divisor=2):
    return number % divisor

remainder(20)           # Uses default divisor=2
remainder(20, 7)        # Overrides default divisor
remainder(number=20, divisor=7)
```

You can also unpack keyword arguments from a dictionary:

```python
my_kwargs = {'number': 20, 'divisor': 7}
print(remainder(**my_kwargs))
```

---

#### **Item 24: Use `None` and Docstrings to Specify Dynamic Default Arguments**

Sometimes, you need a default argument that changes over time (e.g., a timestamp). Using mutable types or dynamic values directly can lead to bugs:

```python
def log(message, when=datetime.now()):  # Incorrect
    print(f"{when}: {message}")
```

This always uses the time when the function was defined, not when it is called. The correct approach is:

```python
def log(message, when=None):
    if when is None:
        when = datetime.now()
    print(f"{when}: {message}")
```

This method avoids the issue by using `None` as the default and specifying the behavior in the function body.

---

#### **Item 25: Enforce Clarity with Keyword-Only and Positional-Only Arguments**

To ensure clarity, especially in functions with many parameters, use **keyword-only arguments** by placing a `*` in the parameter list:

```python
def safe_division(number, divisor, *, ignore_overflow=False, ignore_zero_division=False):
    ...
```

You can also specify **positional-only arguments** (introduced in Python 3.8) by placing a `/` before keyword arguments:

```python
def safe_division(numerator, denominator, /, *, ignore_overflow=False):
    ...
```

This ensures that certain arguments must always be passed by position, enhancing function call clarity.

---

#### **Item 26: Define Function Decorators with `functools.wraps`**

Decorators allow you to modify functions without altering their code directly. However, using decorators can hide the original function's metadata (like docstrings). Here's an example decorator:

```python
from functools import wraps

def trace(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        print(f"{func.__name__}({args!r}, {kwargs!r}) -> {result!r}")
        return result
    return wrapper

@trace
def fibonacci(n):
    """Return the n-th Fibonacci number."""
    if n in (0, 1):
        return n
    return fibonacci(n-1) + fibonacci(n-2)
```

The `@wraps` decorator ensures that the original function's metadata (like its name and docstring) is preserved.

Without `@wraps`, calling `help(fibonacci)` would return information about the `wrapper` function instead of the original `fibonacci` function.