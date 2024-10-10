## How do you implement a queue in Python?


### Implementing a Queue in Python

A **queue** is a data structure that follows the First In, First Out (FIFO) principle. The first element added to the queue is the first one to be removed. Common operations on a queue include:

- **Enqueue:** Add an element to the end of the queue.
- **Dequeue:** Remove and return the element from the front of the queue.
- **Peek:** Return the element at the front of the queue without removing it.
- **isEmpty:** Check if the queue is empty.

### Implementing a Queue Using `collections.deque`

The `collections.deque` is the most efficient way to implement a queue in Python. It allows O(1) time complexity for appends and pops from both ends of the deque.

```python
from collections import deque

class Queue:
    def __init__(self):
        self.queue = deque()

    def enqueue(self, item):
        """Add an item to the end of the queue."""
        self.queue.append(item)

    def dequeue(self):
        """Remove and return the item from the front of the queue."""
        if not self.is_empty():
            return self.queue.popleft()
        else:
            return "Queue is empty"

    def peek(self):
        """Return the item at the front of the queue without removing it."""
        if not self.is_empty():
            return self.queue[0]
        else:
            return "Queue is empty"

    def is_empty(self):
        """Check if the queue is empty."""
        return len(self.queue) == 0

    def size(self):
        """Return the number of items in the queue."""
        return len(self.queue)
```

### Example Usage

```python
# Create a queue
my_queue = Queue()

# Enqueue items into the queue
my_queue.enqueue(1)
my_queue.enqueue(2)
my_queue.enqueue(3)

# Check the front item
print(my_queue.peek())  # Output: 1

# Dequeue items from the queue
print(my_queue.dequeue())  # Output: 1
print(my_queue.dequeue())  # Output: 2

# Check if the queue is empty
print(my_queue.is_empty())  # Output: False

# Dequeue the last item
print(my_queue.dequeue())  # Output: 3

# Try to dequeue from an empty queue
print(my_queue.dequeue())  # Output: Queue is empty

# Check if the queue is empty again
print(my_queue.is_empty())  # Output: True
```

### Implementing a Queue Using a List

You can also implement a queue using a Python list, but this is less efficient because `pop(0)` operations (dequeue) have O(n) time complexity due to the need to shift all elements.

```python
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, item):
        """Add an item to the end of the queue."""
        self.queue.append(item)

    def dequeue(self):
        """Remove and return the item from the front of the queue."""
        if not self.is_empty():
            return self.queue.pop(0)
        else:
            return "Queue is empty"

    def peek(self):
        """Return the item at the front of the queue without removing it."""
        if not self.is_empty():
            return self.queue[0]
        else:
            return "Queue is empty"

    def is_empty(self):
        """Check if the queue is empty."""
        return len(self.queue) == 0

    def size(self):
        """Return the number of items in the queue."""
        return len(self.queue)
```

### Summary

- A **queue** is a FIFO (First In, First Out) data structure.
- **Deque-based implementation:** `collections.deque` is the most efficient way to implement a queue in Python, with O(1) time complexity for both enqueue and dequeue operations.
- **List-based implementation:** While a list can be used to implement a queue, it is less efficient due to O(n) time complexity for dequeue operations.
- Basic queue operations include `enqueue`, `dequeue`, `peek`, `is_empty`, and `size`.