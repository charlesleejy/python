## 51. How do you implement a stack in Python?


### Implementing a Stack in Python

A **stack** is a data structure that follows the Last In, First Out (LIFO) principle. The most recent element added to the stack is the first one to be removed. Common operations on a stack include:

- **Push:** Add an element to the top of the stack.
- **Pop:** Remove and return the element from the top of the stack.
- **Peek:** Return the element at the top of the stack without removing it.
- **isEmpty:** Check if the stack is empty.

### Implementing a Stack Using a List

Python’s built-in list can be used to implement a stack because lists provide `append()` and `pop()` methods, which are ideal for stack operations.

```python
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, item):
        """Add an item to the top of the stack."""
        self.stack.append(item)

    def pop(self):
        """Remove and return the item from the top of the stack."""
        if not self.is_empty():
            return self.stack.pop()
        else:
            return "Stack is empty"

    def peek(self):
        """Return the item at the top of the stack without removing it."""
        if not self.is_empty():
            return self.stack[-1]
        else:
            return "Stack is empty"

    def is_empty(self):
        """Check if the stack is empty."""
        return len(self.stack) == 0

    def size(self):
        """Return the number of items in the stack."""
        return len(self.stack)
```

### Example Usage

```python
# Create a stack
my_stack = Stack()

# Push items onto the stack
my_stack.push(1)
my_stack.push(2)
my_stack.push(3)

# Check the top item
print(my_stack.peek())  # Output: 3

# Pop items from the stack
print(my_stack.pop())   # Output: 3
print(my_stack.pop())   # Output: 2

# Check if the stack is empty
print(my_stack.is_empty())  # Output: False

# Pop the last item
print(my_stack.pop())   # Output: 1

# Try to pop from an empty stack
print(my_stack.pop())   # Output: Stack is empty

# Check if the stack is empty again
print(my_stack.is_empty())  # Output: True
```

### Implementing a Stack Using `collections.deque`

Another way to implement a stack is to use `collections.deque`, which is optimized for fast append and pop operations from both ends.

```python
from collections import deque

class Stack:
    def __init__(self):
        self.stack = deque()

    def push(self, item):
        self.stack.append(item)

    def pop(self):
        if not self.is_empty():
            return self.stack.pop()
        else:
            return "Stack is empty"

    def peek(self):
        if not self.is_empty():
            return self.stack[-1]
        else:
            return "Stack is empty"

    def is_empty(self):
        return len(self.stack) == 0

    def size(self):
        return len(self.stack)
```

### Summary

- A **stack** is a LIFO (Last In, First Out) data structure.
- **List-based implementation:** Python’s list can be easily used to implement a stack with `append()` for push and `pop()` for pop operations.
- **Deque-based implementation:** `collections.deque` provides a more efficient stack implementation, especially for larger stacks.
- Basic stack operations include `push`, `pop`, `peek`, `is_empty`, and `size`.