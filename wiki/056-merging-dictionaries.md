## 56. How do you merge two dictionaries in Python?


In Python, there are several ways to merge two dictionaries. Here are the most common methods:

### 1. **Using the `update()` Method**

The `update()` method merges the keys and values of one dictionary into another dictionary. It modifies the original dictionary in place.

**Example:**
```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}

dict1.update(dict2)
print(dict1)  # Output: {'a': 1, 'b': 3, 'c': 4}
```

- **Explanation:** The `update()` method adds the key-value pairs from `dict2` to `dict1`. If there is a key conflict, the value from `dict2` overwrites the value in `dict1`.

### 2. **Using the `|` Operator (Python 3.9+)**

Starting from Python 3.9, you can use the `|` operator to merge two dictionaries. This operation returns a new dictionary and does not modify the original ones.

**Example:**
```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}

merged_dict = dict1 | dict2
print(merged_dict)  # Output: {'a': 1, 'b': 3, 'c': 4}
```

- **Explanation:** The `|` operator creates a new dictionary containing the key-value pairs from both `dict1` and `dict2`. In case of key conflicts, the value from `dict2` takes precedence.

### 3. **Using Dictionary Unpacking (`**`)**

You can also merge dictionaries using dictionary unpacking (`**`). This method creates a new dictionary by unpacking the key-value pairs of both dictionaries.

**Example:**
```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}

merged_dict = {**dict1, **dict2}
print(merged_dict)  # Output: {'a': 1, 'b': 3, 'c': 4}
```

- **Explanation:** The `**` operator unpacks the key-value pairs of each dictionary into a new dictionary. In case of key conflicts, the value from the later dictionary (`dict2`) overrides the value from the earlier one (`dict1`).

### 4. **Using the `collections.ChainMap` Class**

The `collections.ChainMap` class can be used to merge multiple dictionaries. This approach does not create a new dictionary but rather a view that combines multiple dictionaries.

**Example:**
```python
from collections import ChainMap

dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}

merged = ChainMap(dict1, dict2)
print(dict(merged))  # Output: {'a': 1, 'b': 2, 'c': 4}
```

- **Explanation:** `ChainMap` groups multiple dictionaries together. Lookups will first search in `dict1`, and if the key is not found, they will continue to `dict2`. Unlike the previous methods, `ChainMap` preserves the order of dictionaries and does not overwrite values.

### Summary

- **`update()` Method:** Modifies the original dictionary in place.
- **`|` Operator (Python 3.9+):** Merges dictionaries and returns a new one.
- **Dictionary Unpacking (`**`):** Merges dictionaries into a new dictionary using unpacking.
- **`collections.ChainMap`:** Provides a combined view of multiple dictionaries without creating a new dictionary.

Choose the method that best fits your use case, whether you need to modify an existing dictionary, create a new one, or work with a combined view of multiple dictionaries.