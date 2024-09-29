### Chapter 1. Pythonic Thinking

#### **Item 1: Know Which Version of Python You’re Using**

It’s important to be aware of the version of Python you are using, as syntax and features can differ significantly between versions. For example, Python 2 and Python 3 have substantial differences, so you must check your environment to ensure compatibility with the version you're targeting.

```bash
python --version
```

In Python, you can use the following code to get detailed information about the version:

```python
import sys

print(sys.version_info)
print(sys.version)
```

---

#### **Item 2: Follow the PEP 8 Style Guide**

**Whitespace Matters**:
- Use 4 spaces for indentation, not tabs.
- Limit lines to 79 characters.
- For long lines, indent the continuation by 4 spaces.
- Separate top-level functions and class definitions with 2 blank lines.
- Within a class, separate methods by 1 blank line.
- Avoid extra spaces around the colon in a dictionary (e.g., `{key: value}`), and use spaces around assignment operators (e.g., `var = value`).
- In function annotations, there’s no space before the colon (e.g., `def function(param: str):`).

**Naming Conventions**:
- Use `lowercase_underscore` for functions, variables, and attributes.
- Use `_leading_underscore` for protected instance attributes.
- Use `__double_leading_underscore` for private instance attributes.
- Use `CapitalizedWords` for class names.
- Use `ALL_CAPS` for module-level constants.
- Use `self` as the name of the first parameter for instance methods and `cls` for class methods.

**Expressions and Statements**:
- Strive to find the one clear and obvious way to do something.
- Use `is not` for comparisons.
- Check for empty lists with `if not list:` and for non-empty lists with `if list:`.
- Avoid single-line `if`, `for`, `while`, and `except` statements.

**Imports**:
- Place all `import` statements at the top of the file.
- Use absolute imports (`from module import function`), and use relative imports (`from . import function`) only within packages.
- Group imports in the following order:
    1. Standard library imports
    2. Third-party imports
    3. Local application imports

---

#### **Item 3: Know the Differences Between `bytes` and `str`**

Python 3 differentiates between `bytes` (raw data) and `str` (text). You should use a **Unicode sandwich** approach:
- Decode bytes as early as possible into `str`.
- Work with `str` throughout your program.
- Encode `str` into bytes only when necessary (e.g., file or network operations).

To convert bytes to a string:
```python
def to_str(bytes_or_str):
    if isinstance(bytes_or_str, bytes):
        return bytes_or_str.decode("utf-8")
    return bytes_or_str
```

To convert a string to bytes:
```python
def to_bytes(bytes_or_str):
    if isinstance(bytes_or_str, str):
        return bytes_or_str.encode("utf-8")
    return bytes_or_str
```

When reading or writing binary data to files, use `"rb"` and `"wb"` modes.

---

#### **Item 4: Prefer Interpolated F-String Over C-style Format Strings and `str.format`**

Avoid older string formatting techniques:
- **Don't use C-style formatting** like this:
```python
"%(do_not)s use C-style strings" % {"do_not": "Avoid"}
```

- **Avoid using `str.format`**:
```python
"{do_not} use this one".format("Avoid")
```

- **Use f-strings (Python 3.6+) instead**:
```python
f_string = f'{use} {this} format'
```

F-strings allow embedding Python expressions directly in strings:
```python
pantry = [('avocados', 1.25), ('bananas', 2.5), ('cherries', 15)]
for i, (item, count) in enumerate(pantry):
    print(f"#{i+1}: {item.title():<10s} = {round(count)}")
```

You can also use f-strings for precision formatting:
```python
places = 3
number = 1.23456
print(f"My number is {number:.{places}f}")
```

---

#### **Item 5: Write Helper Functions Instead of Complex Expressions**

To improve readability, break complex expressions into simpler, reusable helper functions. For instance, extracting integer values from a query string can be done using helper functions:

```python
from urllib.parse import parse_qs

def get_first_int(values, key, default=0):
    found = values.get(key, [""])
    if found[0]:
        return int(found[0])
    return default

my_values = {'red': ['5'], 'blue': ['0'], 'green': ['']}
red = get_first_int(my_values, "red")
blue = get_first_int(my_values, "blue")
green = get_first_int(my_values, "green")
print(red, blue, green)
```

This approach makes the code more readable and maintainable.

---

#### **Item 6: Prefer Multiple Assignments Unpacking Over Indexing**

Python’s tuple unpacking allows cleaner and more expressive code. For example, you can unpack the elements of a tuple into individual variables:

```python
item = ("Peanut butter", "Jelly")
first, second = item
print(f"{first} and {second}")
```

Unpacking can be used in loops as well:
```python
snacks = [("bacon", 350), ("donut", 240), ("muffin", 190)]
for rank, (name, calories) in enumerate(snacks, 1):
    print(f"#{rank}: {name} has {calories} calories")
```

---

#### **Item 7: Prefer `enumerate()` Over `range()`**

While you can loop over sequences using `range()`, it’s more Pythonic to use `enumerate()` to directly access both the index and the element:

```python
flavor_list = ["vanilla", "chocolate", "pecan", "strawberry"]
for i, flavor in enumerate(flavor_list, 1):
    print(f"{i}: {flavor}")
```

This is clearer and eliminates the need to manually index lists.

---

#### **Item 8: Use `zip()` to Process Iterators in Parallel**

To iterate over two or more sequences simultaneously, use `zip()`:

```python
names = ["Cecilia", "Lise", "Marie"]
counts = [7, 4, 5]

for name, count in zip(names, counts):
    print(f"{name} has {count} letters")
```

If the sequences are of different lengths, `zip()` stops at the shortest sequence. Use `itertools.zip_longest()` for longer sequences.

---

#### **Item 9: Avoid `else` Blocks After `for` and `while` Loops**

Although `else` blocks can follow `for` and `while` loops, they behave differently than `else` in `if` statements. In loops, `else` runs after the loop finishes unless the loop is exited via `break`. However, relying on this behavior can make the code harder to read.

---

#### **Item 10: Prevent Repetition with Assignment Expressions**

Python 3.8 introduced the **walrus operator (`:=`)**, which allows assignment inside expressions. It’s useful for eliminating repetition, particularly when you want to both assign a value and use it in the same expression:

```python
if (count := fresh_fruit.get("banana", 0)) >= 2:
    pieces = slice_bananas(count)
    smoothies = make_smoothies(pieces)
```

It can also be used to simulate `do-while` loops, where you want to repeatedly assign and check a value in a loop condition:

```python
while (fresh_fruit := pick_fruit()):
    for fruit, count in fresh_fruit.items():
        batch = make_juice(fruit, count)
```

This avoids redundancy and streamlines the code.