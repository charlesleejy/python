## How do you sort a list in Python?


### Sorting a List in Python

Python provides several ways to sort a list, either in-place (modifying the original list) or by returning a new sorted list. Here are the most common methods:

### 1. **Using the `sort()` Method**

The `sort()` method sorts a list in place, meaning it modifies the original list and does not return a new list.

- **Syntax:**
  ```python
  list.sort(key=None, reverse=False)
  ```
  - **`key`:** A function that serves as a key for the sort comparison. The default value is `None`.
  - **`reverse`:** A boolean value. If `True`, the list is sorted in descending order. The default is `False` (ascending order).

- **Example:**
  ```python
  numbers = [5, 2, 9, 1, 5, 6]
  numbers.sort()
  print(numbers)  # Output: [1, 2, 5, 5, 6, 9]
  ```

- **Example with `reverse=True`:**
  ```python
  numbers.sort(reverse=True)
  print(numbers)  # Output: [9, 6, 5, 5, 2, 1]
  ```

- **Example with `key`:**
  ```python
  words = ["apple", "banana", "cherry", "date"]
  words.sort(key=len)
  print(words)  # Output: ['date', 'apple', 'banana', 'cherry']
  ```
  - **Explanation:** The list is sorted by the length of the strings.

### 2. **Using the `sorted()` Function**

The `sorted()` function returns a new list that is sorted, leaving the original list unchanged.

- **Syntax:**
  ```python
  sorted(iterable, key=None, reverse=False)
  ```

- **Example:**
  ```python
  numbers = [5, 2, 9, 1, 5, 6]
  sorted_numbers = sorted(numbers)
  print(sorted_numbers)  # Output: [1, 2, 5, 5, 6, 9]
  print(numbers)         # Output: [5, 2, 9, 1, 5, 6] (original list is unchanged)
  ```

- **Example with `reverse=True`:**
  ```python
  sorted_numbers_desc = sorted(numbers, reverse=True)
  print(sorted_numbers_desc)  # Output: [9, 6, 5, 5, 2, 1]
  ```

- **Example with `key`:**
  ```python
  words = ["apple", "banana", "cherry", "date"]
  sorted_words = sorted(words, key=len)
  print(sorted_words)  # Output: ['date', 'apple', 'banana', 'cherry']
  ```

### 3. **Sorting a List of Tuples or Objects**

You can use the `key` parameter to sort a list of tuples or objects based on a specific element or attribute.

- **Example: Sorting a List of Tuples**
  ```python
  students = [("John", 25), ("Jane", 22), ("Dave", 30)]
  students.sort(key=lambda x: x[1])
  print(students)  # Output: [('Jane', 22), ('John', 25), ('Dave', 30)]
  ```
  - **Explanation:** The list is sorted by the second element of each tuple (the age).

- **Example: Sorting a List of Custom Objects**
  ```python
  class Student:
      def __init__(self, name, grade):
          self.name = name
          self.grade = grade

      def __repr__(self):
          return f"{self.name}: {self.grade}"

  students = [Student("John", 85), Student("Jane", 92), Student("Dave", 78)]
  students.sort(key=lambda s: s.grade)
  print(students)  # Output: [Dave: 78, John: 85, Jane: 92]
  ```

### Summary

- **`list.sort()`:** Sorts the list in place and returns `None`. It modifies the original list.
- **`sorted()`:** Returns a new sorted list, leaving the original list unchanged.
- Both `sort()` and `sorted()` can take a `key` parameter to specify custom sorting logic and a `reverse` parameter to sort in descending order.

Use `sort()` when you want to sort the list in place, and `sorted()` when you need a new sorted list while preserving the original list.