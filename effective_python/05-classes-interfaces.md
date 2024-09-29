### **Chapter 5. Classes and Interfaces**

Python is an object-oriented language, supporting essential features such as inheritance, polymorphism, and encapsulation. These features allow developers to build reusable, maintainable, and scalable code by organizing their programs around the idea of objects and interfaces. This chapter delves into advanced concepts around class composition, refactoring, and techniques to improve design through abstraction.

---

#### **Item 37: Compose Classes Instead of Nesting Many Levels of Built-in Types**

Python's built-in types like dictionaries and lists are excellent for managing dynamic internal states. However, overusing them for complex data structures often leads to hard-to-maintain code. When you find yourself nesting multiple levels of built-in types, it's a sign that you should refactor to a hierarchy of classes.

#### **Why Not Use Just Dictionaries?**

Consider a scenario where we need to store students' grades. The easiest way might be to use a dictionary to store each student's grades:

```python
class SimpleGradebook:
    def __init__(self):
        self._grades = {}
    def add_student(self, name):
        self._grades[name] = []
    def report_grade(self, name, score):
        self._grades[name].append(score)
    def average_grade(self, name):
        grades = self._grades[name]
        return sum(grades) / len(grades)
```

While this works for simple cases, complications arise when you want to extend functionality. For example, storing grades by subject would result in more deeply nested dictionaries, which leads to more complex code that's difficult to read and maintain.

#### **When To Refactor into Classes**

Instead of nesting dictionaries, refactor to a hierarchy of classes. This allows you to encapsulate logic for specific behaviors and interactions within classes, making your code modular and easier to follow.

Start by breaking down your problem into clear entities and use classes to represent those entities. In the grades example, we could define classes for a `Grade`, `Subject`, and `Student`. This refactor leads to more readable code and a better organization of logic:

```python
class Grade:
    def __init__(self, score, weight):
        self.score = score
        self.weight = weight

class Subject:
    def __init__(self):
        self._grades = []
    def report_grade(self, score, weight):
        self._grades.append(Grade(score, weight))
    def average_grade(self):
        total, total_weight = 0, 0
        for grade in self._grades:
            total += grade.score * grade.weight
            total_weight += grade.weight
        return total / total_weight

class Student:
    def __init__(self):
        self._subjects = defaultdict(Subject)
    def get_subject(self, name):
        return self._subjects[name]
    def average_grade(self):
        total, count = 0, 0
        for subject in self._subjects.values():
            total += subject.average_grade()
            count += 1
        return total / count
```

By refactoring the functionality into these classes, the code becomes easier to understand, extend, and maintain.

---

#### **Item 38: Accept Functions Instead of Classes for Simple Interfaces**

Python treats functions as first-class objects, meaning they can be passed as arguments, returned from other functions, and assigned to variables. For simple interfaces, using functions instead of full-fledged classes can lead to more concise and flexible code.

#### **Example: Using a Function with `defaultdict`**

A classic example is using functions as default values in `defaultdict`. Instead of writing an entire class to handle missing keys, you can pass a simple function:

```python
from collections import defaultdict

def log_missing():
    print("Key added")
    return 0

current = {"green": 12, "blue": 3}
increments = [("red", 5), ("blue", 17), ("orange", 9)]

result = defaultdict(log_missing, current)
for key, amount in increments:
    result[key] += amount

print(dict(result))
```

In this example, when a missing key is encountered, the `log_missing` function is called, which prints a message and returns 0.

#### **Simplifying Stateful Functions with Closures**

If you need state, you can use a closure instead of a class:

```python
def increment_with_report(current, increments):
    added_count = 0
    def missing():
        nonlocal added_count
        added_count += 1
        return 0
    result = defaultdict(missing, current)
    for key, amount in increments:
        result[key] += amount
    return result, added_count
```

Here, the `missing` function maintains state using the `nonlocal` keyword. This is simpler than creating a full class and reduces the need for extra boilerplate code.

#### **Callable Objects**

If you need more complex behavior or state, you can use callable objects with the `__call__` method:

```python
class BetterCountMissing:
    def __init__(self):
        self.added = 0
    def __call__(self):
        self.added += 1
        return 0
```

This allows the object to behave like a function, but with the ability to maintain state.

---

#### **Item 39: Use `@classmethod` Polymorphism to Construct Objects Generically**

Polymorphism allows objects to be used interchangeably even if they are from different classes, as long as they implement the same interface. This concept also applies to classes themselves, enabling you to write generic class methods that can operate on multiple subclasses.

#### **Example: Generic Input Classes in a MapReduce Framework**

In a MapReduce framework, you might want different types of input data, but a common interface to process them. Here's how you can design such a framework using `@classmethod` for polymorphic construction:

```python
class InputData:
    def read(self):
        raise NotImplementedError
    @classmethod
    def generate_inputs(cls, config):
        raise NotImplementedError

class PathInputData(InputData):
    def __init__(self, path):
        self.path = path
    def read(self):
        with open(self.path) as f:
            return f.read()
    @classmethod
    def generate_inputs(cls, config):
        data_dir = config['data_dir']
        for name in os.listdir(data_dir):
            yield cls(os.path.join(data_dir, name))
```

This allows `generate_inputs` to create instances of `PathInputData` (or any other subclass) generically, making it easy to extend the system with new types of input.

---

#### **Item 40: Initialize Parent Classes with `super`**

In Python, using `super()` allows you to initialize parent classes in a controlled manner. This is especially important when dealing with multiple inheritance.

#### **Example: Problems with Direct Initialization**

If you directly call parent class constructors, especially in cases of multiple inheritance, it can lead to incorrect behavior, such as the diamond problem:

```python
class TimesTwo:
    def __init__(self):
        self.value *= 2

class PlusFive:
    def __init__(self):
        self.value += 5

class OneWay(MyBaseClass, TimesTwo, PlusFive):
    def __init__(self, value):
        MyBaseClass.__init__(self, value)
        TimesTwo.__init__(self)
        PlusFive.__init__(self)
```

Using `super()` solves these issues and ensures that parent classes are initialized in the correct order.

```python
class TimesSeven(MyBaseClass):
    def __init__(self, value):
        super().__init__(value)
        self.value *= 7

class PlusNine(MyBaseClass):
    def __init__(self, value):
        super().__init__(value)
        self.value += 9

class GoodWay(TimesSeven, PlusNine):
    def __init__(self, value):
        super().__init__(value)
```

The order of initialization is controlled by Python's method resolution order (MRO), which can be inspected with `ClassName.mro()`.

---

#### **Item 41: Consider Composing Functionality with Mix-in Classes**

Mix-ins are a form of multiple inheritance where a class provides specific functionality without requiring its own state or constructor. Mix-ins allow you to compose small, reusable components and avoid the complexities of deep inheritance hierarchies.

#### **Example: Serializing Objects to Dictionaries**

Consider a mix-in that provides a `to_dict` method, enabling objects to convert themselves into dictionaries:

```python
class ToDictMixin:
    def to_dict(self):
        return self._traverse_dict(self.__dict__)
    def _traverse_dict(self, instance_dict):
        output = {}
        for key, value in instance_dict.items():
            output[key] = self._traverse(key, value)
        return output
```

You can now easily extend this functionality to other classes:

```python
class BinaryTree(ToDictMixin):
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right
```

---

#### **Item 42: Prefer Public Attributes Over Private Ones**

In Python, there are public and private attributes. However, private attributes are more of a convention in Python. It's better to prefer public attributes in most cases, as Python emphasizes openness and simplicity. Use private attributes only when you need to protect against accidental name collisions.

#### **Example: Accessing Public vs Private Fields**

```python
class MyObject:
    def __init__(self):
        self.public_field = 5
        self.__private_field = 10
```

The private attribute `__private_field` is inaccessible outside the class due to name mangling, but public attributes can be accessed directly. For maintainability, document your public attributes clearly, and avoid unnecessary use of private attributes unless dealing with sensitive data.

---

#### **Item 43: Inherit from `collections.abc` for Custom Container Types**

Python's `collections.abc` module provides abstract base classes (ABCs) for common container types like `list`, `dict`, and `set`. By inheriting from these classes, you can create custom container types that behave like the built-in types but with added functionality.

#### **Example: Creating a Custom Sequence Type**

```python
from collections.abc import Sequence

class SequenceNode(Sequence):
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
    def __len__(self):
        # Implement length based on your structure
        pass
    def __getitem__(self, index):
        # Implement getitem for indexing
        pass
```

By inheriting from `Sequence`, you only need to implement a few methods, and Python will provide the rest of the sequence behavior (e.g., slicing, indexing, etc.).

---