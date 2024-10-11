### How Do You Prevent a Class from Being Inherited in Python?

In Python, you can prevent a class from being inherited by using **final classes** or **metaclass-based approaches**. Unlike some other languages (like Java or C++) where you can directly declare a class as `final` to prevent inheritance, Python doesn't have built-in support for this. However, there are several techniques you can use to achieve this behavior.

---

### Methods to Prevent a Class from Being Inherited

#### 1. **Using `Final` from `typing` Module (Python 3.8+)**

Starting from Python 3.8, you can use the `Final` decorator from the `typing` module to indicate that a class should not be subclassed. Although this doesn't strictly prevent inheritance at runtime, it acts as a **type hint** and tools like **mypy** can be used to enforce this constraint during static analysis.

```python
from typing import Final

@Final
class BaseClass:
    def method(self):
        print("Base class method")

# This will raise a static type-checking error if you're using a type checker like mypy
class DerivedClass(BaseClass):  # Error: Cannot subclass 'BaseClass' because it is a final class
    pass
```

**Explanation**:
- The `@Final` decorator indicates that `BaseClass` is a final class and cannot be inherited.
- Static type checkers such as **mypy** will flag an error if you attempt to inherit from a final class.

---

#### 2. **Using a Custom Metaclass**

You can define a **custom metaclass** to prevent inheritance by raising an exception when a subclass is defined. Metaclasses allow you to customize the behavior of class creation, and in this case, you can use one to prevent subclasses from being created.

```python
# Custom metaclass that prevents inheritance
class NoInheritanceMeta(type):
    def __new__(cls, name, bases, attrs):
        for base in bases:
            if isinstance(base, NoInheritanceMeta):
                raise TypeError(f"Cannot inherit from {base.__name__}")
        return super().__new__(cls, name, bases, attrs)

# Base class with the custom metaclass
class BaseClass(metaclass=NoInheritanceMeta):
    pass

# Attempt to inherit from BaseClass will raise a TypeError
class DerivedClass(BaseClass):  # TypeError: Cannot inherit from BaseClass
    pass
```

**Explanation**:
- The custom metaclass `NoInheritanceMeta` raises a `TypeError` when an attempt is made to subclass a class that uses this metaclass.
- This approach enforces the prevention of inheritance at runtime, making it impossible to subclass `BaseClass`.

---

#### 3. **Using `__init_subclass__()` Method (Python 3.6+)**

The `__init_subclass__()` method in Python can be overridden to control the behavior of class inheritance. By overriding this method, you can raise an exception when a class tries to inherit from a specific class.

```python
class BaseClass:
    def __init_subclass__(cls, **kwargs):
        raise TypeError(f"Subclassing of {cls.__name__} is not allowed")

# Attempt to inherit from BaseClass will raise a TypeError
class DerivedClass(BaseClass):  # TypeError: Subclassing of DerivedClass is not allowed
    pass
```

**Explanation**:
- The `__init_subclass__()` method is called when a class is subclassed.
- By raising a `TypeError` in `__init_subclass__()`, you prevent the class from being inherited.

---

### Summary

To prevent a class from being inherited in Python, you can use several techniques depending on your requirements:

| **Method**                                | **Description**                                                                 |
|-------------------------------------------|---------------------------------------------------------------------------------|
| **Using `Final` from `typing` (Python 3.8+)** | Acts as a type hint, preventing inheritance during static type checking.        |
| **Custom Metaclass**                      | Enforces the restriction at runtime by raising an exception when a subclass is created. |
| **Overriding `__init_subclass__()`**      | Raises an error when a class is subclassed, preventing inheritance.             |

Each method provides a different level of enforcement, from static type checking (with `Final`) to runtime enforcement (with a custom metaclass or `__init_subclass__()`). Depending on your use case, one of these approaches can be used to ensure that your class cannot be inherited.