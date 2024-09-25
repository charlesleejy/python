## 96. How do you use `staticmethod` and `classmethod` in Python?


In Python, `staticmethod` and `classmethod` are decorators that define methods within a class that are not bound to an instance of the class. They allow you to define methods that can be called on the class itself rather than on an instance. Here’s how they work:

### 1. **`staticmethod`**

A `staticmethod` is a method that does not require access to the instance (`self`) or class (`cls`) within which it is defined. It behaves like a regular function but belongs to the class’s namespace.

#### **When to Use `staticmethod`**

- Use `staticmethod` when the method doesn’t need to access or modify class or instance attributes.
- It is used to group functions that logically belong to the class but don’t need to interact with its state.

#### **How to Define and Use `staticmethod`**

**Example:**

```python
class MathOperations:
    @staticmethod
    def add(a, b):
        return a + b

    @staticmethod
    def multiply(a, b):
        return a * b

# Usage
print(MathOperations.add(5, 3))       # Output: 8
print(MathOperations.multiply(5, 3))  # Output: 15
```

- **Explanation:** The `add` and `multiply` methods are defined as `staticmethod`s, so they can be called on the class without needing an instance. They don’t interact with the class or instance state.

### 2. **`classmethod`**

A `classmethod` is a method that receives the class as its first argument, conventionally named `cls`. It can access and modify class state that applies across all instances of the class.

#### **When to Use `classmethod`**

- Use `classmethod` when you need to access or modify the class state or when you need an alternative constructor for the class.
- It is commonly used for factory methods that return an instance of the class.

#### **How to Define and Use `classmethod`**

**Example:**

```python
class Employee:
    raise_percentage = 1.05  # Class attribute

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    @classmethod
    def set_raise_percentage(cls, percentage):
        cls.raise_percentage = percentage

    @classmethod
    def from_string(cls, employee_string):
        name, salary = employee_string.split('-')
        return cls(name, float(salary))

    def apply_raise(self):
        self.salary *= self.raise_percentage

# Usage
Employee.set_raise_percentage(1.10)  # Modify class attribute
emp = Employee.from_string("John-50000")  # Create instance using a class method

print(emp.name)   # Output: John
print(emp.salary) # Output: 50000
emp.apply_raise()
print(emp.salary) # Output: 55000
```

- **Explanation:** 
  - `set_raise_percentage` is a `classmethod` that modifies the class attribute `raise_percentage`.
  - `from_string` is a factory method that allows creating an `Employee` instance from a string.
  - The `apply_raise` method then uses the `raise_percentage` to modify the instance’s salary.

### Key Differences Between `staticmethod` and `classmethod`

1. **First Argument:**
   - `staticmethod`: Does not receive `self` or `cls` as its first argument.
   - `classmethod`: Receives `cls` as its first argument, allowing access to class attributes and methods.

2. **Usage Context:**
   - `staticmethod`: Used for methods that don’t need to interact with the class or instance.
   - `classmethod`: Used for methods that need to interact with class-level data or require alternative constructors.

### Summary

- **`staticmethod`:** Defines a method that doesn’t interact with the class or instance. Use it for utility methods that logically belong to a class but don’t need access to the class’s state.
- **`classmethod`:** Defines a method that interacts with the class itself, not the instance. Use it for factory methods, modifying class attributes, or implementing alternative constructors.

These decorators help organize your code by clearly separating methods that operate on instances, classes, or neither, making your code more readable and maintainable.