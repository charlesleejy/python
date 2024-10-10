## Explain the concept of polymorphism in Python.


### Polymorphism in Python

**Polymorphism** is a core concept in object-oriented programming (OOP) that allows objects of different classes to be treated as objects of a common superclass. It also refers to the ability of different classes to provide a unique implementation of methods that share the same name. The word "polymorphism" comes from Greek, meaning "many forms."

### Key Aspects of Polymorphism

1. **Method Overriding (Runtime Polymorphism)**
   - **Definition:** Polymorphism is achieved through method overriding, where a subclass provides a specific implementation of a method that is already defined in its superclass.
   - **Example:**
     ```python
     class Animal:
         def sound(self):
             return "Some generic sound"

     class Dog(Animal):
         def sound(self):
             return "Bark"

     class Cat(Animal):
         def sound(self):
             return "Meow"

     def make_sound(animal):
         print(animal.sound())

     dog = Dog()
     cat = Cat()

     make_sound(dog)  # Output: Bark
     make_sound(cat)  # Output: Meow
     ```

   - **Explanation:** Both `Dog` and `Cat` classes override the `sound` method of the `Animal` class. The `make_sound` function accepts an `Animal` object, but it correctly calls the `sound` method of the specific subclass passed to it, demonstrating polymorphism.

2. **Polymorphism with Functions and Objects**
   - **Definition:** Polymorphism also allows a function to accept different types of objects, and each object can have its unique implementation of the method.
   - **Example:**
     ```python
     class Bird:
         def fly(self):
             return "Flies in the sky"

     class Airplane:
         def fly(self):
             return "Flies in the air"

     def take_flight(flying_object):
         print(flying_object.fly())

     bird = Bird()
     airplane = Airplane()

     take_flight(bird)       # Output: Flies in the sky
     take_flight(airplane)   # Output: Flies in the air
     ```

   - **Explanation:** The `take_flight` function works with any object that has a `fly` method, regardless of the object's class. This is a key feature of polymorphism, where a single function can handle objects of different types.

3. **Polymorphism with Abstract Base Classes (ABC)**
   - **Definition:** Abstract Base Classes (ABCs) provide a way to define a common interface for a group of subclasses. These subclasses must provide specific implementations for the abstract methods, ensuring polymorphic behavior.
   - **Example:**
     ```python
     from abc import ABC, abstractmethod

     class Shape(ABC):
         @abstractmethod
         def area(self):
             pass

     class Circle(Shape):
         def __init__(self, radius):
             self.radius = radius

         def area(self):
             return 3.14 * self.radius * self.radius

     class Square(Shape):
         def __init__(self, side):
             self.side = side

         def area(self):
             return self.side * self.side

     def print_area(shape):
         print(shape.area())

     circle = Circle(5)
     square = Square(4)

     print_area(circle)  # Output: 78.5
     print_area(square)  # Output: 16
     ```

   - **Explanation:** Both `Circle` and `Square` implement the `area` method from the `Shape` abstract base class. The `print_area` function can take any object that is a subclass of `Shape` and call its `area` method, demonstrating polymorphism.

4. **Polymorphism in Built-in Functions**
   - Python's built-in functions like `len()`, `sorted()`, and `+` (addition operator) work with different types of objects, demonstrating polymorphism.
   - **Example:**
     ```python
     print(len("hello"))  # Output: 5
     print(len([1, 2, 3]))  # Output: 3

     print(1 + 2)  # Output: 3
     print("Hello " + "World")  # Output: Hello World
     ```

   - **Explanation:** The `len()` function works with both strings and lists, and the `+` operator works with both numbers and strings, showing that the same function/operator can work with different types.

### Summary

- **Polymorphism** in Python allows objects of different classes to be treated through a common interface, promoting flexibility and reusability.
- It is achieved through method overriding, where different classes provide their own implementation of a method with the same name.
- Polymorphism allows functions and methods to work with objects of different types, enabling a high level of abstraction and code flexibility.