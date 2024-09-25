## 40. What are abstract classes, and how do you create them in Python?


### Abstract Classes in Python

**Abstract classes** are classes that cannot be instantiated directly and are meant to be subclasses. They serve as blueprints for other classes, defining methods that must be implemented by any subclass. Abstract classes allow you to define a common interface for a group of subclasses while ensuring that certain methods are implemented in each subclass.

### Key Features of Abstract Classes

1. **Cannot Be Instantiated:**
   - Abstract classes cannot be instantiated on their own. They are intended to be subclassed, and their purpose is to provide a common structure for derived classes.

2. **Contain Abstract Methods:**
   - Abstract methods are methods that are declared but contain no implementation. Subclasses must override and provide concrete implementations for these abstract methods.

3. **Use the `abc` Module:**
   - Python’s `abc` (Abstract Base Classes) module provides the tools to create abstract classes. The `ABC` class from the `abc` module is used as the base class for defining abstract classes, and the `@abstractmethod` decorator is used to declare abstract methods.

### Creating Abstract Classes in Python

1. **Importing the Required Components:**
   - You need to import `ABC` and `abstractmethod` from the `abc` module to create an abstract class.

2. **Defining an Abstract Class:**
   - The abstract class should inherit from `ABC`.
   - Use the `@abstractmethod` decorator to define abstract methods.

3. **Example: Abstract Class in Python**
   ```python
   from abc import ABC, abstractmethod

   class Shape(ABC):
       @abstractmethod
       def area(self):
           pass

       @abstractmethod
       def perimeter(self):
           pass

   class Circle(Shape):
       def __init__(self, radius):
           self.radius = radius

       def area(self):
           return 3.14 * self.radius ** 2

       def perimeter(self):
           return 2 * 3.14 * self.radius

   class Rectangle(Shape):
       def __init__(self, width, height):
           self.width = width
           self.height = height

       def area(self):
           return self.width * self.height

       def perimeter(self):
           return 2 * (self.width + self.height)

   # Attempting to instantiate Shape directly will raise an error:
   # shape = Shape()  # TypeError: Can't instantiate abstract class Shape with abstract methods area, perimeter

   circle = Circle(5)
   rectangle = Rectangle(4, 6)

   print("Circle Area:", circle.area())        # Output: Circle Area: 78.5
   print("Circle Perimeter:", circle.perimeter())  # Output: Circle Perimeter: 31.400000000000002

   print("Rectangle Area:", rectangle.area())        # Output: Rectangle Area: 24
   print("Rectangle Perimeter:", rectangle.perimeter())  # Output: Rectangle Perimeter: 20
   ```

   - **Explanation:**
     - The `Shape` class is an abstract class that defines the interface for `area` and `perimeter` methods.
     - The `Circle` and `Rectangle` classes inherit from `Shape` and provide concrete implementations for the abstract methods.
     - Attempting to instantiate the `Shape` class directly will raise a `TypeError` because it contains abstract methods.

### Key Points

- **Abstract Classes:**
  - Defined using the `ABC` class from the `abc` module.
  - Contain one or more abstract methods, defined using the `@abstractmethod` decorator.
  - Cannot be instantiated directly; they must be subclassed.

- **Abstract Methods:**
  - Methods declared in an abstract class that have no implementation.
  - Subclasses are required to override these methods and provide concrete implementations.

### Use Cases for Abstract Classes

- **Interface Definition:** Abstract classes are used to define a common interface for a group of related classes.
- **Enforcing Method Implementation:** Abstract methods ensure that all subclasses implement certain critical methods.
- **Partial Implementation:** Abstract classes can provide some common functionality while leaving specific details to subclasses.

### Summary

- **Abstract classes** in Python provide a way to define a template for other classes, enforcing a consistent interface and ensuring that certain methods are implemented in derived classes.
- They are created using the `ABC` class and `@abstractmethod` decorator from the `abc` module.
- Abstract classes are essential for designing large and complex systems where consistent interfaces and behavior across multiple classes are required.