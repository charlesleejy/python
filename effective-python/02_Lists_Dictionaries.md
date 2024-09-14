### Chapter 2. Lists and Dictionaries

---

#### **Item 11: Know How to Slice Sequences**

In Python, slicing allows you to extract parts of sequences like lists, strings, and bytes. Here’s the basic slicing syntax:

```python
somelist[start:end]
```

Here are examples of different slicing variations:

```python
a = ["a", "b", "c", "d", "e", "f", "g", "h"]

a[:]     # ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
a[:5]    # ['a', 'b', 'c', 'd', 'e']
a[:-1]   # ['a', 'b', 'c', 'd', 'e', 'f', 'g']
a[4:]    # ['e', 'f', 'g', 'h']
a[-3:]   # ['f', 'g', 'h']
a[2:5]   # ['c', 'd', 'e']
a[2:-1]  # ['c', 'd', 'e', 'f', 'g']
a[-3:-1] # ['f', 'g']
```

- Slicing doesn’t raise an error if indices are out of range. You can use this behavior to limit results to a max length:
```python
first_twenty_items = a[:20]
last_twenty_items = a[-20:]
```

- **Negative indexes** can be tricky, e.g., `somelist[-0:]` is equivalent to `somelist[:]`.

- Slicing creates a **new list**, leaving the original list unchanged:
```python
b = a[3:]
print("Before:  ", b)
b[1] = 99
print("After:   ", b)
print("No change:", a)
```

However, when you assign a slice, it replaces the original range:
```python
a[2:7] = [99, 00, 888]
print(a)
```

To **copy** the list, use:
```python
b = a[:]
```

To **replace** the entire list:
```python
a[:] = [101, 102, 103]
```

---

#### **Item 12: Avoid Striding and Slicing in a Single Expression**

Striding allows you to skip elements in a sequence using the syntax:

```python
somelist[start:end:stride]
```

Examples:
```python
x = ["red", "orange", "yellow", "green", "blue", "purple"]
odds = x[::2]
evens = x[1::2]
print(odds)
print(evens)
```

Reversing a byte string:
```python
x = b"mongoose"
y = x[::-1]
print(y)
```

For **UTF-8 strings**, reversing works similarly, but be cautious with **unicode** byte strings.

Complex examples:
```python
x[::2]      # ['a', 'c', 'e', 'g']
x[::-2]     # ['h', 'f', 'd', 'b']
x[2::2]     # ['c', 'e', 'g']
x[-2::-2]   # ['g', 'e', 'c', 'a']
```

While you can combine **striding** and **slicing**, it’s often better to separate them for clarity:
```python
y = x[::2]
z = x[1:-1]
```

---

#### **Item 13: Prefer Catch-All Unpacking Over Slicing**

With **catch-all unpacking**, you don’t need to know the exact length of a list. The starred expression (`*`) helps capture remaining values.

Example:
```python
car_ages = [0, 9, 4, 8, 7, 20, 19, 1, 6, 15]
car_ages_descending = sorted(car_ages, reverse=True)
oldest, second_oldest, *others = car_ages_descending
print(oldest, second_oldest, others)
```

You can use the starred expression anywhere:
```python
oldest, *others, youngest = car_ages_descending
print(oldest, youngest, others)
```

**Note**:
- You must have at least one non-starred element.
```python
*others = car_ages_descending
```
Raises:
```python
SyntaxError: starred assignment target must be in a list or tuple
```

Multiple starred expressions are not allowed:
```python
first, *middle, *second_middle, last = [1, 2, 3, 4]
```
Raises:
```python
SyntaxError: two starred expressions in assignment
```

---

#### **Item 14: Sort by Complex Criteria Using `key` Parameter**

Python’s `sort()` method works on built-in types. For custom objects or more complex criteria, use the `key` parameter, which takes a function.

Example with custom objects:
```python
class Tool:
    def __init__(self, name, weight):
        self.name = name
        self.weight = weight

    def __repr__(self):
        return f"Tool({self.name!r}, {self.weight})"

tools = [Tool("level", 3.5), Tool("hammer", 1.25), Tool("chisel", 0.25)]
tools.sort(key=lambda x: x.name)
print(tools)
```

For case-insensitive sorting:
```python
places = ["home", "work", "New York", "Paris"]
places.sort(key=lambda x: x.lower())
```

Sorting with multiple criteria:
```python
power_tools.sort(key=lambda x: (x.weight, x.name))
```

---

#### **Item 15: Be Cautious When Relying on `dict` Insertion Ordering**

Starting with Python 3.6, `dict` maintains insertion order. However, don’t rely on this behavior in earlier versions. Instead, consider using `OrderedDict` from the `collections` module.

To preserve insertion order:
```python
from collections.abc import MutableMapping

class SortedDict(MutableMapping):
    def __iter__(self):
        keys = list(self.data.keys())
        keys.sort()
        for key in keys:
            yield key
```

---

#### **Item 16: Prefer `get` Over `in` and `KeyError` to Handle Missing Dictionary Keys**

When accessing dictionary keys, it’s common to handle cases where keys are missing.

Example:
```python
counter = {"pumpernickel": 2, "sourdough": 1}
count = counter.get("wheat", 0)
counter["wheat"] = count + 1
```

Instead of:
```python
if key in counter:
    count = counter[key]
else:
    count = 0
```

You can also use the `KeyError` exception for error handling:
```python
try:
    count = counter[key]
except KeyError:
    count = 0
```

The `get` method is usually the cleanest and most efficient approach.

---

#### **Item 17: Prefer `defaultdict` Over `setdefault` for Handling Missing Items in Internal State**

When managing complex dictionary structures, use `defaultdict` to handle missing keys automatically:

```python
from collections import defaultdict

class Visits:
    def __init__(self):
        self.data = defaultdict(set)

    def add(self, country, city):
        self.data[country].add(city)

visits = Visits()
visits.add("England", "London")
```

---

#### **Item 18: Know How to Construct Key-Dependent Default Values with `__missing__`**

For more complex scenarios, you can define a custom `__missing__` method in a dictionary subclass to handle missing keys efficiently.

Example:
```python
class Pictures(dict):
    def __missing__(self, key):
        value = open_picture(key)
        self[key] = value
        return value

pictures = Pictures()
handle = pictures[path]
```

This approach can be more elegant than using `defaultdict` or `setdefault` when custom behavior is needed.