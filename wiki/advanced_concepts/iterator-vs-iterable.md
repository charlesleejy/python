## What is the difference between an iterator and an iterable?


### Difference Between an Iterator and an Iterable in Python

**Iterators** and **iterables** are related concepts in Python, but they serve different purposes. Understanding the distinction between them is key to effectively working with loops, sequences, and data streams in Python.

### 1. **Iterable**

- **Definition:** An iterable is any Python object that can return an iterator. An object is considered iterable if it implements the `__iter__()` method, which returns an iterator object. Common examples of iterables include lists, tuples, strings, dictionaries, and sets.
- **Examples:** Lists, tuples, strings, dictionaries, sets, and files are all iterable objects.
- **How It Works:** When you use a `for` loop on an iterable, Python internally calls the `__iter__()` method on the object, which returns an iterator. The loop then repeatedly calls the `__next__()` method on the iterator to get each element, until the `StopIteration` exception is raised.

- **Example:**
  ```python
  my_list = [1, 2, 3]
  for item in my_list:
      print(item)
  ```
  - **Explanation:** `my_list` is an iterable, so you can loop over it. The `for` loop automatically creates an iterator from the list and retrieves each element.

### 2. **Iterator**

- **Definition:** An iterator is an object that represents a stream of data. It implements the `__iter__()` method (which returns the iterator object itself) and the `__next__()` method (which returns the next item in the sequence). When there are no more items to return, `__next__()` raises a `StopIteration` exception.
- **Examples:** Any object that implements the iterator protocol (i.e., both `__iter__()` and `__next__()` methods) is an iterator. You can create an iterator using the `iter()` function on an iterable.

- **How It Works:** An iterator keeps track of its position in the sequence and fetches elements one at a time using the `__next__()` method. When the iterator is exhausted, `__next__()` raises a `StopIteration` exception, signaling the end of the iteration.

- **Example:**
  ```python
  my_list = [1, 2, 3]
  my_iter = iter(my_list)

  print(next(my_iter))  # Output: 1
  print(next(my_iter))  # Output: 2
  print(next(my_iter))  # Output: 3
  # print(next(my_iter))  # Raises StopIteration
  ```
  - **Explanation:** `my_iter` is an iterator created from `my_list`. Each call to `next(my_iter)` retrieves the next item from the list until `StopIteration` is raised.

### Key Differences Between Iterators and Iterables

1. **Definition:**
   - **Iterable:** An object capable of returning an iterator. It must implement the `__iter__()` method.
   - **Iterator:** An object that allows you to iterate over a sequence of values. It must implement both the `__iter__()` and `__next__()` methods.

2. **Usage:**
   - **Iterable:** Can be passed to a `for` loop or any function that expects an iterable, like `sum()`, `min()`, or `sorted()`.
   - **Iterator:** Used to fetch elements one at a time, typically using the `next()` function.

3. **State:**
   - **Iterable:** Does not maintain any state; a new iterator is created each time you iterate over it.
   - **Iterator:** Maintains state between calls to `next()`, remembering the current position in the sequence.

4. **Examples:**
   - **Iterable:** Lists, tuples, dictionaries, strings, sets.
   - **Iterator:** The object returned by `iter()` when called on an iterable.

### Summary

- An **iterable** is any Python object that can be looped over (e.g., lists, strings, tuples). It returns an iterator when the `__iter__()` method is called, enabling iteration.
- An **iterator** is an object that produces the items of a sequence one at a time. It keeps track of its current position and raises `StopIteration` when there are no more items to return.

In summary, **all iterators are iterables**, but not all iterables are iterators. An iterable can be used to create an iterator, which can then be used to access the elements one by one using `next()`.