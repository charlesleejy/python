### Role of `property()` and `@property` Decorator in Python

The `property()` function and the `@property` decorator in Python are tools used to implement **encapsulation** and to provide a cleaner and more Pythonic way to define **getter**, **setter**, and **deleter** methods. These methods allow you to access and modify the **private or protected attributes** of a class, while still maintaining control over how those attributes are accessed and modified.

---

### 1. **The `property()` Function**

The **`property()` function** is used to create property attributes in a class. It allows you to convert method calls into attribute access and is commonly used to define getter and setter methods in an elegant way. By using the `property()` function, you can bind getter, setter, and deleter functions to an attribute, allowing for more controlled access to the attribute.

#### Syntax of `property()`:

```python
property(fget=None, fset=None, fdel=None, doc=None)
```

- **`fget`**: Function to get the attribute value.
- **`fset`**: Function to set the attribute value.
- **`fdel`**: Function to delete the attribute.
- **`doc`**: Optional documentation string.

#### Example Using `property()`:

```python
class Person:
    def __init__(self, name):
        self._name = name

    # Getter method
    def get_name(self):
        return self._name

    # Setter method
    def set_name(self, value):
        if isinstance(value, str) and len(value) > 0:
            self._name = value
        else:
            raise ValueError("Name must be a non-empty string.")

    # Defining property for name using property()
    name = property(get_name, set_name)

# Using the Person class
person = Person("John")
print(person.name)   # Output: John

person.name = "Alice"
print(person.name)   # Output: Alice

# Trying to set an invalid name will raise an error
# person.name = ""  # Raises ValueError
```

**Explanation**:
- The `property()` function is used to define `name` as a property. It ties the `get_name` method to the getter and the `set_name` method to the setter.
- Now, `person.name` can be accessed like an attribute, but it uses the `get_name` and `set_name` methods behind the scenes.

---

### 2. **The `@property` Decorator**

The **`@property` decorator** is a more Pythonic and cleaner way to define properties in Python. It allows you to define a getter method first and then attach the setter and deleter methods using `@<attribute>.setter` and `@<attribute>.deleter` decorators. This approach makes your code more readable and concise.

#### Example Using `@property` Decorator:

```python
class Person:
    def __init__(self, name):
        self._name = name

    # Getter method using @property decorator
    @property
    def name(self):
        return self._name

    # Setter method using @name.setter decorator
    @name.setter
    def name(self, value):
        if isinstance(value, str) and len(value) > 0:
            self._name = value
        else:
            raise ValueError("Name must be a non-empty string.")

# Using the Person class
person = Person("John")
print(person.name)   # Output: John

person.name = "Alice"
print(person.name)   # Output: Alice

# Trying to set an invalid name will raise an error
# person.name = ""  # Raises ValueError
```

**Explanation**:
- The `@property` decorator is used to create a getter method for the `name` attribute.
- The `@name.setter` decorator is then used to define a setter method that controls how `name` is set.
- The `name` attribute can now be accessed and modified like a regular attribute, but the getter and setter methods provide encapsulation and validation.

---

### Key Differences Between `property()` and `@property` Decorator

| **Aspect**                      | **`property()` Function**                           | **`@property` Decorator**                        |
|----------------------------------|----------------------------------------------------|--------------------------------------------------|
| **Syntax**                       | Requires calling `property()` explicitly.          | Uses decorators, making the code more concise.   |
| **Readability**                  | Can be less readable with complex getter/setter methods. | More Pythonic and clean with easy-to-read syntax.|
| **Definition of Getter/Setter**  | Methods are passed as arguments to `property()`.   | Uses `@property` for getter and `@<attribute>.setter` for setter. |
| **Use Case**                     | Typically used for older code or when backward compatibility is needed. | Preferred for modern Python code for clarity and simplicity. |

---

### Example: Full Use of Getter, Setter, and Deleter with `@property`

You can also define **deleters** for attributes using `@<attribute>.deleter`. This allows you to control how attributes are deleted.

```python
class Person:
    def __init__(self, name):
        self._name = name

    # Getter method using @property
    @property
    def name(self):
        return self._name

    # Setter method using @name.setter
    @name.setter
    def name(self, value):
        if isinstance(value, str) and len(value) > 0:
            self._name = value
        else:
            raise ValueError("Name must be a non-empty string.")

    # Deleter method using @name.deleter
    @name.deleter
    def name(self):
        print("Deleting name...")
        del self._name

# Using the Person class
person = Person("John")
print(person.name)   # Output: John

person.name = "Alice"  # Using the setter
print(person.name)   # Output: Alice

del person.name      # Using the deleter
# Output: Deleting name...
```

**Explanation**:
- `@property` defines the getter method for `name`.
- `@name.setter` defines the setter method, allowing controlled modifications.
- `@name.deleter` defines how the `name` attribute is deleted, allowing you to add custom behavior when the attribute is deleted (e.g., logging or cleanup).

---

### Benefits of Using `@property` Decorator

1. **Cleaner Syntax**: Using the `@property` decorator provides a more readable and concise way to define getters and setters. It avoids having to use the `property()` function explicitly, making the code more Pythonic.
   
2. **Encapsulation**: The `@property` decorator allows you to control access to private attributes. This means you can keep attributes private and control how they are read, written, or deleted, providing better encapsulation and validation.

3. **Consistency**: `@property` lets you maintain a consistent interface. Initially, you can expose attributes directly, and later, when you need more control (like validation), you can add a getter and setter without changing how the attribute is accessed externally.

4. **Flexibility**: With `@property`, you can change the internal implementation of attributes without changing how the class is used. For example, you can initially expose a simple attribute, but later add more complex logic in getter and setter methods without breaking the interface.

---

### Summary of `property()` and `@property`

- **`property()`**: A function used to define getter, setter, and deleter methods for attributes. It takes functions as arguments to define the behavior of accessing and modifying attributes. This is a more manual approach to defining properties.
  
- **`@property` Decorator**: A more Pythonic and clean way to define properties. It allows you to define getter, setter, and deleter methods using decorators. This approach makes the code more readable and intuitive while providing encapsulation and validation.

### When to Use
- Use `@property` when you want to **control attribute access** with a clean and Pythonic syntax. It’s the preferred approach in modern Python code.
- Use `property()` if you need to stick to older coding styles or need more explicit control over getter, setter, and deleter functions, although `@property` is generally more recommended for readability.

By using `@property`, you can create clean, maintainable, and encapsulated classes that provide attribute-like access while still allowing for logic such as validation, logging, or side-effects during access and modification.