### What Are Abstract Classes in Python?

An **abstract class** in Python is a class that cannot be instantiated directly and is designed to be subclassed. It serves as a blueprint for other classes, enforcing certain methods or properties that must be implemented in any concrete (non-abstract) subclass. The purpose of abstract classes is to provide a common interface that all subclasses must follow, making sure that certain methods are implemented in the child classes, but leaving the actual implementation details up to them.

Abstract classes allow you to define methods that must be implemented in the subclasses but don’t provide an implementation themselves. This is useful in object-oriented programming (OOP) when you want to establish a common protocol across different subclasses but leave the actual method behavior to each subclass.

In Python, abstract classes are defined using the **`abc`** (Abstract Base Classes) module, which is part of the standard library.

---

### Key Characteristics of Abstract Classes:

1. **Cannot be Instantiated**: You cannot create an instance of an abstract class directly. The purpose of an abstract class is to be inherited by other classes.
   
2. **Must Have Abstract Methods**: Abstract classes contain one or more **abstract methods**. These methods are declared, but they don’t contain any implementation (body).
   
3. **Abstract Methods Must Be Overridden**: Any subclass of the abstract class must provide an implementation for all abstract methods.

4. **Partially Implemented Classes**: Abstract classes can also have fully implemented methods, but they must contain at least one abstract method.

5. **Use of `@abstractmethod` Decorator**: Abstract methods are defined using the `@abstractmethod` decorator, provided by the `abc` module.

---

### Defining Abstract Classes in Python

Abstract classes are defined by:
1. Importing the `abc` module.
2. Using `ABC` as the base class for your abstract class (where `ABC` stands for Abstract Base Class).
3. Marking methods as abstract using the `@abstractmethod` decorator.

#### Example of an Abstract Class:

```python
from abc import ABC, abstractmethod

# Defining an abstract class
class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
    
    @abstractmethod
    def perimeter(self):
        pass

# Trying to instantiate an abstract class will raise an error
# shape = Shape()  # This will raise TypeError: Can't instantiate abstract class Shape with abstract methods area, perimeter
```

In this example, `Shape` is an abstract class with two abstract methods, `area()` and `perimeter()`. These methods are defined but have no implementation. Any concrete subclass of `Shape` must provide an implementation for both `area()` and `perimeter()`.

---

### Subclassing an Abstract Class

When subclassing an abstract class, you are required to implement all abstract methods. Otherwise, the subclass will also be treated as abstract, and you won’t be able to instantiate it.

#### Example of a Subclass:

```python
# Concrete class inheriting from the abstract class
class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    # Implementing the abstract methods
    def area(self):
        return 3.14 * (self.radius ** 2)

    def perimeter(self):
        return 2 * 3.14 * self.radius

# Creating an instance of the subclass
circle = Circle(5)
print("Area:", circle.area())         # Output: Area: 78.5
print("Perimeter:", circle.perimeter())  # Output: Perimeter: 31.400000000000002
```

**Explanation**:
- The `Circle` class is a concrete subclass of the abstract class `Shape`.
- The `Circle` class provides implementations for the `area()` and `perimeter()` methods, fulfilling the requirements of the `Shape` class.
- Now, an instance of `Circle` can be created, and its methods can be used.

---

### Abstract Classes with Partially Implemented Methods

An abstract class can also contain fully implemented methods, in addition to abstract methods. This allows you to define default behavior for some methods, while still requiring the subclass to implement specific methods.

#### Example:

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass
    
    def sleep(self):
        print("The animal is sleeping.")

# Concrete class inheriting from the abstract class
class Dog(Animal):
    def sound(self):
        return "Bark"

# Creating an instance of Dog
dog = Dog()
print(dog.sound())  # Output: Bark
dog.sleep()         # Output: The animal is sleeping.
```

**Explanation**:
- The `Animal` class defines one abstract method `sound()` and one fully implemented method `sleep()`.
- The `Dog` class must implement the `sound()` method, but it inherits the `sleep()` method directly from `Animal`.
- You can now create instances of `Dog` and use both the `sound()` and `sleep()` methods.

---

### Use Cases for Abstract Classes

1. **Enforcing a Contract**: Abstract classes are useful when you want to enforce a particular interface or behavior across multiple subclasses. For example, if you have different types of shapes (Circle, Square, etc.), you can ensure that every subclass implements methods like `area()` and `perimeter()`.

2. **Polymorphism**: Abstract classes enable polymorphism, where different subclasses can be treated as instances of the parent abstract class. This is particularly useful when writing reusable, flexible code that operates on many different subclasses that share a common interface.

3. **Reusable Code**: Abstract classes allow you to write reusable methods that apply to all subclasses while requiring each subclass to implement certain methods. This keeps the code DRY (Don’t Repeat Yourself).

---

### Checking if a Class is Abstract

You can check whether a class is abstract by using the `ABCMeta` metaclass from the `abc` module.

#### Example:

```python
from abc import ABC

class MyClass(ABC):
    pass

print(issubclass(MyClass, ABC))  # Output: True
```

This checks whether `MyClass` is a subclass of `ABC` (which defines abstract base classes).

---

### Important Notes:

1. **Cannot Instantiate Abstract Classes**: You cannot directly create an instance of an abstract class. Doing so will raise a `TypeError`. Only concrete subclasses (that implement all abstract methods) can be instantiated.
   
2. **Optional Abstract Methods**: You can choose how many abstract methods an abstract class has. There could be one or several, and the rest of the methods can be fully implemented.

3. **Abstract Class with No Abstract Methods**: Technically, it is possible to create an abstract class without any abstract methods, but it won’t be useful in most cases. It would simply act as a base class that cannot be instantiated.

---

### Summary

- **Abstract classes** in Python are classes that cannot be instantiated directly and are meant to be inherited by other classes.
- They are defined using the `ABC` class from the `abc` module, and abstract methods are marked using the `@abstractmethod` decorator.
- **Abstract methods** are methods that have no implementation in the abstract class, and must be implemented by any concrete subclass.
- Concrete subclasses must implement all abstract methods of the parent class, otherwise, they cannot be instantiated.
- Abstract classes are useful for enforcing a consistent interface across multiple subclasses and implementing polymorphism.

Abstract classes provide a structured way to define common interfaces, making your code more flexible, extensible, and easy to maintain.